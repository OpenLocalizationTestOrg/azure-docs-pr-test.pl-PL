---
title: Projektowania i implementacji bazy danych programu Oracle na platformie Azure | Dokumentacja firmy Microsoft
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
ms.openlocfilehash: 1af7e1d40a0eb129875dd6a30ac899f2025bee13
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="design-and-implement-an-oracle-database-in-azure"></a><span data-ttu-id="7d38c-103">Projektowania i implementacji bazy danych programu Oracle na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="7d38c-103">Design and implement an Oracle database in Azure</span></span>

## <a name="assumptions"></a><span data-ttu-id="7d38c-104">Wartości domyślne</span><span class="sxs-lookup"><span data-stu-id="7d38c-104">Assumptions</span></span>

- <span data-ttu-id="7d38c-105">Planujesz przeprowadzić migrację bazy danych Oracle z lokalnej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="7d38c-105">You're planning to migrate an Oracle database from on-premises to Azure.</span></span>
- <span data-ttu-id="7d38c-106">Masz opis różnych metryk w raportach Oracle AWR.</span><span class="sxs-lookup"><span data-stu-id="7d38c-106">You have an understanding of the various metrics in Oracle AWR reports.</span></span>
- <span data-ttu-id="7d38c-107">Możesz wiedzę na temat linii bazowej wydajności aplikacji oraz wykorzystania platformy.</span><span class="sxs-lookup"><span data-stu-id="7d38c-107">You have a baseline understanding of application performance and platform utilization.</span></span>

## <a name="goals"></a><span data-ttu-id="7d38c-108">Cele</span><span class="sxs-lookup"><span data-stu-id="7d38c-108">Goals</span></span>

- <span data-ttu-id="7d38c-109">Zrozumienie, jak zoptymalizować wdrożenia programu Oracle na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="7d38c-109">Understand how to optimize your Oracle deployment in Azure.</span></span>
- <span data-ttu-id="7d38c-110">Poznaj opcje dla bazy danych Oracle w środowisku Azure dostrajania wydajności.</span><span class="sxs-lookup"><span data-stu-id="7d38c-110">Explore performance tuning options for an Oracle database in an Azure environment.</span></span>

## <a name="the-differences-between-an-on-premises-and-azure-implementation"></a><span data-ttu-id="7d38c-111">Różnice między lokalnymi i Azure implementacji</span><span class="sxs-lookup"><span data-stu-id="7d38c-111">The differences between an on-premises and Azure implementation</span></span> 

<span data-ttu-id="7d38c-112">Poniżej przedstawiono kilka ważnych rzeczy, które należy wziąć pod uwagę podczas migrowania aplikacji lokalnych do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7d38c-112">Following are some important things to keep in mind when you're migrating on-premises applications to Azure.</span></span> 

<span data-ttu-id="7d38c-113">Jedną istotną różnicą jest to, że w implementacji platformy Azure, zasobów, takich jak maszyn wirtualnych, dysków i sieci wirtualne są współużytkowane przez innych klientów.</span><span class="sxs-lookup"><span data-stu-id="7d38c-113">One important difference is that in an Azure implementation, resources such as VMs, disks, and virtual networks are shared among other clients.</span></span> <span data-ttu-id="7d38c-114">Ponadto zasobów może być ograniczony na podstawie wymagań.</span><span class="sxs-lookup"><span data-stu-id="7d38c-114">In addition, resources can be throttled based on the requirements.</span></span> <span data-ttu-id="7d38c-115">Zamiast koncentrujących się na temat niepowodzenia (MTBF), Azure więcej koncentruje się na pozostałych awarii (MTTR).</span><span class="sxs-lookup"><span data-stu-id="7d38c-115">Instead of focusing on avoiding failing (MTBF), Azure is more focused on surviving the failure (MTTR).</span></span>

<span data-ttu-id="7d38c-116">W poniższej tabeli wymieniono niektóre różnice między implementacją lokalną i Azure implementacji bazy danych programu Oracle.</span><span class="sxs-lookup"><span data-stu-id="7d38c-116">The following table lists some of the differences between an on-premises implementation and an Azure implementation of an Oracle database.</span></span>

> 
> |  | <span data-ttu-id="7d38c-117">**Implementacja lokalna**</span><span class="sxs-lookup"><span data-stu-id="7d38c-117">**On-premises implementation**</span></span> | <span data-ttu-id="7d38c-118">**Implementacja Azure**</span><span class="sxs-lookup"><span data-stu-id="7d38c-118">**Azure implementation**</span></span> |
> | --- | --- | --- |
> | <span data-ttu-id="7d38c-119">**Sieć**</span><span class="sxs-lookup"><span data-stu-id="7d38c-119">**Networking**</span></span> |<span data-ttu-id="7d38c-120">LAN/WAN</span><span class="sxs-lookup"><span data-stu-id="7d38c-120">LAN/WAN</span></span>  |<span data-ttu-id="7d38c-121">SDN (technologia Sdn)</span><span class="sxs-lookup"><span data-stu-id="7d38c-121">SDN (software-defined networking)</span></span>|
> | <span data-ttu-id="7d38c-122">**Grupy zabezpieczeń**</span><span class="sxs-lookup"><span data-stu-id="7d38c-122">**Security group**</span></span> |<span data-ttu-id="7d38c-123">Ograniczenia adresu IP i portu narzędzi</span><span class="sxs-lookup"><span data-stu-id="7d38c-123">IP/port restriction tools</span></span> |[<span data-ttu-id="7d38c-124">Grupy zabezpieczeń sieci (NSG)</span><span class="sxs-lookup"><span data-stu-id="7d38c-124">Network Security Group (NSG)</span></span>](https://azure.microsoft.com/blog/network-security-groups) |
> | <span data-ttu-id="7d38c-125">**Odporność**</span><span class="sxs-lookup"><span data-stu-id="7d38c-125">**Resilience**</span></span> |<span data-ttu-id="7d38c-126">MTBF (Średni czas między awariami)</span><span class="sxs-lookup"><span data-stu-id="7d38c-126">MTBF (mean time between failures)</span></span> |<span data-ttu-id="7d38c-127">MTTR (Średni czas do odzyskiwania)</span><span class="sxs-lookup"><span data-stu-id="7d38c-127">MTTR (mean time to recovery)</span></span>|
> | <span data-ttu-id="7d38c-128">**Planowana konserwacja**</span><span class="sxs-lookup"><span data-stu-id="7d38c-128">**Planned maintenance**</span></span> |<span data-ttu-id="7d38c-129">Stosowanie poprawek do uaktualnienia</span><span class="sxs-lookup"><span data-stu-id="7d38c-129">Patching/upgrades</span></span>|<span data-ttu-id="7d38c-130">[Zestawy dostępności](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) (poprawki/uaktualniania zarządzane przez usługę Azure)</span><span class="sxs-lookup"><span data-stu-id="7d38c-130">[Availability sets](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) (patching/upgrades managed by Azure)</span></span> |
> | <span data-ttu-id="7d38c-131">**Zasób**</span><span class="sxs-lookup"><span data-stu-id="7d38c-131">**Resource**</span></span> |<span data-ttu-id="7d38c-132">Dedykowany</span><span class="sxs-lookup"><span data-stu-id="7d38c-132">Dedicated</span></span>  |<span data-ttu-id="7d38c-133">Współużytkowane z innymi klientami</span><span class="sxs-lookup"><span data-stu-id="7d38c-133">Shared with other clients</span></span>|
> | <span data-ttu-id="7d38c-134">**Regiony**</span><span class="sxs-lookup"><span data-stu-id="7d38c-134">**Regions**</span></span> |<span data-ttu-id="7d38c-135">Centra danych</span><span class="sxs-lookup"><span data-stu-id="7d38c-135">Datacenters</span></span> |[<span data-ttu-id="7d38c-136">Pary regionu</span><span class="sxs-lookup"><span data-stu-id="7d38c-136">Region pairs</span></span>](https://docs.microsoft.com/azure/virtual-machines/windows/regions-and-availability)|
> | <span data-ttu-id="7d38c-137">**Storage**</span><span class="sxs-lookup"><span data-stu-id="7d38c-137">**Storage**</span></span> |<span data-ttu-id="7d38c-138">Dyski fizyczne/w sieci SAN</span><span class="sxs-lookup"><span data-stu-id="7d38c-138">SAN/physical disks</span></span> |[<span data-ttu-id="7d38c-139">Zarządzane Azure magazynu</span><span class="sxs-lookup"><span data-stu-id="7d38c-139">Azure-managed storage</span></span>](https://azure.microsoft.com/pricing/details/managed-disks/?v=17.23h)|
> | <span data-ttu-id="7d38c-140">**Skalowanie**</span><span class="sxs-lookup"><span data-stu-id="7d38c-140">**Scale**</span></span> |<span data-ttu-id="7d38c-141">Skalowanie w pionie</span><span class="sxs-lookup"><span data-stu-id="7d38c-141">Vertical scale</span></span> |<span data-ttu-id="7d38c-142">Skalowanie w poziomie</span><span class="sxs-lookup"><span data-stu-id="7d38c-142">Horizontal scale</span></span>|


### <a name="requirements"></a><span data-ttu-id="7d38c-143">Wymagania</span><span class="sxs-lookup"><span data-stu-id="7d38c-143">Requirements</span></span>

- <span data-ttu-id="7d38c-144">Określ częstotliwość rozmiaru i wzrostu bazy danych.</span><span class="sxs-lookup"><span data-stu-id="7d38c-144">Determine the database size and growth rate.</span></span>
- <span data-ttu-id="7d38c-145">Określenie wymagań w zakresie IOPS, które można oszacować na podstawie raportów Oracle AWR lub innych narzędzi do monitorowania sieci.</span><span class="sxs-lookup"><span data-stu-id="7d38c-145">Determine the IOPS requirements, which you can estimate based on Oracle AWR reports or other network monitoring tools.</span></span>

## <a name="configuration-options"></a><span data-ttu-id="7d38c-146">Opcje konfiguracji</span><span class="sxs-lookup"><span data-stu-id="7d38c-146">Configuration options</span></span>

<span data-ttu-id="7d38c-147">Istnieją cztery potencjalnych obszarów, które można dostosować w celu zwiększenia wydajności w środowisku platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="7d38c-147">There are four potential areas that you can tune to improve performance in an Azure environment:</span></span>

- <span data-ttu-id="7d38c-148">Rozmiar maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="7d38c-148">Virtual machine size</span></span>
- <span data-ttu-id="7d38c-149">Przepustowość sieci</span><span class="sxs-lookup"><span data-stu-id="7d38c-149">Network throughput</span></span>
- <span data-ttu-id="7d38c-150">Typy dysków i konfiguracji</span><span class="sxs-lookup"><span data-stu-id="7d38c-150">Disk types and configurations</span></span>
- <span data-ttu-id="7d38c-151">Ustawienia pamięci podręcznej dysku</span><span class="sxs-lookup"><span data-stu-id="7d38c-151">Disk cache settings</span></span>

### <a name="generate-an-awr-report"></a><span data-ttu-id="7d38c-152">Generowanie raportu AWR</span><span class="sxs-lookup"><span data-stu-id="7d38c-152">Generate an AWR report</span></span>

<span data-ttu-id="7d38c-153">Jeśli korzystasz z istniejącej bazy danych programu Oracle i jest planowana migracja do platformy Azure, masz kilka opcji.</span><span class="sxs-lookup"><span data-stu-id="7d38c-153">If you have an existing an Oracle database and are planning to migrate to Azure, you have several options.</span></span> <span data-ttu-id="7d38c-154">Można uruchomić raport Oracle AWR można pobrać metryki (IOPS, MB/s, GiBs i tak dalej).</span><span class="sxs-lookup"><span data-stu-id="7d38c-154">You can run the Oracle AWR report to get the metrics (IOPS, Mbps, GiBs, and so on).</span></span> <span data-ttu-id="7d38c-155">Następnie wybierz maszynę Wirtualną na podstawie zebranych metryk.</span><span class="sxs-lookup"><span data-stu-id="7d38c-155">Then choose the VM based on the metrics that you collected.</span></span> <span data-ttu-id="7d38c-156">Lub można skontaktuj się z zespołem infrastruktury, aby uzyskać podobne informacje.</span><span class="sxs-lookup"><span data-stu-id="7d38c-156">Or you can contact your infrastructure team to get similar information.</span></span>

<span data-ttu-id="7d38c-157">Należy rozważyć działania raportu AWR podczas obciążeń zarówno regularne i szczytu, więc możesz porównać.</span><span class="sxs-lookup"><span data-stu-id="7d38c-157">You might consider running your AWR report during both regular and peak workloads, so you can compare.</span></span> <span data-ttu-id="7d38c-158">Na podstawie tych raportów, można rozmiar maszyn wirtualnych na podstawie obciążenia średnia lub maksymalne obciążenie.</span><span class="sxs-lookup"><span data-stu-id="7d38c-158">Based on these reports, you can size the VMs based on either the average workload or the maximum workload.</span></span>

<span data-ttu-id="7d38c-159">Poniżej przedstawiono przykładowy sposób wygenerować raport AWR:</span><span class="sxs-lookup"><span data-stu-id="7d38c-159">Following is an example of how to generate an AWR report:</span></span>

```bash
$ sqlplus / as sysdba
SQL> EXEC DBMS_WORKLOAD_REPOSITORY.CREATE_SNAPSHOT;
SQL> @?/rdbms/admin/awrrpt.sql
```

### <a name="key-metrics"></a><span data-ttu-id="7d38c-160">Kluczowych metryk</span><span class="sxs-lookup"><span data-stu-id="7d38c-160">Key metrics</span></span>

<span data-ttu-id="7d38c-161">Metryki, który można uzyskać z raportu AWR są następujące:</span><span class="sxs-lookup"><span data-stu-id="7d38c-161">Following are the metrics that you can obtain from the AWR report:</span></span>

- <span data-ttu-id="7d38c-162">Całkowita liczba rdzeni</span><span class="sxs-lookup"><span data-stu-id="7d38c-162">Total number of cores</span></span>
- <span data-ttu-id="7d38c-163">Szybkość zegara Procesora</span><span class="sxs-lookup"><span data-stu-id="7d38c-163">CPU clock speed</span></span>
- <span data-ttu-id="7d38c-164">Całkowitej ilości pamięci w GB</span><span class="sxs-lookup"><span data-stu-id="7d38c-164">Total memory in GB</span></span>
- <span data-ttu-id="7d38c-165">Użycie procesora CPU</span><span class="sxs-lookup"><span data-stu-id="7d38c-165">CPU utilization</span></span>
- <span data-ttu-id="7d38c-166">Szczytowa szybkość transferu danych</span><span class="sxs-lookup"><span data-stu-id="7d38c-166">Peak data transfer rate</span></span>
- <span data-ttu-id="7d38c-167">Liczba operacji We/Wy zmiany (odczyt/zapis)</span><span class="sxs-lookup"><span data-stu-id="7d38c-167">Rate of I/O changes (read/write)</span></span>
- <span data-ttu-id="7d38c-168">Wykonaj ponownie szybkość dziennika (MB/s)</span><span class="sxs-lookup"><span data-stu-id="7d38c-168">Redo log rate (MBPs)</span></span>
- <span data-ttu-id="7d38c-169">Przepustowość sieci</span><span class="sxs-lookup"><span data-stu-id="7d38c-169">Network throughput</span></span>
- <span data-ttu-id="7d38c-170">Szybkość opóźnienia sieci (niski/wysoka)</span><span class="sxs-lookup"><span data-stu-id="7d38c-170">Network latency rate (low/high)</span></span>
- <span data-ttu-id="7d38c-171">Rozmiar bazy danych w GB</span><span class="sxs-lookup"><span data-stu-id="7d38c-171">Database size in GB</span></span>
- <span data-ttu-id="7d38c-172">Bajty odebrane za pomocą programu SQL * Net od i do klienta</span><span class="sxs-lookup"><span data-stu-id="7d38c-172">Bytes received via SQL*Net from/to client</span></span>

### <a name="virtual-machine-size"></a><span data-ttu-id="7d38c-173">Rozmiar maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="7d38c-173">Virtual machine size</span></span>

#### <a name="1-estimate-vm-size-based-on-cpu-memory-and-io-usage-from-the-awr-report"></a><span data-ttu-id="7d38c-174">1. Szacowanie rozmiaru maszyny Wirtualnej na podstawie użycia procesora CPU, pamięci i we/wy z raportu AWR</span><span class="sxs-lookup"><span data-stu-id="7d38c-174">1. Estimate VM size based on CPU, memory, and I/O usage from the AWR report</span></span>

<span data-ttu-id="7d38c-175">Jedyną operacją, której może wyglądać na jest najwyższym pięć zdarzenia czasu pierwszego planu, które wskazują skutkującej wąskich gardeł systemu.</span><span class="sxs-lookup"><span data-stu-id="7d38c-175">One thing you might look at is the top five timed foreground events that indicate where the system bottlenecks are.</span></span>

<span data-ttu-id="7d38c-176">Na przykład na poniższym diagramie synchronizacji plików dziennika jest u góry.</span><span class="sxs-lookup"><span data-stu-id="7d38c-176">For example, in the following diagram, the log file sync is at the top.</span></span> <span data-ttu-id="7d38c-177">Wskazuje liczbę czeka przed LGWR zapisuje buforu dziennika Powtórz pliku dziennika.</span><span class="sxs-lookup"><span data-stu-id="7d38c-177">It indicates the number of waits that are required before the LGWR writes the log buffer to the redo log file.</span></span> <span data-ttu-id="7d38c-178">Te wyniki wskazują, że lepiej wykonuje magazynu lub dyski są wymagane.</span><span class="sxs-lookup"><span data-stu-id="7d38c-178">These results indicate that better performing storage or disks are required.</span></span> <span data-ttu-id="7d38c-179">Ponadto na diagramie przedstawiono również liczbę procesora CPU (rdzenie) i ilość pamięci.</span><span class="sxs-lookup"><span data-stu-id="7d38c-179">In addition, the diagram also shows the number of CPU (cores) and the amount of memory.</span></span>

![Zrzut ekranu przedstawiający stronę raportu AWR](./media/oracle-design/cpu_memory_info.png)

<span data-ttu-id="7d38c-181">Na poniższym diagramie przedstawiono całkowita liczba operacji We/Wy odczytu i zapisu.</span><span class="sxs-lookup"><span data-stu-id="7d38c-181">The following diagram shows the total I/O of read and write.</span></span> <span data-ttu-id="7d38c-182">Znaleziono 59 GB do odczytu i 247.3 zapisane w czasie raportu.</span><span class="sxs-lookup"><span data-stu-id="7d38c-182">There were 59 GB read and 247.3 GB written during the time of the report.</span></span>

![Zrzut ekranu przedstawiający stronę raportu AWR](./media/oracle-design/io_info.png)

#### <a name="2-choose-a-vm"></a><span data-ttu-id="7d38c-184">2. Wybierz Maszynę wirtualną</span><span class="sxs-lookup"><span data-stu-id="7d38c-184">2. Choose a VM</span></span>

<span data-ttu-id="7d38c-185">Na podstawie informacji zebranych z raportu AWR, następnym krokiem jest wybranie maszyny Wirtualnej o rozmiarze podobne, który spełnia wymagania.</span><span class="sxs-lookup"><span data-stu-id="7d38c-185">Based on the information that you collected from the AWR report, the next step is to choose a VM of a similar size that meets your requirements.</span></span> <span data-ttu-id="7d38c-186">Listę dostępnych maszyn wirtualnych można znaleźć w artykule [zoptymalizowanych pod kątem pamięci](https://docs.microsoft.com/azure/virtual-machinFine tune es/virtual-machines-windows-sizes-memory).</span><span class="sxs-lookup"><span data-stu-id="7d38c-186">You can find a list of available VMs in the article [Memory optimized](https://docs.microsoft.com/azure/virtual-machinFine tune es/virtual-machines-windows-sizes-memory).</span></span>

#### <a name="3-fine-tune-the-vm-sizing-with-a-similar-vm-series-based-on-the-acu"></a><span data-ttu-id="7d38c-187">3. Dostosowywanie rozmiaru maszyny Wirtualnej z podobnych seria maszyn wirtualnych w oparciu ACU</span><span class="sxs-lookup"><span data-stu-id="7d38c-187">3. Fine-tune the VM sizing with a similar VM series based on the ACU</span></span>

<span data-ttu-id="7d38c-188">Po wybraniu maszyny Wirtualnej, należy zwrócić uwagę na ACU dla maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="7d38c-188">After you've chosen the VM, pay attention to the ACU for the VM.</span></span> <span data-ttu-id="7d38c-189">Możesz wybrać inną maszynę Wirtualną na podstawie wartości ACU dostosowany do potrzeb.</span><span class="sxs-lookup"><span data-stu-id="7d38c-189">You might choose a different VM based on the ACU value that better suits your requirements.</span></span> <span data-ttu-id="7d38c-190">Aby uzyskać więcej informacji, zobacz [jednostki rozwiązań usługi obliczenia Azure](https://docs.microsoft.com/azure/virtual-machines/windows/acu).</span><span class="sxs-lookup"><span data-stu-id="7d38c-190">For more information, see [Azure compute unit](https://docs.microsoft.com/azure/virtual-machines/windows/acu).</span></span>

![Zrzut ekranu przedstawiający stronę jednostki ACU](./media/oracle-design/acu_units.png)

### <a name="network-throughput"></a><span data-ttu-id="7d38c-192">Przepustowość sieci</span><span class="sxs-lookup"><span data-stu-id="7d38c-192">Network throughput</span></span>

<span data-ttu-id="7d38c-193">Na poniższym diagramie przedstawiono relację między przepływności i IOPS:</span><span class="sxs-lookup"><span data-stu-id="7d38c-193">The following diagram shows the relation between throughput and IOPS:</span></span>

![Zrzut ekranu przedstawiający przepływność](./media/oracle-design/throughput.png)

<span data-ttu-id="7d38c-195">Przepustowość sieci całkowita jest szacowana na podstawie następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="7d38c-195">The total network throughput is estimated based on the following information:</span></span>
- <span data-ttu-id="7d38c-196">SQL * Net ruchu</span><span class="sxs-lookup"><span data-stu-id="7d38c-196">SQL*Net traffic</span></span>
- <span data-ttu-id="7d38c-197">MB/s x wielu serwerów (strumienia wychodzącego takich jak Oracle Data Guard)</span><span class="sxs-lookup"><span data-stu-id="7d38c-197">MBps x number of servers (outbound stream such as Oracle Data Guard)</span></span>
- <span data-ttu-id="7d38c-198">Innych czynników, takich jak replikacja aplikacji</span><span class="sxs-lookup"><span data-stu-id="7d38c-198">Other factors, such as application replication</span></span>

![Zrzut ekranu przedstawiający SQL * przepustowość sieci](./media/oracle-design/sqlnet_info.png)

<span data-ttu-id="7d38c-200">Zgodnie z wymaganiami przepustowości sieci, istnieją różne typy bramy można wybrać.</span><span class="sxs-lookup"><span data-stu-id="7d38c-200">Based on your network bandwidth requirements, there are various gateway types for you to choose from.</span></span> <span data-ttu-id="7d38c-201">Obejmują one basic, VpnGw i usługa Azure ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="7d38c-201">These include basic, VpnGw, and Azure ExpressRoute.</span></span> <span data-ttu-id="7d38c-202">Aby uzyskać więcej informacji, zobacz [bramy sieci VPN, na stronie dotyczącej cen](https://azure.microsoft.com/en-us/pricing/details/vpn-gateway/?v=17.23h).</span><span class="sxs-lookup"><span data-stu-id="7d38c-202">For more information, see the [VPN gateway pricing page](https://azure.microsoft.com/en-us/pricing/details/vpn-gateway/?v=17.23h).</span></span>

<span data-ttu-id="7d38c-203">**Zalecenia**</span><span class="sxs-lookup"><span data-stu-id="7d38c-203">**Recommendations**</span></span>

- <span data-ttu-id="7d38c-204">Opóźnienie sieci wyższy jest porównywany z lokalnego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="7d38c-204">Network latency is higher compared to an on-premises deployment.</span></span> <span data-ttu-id="7d38c-205">Zmniejszenie sieci round rund może znacznie poprawić wydajność.</span><span class="sxs-lookup"><span data-stu-id="7d38c-205">Reducing network round trips can greatly improve performance.</span></span>
- <span data-ttu-id="7d38c-206">Aby ograniczyć liczbę operacji, konsolidację aplikacji, które mają wysokie transakcji lub "chatty" aplikacji na tej samej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="7d38c-206">To reduce round-trips, consolidate applications that have high transactions or “chatty” apps on the same virtual machine.</span></span>

### <a name="disk-types-and-configurations"></a><span data-ttu-id="7d38c-207">Typy dysków i konfiguracji</span><span class="sxs-lookup"><span data-stu-id="7d38c-207">Disk types and configurations</span></span>

- <span data-ttu-id="7d38c-208">*Domyślna dysków systemu operacyjnego*: tych typów dysków oferują trwałych danych i buforowania.</span><span class="sxs-lookup"><span data-stu-id="7d38c-208">*Default OS disks*: These disk types offer persistent data and caching.</span></span> <span data-ttu-id="7d38c-209">Są zoptymalizowane pod kątem dostępu do systemu operacyjnego podczas uruchamiania, a nie są przeznaczone dla jednej transakcyjnej lub magazynu danych obciążenia (analitycznych).</span><span class="sxs-lookup"><span data-stu-id="7d38c-209">They are optimized for OS access at startup, and aren't designed for either transactional or data warehouse (analytical) workloads.</span></span>

- <span data-ttu-id="7d38c-210">*Niezarządzane dysków*: Z tych typów dysku zarządzasz kont magazynu, w których są przechowywane pliki wirtualnego dysku twardego (VHD), które odpowiadają dysków maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="7d38c-210">*Unmanaged disks*: With these disk types, you manage the storage accounts that store the virtual hard disk (VHD) files that correspond to your VM disks.</span></span> <span data-ttu-id="7d38c-211">Pliki VHD są przechowywane jako stronicowe obiekty BLOB na kontach magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="7d38c-211">VHD files are stored as page blobs in Azure storage accounts.</span></span>

- <span data-ttu-id="7d38c-212">*Dyski zarządzane*: Azure zarządza kontami magazynu, których używasz dla dysków maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="7d38c-212">*Managed disks*: Azure manages the storage accounts that you use for your VM disks.</span></span> <span data-ttu-id="7d38c-213">Należy określić typ dysku (standardowy lub premium) oraz rozmiar dysku, które są potrzebne.</span><span class="sxs-lookup"><span data-stu-id="7d38c-213">You specify the disk type (premium or standard) and the size of the disk that you need.</span></span> <span data-ttu-id="7d38c-214">Azure tworzy i którymi zarządza dysku dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="7d38c-214">Azure creates and manages the disk for you.</span></span>

- <span data-ttu-id="7d38c-215">*Dyski magazynu Premium*: tych typów dysków są najbardziej odpowiednie dla obciążeń produkcyjnych.</span><span class="sxs-lookup"><span data-stu-id="7d38c-215">*Premium storage disks*: These disk types are best suited for production workloads.</span></span> <span data-ttu-id="7d38c-216">Magazyn w warstwie Premium obsługuje dyski maszyn wirtualnych, które można dołączyć do określonego rozmiaru serii maszyn wirtualnych, takie jak seria DS, DSv2 i GS oraz F maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="7d38c-216">Premium storage supports VM disks that can be attached to specific size-series VMs, such as DS, DSv2, GS, and F series VMs.</span></span> <span data-ttu-id="7d38c-217">Dysku premium jest dostarczany z różnych rozmiarach i można wybrać dyski od 32 GB do 4096 GB.</span><span class="sxs-lookup"><span data-stu-id="7d38c-217">The premium disk comes with different sizes, and you can choose between disks ranging from 32 GB to 4,096 GB.</span></span> <span data-ttu-id="7d38c-218">Rozmiar każdego dysku ma specyfikacjami wydajności.</span><span class="sxs-lookup"><span data-stu-id="7d38c-218">Each disk size has its own performance specifications.</span></span> <span data-ttu-id="7d38c-219">W zależności od wymagań aplikacji można dołączyć jeden lub więcej dysków do maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="7d38c-219">Depending on your application requirements, you can attach one or more disks to your VM.</span></span>

<span data-ttu-id="7d38c-220">Podczas tworzenia nowego dysku zarządzanego z portalu, można wybrać **typ konta** dla typu dysku, którego chcesz użyć.</span><span class="sxs-lookup"><span data-stu-id="7d38c-220">When you create a new managed disk from the portal, you can choose the **Account type** for the type of disk you want to use.</span></span> <span data-ttu-id="7d38c-221">Należy pamiętać, że nie wszystkie dostępne dyski są wyświetlane w menu rozwijanym.</span><span class="sxs-lookup"><span data-stu-id="7d38c-221">Keep in mind that not all available disks are shown in the drop-down menu.</span></span> <span data-ttu-id="7d38c-222">Po wybraniu określonego rozmiaru maszyny Wirtualnej, menu pokazuje tylko magazynu premium dostępne jednostki SKU, które są oparte na rozmiar tej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="7d38c-222">After you choose a particular VM size, the menu shows only the available premium storage SKUs that are based on that VM size.</span></span>

![Zrzut ekranu przedstawiający stronę dysków zarządzanych](./media/oracle-design/premium_disk01.png)

<span data-ttu-id="7d38c-224">Aby uzyskać więcej informacji, zobacz [zarządzanych dysków dla maszyny wirtualne i Magazyn w warstwie Premium wysokiej wydajności](https://docs.microsoft.com/azure/storage/storage-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="7d38c-224">For more information, see [High-performance Premium Storage and managed disks for VMs](https://docs.microsoft.com/azure/storage/storage-premium-storage).</span></span>

<span data-ttu-id="7d38c-225">Po skonfigurowaniu magazynu na maszynie Wirtualnej można załadować testu z dysków przed utworzeniem bazy danych.</span><span class="sxs-lookup"><span data-stu-id="7d38c-225">After you configure your storage on a VM, you might want to load test the disks before creating a database.</span></span> <span data-ttu-id="7d38c-226">Znajomość szybkości operacji We/Wy pod względem zarówno opóźnienia i przepływności może pomóc ustalić, czy oczekiwany przepływności z obiektami docelowymi opóźnienia obsługi maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="7d38c-226">Knowing the I/O rate in terms of both latency and throughput can help you determine if the VMs support the expected throughput with latency targets.</span></span>

<span data-ttu-id="7d38c-227">Istnieje wiele narzędzi dla aplikacji testów obciążenia, takich jak Oracle Orion, Sysbench i Fio.</span><span class="sxs-lookup"><span data-stu-id="7d38c-227">There are a number of tools for application load testing, such as Oracle Orion, Sysbench, and Fio.</span></span>

<span data-ttu-id="7d38c-228">Po wdrożeniu bazy danych programu Oracle ponownie uruchomić test obciążenia.</span><span class="sxs-lookup"><span data-stu-id="7d38c-228">Run the load test again after you've deployed an Oracle database.</span></span> <span data-ttu-id="7d38c-229">Uruchom obciążeń regularne i szczytu, a wyniki wskazują linii bazowej środowiska.</span><span class="sxs-lookup"><span data-stu-id="7d38c-229">Start your regular and peak workloads, and the results show you the baseline of your environment.</span></span>

<span data-ttu-id="7d38c-230">Może być większe znaczenie dla rozmiaru magazynu oparte na szybkość IOPS, a nie rozmiaru magazynu.</span><span class="sxs-lookup"><span data-stu-id="7d38c-230">It might be more important to size the storage based on the IOPS rate rather than the storage size.</span></span> <span data-ttu-id="7d38c-231">Na przykład jeśli 5000 IOPS wymagane, ale wymagane jest tylko 200 GB, może nadal otrzymasz dysku premium klasy P30 nawet, jeśli zawiera więcej niż 200 GB przestrzeni dyskowej.</span><span class="sxs-lookup"><span data-stu-id="7d38c-231">For example, if the required IOPS is 5,000, but you only need 200 GB, you might still get the P30 class premium disk even though it comes with more than 200 GB of storage.</span></span>

<span data-ttu-id="7d38c-232">Szybkość IOPS można uzyskać z AWR raportu.</span><span class="sxs-lookup"><span data-stu-id="7d38c-232">The IOPS rate can be obtained from the AWR report.</span></span> <span data-ttu-id="7d38c-233">Określono dziennika Powtórz, fizyczne odczyty i zapisy szybkości.</span><span class="sxs-lookup"><span data-stu-id="7d38c-233">It's determined by the redo log, physical reads, and writes rate.</span></span>

![Zrzut ekranu przedstawiający stronę raportu AWR](./media/oracle-design/awr_report.png)

<span data-ttu-id="7d38c-235">Na przykład rozmiar Powtórz jest 12,200,000 bajtów na sekundę, która jest równa 11.63 MB/s.</span><span class="sxs-lookup"><span data-stu-id="7d38c-235">For example, the redo size is 12,200,000 bytes per second, which is equal to 11.63 MBPs.</span></span>
<span data-ttu-id="7d38c-236">IOPS jest 12,200,000 / 2,358 = 5,174.</span><span class="sxs-lookup"><span data-stu-id="7d38c-236">The IOPS is 12,200,000 / 2,358 = 5,174.</span></span>

<span data-ttu-id="7d38c-237">Po umieszczeniu danych wymagań dotyczących operacji We/Wy, można wybrać kombinację dysków, które są najbardziej odpowiednie do spełnienia tych wymagań.</span><span class="sxs-lookup"><span data-stu-id="7d38c-237">After you have a clear picture of the I/O requirements, you can choose a combination of drives that are best suited to meet those requirements.</span></span>

<span data-ttu-id="7d38c-238">**Zalecenia**</span><span class="sxs-lookup"><span data-stu-id="7d38c-238">**Recommendations**</span></span>

- <span data-ttu-id="7d38c-239">Dla tabel danych rozłożyć obciążenie We/Wy na liczbę dysków za pomocą funkcji ASM Oracle lub zarządzanego magazynu.</span><span class="sxs-lookup"><span data-stu-id="7d38c-239">For data tablespace, spread the I/O workload across a number of disks by using managed storage or Oracle ASM.</span></span>
- <span data-ttu-id="7d38c-240">Jak zwiększa rozmiar bloku we/wy dla operacji intensywnego odczytu i zapisu intensywnie, Dodaj więcej dysków danych.</span><span class="sxs-lookup"><span data-stu-id="7d38c-240">As the I/O block size increases for read-intensive and write-intensive operations, add more data disks.</span></span>
- <span data-ttu-id="7d38c-241">Zwiększ rozmiar bloku dla dużych sekwencyjnych procesów.</span><span class="sxs-lookup"><span data-stu-id="7d38c-241">Increase the block size for large sequential processes.</span></span>
- <span data-ttu-id="7d38c-242">Umożliwia kompresję danych Zmniejsz we/wy (dla danych i indeksów).</span><span class="sxs-lookup"><span data-stu-id="7d38c-242">Use data compression to reduce I/O (for both data and indexes).</span></span>
- <span data-ttu-id="7d38c-243">Oddzielne Powtórz dzienniki systemu i temps, a cofnąć usług terminalowych na dyskach danych.</span><span class="sxs-lookup"><span data-stu-id="7d38c-243">Separate redo logs, system, and temps, and undo TS on separate data disks.</span></span>
- <span data-ttu-id="7d38c-244">Nie należy umieszczać plików aplikacji na domyślne dysków systemu operacyjnego (/ dev/sda).</span><span class="sxs-lookup"><span data-stu-id="7d38c-244">Don't put any application files on default OS disks (/dev/sda).</span></span> <span data-ttu-id="7d38c-245">Te dyski nie są zoptymalizowane dla maszyny Wirtualnej szybkiego czas uruchamiania i nie może zawierać dobrą wydajność aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7d38c-245">These disks aren't optimized for fast VM boot times, and they might not provide good performance for your application.</span></span>

### <a name="disk-cache-settings"></a><span data-ttu-id="7d38c-246">Ustawienia pamięci podręcznej dysku</span><span class="sxs-lookup"><span data-stu-id="7d38c-246">Disk cache settings</span></span>

<span data-ttu-id="7d38c-247">Istnieją trzy opcje buforowania na hoście:</span><span class="sxs-lookup"><span data-stu-id="7d38c-247">There are three options for host caching:</span></span>

- <span data-ttu-id="7d38c-248">*Tylko do odczytu*: wszystkie żądania są buforowane dla przyszłych operacji odczytu.</span><span class="sxs-lookup"><span data-stu-id="7d38c-248">*Read-only*: All requests are cached for future reads.</span></span> <span data-ttu-id="7d38c-249">Zapisuje wszystkie są zachowywane bezpośrednio do magazynu obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="7d38c-249">All writes are persisted directly to Azure Blob storage.</span></span>

- <span data-ttu-id="7d38c-250">*Odczyt i zapis*: jest to "odczytu z wyprzedzeniem" algorytmu.</span><span class="sxs-lookup"><span data-stu-id="7d38c-250">*Read-write*: This is a “read-ahead” algorithm.</span></span> <span data-ttu-id="7d38c-251">Odczyty i zapisy są buforowane dla przyszłych operacji odczytu.</span><span class="sxs-lookup"><span data-stu-id="7d38c-251">The reads and writes are cached for future reads.</span></span> <span data-ttu-id="7d38c-252">Zapisy non-write-through są zachowywane najpierw do lokalnej pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="7d38c-252">Non-write-through writes are persisted to the local cache first.</span></span> <span data-ttu-id="7d38c-253">Dla programu SQL Server zapisy są zachowywane do magazynu Azure, ponieważ używa go do zapisu.</span><span class="sxs-lookup"><span data-stu-id="7d38c-253">For SQL Server, writes are persisted to Azure Storage because it uses write-through.</span></span> <span data-ttu-id="7d38c-254">Zapewnia także uzyskać najmniejsze opóźnienia dysku światła obciążeń.</span><span class="sxs-lookup"><span data-stu-id="7d38c-254">It also provides the lowest disk latency for light workloads.</span></span>

- <span data-ttu-id="7d38c-255">*Brak* (wyłączone): za pomocą tej opcji, można pominąć pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="7d38c-255">*None* (disabled): By using this option, you can bypass the cache.</span></span> <span data-ttu-id="7d38c-256">Wszystkie dane są przekazywane na dysku i utrwalone w magazynie Azure.</span><span class="sxs-lookup"><span data-stu-id="7d38c-256">All the data is transferred to disk and persisted to Azure Storage.</span></span> <span data-ttu-id="7d38c-257">Ta metoda zapewnia najwyższy szybkości operacji We/Wy dla intensywnych obciążeń we/wy.</span><span class="sxs-lookup"><span data-stu-id="7d38c-257">This method gives you the highest I/O rate for I/O intensive workloads.</span></span> <span data-ttu-id="7d38c-258">Należy również wziąć pod uwagę "kosztów transakcji".</span><span class="sxs-lookup"><span data-stu-id="7d38c-258">You also need to take “transaction cost” into consideration.</span></span>

<span data-ttu-id="7d38c-259">**Zalecenia**</span><span class="sxs-lookup"><span data-stu-id="7d38c-259">**Recommendations**</span></span>

<span data-ttu-id="7d38c-260">Aby zmaksymalizować przepustowość, zaleca się uruchamiania z **Brak** dla buforowania na hoście.</span><span class="sxs-lookup"><span data-stu-id="7d38c-260">To maximize the throughput, we recommend that you  start with **None** for host caching.</span></span> <span data-ttu-id="7d38c-261">Dla usługi Premium Storage należy pamiętać o tym, czy należy wyłączyć "bariery" w przypadku zainstalowania systemu plików z **tylko do odczytu** lub **Brak** opcje.</span><span class="sxs-lookup"><span data-stu-id="7d38c-261">For Premium Storage, keep in mind that you must disable the "barriers" when you mount the file system with the **ReadOnly** or **None** options.</span></span> <span data-ttu-id="7d38c-262">Zaktualizuj plik /etc/fstab z identyfikatorem UUID na dyskach.</span><span class="sxs-lookup"><span data-stu-id="7d38c-262">Update the /etc/fstab file with the UUID to the disks.</span></span>

<span data-ttu-id="7d38c-263">Aby uzyskać więcej informacji, zobacz [magazyn w warstwie Premium dla maszyn wirtualnych systemu Linux](https://docs.microsoft.com/azure/storage/storage-premium-storage#premium-storage-for-linux-vms).</span><span class="sxs-lookup"><span data-stu-id="7d38c-263">For more information, see [Premium Storage for Linux VMs](https://docs.microsoft.com/azure/storage/storage-premium-storage#premium-storage-for-linux-vms).</span></span>

![Zrzut ekranu przedstawiający stronę dysków zarządzanych](./media/oracle-design/premium_disk02.png)

- <span data-ttu-id="7d38c-265">W przypadku dysków systemu operacyjnego, użyj domyślnej **odczytu/zapisu** buforowania.</span><span class="sxs-lookup"><span data-stu-id="7d38c-265">For OS disks, use default **Read/Write** caching.</span></span>
- <span data-ttu-id="7d38c-266">Dla systemu, TEMP i cofania użyj **Brak** do buforowania.</span><span class="sxs-lookup"><span data-stu-id="7d38c-266">For SYSTEM, TEMP, and UNDO use **None** for caching.</span></span>
- <span data-ttu-id="7d38c-267">W przypadku danych, użyj **Brak** do buforowania.</span><span class="sxs-lookup"><span data-stu-id="7d38c-267">For DATA, use **None** for caching.</span></span> <span data-ttu-id="7d38c-268">Ale jeśli bazy danych jest tylko do odczytu lub intensywnego odczytu, użyj **tylko do odczytu** buforowania.</span><span class="sxs-lookup"><span data-stu-id="7d38c-268">But if your database is read-only or read-intensive, use **Read-only** caching.</span></span>

<span data-ttu-id="7d38c-269">Po zapisaniu ustawień dysku danych, chyba że Odinstaluj dysku na poziomie systemu operacyjnego i ponownie zainstaluj po wprowadzeniu zmiany nie można zmienić ustawienia pamięci podręcznej hosta.</span><span class="sxs-lookup"><span data-stu-id="7d38c-269">After your data disk setting is saved, you can't change the host cache setting unless you unmount the drive at the OS level and then remount it after you've made the change.</span></span>


## <a name="security"></a><span data-ttu-id="7d38c-270">Bezpieczeństwo</span><span class="sxs-lookup"><span data-stu-id="7d38c-270">Security</span></span>

<span data-ttu-id="7d38c-271">Po Konfigurowanie i skonfigurowania środowiska platformy Azure, następnym krokiem jest zabezpieczenia sieci.</span><span class="sxs-lookup"><span data-stu-id="7d38c-271">After you have set up and configured your Azure environment, the next step is to secure your network.</span></span> <span data-ttu-id="7d38c-272">Poniżej przedstawiono kilka zaleceń:</span><span class="sxs-lookup"><span data-stu-id="7d38c-272">Here are some recommendations:</span></span>

- <span data-ttu-id="7d38c-273">*Zasady grupy NSG*: grupy NSG można zdefiniować przy podsieci lub kartę sieciową.</span><span class="sxs-lookup"><span data-stu-id="7d38c-273">*NSG policy*: NSG can be defined by a subnet or NIC.</span></span> <span data-ttu-id="7d38c-274">Jest łatwiejsze w celu kontroli dostępu na poziomie podsieci zarówno zabezpieczeń i Wymuś routingu dla elementów, jak zapór aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7d38c-274">It's simpler to control access at the subnet level both for security and force routing for things like application firewalls.</span></span>

- <span data-ttu-id="7d38c-275">*Jumpbox*: bezpieczniejszego dostępu administratorów nie należy bezpośrednio łączyć usługi aplikacji lub bazę danych.</span><span class="sxs-lookup"><span data-stu-id="7d38c-275">*Jumpbox*: For more secure access, administrators should not directly connect to the application service or database.</span></span> <span data-ttu-id="7d38c-276">Jumpbox jest używane jako nośniki między administratora komputera i zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7d38c-276">A jumpbox is used as a media between the administrator machine and Azure resources.</span></span>
<span data-ttu-id="7d38c-277">![Zrzut ekranu przedstawiający stronę topologii Jumpbox](./media/oracle-design/jumpbox.png)</span><span class="sxs-lookup"><span data-stu-id="7d38c-277">![Screenshot of the Jumpbox topology page](./media/oracle-design/jumpbox.png)</span></span>

    <span data-ttu-id="7d38c-278">Administrator komputera powinien oferować ograniczonej IP dostęp do jumpbox tylko.</span><span class="sxs-lookup"><span data-stu-id="7d38c-278">The administrator machine should offer IP-restricted access to the jumpbox only.</span></span> <span data-ttu-id="7d38c-279">Jumpbox powinien mieć dostęp do aplikacji i baz danych.</span><span class="sxs-lookup"><span data-stu-id="7d38c-279">The jumpbox should have access to the application and database.</span></span>

- <span data-ttu-id="7d38c-280">*Sieć prywatna* (podsieci): zaleca się, że masz aplikacji usługi i bazy danych w różnych podsieciach, lepszą kontrolę można ustawić przez zasady grupy NSG.</span><span class="sxs-lookup"><span data-stu-id="7d38c-280">*Private network* (subnets): We recommend that you have the application service and database on separate subnets, so better control can be set by NSG policy.</span></span>


## <a name="additional-reading"></a><span data-ttu-id="7d38c-281">Dodatkowe materiały</span><span class="sxs-lookup"><span data-stu-id="7d38c-281">Additional reading</span></span>

- [<span data-ttu-id="7d38c-282">Configure Oracle ASM (Konfigurowanie programu Oracle ASM)</span><span class="sxs-lookup"><span data-stu-id="7d38c-282">Configure Oracle ASM</span></span>](configure-oracle-asm.md)
- [<span data-ttu-id="7d38c-283">Skonfiguruj Oracle Data Guard</span><span class="sxs-lookup"><span data-stu-id="7d38c-283">Configure Oracle Data Guard</span></span>](configure-oracle-dataguard.md)
- [<span data-ttu-id="7d38c-284">Konfigurowanie bramy Golden Oracle</span><span class="sxs-lookup"><span data-stu-id="7d38c-284">Configure Oracle Golden Gate</span></span>](configure-oracle-golden-gate.md)
- [<span data-ttu-id="7d38c-285">Oracle kopii zapasowych i odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="7d38c-285">Oracle backup and recovery</span></span>](oracle-backup-recovery.md)

## <a name="next-steps"></a><span data-ttu-id="7d38c-286">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7d38c-286">Next steps</span></span>

- [<span data-ttu-id="7d38c-287">Samouczek: Tworzenie maszyn wirtualnych wysokiej dostępności</span><span class="sxs-lookup"><span data-stu-id="7d38c-287">Tutorial: Create highly available VMs</span></span>](../../linux/create-cli-complete.md)
- [<span data-ttu-id="7d38c-288">Eksploruj przykłady Azure CLI wdrożenia maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="7d38c-288">Explore VM deployment Azure CLI samples</span></span>](../../linux/cli-samples.md)
