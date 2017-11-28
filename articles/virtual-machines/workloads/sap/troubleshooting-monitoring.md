---
title: "aaaTroubleshooting i monitorowania programu SAP HANA na platformie Azure (wystąpienia duże) | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 1f1cd35820e227fd99af495431cd4b826aa53600
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootroubleshoot-and-monitor-sap-hana-large-instances-on-azure"></a><span data-ttu-id="267d2-103">Jak tootroubleshoot i monitor SAP HANA (duże wystąpień) w systemie Azure</span><span class="sxs-lookup"><span data-stu-id="267d2-103">How tootroubleshoot and monitor SAP HANA (large instances) on Azure</span></span>


## <a name="monitoring-in-sap-hana-on-azure-large-instances"></a><span data-ttu-id="267d2-104">Monitorowanie SAP HANA na platformie Azure (wystąpienia duże)</span><span class="sxs-lookup"><span data-stu-id="267d2-104">Monitoring in SAP HANA on Azure (Large Instances)</span></span>

<span data-ttu-id="267d2-105">SAP HANA na platformie Azure (wystąpienia duże) nie różni się od innych wdrożeń IaaS — muszą toomonitor co hello systemu operacyjnego, a aplikacja hello jest to, jak korzystać z tych hello następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="267d2-105">SAP HANA on Azure (Large Instances) is no different from any other IaaS deployment — you need toomonitor what hello OS and hello application is doing and how these consume hello following resources:</span></span>

- <span data-ttu-id="267d2-106">Procesor CPU</span><span class="sxs-lookup"><span data-stu-id="267d2-106">CPU</span></span>
- <span data-ttu-id="267d2-107">Memory (Pamięć)</span><span class="sxs-lookup"><span data-stu-id="267d2-107">Memory</span></span>
- <span data-ttu-id="267d2-108">Przepustowość sieci</span><span class="sxs-lookup"><span data-stu-id="267d2-108">Network bandwidth</span></span>
- <span data-ttu-id="267d2-109">Miejsce na dysku</span><span class="sxs-lookup"><span data-stu-id="267d2-109">Disk space</span></span>

<span data-ttu-id="267d2-110">Zgodnie z maszyn wirtualnych Azure należy toofigure czy hello klasy zasobów o nazwie powyżej są wystarczające, lub czy pobrać te wyczerpany.</span><span class="sxs-lookup"><span data-stu-id="267d2-110">As with Azure Virtual Machines you need toofigure out whether hello resource classes named above are sufficient, or whether these get depleted.</span></span> <span data-ttu-id="267d2-111">Poniżej przedstawiono więcej szczegółów na każdym z różnych klas hello:</span><span class="sxs-lookup"><span data-stu-id="267d2-111">Here is more detail on each of hello different classes:</span></span>

<span data-ttu-id="267d2-112">**Zużycie zasobów procesora CPU:** hello zdefiniowanego dla niektórych obciążeń przed HANA SAP jest wymuszone toomake się upewnić, że powinien być za mało toowork dostępne zasoby procesora CPU przez hello dane są przechowywane w pamięci.</span><span class="sxs-lookup"><span data-stu-id="267d2-112">**CPU resource consumption:** hello ratio that SAP defined for certain workload against HANA is enforced toomake sure that there should be enough CPU resources available toowork through hello data that is stored in memory.</span></span> <span data-ttu-id="267d2-113">Niemniej jednak może być przypadki, w którym HANA zużywa wiele zasobów procesora, wykonywanie kwerend indeksów toomissing lub podobne problemy.</span><span class="sxs-lookup"><span data-stu-id="267d2-113">Nevertheless, there might be cases where HANA consumes a lot of CPU executing queries due toomissing indexes or similar issues.</span></span> <span data-ttu-id="267d2-114">Oznacza to, że należy monitorować zużycia zasobów procesora CPU hello HANA dużych wystąpienia jednostki, a także zasobów Procesora używanych przez hello określonych usług HANA.</span><span class="sxs-lookup"><span data-stu-id="267d2-114">This means you should monitor CPU resource consumption of hello HANA large instance unit as well as CPU resources consumed by hello specific HANA services.</span></span>

<span data-ttu-id="267d2-115">**Zużycie pamięci:** jest ważne toomonitor z wewnątrz HANA, a także poza HANA na powitania jednostki.</span><span class="sxs-lookup"><span data-stu-id="267d2-115">**Memory consumption:** Is important toomonitor from within HANA, as well as outside of HANA on hello unit.</span></span> <span data-ttu-id="267d2-116">W ramach HANA monitorować jak hello danych zajmuje przydzielonej pamięci w kolejności toostay w hello wymagane zmiany rozmiaru wytyczne SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="267d2-116">Within HANA, monitor how hello data is consuming HANA allocated memory in order toostay within hello required sizing guidelines of SAP.</span></span> <span data-ttu-id="267d2-117">Należy zawsze toomonitor zużycie pamięci na powitania dużych wystąpienia poziomu toomake się, że dodatkowe zainstalowanych z systemem innym niż — HANA oprogramowania nie zużywa zbyt dużej ilości pamięci i w związku z tym konkurują ze HANA pamięci.</span><span class="sxs-lookup"><span data-stu-id="267d2-117">You also want toomonitor memory consumption on hello Large Instance level toomake sure that additional installed non-HANA software does not consume too much memory, and therefore compete with HANA for memory.</span></span>

<span data-ttu-id="267d2-118">**Przepustowość sieci:** hello bramy sieci wirtualnej Azure ma ograniczoną przepustowość danych do hello sieci wirtualnej Azure, dlatego warto odebrane przez wszystkie dane hello toomonitor hello maszyn wirtualnych Azure w ramach toofigure sieci wirtualnej, jak blisko jest toohello limitów hello Azure wybrano jednostki SKU bramy.</span><span class="sxs-lookup"><span data-stu-id="267d2-118">**Network bandwidth:** hello Azure VNet gateway is limited in bandwidth of data moving into hello Azure VNet, so it is helpful toomonitor hello data received by all hello Azure VMs within a VNet toofigure out how close you are toohello limits of hello Azure gateway SKU you selected.</span></span> <span data-ttu-id="267d2-119">W jednostce wystąpienia dużych HANA hello sprawia, że znaczeniu toomonitor przychodzący i wychodzący ruch sieciowy również i Śledź tookeep hello woluminów, które są obsługiwane w czasie.</span><span class="sxs-lookup"><span data-stu-id="267d2-119">On hello HANA Large Instance unit, it does make sense toomonitor incoming and outgoing network traffic as well, and tookeep track of hello volumes that are handled over time.</span></span>

<span data-ttu-id="267d2-120">**Miejsce na dysku:** użycie miejsca na dysku zwykle zwiększa się wraz z upływem czasu.</span><span class="sxs-lookup"><span data-stu-id="267d2-120">**Disk space:** Disk space consumption usually increases over time.</span></span> <span data-ttu-id="267d2-121">Istnieje wiele powodów, ale większość wszystkich: wzrasta ilość danych, wykonywania kopii zapasowej dziennika transakcji, przechowywanie plików śledzenia i wykonywania migawek magazynu.</span><span class="sxs-lookup"><span data-stu-id="267d2-121">There are many reasons for this, but most of all are: data volume increases, execution of transaction log backups, storing trace files, and performing storage snapshots.</span></span> <span data-ttu-id="267d2-122">Dlatego jest ważne toomonitor użycie miejsca na dysku i zarządzać miejscem na dysku hello skojarzonego z jednostką wystąpienia dużych HANA hello.</span><span class="sxs-lookup"><span data-stu-id="267d2-122">Therefore, it is important toomonitor disk space usage and manage hello disk space associated with hello HANA Large Instance unit.</span></span>

## <a name="monitoring-and-troubleshooting-from-hana-side"></a><span data-ttu-id="267d2-123">Monitorowanie i rozwiązywanie problemów z HANA strony</span><span class="sxs-lookup"><span data-stu-id="267d2-123">Monitoring and troubleshooting from HANA side</span></span>

<span data-ttu-id="267d2-124">W kolejności tooeffectively analizować problemy pokrewne tooSAP HANA na platformie Azure (wystąpienia duże), jest przydatne toonarrow dół hello główną przyczynę problemu.</span><span class="sxs-lookup"><span data-stu-id="267d2-124">In order tooeffectively analyze problems related tooSAP HANA on Azure (Large Instances), it is useful toonarrow down hello root cause of a problem.</span></span> <span data-ttu-id="267d2-125">SAP został opublikowany dużą ilość toohelp dokumentacji użytkownik.</span><span class="sxs-lookup"><span data-stu-id="267d2-125">SAP has published a large amount of documentation toohelp you.</span></span>

<span data-ttu-id="267d2-126">Zastosowanie wydajności HANA pokrewne tooSAP — często zadawane pytania można znaleźć w powitania po SAP uwagi:</span><span class="sxs-lookup"><span data-stu-id="267d2-126">Applicable FAQs related tooSAP HANA performance can be found in hello following SAP Notes:</span></span>

- [<span data-ttu-id="267d2-127">Uwaga SAP #2222200 — często zadawane pytania: SAP HANA sieci</span><span class="sxs-lookup"><span data-stu-id="267d2-127">SAP Note #2222200 – FAQ: SAP HANA Network</span></span>](https://launchpad.support.sap.com/#/notes/2222200)
- [<span data-ttu-id="267d2-128">Uwaga SAP #2100040 — często zadawane pytania: SAP HANA Procesora</span><span class="sxs-lookup"><span data-stu-id="267d2-128">SAP Note #2100040 – FAQ: SAP HANA CPU</span></span>](https://launchpad.support.sap.com/#/notes/0002100040)
- [<span data-ttu-id="267d2-129">Uwaga SAP #199997 — często zadawane pytania: SAP HANA pamięci</span><span class="sxs-lookup"><span data-stu-id="267d2-129">SAP Note #199997 – FAQ: SAP HANA Memory</span></span>](https://launchpad.support.sap.com/#/notes/2177064)
- [<span data-ttu-id="267d2-130">SAP Uwaga #200000 — często zadawane pytania: Optymalizacja wydajności HANA SAP</span><span class="sxs-lookup"><span data-stu-id="267d2-130">SAP Note #200000 – FAQ: SAP HANA Performance Optimization</span></span>](https://launchpad.support.sap.com/#/notes/2000000)
- [<span data-ttu-id="267d2-131">Uwaga SAP #199930 — często zadawane pytania: SAP HANA we/wy analizy</span><span class="sxs-lookup"><span data-stu-id="267d2-131">SAP Note #199930 – FAQ: SAP HANA I/O Analysis</span></span>](https://launchpad.support.sap.com/#/notes/1999930)
- [<span data-ttu-id="267d2-132">Uwaga SAP #2177064 — często zadawane pytania: Uruchom ponownie SAP HANA usługi i awarii</span><span class="sxs-lookup"><span data-stu-id="267d2-132">SAP Note #2177064 – FAQ: SAP HANA Service Restart and Crashes</span></span>](https://launchpad.support.sap.com/#/notes/2177064)

<span data-ttu-id="267d2-133">**SAP HANA alertów**</span><span class="sxs-lookup"><span data-stu-id="267d2-133">**SAP HANA Alerts**</span></span>

<span data-ttu-id="267d2-134">Pierwszym krokiem w dzienniku hello bieżącego SAP HANA alertu.</span><span class="sxs-lookup"><span data-stu-id="267d2-134">As a first step, check hello current SAP HANA alert logs.</span></span> <span data-ttu-id="267d2-135">W systemie SAP HANA Studio Przejdź zbyt**konsoli administracyjnej: alerty: Pokaż: wszystkie alerty**.</span><span class="sxs-lookup"><span data-stu-id="267d2-135">In SAP HANA Studio, go too**Administration Console: Alerts: Show: all alerts**.</span></span> <span data-ttu-id="267d2-136">Na tej karcie zostaną wyświetlone wszystkie alerty SAP HANA określone wartości (wolnej pamięci fizycznej, użycie procesora CPU, itp.), które dzielą się poza hello ustawić minimalną i maksymalną progów.</span><span class="sxs-lookup"><span data-stu-id="267d2-136">This tab will show all SAP HANA alerts for specific values (free physical memory, CPU utilization, etc.) that fall outside of hello set minimum and maximum thresholds.</span></span> <span data-ttu-id="267d2-137">Domyślnie sprawdza są odświeżane automatycznie co 15 minut.</span><span class="sxs-lookup"><span data-stu-id="267d2-137">By default, checks are auto-refreshed every 15 minutes.</span></span>

![W systemie SAP HANA Studio Przejdź tooAdministration konsoli: alerty: Pokaż: wszystkie alerty](./media/troubleshooting-monitoring/image1-show-alerts.png)

<span data-ttu-id="267d2-139">**PROCESOR CPU**</span><span class="sxs-lookup"><span data-stu-id="267d2-139">**CPU**</span></span>

<span data-ttu-id="267d2-140">Alert wyzwolony powodu ustawienie progu tooimproper rozwiązanie jest wartość domyślną toohello tooreset lub bardziej przystępne wartość progową.</span><span class="sxs-lookup"><span data-stu-id="267d2-140">For an alert triggered due tooimproper threshold setting, a resolution is tooreset toohello default value or a more reasonable threshold value.</span></span>

![Zresetuj wartość domyślną toohello lub bardziej przystępne wartość progowa](./media/troubleshooting-monitoring/image2-cpu-utilization.png)

<span data-ttu-id="267d2-142">powitania po alertów może wskazywać problemy zasobów Procesora:</span><span class="sxs-lookup"><span data-stu-id="267d2-142">hello following alerts may indicate CPU resource problems:</span></span>

- <span data-ttu-id="267d2-143">Użycie procesora CPU hosta (alertu 5)</span><span class="sxs-lookup"><span data-stu-id="267d2-143">Host CPU Usage (Alert 5)</span></span>
- <span data-ttu-id="267d2-144">Operacja punktu zapisu najnowszych (28 alertów)</span><span class="sxs-lookup"><span data-stu-id="267d2-144">Most recent savepoint operation (Alert 28)</span></span>
- <span data-ttu-id="267d2-145">Czas trwania punktu zapisu (54 alertów)</span><span class="sxs-lookup"><span data-stu-id="267d2-145">Savepoint duration (Alert 54)</span></span>

<span data-ttu-id="267d2-146">Można zauważyć wysokie użycie procesora CPU w Twojej bazie danych SAP HANA z jednego z następujących hello:</span><span class="sxs-lookup"><span data-stu-id="267d2-146">You may notice high CPU consumption on your SAP HANA database from one of hello following:</span></span>

- <span data-ttu-id="267d2-147">Alert 5 (użycie procesora CPU hosta) jest wywoływane bieżące lub wcześniejsze użycia procesora CPU</span><span class="sxs-lookup"><span data-stu-id="267d2-147">Alert 5 (Host CPU usage) is raised for current or past CPU usage</span></span>
- <span data-ttu-id="267d2-148">Hello wyświetlane użycie procesora CPU na powitania ekran Przegląd</span><span class="sxs-lookup"><span data-stu-id="267d2-148">hello displayed CPU usage on hello overview screen</span></span>

![Wyświetlane użycie procesora CPU na powitania ekran Przegląd](./media/troubleshooting-monitoring/image3-cpu-usage.png)

<span data-ttu-id="267d2-150">w przeszłości hello Hello wykres obciążenia mogą być wyświetlane wysokie użycie procesora CPU lub wysokie zużycie:</span><span class="sxs-lookup"><span data-stu-id="267d2-150">hello Load graph might show high CPU consumption, or high consumption in hello past:</span></span>

![Wykres obciążenia Hello mogą być wyświetlane w przeszłości hello wysokie użycie procesora CPU lub wysokie zużycie](./media/troubleshooting-monitoring/image4-load-graph.png)

<span data-ttu-id="267d2-152">Alert wyzwolony powodu wykorzystania procesora CPU toohigh może być spowodowane przez kilka przyczyn, w tym między innymi: wykonanie pewnych transakcji, ładowanie danych, wysunięć zadania, długotrwałą instrukcji SQL i wydajności zapytania (na przykład z BW na HANA moduły).</span><span class="sxs-lookup"><span data-stu-id="267d2-152">An alert triggered due toohigh CPU utilization could be caused by several reasons, including, but not limited to: execution of certain transactions, data loading, hanging of jobs, long running SQL statements, and bad query performance (for example, with BW on HANA cubes).</span></span>

<span data-ttu-id="267d2-153">Można znaleźć toohello [SAP HANA rozwiązywania problemów: pokrewne powoduje procesora CPU i rozwiązań](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4f/bc915462db406aa2fe92b708b95189/content.htm?frameset=/en/db/6ca50424714af8b370960c04ce667b/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=46&amp;show_children=false) lokacji szczegółowe kroki rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="267d2-153">Refer toohello [SAP HANA Troubleshooting: CPU Related Causes and Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4f/bc915462db406aa2fe92b708b95189/content.htm?frameset=/en/db/6ca50424714af8b370960c04ce667b/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=46&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="267d2-154">**System operacyjny**</span><span class="sxs-lookup"><span data-stu-id="267d2-154">**Operating System**</span></span>

<span data-ttu-id="267d2-155">Jedną z najważniejszych hello sprawdza, czy SAP HANA w systemie Linux jest toomake się upewnić, że wyłączono przezroczysty dużych stron, zobacz [&#2131662; Uwaga SAP — przezroczysty dużych stron (THP) na serwerach z SAP HANA](https://launchpad.support.sap.com/#/notes/2131662).</span><span class="sxs-lookup"><span data-stu-id="267d2-155">One of hello most important checks for SAP HANA on Linux is toomake sure that Transparent Huge Pages are disabled, see [SAP Note #2131662 – Transparent Huge Pages (THP) on SAP HANA Servers](https://launchpad.support.sap.com/#/notes/2131662).</span></span>

- <span data-ttu-id="267d2-156">Możesz sprawdzić, czy przezroczyste dużych stron są włączone za pośrednictwem hello następujące polecenia Linux: **cat /sys/kernel/mm/transparent\_hugepage lub nie włączono**</span><span class="sxs-lookup"><span data-stu-id="267d2-156">You can check if Transparent Huge Pages are enabled through hello following Linux command: **cat /sys/kernel/mm/transparent\_hugepage/enabled**</span></span>
- <span data-ttu-id="267d2-157">Jeśli _zawsze_ jest ujęta w nawiasy kwadratowe zgodnie z poniższymi instrukcjami, oznacza to, czy przezroczyste dużych stron hello są włączone: [zawsze] madvise nigdy nie; Jeśli _nigdy nie_ jest ujęta w nawiasy kwadratowe zgodnie z poniższymi instrukcjami, oznacza to, że hello przezroczysty Wyłączono dużych stron: zawsze madvise [nigdy nie]</span><span class="sxs-lookup"><span data-stu-id="267d2-157">If _always_ is enclosed in brackets as below, it means that hello Transparent Huge Pages are enabled: [always] madvise never; if _never_ is enclosed in brackets as below, it means that hello Transparent Huge Pages are disabled: always madvise [never]</span></span>

<span data-ttu-id="267d2-158">Hello następujące polecenia Linux powinien zwrócić nic: **obr. / min — odpowiedzi na pytania | grep ulimit.**</span><span class="sxs-lookup"><span data-stu-id="267d2-158">hello following Linux command should return nothing: **rpm -qa | grep ulimit.**</span></span> <span data-ttu-id="267d2-159">Jeśli zostanie wyświetlona _ulimit_ jest zainstalowane, odinstaluj go bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="267d2-159">If it appears _ulimit_ is installed, uninstall it immediately.</span></span>

<span data-ttu-id="267d2-160">**Pamięci**</span><span class="sxs-lookup"><span data-stu-id="267d2-160">**Memory**</span></span>

<span data-ttu-id="267d2-161">Można zaobserwować hello wielkość pamięci przydzielonej przez hello SAP HANA bazy danych jest większa niż oczekiwano.</span><span class="sxs-lookup"><span data-stu-id="267d2-161">You may observe that hello amount of memory allocated by hello SAP HANA database is higher than expected.</span></span> <span data-ttu-id="267d2-162">Witaj następujące alerty wskazują na problemy z wysokie użycie pamięci:</span><span class="sxs-lookup"><span data-stu-id="267d2-162">hello following alerts indicate issues with high memory usage:</span></span>

- <span data-ttu-id="267d2-163">Użycie pamięci fizycznej hosta (alertu 1)</span><span class="sxs-lookup"><span data-stu-id="267d2-163">Host physical memory usage (Alert 1)</span></span>
- <span data-ttu-id="267d2-164">Użycie pamięci serwera nazw (12 alertów)</span><span class="sxs-lookup"><span data-stu-id="267d2-164">Memory usage of name server (Alert 12)</span></span>
- <span data-ttu-id="267d2-165">Łączne użycie pamięci magazynu kolumn w tabelach (40 alertów)</span><span class="sxs-lookup"><span data-stu-id="267d2-165">Total memory usage of Column Store tables (Alert 40)</span></span>
- <span data-ttu-id="267d2-166">Użycie pamięci usług (43 alertów)</span><span class="sxs-lookup"><span data-stu-id="267d2-166">Memory usage of services (Alert 43)</span></span>
- <span data-ttu-id="267d2-167">Użycie pamięci magazynu głównego magazynu kolumn tabel (45 alertów)</span><span class="sxs-lookup"><span data-stu-id="267d2-167">Memory usage of main storage of Column Store tables (Alert 45)</span></span>
- <span data-ttu-id="267d2-168">Pliki zrzutu środowiska uruchomieniowego (46 alertów)</span><span class="sxs-lookup"><span data-stu-id="267d2-168">Runtime dump files (Alert 46)</span></span>

<span data-ttu-id="267d2-169">Zobacz toohello [SAP HANA rozwiązywania problemów: problemy z pamięcią](http://help.sap.com/saphelp_hanaplatform/helpdata/en/db/6ca50424714af8b370960c04ce667b/content.htm?frameset=/en/59/5eaa513dde43758b51378ab3315ebb/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=26&amp;show_children=false) lokacji szczegółowe kroki rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="267d2-169">Refer toohello [SAP HANA Troubleshooting: Memory Problems](http://help.sap.com/saphelp_hanaplatform/helpdata/en/db/6ca50424714af8b370960c04ce667b/content.htm?frameset=/en/59/5eaa513dde43758b51378ab3315ebb/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=26&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="267d2-170">**Sieć**</span><span class="sxs-lookup"><span data-stu-id="267d2-170">**Network**</span></span>

<span data-ttu-id="267d2-171">Odwołuje się zbyt[SAP Uwaga #2081065 — Rozwiązywanie problemów z programem SAP HANA sieci](https://launchpad.support.sap.com/#/notes/2081065) i wykonywać rozwiązywania problemów w tej uwagi SAP hello sieciowych.</span><span class="sxs-lookup"><span data-stu-id="267d2-171">Refer too[SAP Note #2081065 – Troubleshooting SAP HANA Network](https://launchpad.support.sap.com/#/notes/2081065) and perform hello network troubleshooting steps in this SAP Note.</span></span>

1. <span data-ttu-id="267d2-172">Analizowanie czasu Rundy między serwerem a klientem.</span><span class="sxs-lookup"><span data-stu-id="267d2-172">Analyzing round-trip time between server and client.</span></span>
  <span data-ttu-id="267d2-173">A.</span><span class="sxs-lookup"><span data-stu-id="267d2-173">A.</span></span> <span data-ttu-id="267d2-174">Uruchom skrypt SQL hello [ _HANA\_sieci\_klientów_](https://launchpad.support.sap.com/#/notes/1969700)_._</span><span class="sxs-lookup"><span data-stu-id="267d2-174">Run hello SQL script [_HANA\_Network\_Clients_](https://launchpad.support.sap.com/#/notes/1969700)_._</span></span>
  
2. <span data-ttu-id="267d2-175">Przeanalizuj komunikacji między węzłami.</span><span class="sxs-lookup"><span data-stu-id="267d2-175">Analyze internode communication.</span></span>
  <span data-ttu-id="267d2-176">A.</span><span class="sxs-lookup"><span data-stu-id="267d2-176">A.</span></span> <span data-ttu-id="267d2-177">Uruchom skrypt SQL [ _HANA\_sieci\_usług_](https://launchpad.support.sap.com/#/notes/1969700)_._</span><span class="sxs-lookup"><span data-stu-id="267d2-177">Run SQL script [_HANA\_Network\_Services_](https://launchpad.support.sap.com/#/notes/1969700)_._</span></span>

3. <span data-ttu-id="267d2-178">Uruchom polecenie Linux **ifconfig** (hello dane wyjściowe zawierają, jeśli występują strat pakietów).</span><span class="sxs-lookup"><span data-stu-id="267d2-178">Run Linux command **ifconfig** (hello output shows if any packet losses are occurring).</span></span>
4. <span data-ttu-id="267d2-179">Uruchom polecenie Linux **tcpdump**.</span><span class="sxs-lookup"><span data-stu-id="267d2-179">Run Linux command **tcpdump**.</span></span>

<span data-ttu-id="267d2-180">Należy także użyć typu open source hello [dotyczące programu Iperf;](https://iperf.fr/) narzędzia (lub podobny) wydajność sieci toomeasure rzeczywistej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="267d2-180">Also, use hello open source [IPERF](https://iperf.fr/) tool (or similar) toomeasure real application network performance.</span></span>

<span data-ttu-id="267d2-181">Zobacz toohello [SAP HANA rozwiązywania problemów: wydajność sieci i występują problemy z łącznością](http://help.sap.com/saphelp_hanaplatform/helpdata/en/a3/ccdff1aedc4720acb24ed8826938b6/content.htm?frameset=/en/dc/6ff98fa36541e997e4c719a632cbd8/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=142&amp;show_children=false) lokacji szczegółowe kroki rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="267d2-181">Refer toohello [SAP HANA Troubleshooting: Networking Performance and Connectivity Problems](http://help.sap.com/saphelp_hanaplatform/helpdata/en/a3/ccdff1aedc4720acb24ed8826938b6/content.htm?frameset=/en/dc/6ff98fa36541e997e4c719a632cbd8/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=142&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="267d2-182">**Storage**</span><span class="sxs-lookup"><span data-stu-id="267d2-182">**Storage**</span></span>

<span data-ttu-id="267d2-183">Z perspektywy użytkownika końcowego aplikacji (lub hello system jako całość) działa wolno, nie odpowiada lub nawet może wydawać toohang, jeśli występują problemy z wydajnością we/wy.</span><span class="sxs-lookup"><span data-stu-id="267d2-183">From an end-user perspective, an application (or hello system as a whole) runs sluggishly, is unresponsive, or can even seem toohang if there are issues with I/O performance.</span></span> <span data-ttu-id="267d2-184">W hello **woluminów** kartę SAP HANA Studio zawiera hello dołączone woluminy i woluminy są używane przez każdej usługi.</span><span class="sxs-lookup"><span data-stu-id="267d2-184">In hello **Volumes** tab in SAP HANA Studio, you can see hello attached volumes, and what volumes are used by each service.</span></span>

![Na karcie woluminów hello w SAP HANA Studio można zauważyć, że hello dołączone woluminy i woluminy są używane przez każdego usługi](./media/troubleshooting-monitoring/image5-volumes-tab-a.png)

<span data-ttu-id="267d2-186">Dołączone woluminy w dolnej części ekranu hello, które można wyświetlić szczegóły hello hello woluminów, takie jak pliki i statystyki we/wy.</span><span class="sxs-lookup"><span data-stu-id="267d2-186">Attached volumes in hello lower part of hello screen you can see details of hello volumes, such as files and I/O statistics.</span></span>

![Dołączone woluminy w dolnej części ekranu hello, które można wyświetlić szczegóły hello hello woluminów, takie jak pliki i statystyki we/wy](./media/troubleshooting-monitoring/image6-volumes-tab-b.png)

<span data-ttu-id="267d2-188">Można znaleźć toohello [SAP HANA rozwiązywania problemów: We/Wy pokrewne główne przyczyny i rozwiązania](http://help.sap.com/saphelp_hanaplatform/helpdata/en/dc/6ff98fa36541e997e4c719a632cbd8/content.htm?frameset=/en/47/4cb08a715c42fe9f7cc5efdc599959/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=55&amp;show_children=false) i [SAP HANA Rozwiązywanie problemów z: dysku pokrewne główne przyczyny i rozwiązania](http://help.sap.com/saphelp_hanaplatform/helpdata/en/47/4cb08a715c42fe9f7cc5efdc599959/content.htm?frameset=/en/44/3e1db4f73d42da859008df4f69e37a/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=53&amp;show_children=false) lokacji szczegółowe kroki rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="267d2-188">Refer toohello [SAP HANA Troubleshooting: I/O Related Root Causes and Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/dc/6ff98fa36541e997e4c719a632cbd8/content.htm?frameset=/en/47/4cb08a715c42fe9f7cc5efdc599959/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=55&amp;show_children=false) and [SAP HANA Troubleshooting: Disk Related Root Causes and Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/47/4cb08a715c42fe9f7cc5efdc599959/content.htm?frameset=/en/44/3e1db4f73d42da859008df4f69e37a/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=53&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="267d2-189">**Narzędzia diagnostyczne**</span><span class="sxs-lookup"><span data-stu-id="267d2-189">**Diagnostic Tools**</span></span>

<span data-ttu-id="267d2-190">Wykonaj sprawdzenie kondycji programu SAP HANA za pośrednictwem HANA\_konfiguracji\_Minichecks.</span><span class="sxs-lookup"><span data-stu-id="267d2-190">Perform an SAP HANA Health Check through HANA\_Configuration\_Minichecks.</span></span> <span data-ttu-id="267d2-191">To narzędzie zwraca potencjalnie krytycznych problemów technicznych, które powinny już mieć został zgłoszony jako ostrzeżenia w SAP HANA Studio.</span><span class="sxs-lookup"><span data-stu-id="267d2-191">This tool returns potentially critical technical issues that should have already been raised as alerts in SAP HANA Studio.</span></span>

<span data-ttu-id="267d2-192">Odwołuje się zbyt[&#1969700; Uwaga SAP — kolekcja instrukcji SQL dla SAP HANA](https://launchpad.support.sap.com/#/notes/1969700) i Pobierz hello SQL Statements.zip pliku dołączonego toothat Uwaga.</span><span class="sxs-lookup"><span data-stu-id="267d2-192">Refer too[SAP Note #1969700 – SQL statement collection for SAP HANA](https://launchpad.support.sap.com/#/notes/1969700) and download hello SQL Statements.zip file attached toothat note.</span></span> <span data-ttu-id="267d2-193">Należy zapisać ten plik zip na lokalnym dysku twardym powitania.</span><span class="sxs-lookup"><span data-stu-id="267d2-193">Store this .zip file on hello local hard drive.</span></span>

<span data-ttu-id="267d2-194">W SAP HANA Studio na powitania **informacje o systemie** karcie, kliknij prawym przyciskiem myszy hello **nazwa** kolumny i wybierz **instrukcje SQL importu**.</span><span class="sxs-lookup"><span data-stu-id="267d2-194">In SAP HANA Studio, on hello **System Information** tab, right-click in hello **Name** column and select **Import SQL Statements**.</span></span>

![W SAP HANA Studio, na karcie informacji o systemie hello kliknij prawym przyciskiem myszy hello kolumny z nazwami, a następnie wybierz importu instrukcje SQL](./media/troubleshooting-monitoring/image7-import-statements-a.png)

<span data-ttu-id="267d2-196">Plik SQL Statements.zip SELECT hello przechowywany lokalnie, a folder z odpowiedniej instrukcji SQL hello zostaną zaimportowane.</span><span class="sxs-lookup"><span data-stu-id="267d2-196">Select hello SQL Statements.zip file stored locally, and a folder with hello corresponding SQL statements will be imported.</span></span> <span data-ttu-id="267d2-197">W tym momencie powitalne szereg różnych testów diagnostycznych mogą być uruchamiane z tych instrukcji SQL.</span><span class="sxs-lookup"><span data-stu-id="267d2-197">At this point, hello many different diagnostic checks can be run with these SQL statements.</span></span>

<span data-ttu-id="267d2-198">Na przykład wymagania dotyczące przepustowości replikacji systemu SAP HANA tootest, kliknij prawym przyciskiem myszy hello **przepustowości** instrukcji w obszarze **replikacji: przepustowości** i wybierz **Otwórz** w konsoli programu SQL.</span><span class="sxs-lookup"><span data-stu-id="267d2-198">For example, tootest SAP HANA System Replication bandwidth requirements, right-click hello **Bandwidth** statement under **Replication: Bandwidth** and select **Open** in SQL Console.</span></span>

<span data-ttu-id="267d2-199">pełną instrukcję SQL Hello otwiera zezwalanie toobe parametrów wejściowych (modyfikacji sekcja) zmienione, a następnie wykonać.</span><span class="sxs-lookup"><span data-stu-id="267d2-199">hello complete SQL statement opens allowing input parameters (modification section) toobe changed and then executed.</span></span>

![zezwolenie na obecność toobe parametrów wejściowych (modyfikacji sekcja) zmienione, a następnie wykonać otwiera Hello pełną instrukcję SQL](./media/troubleshooting-monitoring/image8-import-statements-b.png)

<span data-ttu-id="267d2-201">Innym przykładem jest kliknięcie prawym przyciskiem myszy w instrukcjach hello w obszarze **replikacji: omówienie**.</span><span class="sxs-lookup"><span data-stu-id="267d2-201">Another example is right-clicking on hello statements under **Replication: Overview**.</span></span> <span data-ttu-id="267d2-202">Wybierz **Execute** z menu kontekstowego hello:</span><span class="sxs-lookup"><span data-stu-id="267d2-202">Select **Execute** from hello context menu:</span></span>

![Innym przykładem jest kliknięcie prawym przyciskiem myszy w instrukcjach hello w ramach replikacji: omówienie.](./media/troubleshooting-monitoring/image9-import-statements-c.png)

<span data-ttu-id="267d2-205">Powoduje to informacje pomocne przy rozwiązywaniu problemów:</span><span class="sxs-lookup"><span data-stu-id="267d2-205">This results in information that helps with troubleshooting:</span></span>

![Spowoduje to informacje, które ułatwią rozwiązywanie problemów](./media/troubleshooting-monitoring/image10-import-statements-d.png)

<span data-ttu-id="267d2-207">Witaj takie same dla HANA\_konfiguracji\_Minichecks i zaznacz pole wyboru dla dowolnej _X_ znaczników hello _C_ kolumny (krytyczne).</span><span class="sxs-lookup"><span data-stu-id="267d2-207">Do hello same for HANA\_Configuration\_Minichecks and check for any _X_ marks in hello _C_ (Critical) column.</span></span>

<span data-ttu-id="267d2-208">Przykładowe wyniki:</span><span class="sxs-lookup"><span data-stu-id="267d2-208">Sample outputs:</span></span>

<span data-ttu-id="267d2-209">**HANA\_konfiguracji\_MiniChecks\_Rev102.01 + 1** kontroli ogólne SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="267d2-209">**HANA\_Configuration\_MiniChecks\_Rev102.01+1** for general SAP HANA checks.</span></span>

![HANA\_konfiguracji\_MiniChecks\_Rev102.01 + 1 dla ogólnych kontroli SAP HANA](./media/troubleshooting-monitoring/image11-configuration-minichecks.png)

<span data-ttu-id="267d2-211">**HANA\_usług\_omówienie** omówienie co SAP HANA usługi są aktualnie uruchomione.</span><span class="sxs-lookup"><span data-stu-id="267d2-211">**HANA\_Services\_Overview** for an overview of what SAP HANA services are currently running.</span></span>

![HANA\_usług\_omówienie omówienie co SAP HANA usługi są aktualnie uruchomione](./media/troubleshooting-monitoring/image12-services-overview.png)

<span data-ttu-id="267d2-213">**HANA\_usług\_statystyki** dla SAP HANA usługi informacji (CPU, pamięci, itd.).</span><span class="sxs-lookup"><span data-stu-id="267d2-213">**HANA\_Services\_Statistics** for SAP HANA service information (CPU, memory, etc.).</span></span>

![<span data-ttu-id="267d2-214">HANA\_usług\_statystyki dla SAP HANA informacje o usługach</span><span class="sxs-lookup"><span data-stu-id="267d2-214">HANA\_Services\_Statistics for SAP HANA service information</span></span> ](./media/troubleshooting-monitoring/image13-services-statistics.png)

<span data-ttu-id="267d2-215">**HANA\_konfiguracji\_omówienie\_Rev110 +** ogólne informacje na temat hello wystąpieniem SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="267d2-215">**HANA\_Configuration\_Overview\_Rev110+** for general information on hello SAP HANA instance.</span></span>

![HANA\_konfiguracji\_omówienie\_Rev110 + ogólne informacje na temat hello SAP HANA wystąpienia](./media/troubleshooting-monitoring/image14-configuration-overview.png)

<span data-ttu-id="267d2-217">**HANA\_konfiguracji\_parametry\_Rev70 +** toocheck parametrów SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="267d2-217">**HANA\_Configuration\_Parameters\_Rev70+** toocheck SAP HANA parameters.</span></span>

![HANA\_konfiguracji\_parametry\_Rev70 + toocheck SAP HANA parametrów](./media/troubleshooting-monitoring/image15-configuration-parameters.png)

