---
title: "Rozwiązywanie problemów i monitorowanie SAP HANA na platformie Azure (wystąpienia duże) | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów i monitorowanie SAP HANA na platformie Azure (wystąpienia duże)."
services: virtual-machines-linux
documentationcenter: 
author: RicksterCDN
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/01/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ee5be707b443cbe42bf4a492d79390e534d4b91f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-troubleshoot-and-monitor-sap-hana-large-instances-on-azure"></a><span data-ttu-id="4af78-103">Rozwiązywanie problemów i monitorować SAP HANA (duże wystąpień) w systemie Azure</span><span class="sxs-lookup"><span data-stu-id="4af78-103">How to troubleshoot and monitor SAP HANA (large instances) on Azure</span></span>


## <a name="monitoring-in-sap-hana-on-azure-large-instances"></a><span data-ttu-id="4af78-104">Monitorowanie SAP HANA na platformie Azure (wystąpienia duże)</span><span class="sxs-lookup"><span data-stu-id="4af78-104">Monitoring in SAP HANA on Azure (Large Instances)</span></span>

<span data-ttu-id="4af78-105">SAP HANA na platformie Azure (wystąpienia duże) nie różni się od innych wdrożeń IaaS — należy monitorować systemu operacyjnego i aplikacji czynności oraz jak korzystać z tych następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="4af78-105">SAP HANA on Azure (Large Instances) is no different from any other IaaS deployment — you need to monitor what the OS and the application is doing and how these consume the following resources:</span></span>

- <span data-ttu-id="4af78-106">Procesor CPU</span><span class="sxs-lookup"><span data-stu-id="4af78-106">CPU</span></span>
- <span data-ttu-id="4af78-107">Memory (Pamięć)</span><span class="sxs-lookup"><span data-stu-id="4af78-107">Memory</span></span>
- <span data-ttu-id="4af78-108">Przepustowość sieci</span><span class="sxs-lookup"><span data-stu-id="4af78-108">Network bandwidth</span></span>
- <span data-ttu-id="4af78-109">Miejsce na dysku</span><span class="sxs-lookup"><span data-stu-id="4af78-109">Disk space</span></span>

<span data-ttu-id="4af78-110">Zgodnie z maszyn wirtualnych Azure należy ustalić czy klasy zasobów o nazwie powyżej są wystarczające, lub czy pobrać te wyczerpany.</span><span class="sxs-lookup"><span data-stu-id="4af78-110">As with Azure Virtual Machines you need to figure out whether the resource classes named above are sufficient, or whether these get depleted.</span></span> <span data-ttu-id="4af78-111">Poniżej przedstawiono więcej szczegółów na każdym z różnych klas:</span><span class="sxs-lookup"><span data-stu-id="4af78-111">Here is more detail on each of the different classes:</span></span>

<span data-ttu-id="4af78-112">**Zużycie zasobów procesora CPU:** współczynnik SAP zdefiniowane dla niektórych obciążeń przed HANA jest wymuszana aby upewnić się, że powinien być wystarczająco dużo zasobów procesora CPU do pracy za pośrednictwem dane, które są przechowywane w pamięci.</span><span class="sxs-lookup"><span data-stu-id="4af78-112">**CPU resource consumption:** The ratio that SAP defined for certain workload against HANA is enforced to make sure that there should be enough CPU resources available to work through the data that is stored in memory.</span></span> <span data-ttu-id="4af78-113">Niemniej jednak może być przypadki, w którym HANA zużywa dużo Procesora wykonywania zapytań ze względu na brakujące indeksy lub podobne problemy.</span><span class="sxs-lookup"><span data-stu-id="4af78-113">Nevertheless, there might be cases where HANA consumes a lot of CPU executing queries due to missing indexes or similar issues.</span></span> <span data-ttu-id="4af78-114">Oznacza to, że należy monitorować zużycia zasobów procesora CPU HANA dużych wystąpienia jednostki, a także zasobów Procesora używanych przez określone usługi HANA.</span><span class="sxs-lookup"><span data-stu-id="4af78-114">This means you should monitor CPU resource consumption of the HANA large instance unit as well as CPU resources consumed by the specific HANA services.</span></span>

<span data-ttu-id="4af78-115">**Zużycie pamięci:** ważne jest, aby monitorować z wewnątrz HANA, a także poza HANA w jednostce.</span><span class="sxs-lookup"><span data-stu-id="4af78-115">**Memory consumption:** Is important to monitor from within HANA, as well as outside of HANA on the unit.</span></span> <span data-ttu-id="4af78-116">W ramach HANA monitorowanie, jak danych zajmuje przydzielonej pamięci, aby wypełnić założenia wymagane zmiany rozmiaru SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="4af78-116">Within HANA, monitor how the data is consuming HANA allocated memory in order to stay within the required sizing guidelines of SAP.</span></span> <span data-ttu-id="4af78-117">Należy monitorować zużycie pamięci na poziomie wystąpienia duży do upewnij się, że dodatkowe zainstalowanych z systemem innym niż — HANA oprogramowania nie zużywa zbyt dużej ilości pamięci i w związku z tym konkurują ze HANA pamięci.</span><span class="sxs-lookup"><span data-stu-id="4af78-117">You also want to monitor memory consumption on the Large Instance level to make sure that additional installed non-HANA software does not consume too much memory, and therefore compete with HANA for memory.</span></span>

<span data-ttu-id="4af78-118">**Przepustowość sieci:** bramy sieci wirtualnej Azure ma ograniczoną przepustowość danych do sieci wirtualnej Azure, więc jest przydatne do monitorowania danych odebranych przez wszystkie maszyny wirtualne Azure w ramach sieci wirtualnej, aby dowiedzieć się, jak blisko zostaną limitów jednostka SKU bramy Azure możesz zaznaczenia ected.</span><span class="sxs-lookup"><span data-stu-id="4af78-118">**Network bandwidth:** The Azure VNet gateway is limited in bandwidth of data moving into the Azure VNet, so it is helpful to monitor the data received by all the Azure VMs within a VNet to figure out how close you are to the limits of the Azure gateway SKU you selected.</span></span> <span data-ttu-id="4af78-119">W jednostce wystąpienia dużych HANA go sensu przychodzący i wychodzący ruch sieciowy również monitorować i do śledzenia w woluminach, które są obsługiwane w czasie.</span><span class="sxs-lookup"><span data-stu-id="4af78-119">On the HANA Large Instance unit, it does make sense to monitor incoming and outgoing network traffic as well, and to keep track of the volumes that are handled over time.</span></span>

<span data-ttu-id="4af78-120">**Miejsce na dysku:** użycie miejsca na dysku zwykle zwiększa się wraz z upływem czasu.</span><span class="sxs-lookup"><span data-stu-id="4af78-120">**Disk space:** Disk space consumption usually increases over time.</span></span> <span data-ttu-id="4af78-121">Istnieje wiele powodów, ale większość wszystkich: wzrasta ilość danych, wykonywania kopii zapasowej dziennika transakcji, przechowywanie plików śledzenia i wykonywania migawek magazynu.</span><span class="sxs-lookup"><span data-stu-id="4af78-121">There are many reasons for this, but most of all are: data volume increases, execution of transaction log backups, storing trace files, and performing storage snapshots.</span></span> <span data-ttu-id="4af78-122">Dlatego jest ważne monitorować użycie miejsca na dysku i zarządzać nimi skojarzonego z jednostką HANA wystąpienia duża ilość miejsca na dysku.</span><span class="sxs-lookup"><span data-stu-id="4af78-122">Therefore, it is important to monitor disk space usage and manage the disk space associated with the HANA Large Instance unit.</span></span>

## <a name="monitoring-and-troubleshooting-from-hana-side"></a><span data-ttu-id="4af78-123">Monitorowanie i rozwiązywanie problemów z HANA strony</span><span class="sxs-lookup"><span data-stu-id="4af78-123">Monitoring and troubleshooting from HANA side</span></span>

<span data-ttu-id="4af78-124">Aby skutecznie analizować problemy związane z SAP HANA na platformie Azure (wystąpienia duże), jest przydatne do zawężania główną przyczynę problemu.</span><span class="sxs-lookup"><span data-stu-id="4af78-124">In order to effectively analyze problems related to SAP HANA on Azure (Large Instances), it is useful to narrow down the root cause of a problem.</span></span> <span data-ttu-id="4af78-125">SAP został opublikowany dużą ilość dokumentację ułatwiającą.</span><span class="sxs-lookup"><span data-stu-id="4af78-125">SAP has published a large amount of documentation to help you.</span></span>

<span data-ttu-id="4af78-126">Dotyczy — często zadawane pytania dotyczące wydajności SAP HANA znajdują się w uwagach SAP do następujących:</span><span class="sxs-lookup"><span data-stu-id="4af78-126">Applicable FAQs related to SAP HANA performance can be found in the following SAP Notes:</span></span>

- [<span data-ttu-id="4af78-127">Uwaga SAP #2222200 — często zadawane pytania: SAP HANA sieci</span><span class="sxs-lookup"><span data-stu-id="4af78-127">SAP Note #2222200 – FAQ: SAP HANA Network</span></span>](https://launchpad.support.sap.com/#/notes/2222200)
- [<span data-ttu-id="4af78-128">Uwaga SAP #2100040 — często zadawane pytania: SAP HANA Procesora</span><span class="sxs-lookup"><span data-stu-id="4af78-128">SAP Note #2100040 – FAQ: SAP HANA CPU</span></span>](https://launchpad.support.sap.com/#/notes/0002100040)
- [<span data-ttu-id="4af78-129">Uwaga SAP #199997 — często zadawane pytania: SAP HANA pamięci</span><span class="sxs-lookup"><span data-stu-id="4af78-129">SAP Note #199997 – FAQ: SAP HANA Memory</span></span>](https://launchpad.support.sap.com/#/notes/2177064)
- [<span data-ttu-id="4af78-130">SAP Uwaga #200000 — często zadawane pytania: Optymalizacja wydajności HANA SAP</span><span class="sxs-lookup"><span data-stu-id="4af78-130">SAP Note #200000 – FAQ: SAP HANA Performance Optimization</span></span>](https://launchpad.support.sap.com/#/notes/2000000)
- [<span data-ttu-id="4af78-131">Uwaga SAP #199930 — często zadawane pytania: SAP HANA we/wy analizy</span><span class="sxs-lookup"><span data-stu-id="4af78-131">SAP Note #199930 – FAQ: SAP HANA I/O Analysis</span></span>](https://launchpad.support.sap.com/#/notes/1999930)
- [<span data-ttu-id="4af78-132">Uwaga SAP #2177064 — często zadawane pytania: Uruchom ponownie SAP HANA usługi i awarii</span><span class="sxs-lookup"><span data-stu-id="4af78-132">SAP Note #2177064 – FAQ: SAP HANA Service Restart and Crashes</span></span>](https://launchpad.support.sap.com/#/notes/2177064)

<span data-ttu-id="4af78-133">**SAP HANA alertów**</span><span class="sxs-lookup"><span data-stu-id="4af78-133">**SAP HANA Alerts**</span></span>

<span data-ttu-id="4af78-134">Pierwszym krokiem zapoznaj się z dziennikami alertu bieżącego SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="4af78-134">As a first step, check the current SAP HANA alert logs.</span></span> <span data-ttu-id="4af78-135">W systemie SAP HANA Studio przejdź do **konsoli administracyjnej: alerty: Pokaż: wszystkie alerty**.</span><span class="sxs-lookup"><span data-stu-id="4af78-135">In SAP HANA Studio, go to **Administration Console: Alerts: Show: all alerts**.</span></span> <span data-ttu-id="4af78-136">Na tej karcie zostaną wyświetlone wszystkie alerty SAP HANA określone wartości (wolnej pamięci fizycznej, użycie procesora CPU, itp.), które dzielą się poza Ustaw progi minimalną i maksymalną.</span><span class="sxs-lookup"><span data-stu-id="4af78-136">This tab will show all SAP HANA alerts for specific values (free physical memory, CPU utilization, etc.) that fall outside of the set minimum and maximum thresholds.</span></span> <span data-ttu-id="4af78-137">Domyślnie sprawdza są odświeżane automatycznie co 15 minut.</span><span class="sxs-lookup"><span data-stu-id="4af78-137">By default, checks are auto-refreshed every 15 minutes.</span></span>

![W systemie SAP HANA Studio przejdź do konsoli administracyjnej: alerty: Pokaż: wszystkie alerty](./media/troubleshooting-monitoring/image1-show-alerts.png)

<span data-ttu-id="4af78-139">**PROCESOR CPU**</span><span class="sxs-lookup"><span data-stu-id="4af78-139">**CPU**</span></span>

<span data-ttu-id="4af78-140">Alert wywołany z powodu ustawienia nieprawidłowej wartości progowej rozwiązanie jest resetowane do wartości domyślnej lub bardziej przystępne wartość progową.</span><span class="sxs-lookup"><span data-stu-id="4af78-140">For an alert triggered due to improper threshold setting, a resolution is to reset to the default value or a more reasonable threshold value.</span></span>

![Zresetuj wartość domyślną lub bardziej przystępne wartość progu](./media/troubleshooting-monitoring/image2-cpu-utilization.png)

<span data-ttu-id="4af78-142">Następujące alerty może wskazywać na problemy z zasobami Procesora:</span><span class="sxs-lookup"><span data-stu-id="4af78-142">The following alerts may indicate CPU resource problems:</span></span>

- <span data-ttu-id="4af78-143">Użycie procesora CPU hosta (alertu 5)</span><span class="sxs-lookup"><span data-stu-id="4af78-143">Host CPU Usage (Alert 5)</span></span>
- <span data-ttu-id="4af78-144">Operacja punktu zapisu najnowszych (28 alertów)</span><span class="sxs-lookup"><span data-stu-id="4af78-144">Most recent savepoint operation (Alert 28)</span></span>
- <span data-ttu-id="4af78-145">Czas trwania punktu zapisu (54 alertów)</span><span class="sxs-lookup"><span data-stu-id="4af78-145">Savepoint duration (Alert 54)</span></span>

<span data-ttu-id="4af78-146">Można zauważyć wysokie użycie procesora CPU w Twojej bazie danych SAP HANA z jednego z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="4af78-146">You may notice high CPU consumption on your SAP HANA database from one of the following:</span></span>

- <span data-ttu-id="4af78-147">Alert 5 (użycie procesora CPU hosta) jest wywoływane bieżące lub wcześniejsze użycia procesora CPU</span><span class="sxs-lookup"><span data-stu-id="4af78-147">Alert 5 (Host CPU usage) is raised for current or past CPU usage</span></span>
- <span data-ttu-id="4af78-148">Użycie procesora CPU wyświetlanych na ekranie — omówienie</span><span class="sxs-lookup"><span data-stu-id="4af78-148">The displayed CPU usage on the overview screen</span></span>

![Wyświetlane użycie procesora CPU na ekran Przegląd](./media/troubleshooting-monitoring/image3-cpu-usage.png)

<span data-ttu-id="4af78-150">W przeszłości wykres obciążenia mogą być wyświetlane wysokie użycie procesora CPU lub wysokie zużycie:</span><span class="sxs-lookup"><span data-stu-id="4af78-150">The Load graph might show high CPU consumption, or high consumption in the past:</span></span>

![Wykres obciążenia mogą być wyświetlane w przeszłości wysokie użycie procesora CPU lub wysokie zużycie](./media/troubleshooting-monitoring/image4-load-graph.png)

<span data-ttu-id="4af78-152">Alert wyzwolony ze względu na wysokie wykorzystanie procesora CPU może być spowodowane przez kilka przyczyn, w tym między innymi: wykonanie pewnych transakcji, ładowanie danych, wysunięć zadania, długotrwałą instrukcji SQL i wydajności zapytania (na przykład z BW na HANA moduły).</span><span class="sxs-lookup"><span data-stu-id="4af78-152">An alert triggered due to high CPU utilization could be caused by several reasons, including, but not limited to: execution of certain transactions, data loading, hanging of jobs, long running SQL statements, and bad query performance (for example, with BW on HANA cubes).</span></span>

<span data-ttu-id="4af78-153">Zapoznaj się [SAP HANA Rozwiązywanie problemów z: pokrewne powoduje procesora CPU i rozwiązań](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4f/bc915462db406aa2fe92b708b95189/content.htm?frameset=/en/db/6ca50424714af8b370960c04ce667b/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=46&amp;show_children=false) lokacji szczegółowe kroki rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="4af78-153">Refer to the [SAP HANA Troubleshooting: CPU Related Causes and Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4f/bc915462db406aa2fe92b708b95189/content.htm?frameset=/en/db/6ca50424714af8b370960c04ce667b/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=46&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="4af78-154">**System operacyjny**</span><span class="sxs-lookup"><span data-stu-id="4af78-154">**Operating System**</span></span>

<span data-ttu-id="4af78-155">Jednym z najważniejszych wyszukuje SAP HANA w systemie Linux jest upewnij się, że wyłączono przezroczysty dużych stron, zobacz [&#2131662; Uwaga SAP — przezroczysty dużych stron (THP) na serwerach z SAP HANA](https://launchpad.support.sap.com/#/notes/2131662).</span><span class="sxs-lookup"><span data-stu-id="4af78-155">One of the most important checks for SAP HANA on Linux is to make sure that Transparent Huge Pages are disabled, see [SAP Note #2131662 – Transparent Huge Pages (THP) on SAP HANA Servers](https://launchpad.support.sap.com/#/notes/2131662).</span></span>

- <span data-ttu-id="4af78-156">Możesz sprawdzić, czy przezroczyste dużych stron są włączone, za pomocą następującego polecenia Linux: **cat /sys/kernel/mm/transparent\_hugepage lub nie włączono**</span><span class="sxs-lookup"><span data-stu-id="4af78-156">You can check if Transparent Huge Pages are enabled through the following Linux command: **cat /sys/kernel/mm/transparent\_hugepage/enabled**</span></span>
- <span data-ttu-id="4af78-157">Jeśli _zawsze_ jest ujęta w nawiasy kwadratowe zgodnie z poniższymi instrukcjami, oznacza to, czy przezroczyste dużych stron są włączone: [zawsze] madvise nigdy nie; Jeśli _nigdy nie_ jest ujęta w nawiasy kwadratowe zgodnie z poniższymi instrukcjami, oznacza, że ogromnych przezroczysty Strony są wyłączone: zawsze madvise [nigdy nie]</span><span class="sxs-lookup"><span data-stu-id="4af78-157">If _always_ is enclosed in brackets as below, it means that the Transparent Huge Pages are enabled: [always] madvise never; if _never_ is enclosed in brackets as below, it means that the Transparent Huge Pages are disabled: always madvise [never]</span></span>

<span data-ttu-id="4af78-158">Polecenie Linux powinien zwrócić nic: **obr. / min — odpowiedzi na pytania | grep ulimit.**</span><span class="sxs-lookup"><span data-stu-id="4af78-158">The following Linux command should return nothing: **rpm -qa | grep ulimit.**</span></span> <span data-ttu-id="4af78-159">Jeśli zostanie wyświetlona _ulimit_ jest zainstalowane, odinstaluj go bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="4af78-159">If it appears _ulimit_ is installed, uninstall it immediately.</span></span>

<span data-ttu-id="4af78-160">**Pamięci**</span><span class="sxs-lookup"><span data-stu-id="4af78-160">**Memory**</span></span>

<span data-ttu-id="4af78-161">Można zauważyć, że ilość pamięci przydzielonej przez bazę danych SAP HANA jest większa niż oczekiwano.</span><span class="sxs-lookup"><span data-stu-id="4af78-161">You may observe that the amount of memory allocated by the SAP HANA database is higher than expected.</span></span> <span data-ttu-id="4af78-162">Następujące alerty wskazują na problemy z wysokie użycie pamięci:</span><span class="sxs-lookup"><span data-stu-id="4af78-162">The following alerts indicate issues with high memory usage:</span></span>

- <span data-ttu-id="4af78-163">Użycie pamięci fizycznej hosta (alertu 1)</span><span class="sxs-lookup"><span data-stu-id="4af78-163">Host physical memory usage (Alert 1)</span></span>
- <span data-ttu-id="4af78-164">Użycie pamięci serwera nazw (12 alertów)</span><span class="sxs-lookup"><span data-stu-id="4af78-164">Memory usage of name server (Alert 12)</span></span>
- <span data-ttu-id="4af78-165">Łączne użycie pamięci magazynu kolumn w tabelach (40 alertów)</span><span class="sxs-lookup"><span data-stu-id="4af78-165">Total memory usage of Column Store tables (Alert 40)</span></span>
- <span data-ttu-id="4af78-166">Użycie pamięci usług (43 alertów)</span><span class="sxs-lookup"><span data-stu-id="4af78-166">Memory usage of services (Alert 43)</span></span>
- <span data-ttu-id="4af78-167">Użycie pamięci magazynu głównego magazynu kolumn tabel (45 alertów)</span><span class="sxs-lookup"><span data-stu-id="4af78-167">Memory usage of main storage of Column Store tables (Alert 45)</span></span>
- <span data-ttu-id="4af78-168">Pliki zrzutu środowiska uruchomieniowego (46 alertów)</span><span class="sxs-lookup"><span data-stu-id="4af78-168">Runtime dump files (Alert 46)</span></span>

<span data-ttu-id="4af78-169">Zapoznaj się [SAP HANA rozwiązywania problemów: problemy z pamięcią](http://help.sap.com/saphelp_hanaplatform/helpdata/en/db/6ca50424714af8b370960c04ce667b/content.htm?frameset=/en/59/5eaa513dde43758b51378ab3315ebb/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=26&amp;show_children=false) lokacji szczegółowe kroki rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="4af78-169">Refer to the [SAP HANA Troubleshooting: Memory Problems](http://help.sap.com/saphelp_hanaplatform/helpdata/en/db/6ca50424714af8b370960c04ce667b/content.htm?frameset=/en/59/5eaa513dde43758b51378ab3315ebb/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=26&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="4af78-170">**Sieć**</span><span class="sxs-lookup"><span data-stu-id="4af78-170">**Network**</span></span>

<span data-ttu-id="4af78-171">Zapoznaj się [SAP Uwaga #2081065 — Rozwiązywanie problemów z programem SAP HANA sieci](https://launchpad.support.sap.com/#/notes/2081065) i wykonywać rozwiązywania problemów w tej uwagi SAP sieciowych.</span><span class="sxs-lookup"><span data-stu-id="4af78-171">Refer to [SAP Note #2081065 – Troubleshooting SAP HANA Network](https://launchpad.support.sap.com/#/notes/2081065) and perform the network troubleshooting steps in this SAP Note.</span></span>

1. <span data-ttu-id="4af78-172">Analizowanie czasu Rundy między serwerem a klientem.</span><span class="sxs-lookup"><span data-stu-id="4af78-172">Analyzing round-trip time between server and client.</span></span>
  <span data-ttu-id="4af78-173">A.</span><span class="sxs-lookup"><span data-stu-id="4af78-173">A.</span></span> <span data-ttu-id="4af78-174">Uruchom skrypt SQL [ _HANA\_sieci\_klientów_](https://launchpad.support.sap.com/#/notes/1969700)_._</span><span class="sxs-lookup"><span data-stu-id="4af78-174">Run the SQL script [_HANA\_Network\_Clients_](https://launchpad.support.sap.com/#/notes/1969700)_._</span></span>
  
2. <span data-ttu-id="4af78-175">Przeanalizuj komunikacji między węzłami.</span><span class="sxs-lookup"><span data-stu-id="4af78-175">Analyze internode communication.</span></span>
  <span data-ttu-id="4af78-176">A.</span><span class="sxs-lookup"><span data-stu-id="4af78-176">A.</span></span> <span data-ttu-id="4af78-177">Uruchom skrypt SQL [ _HANA\_sieci\_usług_](https://launchpad.support.sap.com/#/notes/1969700)_._</span><span class="sxs-lookup"><span data-stu-id="4af78-177">Run SQL script [_HANA\_Network\_Services_](https://launchpad.support.sap.com/#/notes/1969700)_._</span></span>

3. <span data-ttu-id="4af78-178">Uruchom polecenie Linux **ifconfig** (dane wyjściowe zawierają, jeśli występują strat pakietów).</span><span class="sxs-lookup"><span data-stu-id="4af78-178">Run Linux command **ifconfig** (the output shows if any packet losses are occurring).</span></span>
4. <span data-ttu-id="4af78-179">Uruchom polecenie Linux **tcpdump**.</span><span class="sxs-lookup"><span data-stu-id="4af78-179">Run Linux command **tcpdump**.</span></span>

<span data-ttu-id="4af78-180">Należy także użyć typu open source [dotyczące programu Iperf;](https://iperf.fr/) narzędzia (lub podobny) do mierzenia wydajności sieci rzeczywistej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4af78-180">Also, use the open source [IPERF](https://iperf.fr/) tool (or similar) to measure real application network performance.</span></span>

<span data-ttu-id="4af78-181">Zapoznaj się [SAP HANA rozwiązywania problemów: wydajność sieci i występują problemy z łącznością](http://help.sap.com/saphelp_hanaplatform/helpdata/en/a3/ccdff1aedc4720acb24ed8826938b6/content.htm?frameset=/en/dc/6ff98fa36541e997e4c719a632cbd8/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=142&amp;show_children=false) lokacji szczegółowe kroki rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="4af78-181">Refer to the [SAP HANA Troubleshooting: Networking Performance and Connectivity Problems](http://help.sap.com/saphelp_hanaplatform/helpdata/en/a3/ccdff1aedc4720acb24ed8826938b6/content.htm?frameset=/en/dc/6ff98fa36541e997e4c719a632cbd8/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=142&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="4af78-182">**Storage**</span><span class="sxs-lookup"><span data-stu-id="4af78-182">**Storage**</span></span>

<span data-ttu-id="4af78-183">Z perspektywy użytkownika końcowego aplikacja (lub system jako całość) działa wolno, nie odpowiada lub nawet może wydawać się zawieszenie, jeśli występują problemy z wydajnością we/wy.</span><span class="sxs-lookup"><span data-stu-id="4af78-183">From an end-user perspective, an application (or the system as a whole) runs sluggishly, is unresponsive, or can even seem to hang if there are issues with I/O performance.</span></span> <span data-ttu-id="4af78-184">W **woluminów** kartę w SAP HANA Studio widoczne dołączone woluminy i woluminy są używane przez każdej usługi.</span><span class="sxs-lookup"><span data-stu-id="4af78-184">In the **Volumes** tab in SAP HANA Studio, you can see the attached volumes, and what volumes are used by each service.</span></span>

![Na karcie woluminy w SAP HANA Studio widoczne dołączone woluminy i woluminy są używane przez każdego usługi](./media/troubleshooting-monitoring/image5-volumes-tab-a.png)

<span data-ttu-id="4af78-186">Dołączone woluminy w dolnej części ekranu można wyświetlić szczegóły woluminów, takie jak pliki i statystyki we/wy.</span><span class="sxs-lookup"><span data-stu-id="4af78-186">Attached volumes in the lower part of the screen you can see details of the volumes, such as files and I/O statistics.</span></span>

![Dołączone woluminy w dolnej części ekranu można wyświetlić szczegóły woluminów, takie jak pliki i statystyki we/wy](./media/troubleshooting-monitoring/image6-volumes-tab-b.png)

<span data-ttu-id="4af78-188">Zapoznaj się [SAP HANA Rozwiązywanie problemów z: We/Wy pokrewne główne przyczyny i rozwiązania](http://help.sap.com/saphelp_hanaplatform/helpdata/en/dc/6ff98fa36541e997e4c719a632cbd8/content.htm?frameset=/en/47/4cb08a715c42fe9f7cc5efdc599959/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=55&amp;show_children=false) i [SAP HANA Rozwiązywanie problemów z: dysku pokrewne główne przyczyny i rozwiązania](http://help.sap.com/saphelp_hanaplatform/helpdata/en/47/4cb08a715c42fe9f7cc5efdc599959/content.htm?frameset=/en/44/3e1db4f73d42da859008df4f69e37a/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=53&amp;show_children=false) lokacji szczegółowe kroki rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="4af78-188">Refer to the [SAP HANA Troubleshooting: I/O Related Root Causes and Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/dc/6ff98fa36541e997e4c719a632cbd8/content.htm?frameset=/en/47/4cb08a715c42fe9f7cc5efdc599959/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=55&amp;show_children=false) and [SAP HANA Troubleshooting: Disk Related Root Causes and Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/47/4cb08a715c42fe9f7cc5efdc599959/content.htm?frameset=/en/44/3e1db4f73d42da859008df4f69e37a/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=53&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="4af78-189">**Narzędzia diagnostyczne**</span><span class="sxs-lookup"><span data-stu-id="4af78-189">**Diagnostic Tools**</span></span>

<span data-ttu-id="4af78-190">Wykonaj sprawdzenie kondycji programu SAP HANA za pośrednictwem HANA\_konfiguracji\_Minichecks.</span><span class="sxs-lookup"><span data-stu-id="4af78-190">Perform an SAP HANA Health Check through HANA\_Configuration\_Minichecks.</span></span> <span data-ttu-id="4af78-191">To narzędzie zwraca potencjalnie krytycznych problemów technicznych, które powinny już mieć został zgłoszony jako ostrzeżenia w SAP HANA Studio.</span><span class="sxs-lookup"><span data-stu-id="4af78-191">This tool returns potentially critical technical issues that should have already been raised as alerts in SAP HANA Studio.</span></span>

<span data-ttu-id="4af78-192">Zapoznaj się [&#1969700; Uwaga SAP — kolekcja instrukcji SQL dla SAP HANA](https://launchpad.support.sap.com/#/notes/1969700) i Pobierz plik SQL Statements.zip dołączony do tej uwagi.</span><span class="sxs-lookup"><span data-stu-id="4af78-192">Refer to [SAP Note #1969700 – SQL statement collection for SAP HANA](https://launchpad.support.sap.com/#/notes/1969700) and download the SQL Statements.zip file attached to that note.</span></span> <span data-ttu-id="4af78-193">Należy zapisać ten plik zip na lokalnym dysku twardym.</span><span class="sxs-lookup"><span data-stu-id="4af78-193">Store this .zip file on the local hard drive.</span></span>

<span data-ttu-id="4af78-194">W systemie SAP HANA Studio na **informacje o systemie** karcie, kliknij prawym przyciskiem myszy w **nazwa** kolumny i wybierz **instrukcje SQL importu**.</span><span class="sxs-lookup"><span data-stu-id="4af78-194">In SAP HANA Studio, on the **System Information** tab, right-click in the **Name** column and select **Import SQL Statements**.</span></span>

![W SAP HANA Studio, na karcie informacji o systemie kliknij prawym przyciskiem myszy nazwę kolumny, a następnie wybierz importu instrukcje SQL](./media/troubleshooting-monitoring/image7-import-statements-a.png)

<span data-ttu-id="4af78-196">Wybierz plik SQL Statements.zip przechowywane lokalnie, a nie zostaną zaimportowane do folderu z odpowiedniej instrukcji SQL.</span><span class="sxs-lookup"><span data-stu-id="4af78-196">Select the SQL Statements.zip file stored locally, and a folder with the corresponding SQL statements will be imported.</span></span> <span data-ttu-id="4af78-197">W tym momencie można uruchomić wiele różnych kontroli diagnostycznych z tych instrukcji SQL.</span><span class="sxs-lookup"><span data-stu-id="4af78-197">At this point, the many different diagnostic checks can be run with these SQL statements.</span></span>

<span data-ttu-id="4af78-198">Na przykład, aby sprawdzić wymagania dotyczące przepustowości replikacji systemu SAP HANA, kliknij prawym przyciskiem myszy **przepustowości** instrukcji w obszarze **replikacji: przepustowości** i wybierz **Otwórz** w Konsola programu SQL.</span><span class="sxs-lookup"><span data-stu-id="4af78-198">For example, to test SAP HANA System Replication bandwidth requirements, right-click the **Bandwidth** statement under **Replication: Bandwidth** and select **Open** in SQL Console.</span></span>

<span data-ttu-id="4af78-199">Pełną instrukcję SQL zostanie otwarty, umożliwiając parametrów wejściowych (modyfikacji sekcja) zostać zmienione, a następnie wykonać.</span><span class="sxs-lookup"><span data-stu-id="4af78-199">The complete SQL statement opens allowing input parameters (modification section) to be changed and then executed.</span></span>

![Otwiera pełną instrukcję SQL stosowanie parametrów wejściowych (modyfikacji sekcja) zostać zmienione, a następnie wykonać](./media/troubleshooting-monitoring/image8-import-statements-b.png)

<span data-ttu-id="4af78-201">Innym przykładem jest kliknięcie prawym przyciskiem myszy w instrukcjach w obszarze **replikacji: omówienie**.</span><span class="sxs-lookup"><span data-stu-id="4af78-201">Another example is right-clicking on the statements under **Replication: Overview**.</span></span> <span data-ttu-id="4af78-202">Wybierz **Execute** z menu kontekstowego:</span><span class="sxs-lookup"><span data-stu-id="4af78-202">Select **Execute** from the context menu:</span></span>

![Innym przykładem jest kliknięcie prawym przyciskiem myszy w instrukcjach w ramach replikacji: omówienie.](./media/troubleshooting-monitoring/image9-import-statements-c.png)

<span data-ttu-id="4af78-205">Powoduje to informacje pomocne przy rozwiązywaniu problemów:</span><span class="sxs-lookup"><span data-stu-id="4af78-205">This results in information that helps with troubleshooting:</span></span>

![Spowoduje to informacje, które ułatwią rozwiązywanie problemów](./media/troubleshooting-monitoring/image10-import-statements-d.png)

<span data-ttu-id="4af78-207">Wykonaj te same czynności dla HANA\_konfiguracji\_Minichecks i zaznacz pole wyboru dla dowolnej _X_ oznacza w _C_ kolumny (krytyczne).</span><span class="sxs-lookup"><span data-stu-id="4af78-207">Do the same for HANA\_Configuration\_Minichecks and check for any _X_ marks in the _C_ (Critical) column.</span></span>

<span data-ttu-id="4af78-208">Przykładowe wyniki:</span><span class="sxs-lookup"><span data-stu-id="4af78-208">Sample outputs:</span></span>

<span data-ttu-id="4af78-209">**HANA\_konfiguracji\_MiniChecks\_Rev102.01 + 1** kontroli ogólne SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="4af78-209">**HANA\_Configuration\_MiniChecks\_Rev102.01+1** for general SAP HANA checks.</span></span>

![HANA\_konfiguracji\_MiniChecks\_Rev102.01 + 1 dla ogólnych kontroli SAP HANA](./media/troubleshooting-monitoring/image11-configuration-minichecks.png)

<span data-ttu-id="4af78-211">**HANA\_usług\_omówienie** omówienie co SAP HANA usługi są aktualnie uruchomione.</span><span class="sxs-lookup"><span data-stu-id="4af78-211">**HANA\_Services\_Overview** for an overview of what SAP HANA services are currently running.</span></span>

![HANA\_usług\_omówienie omówienie co SAP HANA usługi są aktualnie uruchomione](./media/troubleshooting-monitoring/image12-services-overview.png)

<span data-ttu-id="4af78-213">**HANA\_usług\_statystyki** dla SAP HANA usługi informacji (CPU, pamięci, itd.).</span><span class="sxs-lookup"><span data-stu-id="4af78-213">**HANA\_Services\_Statistics** for SAP HANA service information (CPU, memory, etc.).</span></span>

![<span data-ttu-id="4af78-214">HANA\_usług\_statystyki dla SAP HANA informacje o usługach</span><span class="sxs-lookup"><span data-stu-id="4af78-214">HANA\_Services\_Statistics for SAP HANA service information</span></span> ](./media/troubleshooting-monitoring/image13-services-statistics.png)

<span data-ttu-id="4af78-215">**HANA\_konfiguracji\_omówienie\_Rev110 +** ogólne informacje na temat wystąpienia SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="4af78-215">**HANA\_Configuration\_Overview\_Rev110+** for general information on the SAP HANA instance.</span></span>

![HANA\_konfiguracji\_omówienie\_Rev110 + ogólne informacje na temat wystąpienia SAP HANA](./media/troubleshooting-monitoring/image14-configuration-overview.png)

<span data-ttu-id="4af78-217">**HANA\_konfiguracji\_parametry\_Rev70 +** do sprawdzenia parametrów SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="4af78-217">**HANA\_Configuration\_Parameters\_Rev70+** to check SAP HANA parameters.</span></span>

![HANA\_konfiguracji\_parametry\_Rev70 +, aby sprawdzić SAP HANA parametrów](./media/troubleshooting-monitoring/image15-configuration-parameters.png)

