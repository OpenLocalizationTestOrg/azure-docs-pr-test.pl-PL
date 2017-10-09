---
title: "aaaContainer monitorowanie rozwiązania Azure Log Analytics | Dokumentacja firmy Microsoft"
description: "Hello monitorowania kontenera rozwiązania analizy dzienników ułatwia wyświetlanie i zarządzanie Docker i Windows hostów kontenera w jednym miejscu."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: e1e4b52b-92d5-4bfa-8a09-ff8c6b5a9f78
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: magoedte;banders
ms.openlocfilehash: 2eed1dd81c22faef78a375fca3ebece9e5300c09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="container-monitoring-solution-in-log-analytics"></a><span data-ttu-id="c751a-103">Kontener rozwiązania monitorowanie analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="c751a-103">Container Monitoring solution in Log Analytics</span></span>

![Symbol kontenerów](./media/log-analytics-containers/containers-symbol.png)

<span data-ttu-id="c751a-105">W tym artykule opisano, jak monitorowanie kontenera rozwiązania analizy dzienników, która ułatwia wyświetlanie i zarządzanie Docker i Windows hello tooset się i użyj hostów kontenera w jednym miejscu.</span><span class="sxs-lookup"><span data-stu-id="c751a-105">This article describes how tooset up and use hello Container Monitoring solution in Log Analytics, which helps you view and manage your Docker and Windows container hosts in a single location.</span></span> <span data-ttu-id="c751a-106">Docker jest systemu wirtualizacji oprogramowania używane toocreate kontenerów, które automatyzują tootheir wdrożenia oprogramowania IT infrastruktury.</span><span class="sxs-lookup"><span data-stu-id="c751a-106">Docker is a software virtualization system used toocreate containers that automate software deployment tootheir IT infrastructure.</span></span>

<span data-ttu-id="c751a-107">Witaj rozwiązania wyświetlany działają kontenery, obrazów kontenera nich uruchomiony, i gdy działają kontenery.</span><span class="sxs-lookup"><span data-stu-id="c751a-107">hello solution shows which containers are running, what container image they’re running, and where containers are running.</span></span> <span data-ttu-id="c751a-108">Można wyświetlić szczegółowe informacje o inspekcji przedstawiający poleceń używanych przez kontenery.</span><span class="sxs-lookup"><span data-stu-id="c751a-108">You can view detailed audit information showing commands used with containers.</span></span> <span data-ttu-id="c751a-109">I rozwiązywać kontenery wyświetlanie i wyszukując scentralizowane dzienniki bez konieczności widoku tooremotely Docker lub hosty z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="c751a-109">And, you can troubleshoot containers by viewing and searching centralized logs without having tooremotely view Docker or Windows hosts.</span></span> <span data-ttu-id="c751a-110">Można znaleźć kontenerów, które mogą być zakłócenia i spójniejsze nadmiarowe zasobów na hoście.</span><span class="sxs-lookup"><span data-stu-id="c751a-110">You can find containers that may be noisy and consuming excess resources on a host.</span></span> <span data-ttu-id="c751a-111">I można wyświetlić scentralizowane procesora CPU, pamięci, magazynu i użycia i wydajności informacje o sieci dla kontenerów.</span><span class="sxs-lookup"><span data-stu-id="c751a-111">And, you can view centralized CPU, memory, storage, and network usage and performance information for containers.</span></span> <span data-ttu-id="c751a-112">Na komputerach z systemem Windows, można scentralizować i porównaj dzienniki systemu Windows Server, Hyper-V i kontenery Docker.</span><span class="sxs-lookup"><span data-stu-id="c751a-112">On computers running Windows, you can centralize and compare logs from Windows Server, Hyper-V, and Docker containers.</span></span> <span data-ttu-id="c751a-113">rozwiązanie Hello obsługuje powitania po orchestrators kontenera:</span><span class="sxs-lookup"><span data-stu-id="c751a-113">hello solution supports hello following container orchestrators:</span></span>

- <span data-ttu-id="c751a-114">Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="c751a-114">Docker Swarm</span></span>
- <span data-ttu-id="c751a-115">DC/OS</span><span class="sxs-lookup"><span data-stu-id="c751a-115">DC/OS</span></span>
- <span data-ttu-id="c751a-116">Kubernetes</span><span class="sxs-lookup"><span data-stu-id="c751a-116">Kubernetes</span></span>
- <span data-ttu-id="c751a-117">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c751a-117">Service Fabric</span></span>
- <span data-ttu-id="c751a-118">Red Hat OpenShift</span><span class="sxs-lookup"><span data-stu-id="c751a-118">Red Hat OpenShift</span></span>


<span data-ttu-id="c751a-119">Witaj Poniższy diagram przedstawia relacje hello różnych hostów kontenera i agentów z usługą OMS.</span><span class="sxs-lookup"><span data-stu-id="c751a-119">hello following diagram shows hello relationships between various container hosts and agents with OMS.</span></span>

![Diagram kontenerów](./media/log-analytics-containers/containers-diagram.png)

## <a name="system-requirements"></a><span data-ttu-id="c751a-121">Wymagania systemowe</span><span class="sxs-lookup"><span data-stu-id="c751a-121">System requirements</span></span>

<span data-ttu-id="c751a-122">Przed rozpoczęciem należy przejrzeć następujące szczegóły tooverify spełnia wymagania wstępne hello hello.</span><span class="sxs-lookup"><span data-stu-id="c751a-122">Before starting, review hello following details tooverify you meet hello prerequisites.</span></span>

### <a name="container-monitoring-solution-support-for-docker-orchestrator-and-os-platform"></a><span data-ttu-id="c751a-123">Rozwiązanie monitorowania kontener obsługuje platformy Docker Orchestrator i systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="c751a-123">Container monitoring solution support for Docker Orchestrator and OS platform</span></span>
<span data-ttu-id="c751a-124">Witaj poniższej tabeli przedstawiono hello aranżacji Docker i systemu operacyjnego monitorowania obsługę kontenera magazynu, wydajności i dzienniki z analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="c751a-124">hello following table outlines hello Docker orchestration and operating system monitoring support of container inventory, performance, and logs with Log Analytics.</span></span>   

| | <span data-ttu-id="c751a-125">ACS</span><span class="sxs-lookup"><span data-stu-id="c751a-125">ACS</span></span> | <span data-ttu-id="c751a-126">Linux</span><span class="sxs-lookup"><span data-stu-id="c751a-126">Linux</span></span> | <span data-ttu-id="c751a-127">Windows</span><span class="sxs-lookup"><span data-stu-id="c751a-127">Windows</span></span> | <span data-ttu-id="c751a-128">Kontener</span><span class="sxs-lookup"><span data-stu-id="c751a-128">Container</span></span><br><span data-ttu-id="c751a-129">Spis</span><span class="sxs-lookup"><span data-stu-id="c751a-129">Inventory</span></span> | <span data-ttu-id="c751a-130">Image (Obraz)</span><span class="sxs-lookup"><span data-stu-id="c751a-130">Image</span></span><br><span data-ttu-id="c751a-131">Spis</span><span class="sxs-lookup"><span data-stu-id="c751a-131">Inventory</span></span> | <span data-ttu-id="c751a-132">Węzeł</span><span class="sxs-lookup"><span data-stu-id="c751a-132">Node</span></span><br><span data-ttu-id="c751a-133">Spis</span><span class="sxs-lookup"><span data-stu-id="c751a-133">Inventory</span></span> | <span data-ttu-id="c751a-134">Kontener</span><span class="sxs-lookup"><span data-stu-id="c751a-134">Container</span></span><br><span data-ttu-id="c751a-135">Wydajność</span><span class="sxs-lookup"><span data-stu-id="c751a-135">Performance</span></span> | <span data-ttu-id="c751a-136">Kontener</span><span class="sxs-lookup"><span data-stu-id="c751a-136">Container</span></span><br><span data-ttu-id="c751a-137">Wydarzenie</span><span class="sxs-lookup"><span data-stu-id="c751a-137">Event</span></span> | <span data-ttu-id="c751a-138">Wydarzenie</span><span class="sxs-lookup"><span data-stu-id="c751a-138">Event</span></span><br><span data-ttu-id="c751a-139">Log</span><span class="sxs-lookup"><span data-stu-id="c751a-139">Log</span></span> | <span data-ttu-id="c751a-140">Kontener</span><span class="sxs-lookup"><span data-stu-id="c751a-140">Container</span></span><br><span data-ttu-id="c751a-141">Log</span><span class="sxs-lookup"><span data-stu-id="c751a-141">Log</span></span> |
|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|
| <span data-ttu-id="c751a-142">Kubernetes</span><span class="sxs-lookup"><span data-stu-id="c751a-142">Kubernetes</span></span> | <span data-ttu-id="c751a-143">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c751a-143">&#8226;</span></span> | <span data-ttu-id="c751a-144">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c751a-144">&#8226;</span></span> | | <span data-ttu-id="c751a-145">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c751a-145">&#8226;</span></span> | <span data-ttu-id="c751a-146">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c751a-146">&#8226;</span></span> | <span data-ttu-id="c751a-147">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c751a-147">&#8226;</span></span> | <span data-ttu-id="c751a-148">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c751a-148">&#8226;</span></span> | <span data-ttu-id="c751a-149">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c751a-149">&#8226;</span></span> | <span data-ttu-id="c751a-150">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c751a-150">&#8226;</span></span> | <span data-ttu-id="c751a-151">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c751a-151">&#8226;</span></span> |
| <span data-ttu-id="c751a-152">Mesosphere</span><span class="sxs-lookup"><span data-stu-id="c751a-152">Mesosphere</span></span><br><span data-ttu-id="c751a-153">DC/OS</span><span class="sxs-lookup"><span data-stu-id="c751a-153">DC/OS</span></span> | <span data-ttu-id="c751a-154">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c751a-154">&#8226;</span></span> | <span data-ttu-id="c751a-155">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c751a-155">&#8226;</span></span> | | <span data-ttu-id="c751a-156">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c751a-156">&#8226;</span></span> | <span data-ttu-id="c751a-157">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c751a-157">&#8226;</span></span> | <span data-ttu-id="c751a-158">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c751a-158">&#8226;</span></span> | <span data-ttu-id="c751a-159">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c751a-159">&#8226;</span></span>| <span data-ttu-id="c751a-160">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c751a-160">&#8226;</span></span> | <span data-ttu-id="c751a-161">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c751a-161">&#8226;</span></span> | <span data-ttu-id="c751a-162">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c751a-162">&#8226;</span></span> |
| <span data-ttu-id="c751a-163">Docker</span><span class="sxs-lookup"><span data-stu-id="c751a-163">Docker</span></span><br><span data-ttu-id="c751a-164">Swarm</span><span class="sxs-lookup"><span data-stu-id="c751a-164">Swarm</span></span> | <span data-ttu-id="c751a-165">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c751a-165">&#8226;</span></span> | <span data-ttu-id="c751a-166">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c751a-166">&#8226;</span></span> | <span data-ttu-id="c751a-167">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c751a-167">&#8226;</span></span> | <span data-ttu-id="c751a-168">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c751a-168">&#8226;</span></span> | <span data-ttu-id="c751a-169">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c751a-169">&#8226;</span></span> | <span data-ttu-id="c751a-170">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c751a-170">&#8226;</span></span> | <span data-ttu-id="c751a-171">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c751a-171">&#8226;</span></span> | <span data-ttu-id="c751a-172">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c751a-172">&#8226;</span></span> | | <span data-ttu-id="c751a-173">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c751a-173">&#8226;</span></span> |
| <span data-ttu-id="c751a-174">Usługa</span><span class="sxs-lookup"><span data-stu-id="c751a-174">Service</span></span><br><span data-ttu-id="c751a-175">Sieć szkieletowa</span><span class="sxs-lookup"><span data-stu-id="c751a-175">Fabric</span></span> | | | <span data-ttu-id="c751a-176">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c751a-176">&#8226;</span></span> | <span data-ttu-id="c751a-177">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c751a-177">&#8226;</span></span> | <span data-ttu-id="c751a-178">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c751a-178">&#8226;</span></span> | <span data-ttu-id="c751a-179">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c751a-179">&#8226;</span></span> | <span data-ttu-id="c751a-180">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c751a-180">&#8226;</span></span> | <span data-ttu-id="c751a-181">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c751a-181">&#8226;</span></span> | <span data-ttu-id="c751a-182">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c751a-182">&#8226;</span></span> | <span data-ttu-id="c751a-183">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c751a-183">&#8226;</span></span> |
| <span data-ttu-id="c751a-184">Red Hat Otwórz</span><span class="sxs-lookup"><span data-stu-id="c751a-184">Red Hat Open</span></span><br><span data-ttu-id="c751a-185">SHIFT</span><span class="sxs-lookup"><span data-stu-id="c751a-185">Shift</span></span> | | <span data-ttu-id="c751a-186">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c751a-186">&#8226;</span></span> | | <span data-ttu-id="c751a-187">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c751a-187">&#8226;</span></span> | <span data-ttu-id="c751a-188">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c751a-188">&#8226;</span></span>| <span data-ttu-id="c751a-189">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c751a-189">&#8226;</span></span> | <span data-ttu-id="c751a-190">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c751a-190">&#8226;</span></span> | <span data-ttu-id="c751a-191">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c751a-191">&#8226;</span></span> | | <span data-ttu-id="c751a-192">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c751a-192">&#8226;</span></span> |
| <span data-ttu-id="c751a-193">Windows Server</span><span class="sxs-lookup"><span data-stu-id="c751a-193">Windows Server</span></span><br><span data-ttu-id="c751a-194">(autonomiczna)</span><span class="sxs-lookup"><span data-stu-id="c751a-194">(standalone)</span></span> | | | <span data-ttu-id="c751a-195">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c751a-195">&#8226;</span></span> | <span data-ttu-id="c751a-196">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c751a-196">&#8226;</span></span> | <span data-ttu-id="c751a-197">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c751a-197">&#8226;</span></span> | <span data-ttu-id="c751a-198">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c751a-198">&#8226;</span></span> | <span data-ttu-id="c751a-199">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c751a-199">&#8226;</span></span> | <span data-ttu-id="c751a-200">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c751a-200">&#8226;</span></span> | | <span data-ttu-id="c751a-201">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c751a-201">&#8226;</span></span> |
| <span data-ttu-id="c751a-202">Serwer systemu Linux</span><span class="sxs-lookup"><span data-stu-id="c751a-202">Linux Server</span></span><br><span data-ttu-id="c751a-203">(autonomiczna)</span><span class="sxs-lookup"><span data-stu-id="c751a-203">(standalone)</span></span> | | <span data-ttu-id="c751a-204">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c751a-204">&#8226;</span></span> | | <span data-ttu-id="c751a-205">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c751a-205">&#8226;</span></span> | <span data-ttu-id="c751a-206">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c751a-206">&#8226;</span></span> | <span data-ttu-id="c751a-207">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c751a-207">&#8226;</span></span> | <span data-ttu-id="c751a-208">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c751a-208">&#8226;</span></span> | <span data-ttu-id="c751a-209">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c751a-209">&#8226;</span></span> | | <span data-ttu-id="c751a-210">&#8226;</span><span class="sxs-lookup"><span data-stu-id="c751a-210">&#8226;</span></span> |


### <a name="docker-versions-supported-on-linux"></a><span data-ttu-id="c751a-211">Wersje docker obsługiwane w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="c751a-211">Docker versions supported on Linux</span></span>

- <span data-ttu-id="c751a-212">Too1.13 docker 1.11</span><span class="sxs-lookup"><span data-stu-id="c751a-212">Docker 1.11 too1.13</span></span>
- <span data-ttu-id="c751a-213">V17.06 docker CE i EE</span><span class="sxs-lookup"><span data-stu-id="c751a-213">Docker CE and EE v17.06</span></span>

### <a name="x64-linux-distributions-supported-as-container-hosts"></a><span data-ttu-id="c751a-214">x64 dystrybucje systemu Linux obsługiwane jako hosty kontenera</span><span class="sxs-lookup"><span data-stu-id="c751a-214">x64 Linux distributions supported as container hosts</span></span>

- <span data-ttu-id="c751a-215">Ubuntu 14.04 LTS i 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="c751a-215">Ubuntu 14.04 LTS and 16.04 LTS</span></span>
- <span data-ttu-id="c751a-216">CoreOS(stable)</span><span class="sxs-lookup"><span data-stu-id="c751a-216">CoreOS(stable)</span></span>
- <span data-ttu-id="c751a-217">Amazon Linux 2016.09.0</span><span class="sxs-lookup"><span data-stu-id="c751a-217">Amazon Linux 2016.09.0</span></span>
- <span data-ttu-id="c751a-218">openSUSE 13.2</span><span class="sxs-lookup"><span data-stu-id="c751a-218">openSUSE 13.2</span></span>
- <span data-ttu-id="c751a-219">openSUSE LEAP 42.2</span><span class="sxs-lookup"><span data-stu-id="c751a-219">openSUSE LEAP 42.2</span></span>
- <span data-ttu-id="c751a-220">CentOS 7.2 i 7.3</span><span class="sxs-lookup"><span data-stu-id="c751a-220">CentOS 7.2 and 7.3</span></span>
- <span data-ttu-id="c751a-221">SLES 12</span><span class="sxs-lookup"><span data-stu-id="c751a-221">SLES 12</span></span>
- <span data-ttu-id="c751a-222">RHEL 7.2 i 7.3</span><span class="sxs-lookup"><span data-stu-id="c751a-222">RHEL 7.2 and 7.3</span></span>
- <span data-ttu-id="c751a-223">Red Hat OpenShift kontenera platformy (OCP) 3.4 i 3.5</span><span class="sxs-lookup"><span data-stu-id="c751a-223">Red Hat OpenShift Container Platform (OCP) 3.4 and 3.5</span></span>
- <span data-ttu-id="c751a-224">Too1.8.8 DC/OS 1.7.3 ACS Mesosphere</span><span class="sxs-lookup"><span data-stu-id="c751a-224">ACS Mesosphere DC/OS 1.7.3 too1.8.8</span></span>
- <span data-ttu-id="c751a-225">Too1.6 ACS Kubernetes 1.4.5</span><span class="sxs-lookup"><span data-stu-id="c751a-225">ACS Kubernetes 1.4.5 too1.6</span></span>
- <span data-ttu-id="c751a-226">Usługi ACS Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="c751a-226">ACS Docker Swarm</span></span>

### <a name="supported-windows-operating-system"></a><span data-ttu-id="c751a-227">Obsługiwany system operacyjny Windows</span><span class="sxs-lookup"><span data-stu-id="c751a-227">Supported Windows operating system</span></span>

- <span data-ttu-id="c751a-228">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="c751a-228">Windows Server 2016</span></span>
- <span data-ttu-id="c751a-229">Windows 10 Anniversary Edition (Professional lub Enterprise)</span><span class="sxs-lookup"><span data-stu-id="c751a-229">Windows 10 Anniversary Edition (Professional or Enterprise)</span></span>

### <a name="docker-versions-supported-on-windows"></a><span data-ttu-id="c751a-230">Wersje docker obsługiwane w systemie Windows</span><span class="sxs-lookup"><span data-stu-id="c751a-230">Docker versions supported on Windows</span></span>

- <span data-ttu-id="c751a-231">Docker 1.12 i 1.13</span><span class="sxs-lookup"><span data-stu-id="c751a-231">Docker 1.12 and 1.13</span></span>
- <span data-ttu-id="c751a-232">Docker 17.03.0 i nowsze</span><span class="sxs-lookup"><span data-stu-id="c751a-232">Docker 17.03.0 and later</span></span>

## <a name="installing-and-configuring-hello-solution"></a><span data-ttu-id="c751a-233">Instalowanie i konfigurowanie hello rozwiązania</span><span class="sxs-lookup"><span data-stu-id="c751a-233">Installing and configuring hello solution</span></span>
<span data-ttu-id="c751a-234">Użyj powitania po tooinstall informacji i skonfiguruj hello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="c751a-234">Use hello following information tooinstall and configure hello solution.</span></span>

1. <span data-ttu-id="c751a-235">Dodaj hello monitorowania kontenera rozwiązania tooyour obszar roboczy OMS z [witrynę Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ContainersOMS?tab=Overview) lub za pomocą hello procesu opisanego w temacie [rozwiązań analizy dzienników dodać hello galerii rozwiązań](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="c751a-235">Add hello Container Monitoring solution tooyour OMS workspace from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ContainersOMS?tab=Overview) or by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>

2. <span data-ttu-id="c751a-236">Zainstalować i korzystać z agentem pakietu OMS Docker.</span><span class="sxs-lookup"><span data-stu-id="c751a-236">Install and use Docker with an OMS agent.</span></span>  <span data-ttu-id="c751a-237">Oparte na systemie operacyjnym, możesz wybrać z hello następujące metody:</span><span class="sxs-lookup"><span data-stu-id="c751a-237">Based on your operating system, you can choose from hello following methods:</span></span>

  * <span data-ttu-id="c751a-238">W obsługiwanych systemach operacyjnych Linux, zainstaluj i uruchom Docker, a następnie zainstaluj i skonfiguruj hello [Agent pakietu OMS Linux](log-analytics-agent-linux.md).</span><span class="sxs-lookup"><span data-stu-id="c751a-238">On supported Linux operating systems, install and run Docker and then install and configure hello [OMS Agent for Linux](log-analytics-agent-linux.md).</span></span>  
  * <span data-ttu-id="c751a-239">Na CoreOS nie można uruchomić hello Agent pakietu OMS dla systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="c751a-239">On CoreOS, you cannot run hello OMS Agent for Linux.</span></span> <span data-ttu-id="c751a-240">Zamiast tego należy uruchomić konteneryzowanych wersji hello Agent pakietu OMS dla systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="c751a-240">Instead, you run a containerized version of hello OMS Agent for Linux.</span></span> <span data-ttu-id="c751a-241">Przegląd [hostów kontenera systemu Linux, w tym CoreOS](#for-all-linux-container-hosts-including-coreos) lub [hostów kontenera platformy Azure dla instytucji rządowych Linux, w tym CoreOS](#for-all-azure-government-linux-container-hosts-including-coreos) podczas pracy z kontenerami w chmurze Azure dla instytucji rządowych.</span><span class="sxs-lookup"><span data-stu-id="c751a-241">Review [Linux container hosts including CoreOS](#for-all-linux-container-hosts-including-coreos) or [Azure Government Linux container hosts including CoreOS](#for-all-azure-government-linux-container-hosts-including-coreos) if you are working with containers in Azure Government Cloud.</span></span>
  * <span data-ttu-id="c751a-242">W systemie Windows Server 2016 i Windows 10 zainstalować hello aparatem platformy Docker i klienta, a następnie połączyć informacje toogather agenta i wysłać tooLog Analytics.</span><span class="sxs-lookup"><span data-stu-id="c751a-242">On Windows Server 2016 and Windows 10, install hello Docker Engine and client then connect an agent toogather information and send it tooLog Analytics.</span></span>  

### <a name="container-services"></a><span data-ttu-id="c751a-243">Kontener usług</span><span class="sxs-lookup"><span data-stu-id="c751a-243">Container services</span></span>

- <span data-ttu-id="c751a-244">Jeśli masz środowisko Red Hat OpenShift przejrzeć [skonfigurować agenta pakietu OMS dla Red Hat OpenShift](#configure-an-oms-agent-for-red-hat-openshift).</span><span class="sxs-lookup"><span data-stu-id="c751a-244">If you have a Red Hat OpenShift environment, review [Configure an OMS agent for Red Hat OpenShift](#configure-an-oms-agent-for-red-hat-openshift).</span></span>
- <span data-ttu-id="c751a-245">Jeśli masz klaster Kubernetes za pomocą hello usługi kontenera platformy Azure, przejrzyj [monitorować klastra usługi kontenera platformy Azure z Microsoft Operations Management Suite (OMS)](../container-service/kubernetes/container-service-kubernetes-oms.md).</span><span class="sxs-lookup"><span data-stu-id="c751a-245">If you have a Kubernetes cluster using hello Azure Container Service, review [Monitor an Azure Container Service cluster with Microsoft Operations Management Suite (OMS)](../container-service/kubernetes/container-service-kubernetes-oms.md).</span></span>
- <span data-ttu-id="c751a-246">W przypadku klastra usługi kontenera platformy Azure DC/OS więcej w [monitorować klastra usługi kontenera platformy Azure DC/OS w usłudze Operations Management Suite](../container-service/dcos-swarm/container-service-monitoring-oms.md).</span><span class="sxs-lookup"><span data-stu-id="c751a-246">If you have an Azure Container Service DC/OS cluster, learn more at [Monitor an Azure Container Service DC/OS cluster with Operations Management Suite](../container-service/dcos-swarm/container-service-monitoring-oms.md).</span></span>
- <span data-ttu-id="c751a-247">Jeśli masz środowisku trybu Docker Swarm, dowiedzieć się więcej o [skonfigurować agenta pakietu OMS dla rozwiązania Docker Swarm](#configure-an-oms-agent-for-docker-swarm).</span><span class="sxs-lookup"><span data-stu-id="c751a-247">If you have a Docker Swarm mode environment, learn more at [Configure an OMS agent for Docker Swarm](#configure-an-oms-agent-for-docker-swarm).</span></span>
- <span data-ttu-id="c751a-248">Jeśli używasz kontenery z sieci szkieletowej usług dowiedzieć się więcej na [Omówienie usługi Azure Service Fabric](../service-fabric/service-fabric-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c751a-248">If you use containers with Service Fabric, learn more at [Overview of Azure Service Fabric](../service-fabric/service-fabric-overview.md).</span></span>
- <span data-ttu-id="c751a-249">Przejrzyj hello [aparatem platformy Docker w systemie Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon) artykuł, aby uzyskać dodatkowe informacje na temat tooinstall i skonfigurować silnik Docker na komputerach z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="c751a-249">Review hello [Docker Engine on Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon) article for additional information about how tooinstall and configure your Docker Engines on computers running Windows.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c751a-250">Musi być uruchomiona docker **przed** zainstalować hello [Agent pakietu OMS Linux](log-analytics-agent-linux.md) na hostach kontenera.</span><span class="sxs-lookup"><span data-stu-id="c751a-250">Docker must be running **before** you install hello [OMS Agent for Linux](log-analytics-agent-linux.md) on your container hosts.</span></span> <span data-ttu-id="c751a-251">Po zainstalowaniu agenta hello przed zainstalowaniem Docker, należy najpierw hello tooreinstall Agent pakietu OMS dla systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="c751a-251">If you've already installed hello agent before installing Docker, you need tooreinstall hello OMS Agent for Linux.</span></span> <span data-ttu-id="c751a-252">Aby uzyskać więcej informacji na temat rozwiązania Docker Zobacz hello [Docker witryny sieci Web](https://www.docker.com).</span><span class="sxs-lookup"><span data-stu-id="c751a-252">For more information about Docker, see hello [Docker website](https://www.docker.com).</span></span>


## <a name="linux-container-hosts"></a><span data-ttu-id="c751a-253">Hosty kontenera systemu Linux</span><span class="sxs-lookup"><span data-stu-id="c751a-253">Linux container hosts</span></span>

<span data-ttu-id="c751a-254">Po zainstalowaniu Docker Użyj hello następujące ustawienia dla agenta hello tooconfigure hosta kontenera do użycia z Docker.</span><span class="sxs-lookup"><span data-stu-id="c751a-254">After you've installed Docker, use hello following settings for your container host tooconfigure hello agent for use with Docker.</span></span> <span data-ttu-id="c751a-255">Najpierw należy OMS identyfikator i klucz, który można znaleźć w portalu Azure hello.</span><span class="sxs-lookup"><span data-stu-id="c751a-255">First you need your OMS workspace ID and key, which you can find in hello Azure portal.</span></span> <span data-ttu-id="c751a-256">W obszarze roboczym, kliknij przycisk **Szybki Start** > **komputerów** tooview Twojego **identyfikator obszaru roboczego** i **klucz podstawowy**.</span><span class="sxs-lookup"><span data-stu-id="c751a-256">In your workspace, click **Quick Start** > **Computers** tooview your **Workspace ID** and **Primary Key**.</span></span>  <span data-ttu-id="c751a-257">Skopiuj i Wklej zarówno do Twojego ulubionego edytora.</span><span class="sxs-lookup"><span data-stu-id="c751a-257">Copy and paste both into your favorite editor.</span></span>

### <a name="for-all-linux-container-hosts-except-coreos"></a><span data-ttu-id="c751a-258">Dla wszystkich hostów kontenera systemu Linux, z wyjątkiem CoreOS</span><span class="sxs-lookup"><span data-stu-id="c751a-258">For all Linux container hosts except CoreOS</span></span>

- <span data-ttu-id="c751a-259">Aby uzyskać więcej informacji i kroki na jak tooinstall hello Agent pakietu OMS dla systemu Linux, zobacz [połączenia z komputerów z systemem Linux tooOperations Management Suite (OMS)](log-analytics-agent-linux.md).</span><span class="sxs-lookup"><span data-stu-id="c751a-259">For more information and steps on how tooinstall hello OMS Agent for Linux, see [Connect your Linux Computers tooOperations Management Suite (OMS)](log-analytics-agent-linux.md).</span></span>

### <a name="for-all-linux-container-hosts-including-coreos"></a><span data-ttu-id="c751a-260">Dla wszystkich hostów kontenera systemu Linux, łącznie z CoreOS</span><span class="sxs-lookup"><span data-stu-id="c751a-260">For all Linux container hosts including CoreOS</span></span>

<span data-ttu-id="c751a-261">Uruchom hello OMS kontenera, które mają toomonitor.</span><span class="sxs-lookup"><span data-stu-id="c751a-261">Start hello OMS container that you want toomonitor.</span></span> <span data-ttu-id="c751a-262">Zmodyfikuj i użyj hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="c751a-262">Modify and use hello following example:</span></span>

```
sudo docker run --privileged -d -v /var/run/docker.sock:/var/run/docker.sock -e WSID="your workspace id" -e KEY="your key" -h=`hostname` -p 127.0.0.1:25225:25225 --name="omsagent" --restart=always microsoft/oms
```

### <a name="for-all-azure-government-linux-container-hosts-including-coreos"></a><span data-ttu-id="c751a-263">Dla wszystkich hostów kontenera Azure dla instytucji rządowych Linux, łącznie z CoreOS</span><span class="sxs-lookup"><span data-stu-id="c751a-263">For all Azure Government Linux container hosts including CoreOS</span></span>

<span data-ttu-id="c751a-264">Uruchom hello OMS kontenera, które mają toomonitor.</span><span class="sxs-lookup"><span data-stu-id="c751a-264">Start hello OMS container that you want toomonitor.</span></span> <span data-ttu-id="c751a-265">Zmodyfikuj i użyj hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="c751a-265">Modify and use hello following example:</span></span>

```
sudo docker run --privileged -d -v /var/run/docker.sock:/var/run/docker.sock -v /var/log:/var/log -e WSID="your workspace id" -e KEY="your key" -e DOMAIN="opinsights.azure.us" -p 127.0.0.1:25225:25225 -p 127.0.0.1:25224:25224/udp --name="omsagent" -h=`hostname` --restart=always microsoft/oms
```

### <a name="switching-from-using-an-installed-linux-agent-tooone-in-a-container"></a><span data-ttu-id="c751a-266">Zmiana typu zapytania z przy użyciu zainstalowanych tooone agenta systemu Linux w kontenerze</span><span class="sxs-lookup"><span data-stu-id="c751a-266">Switching from using an installed Linux agent tooone in a container</span></span>
<span data-ttu-id="c751a-267">Jeśli wcześniej używana hello bezpośrednio zainstalować agenta i chcesz Użyj tooinstead agenta uruchomionego w kontenerze, należy najpierw usunąć hello Agent pakietu OMS dla systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="c751a-267">If you previously used hello directly-installed agent and want tooinstead use an agent running in a container, you must first remove hello OMS Agent for Linux.</span></span> <span data-ttu-id="c751a-268">Zobacz [hello odinstalowywanie agenta pakietu OMS Linux](log-analytics-agent-linux.md#uninstalling-the-oms-agent-for-linux) toounderstand, jak odinstalować toosuccessfully hello agenta.</span><span class="sxs-lookup"><span data-stu-id="c751a-268">See [Uninstalling hello OMS Agent for Linux](log-analytics-agent-linux.md#uninstalling-the-oms-agent-for-linux) toounderstand how toosuccessfully uninstall hello agent.</span></span>  

### <a name="configure-an-oms-agent-for-docker-swarm"></a><span data-ttu-id="c751a-269">Konfigurowanie agenta pakietu OMS dla rozwiązania Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="c751a-269">Configure an OMS agent for Docker Swarm</span></span>

<span data-ttu-id="c751a-270">Witaj Agent pakietu OMS można uruchomić jako usługę globalnej na Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="c751a-270">You can run hello OMS Agent as a global service on Docker Swarm.</span></span> <span data-ttu-id="c751a-271">Użyj hello następujące informacje toocreate usługi agenta pakietu OMS.</span><span class="sxs-lookup"><span data-stu-id="c751a-271">Use hello following information toocreate an OMS Agent service.</span></span> <span data-ttu-id="c751a-272">Należy tooinsert OMS identyfikator i klucz podstawowy.</span><span class="sxs-lookup"><span data-stu-id="c751a-272">You need tooinsert your OMS Workspace ID and Primary Key.</span></span>

- <span data-ttu-id="c751a-273">Uruchom następujące hello na powitania węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="c751a-273">Run hello following on hello master node.</span></span>

    ```
    sudo docker service create  --name omsagent --mode global  --mount type=bind,source=/var/run/docker.sock,destination=/var/run/docker.sock  -e WSID="<WORKSPACE ID>" -e KEY="<PRIMARY KEY>" -p 25225:25225 -p 25224:25224/udp  --restart-condition=on-failure microsoft/oms
    ```

### <a name="configure-an-oms-agent-for-red-hat-openshift"></a><span data-ttu-id="c751a-274">Konfigurowanie agenta pakietu OMS dla OpenShift Red Hat</span><span class="sxs-lookup"><span data-stu-id="c751a-274">Configure an OMS Agent for Red Hat OpenShift</span></span>
<span data-ttu-id="c751a-275">Istnieją trzy sposoby tooadd hello Agent pakietu OMS tooRed Hat OpenShift toostart zbieranie kontenera danych monitorowania.</span><span class="sxs-lookup"><span data-stu-id="c751a-275">There are three ways tooadd hello OMS Agent tooRed Hat OpenShift toostart collecting container monitoring data.</span></span>

* <span data-ttu-id="c751a-276">[Zainstaluj dla systemu Linux hello Agent pakietu OMS](log-analytics-agent-linux.md) bezpośrednio w każdym węźle OpenShift</span><span class="sxs-lookup"><span data-stu-id="c751a-276">[Install hello OMS Agent for Linux](log-analytics-agent-linux.md) directly on each OpenShift node</span></span>  
* <span data-ttu-id="c751a-277">[Włączanie rozszerzenia maszyny Wirtualnej analizy dziennika](log-analytics-azure-vm-extension.md) w każdym węźle OpenShift znajdującej się na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="c751a-277">[Enable Log Analytics VM Extension](log-analytics-azure-vm-extension.md) on each OpenShift node residing in Azure</span></span>  
* <span data-ttu-id="c751a-278">Zainstaluj agenta pakietu OMS hello jako zestaw demon OpenShift</span><span class="sxs-lookup"><span data-stu-id="c751a-278">Install hello OMS Agent as a OpenShift daemon-set</span></span>  

<span data-ttu-id="c751a-279">W tej sekcji możemy obejmuje jako zbiór demon OpenShift hello kroki wymagane tooinstall hello Agent pakietu OMS.</span><span class="sxs-lookup"><span data-stu-id="c751a-279">In this section we cover hello steps required tooinstall hello OMS Agent as an OpenShift daemon-set.</span></span>  

1. <span data-ttu-id="c751a-280">Zaloguj się na toohello OpenShift głównego węzła i skopiuj hello yaml programu pliku [ocp omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-omsagent.yaml) z usługi GitHub tooyour głównego węzła i zmodyfikować wartość hello za pomocą Identyfikatora obszar roboczy OMS i kluczem podstawowym.</span><span class="sxs-lookup"><span data-stu-id="c751a-280">Sign on toohello OpenShift master node and copy hello yaml file [ocp-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-omsagent.yaml) from GitHub tooyour master node and modify hello value with your OMS Workspace ID and with your Primary Key.</span></span>
2. <span data-ttu-id="c751a-281">Uruchom następujące polecenia toocreate hello projektu dla OMS i ustaw hello konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c751a-281">Run hello following commands toocreate a project for OMS and set hello user account.</span></span>

    ```
    oadm new-project omslogging --node-selector='zone=default'
    oc project omslogging  
    oc create serviceaccount omsagent  
    oadm policy add-cluster-role-to-user cluster-reader   system:serviceaccount:omslogging:omsagent  
    oadm policy add-scc-to-user privileged system:serviceaccount:omslogging:omsagent  
    ```

4. <span data-ttu-id="c751a-282">toodeploy hello demon set, uruchom następujące hello:</span><span class="sxs-lookup"><span data-stu-id="c751a-282">toodeploy hello daemon-set, run hello following:</span></span>

    `oc create -f ocp-omsagent.yaml`

5. <span data-ttu-id="c751a-283">tooverify, który jest skonfigurowany i działa poprawnie, należy wpisać następujące hello:</span><span class="sxs-lookup"><span data-stu-id="c751a-283">tooverify it is configured and working correctly, type hello following:</span></span>

    `oc describe daemonset omsagent`  

    <span data-ttu-id="c751a-284">i przypominało wyjścia hello:</span><span class="sxs-lookup"><span data-stu-id="c751a-284">and hello output should resemble:</span></span>

    ```
    [ocpadmin@khm-0 ~]$ oc describe ds oms  
    Name:           oms  
    Image(s):       microsoft/oms  
    Selector:       name=omsagent  
    Node-Selector:  zone=default  
    Labels:         agentVersion=1.4.0-12  
                    dockerProviderVersion=10.0.0-25  
                    name=omsagent  
    Desired Number of Nodes Scheduled: 3  
    Current Number of Nodes Scheduled: 3  
    Number of Nodes Misscheduled: 0  
    Pods Status:    3 Running / 0 Waiting / 0 Succeeded / 0 Failed  
    No events.  
    ```

<span data-ttu-id="c751a-285">Toosecure kluczy tajnych toouse OMS identyfikator i klucz podstawowy podczas korzystania z pliku zestawu demon yaml programu Agent pakietu OMS hello, wykonać hello następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="c751a-285">If you want toouse secrets toosecure your OMS Workspace ID and Primary Key when using hello OMS Agent daemon-set yaml file, perform hello following steps.</span></span>

1. <span data-ttu-id="c751a-286">Zaloguj się na toohello OpenShift głównego węzła i skopiuj hello yaml programu pliku [ocp-ds-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-ds-omsagent.yaml) i klucz tajny Generowanie skryptu [ocp secretgen.sh](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-secretgen.sh) z usługi GitHub.</span><span class="sxs-lookup"><span data-stu-id="c751a-286">Sign on toohello OpenShift master node and copy hello yaml file [ocp-ds-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-ds-omsagent.yaml) and secret generating script [ocp-secretgen.sh](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-secretgen.sh) from GitHub.</span></span>  <span data-ttu-id="c751a-287">Ten skrypt wygeneruje hello kluczy tajnych yaml programu w pliku klucza podstawowego i identyfikator obszaru roboczego OMS toosecure Twojego secrete informacji.</span><span class="sxs-lookup"><span data-stu-id="c751a-287">This script will generate hello secrets yaml file for OMS Workspace ID and Primary Key toosecure your secrete information.</span></span>  
2. <span data-ttu-id="c751a-288">Uruchom następujące polecenia toocreate hello projektu dla OMS i ustaw hello konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c751a-288">Run hello following commands toocreate a project for OMS and set hello user account.</span></span> <span data-ttu-id="c751a-289">klucz tajny Hello Generowanie skryptu poprosi o podanie Identyfikatora obszar roboczy OMS <WSID> i klucz podstawowy <KEY> i po jego ukończeniu, tworzy plik ocp secret.yaml hello.</span><span class="sxs-lookup"><span data-stu-id="c751a-289">hello secret generating script asks for your OMS Workspace ID <WSID> and Primary Key <KEY> and upon completion, it creates hello ocp-secret.yaml file.</span></span>  

    ```
    oadm new-project omslogging --node-selector='zone=default'  
    oc project omslogging  
    oc create serviceaccount omsagent  
    oadm policy add-cluster-role-to-user cluster-reader   system:serviceaccount:omslogging:omsagent  
    oadm policy add-scc-to-user privileged system:serviceaccount:omslogging:omsagent  
    ```

4. <span data-ttu-id="c751a-290">Wdróż plik tajny hello, uruchamiając następujące hello:</span><span class="sxs-lookup"><span data-stu-id="c751a-290">Deploy hello secret file by running hello following:</span></span>

    `oc create -f ocp-secret.yaml`

5. <span data-ttu-id="c751a-291">Sprawdź wdrożenia, uruchamiając następujące hello:</span><span class="sxs-lookup"><span data-stu-id="c751a-291">Verify deployment by running hello following:</span></span>

    `oc describe secret omsagent-secret`  

    <span data-ttu-id="c751a-292">i przypominało wyjścia hello:</span><span class="sxs-lookup"><span data-stu-id="c751a-292">and hello  output should resemble:</span></span>  

    ```
    [ocpadmin@khocp-master-0 ~]$ oc describe ds oms  
    Name:           oms  
    Image(s):       microsoft/oms  
    Selector:       name=omsagent  
    Node-Selector:  zone=default  
    Labels:         agentVersion=1.4.0-12  
                    dockerProviderVersion=10.0.0-25  
                    name=omsagent  
    Desired Number of Nodes Scheduled: 3  
    Current Number of Nodes Scheduled: 3  
    Number of Nodes Misscheduled: 0  
    Pods Status:    3 Running / 0 Waiting / 0 Succeeded / 0 Failed  
    No events.  
    ```

6. <span data-ttu-id="c751a-293">Wdróż plik zestawu demon yaml programu Agent pakietu OMS hello, uruchamiając następujące hello:</span><span class="sxs-lookup"><span data-stu-id="c751a-293">Deploy hello OMS Agent daemon-set yaml file by running hello following:</span></span>

    `oc create -f ocp-ds-omsagent.yaml`  

7. <span data-ttu-id="c751a-294">Sprawdź wdrożenia, uruchamiając następujące hello:</span><span class="sxs-lookup"><span data-stu-id="c751a-294">Verify deployment by running hello following:</span></span>

    `oc describe ds oms`

    <span data-ttu-id="c751a-295">i przypominało wyjścia hello:</span><span class="sxs-lookup"><span data-stu-id="c751a-295">and hello output should resemble:</span></span>

    ```
    [ocpadmin@khocp-master-0 ~]$ oc describe secret omsagent-secret  
    Name:           omsagent-secret  
    Namespace:      omslogging  
    Labels:         <none>  
    Annotations:    <none>  

    Type:   Opaque  

     Data  
     ====  
     KEY:    89 bytes  
     WSID:   37 bytes  
    ```

### <a name="secure-your-secret-information-for-docker-swarm-and-kubernetes"></a><span data-ttu-id="c751a-296">Zabezpieczanie tajnych informacji o Docker Swarm i Kubernetes</span><span class="sxs-lookup"><span data-stu-id="c751a-296">Secure your secret information for Docker Swarm and Kubernetes</span></span>

<span data-ttu-id="c751a-297">Dla usługi kontenera Kubernetes i Docker Swarm można zabezpieczyć tajny identyfikator OMS i kluczy podstawowych.</span><span class="sxs-lookup"><span data-stu-id="c751a-297">You can secure your secret OMS Workspace ID and Primary Keys for Docker Swarm and Kubernetes container services.</span></span>

#### <a name="secure-secrets-for-docker-swarm"></a><span data-ttu-id="c751a-298">Bezpiecznego hasła dla rozwiązania Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="c751a-298">Secure secrets for Docker Swarm</span></span>

<span data-ttu-id="c751a-299">Dla rozwiązania Docker Swarm, po klucz tajny hello identyfikator obszaru roboczego i klucz podstawowy został utworzony, można uruchomić hello hello usługi Docker dla OMSagent tworzenia.</span><span class="sxs-lookup"><span data-stu-id="c751a-299">For Docker Swarm, once hello secret for Workspace ID and Primary Key is created, you can run hello create hello Docker service for OMSagent.</span></span> <span data-ttu-id="c751a-300">Użyj powitania po toocreate informacji tajnych informacji.</span><span class="sxs-lookup"><span data-stu-id="c751a-300">Use hello following information toocreate your secret information.</span></span>

1. <span data-ttu-id="c751a-301">Uruchom następujące hello na powitania węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="c751a-301">Run hello following on hello master node.</span></span>

    ```
    echo "WSID" | docker secret create WSID -
    echo "KEY" | docker secret create KEY -
    ```

2. <span data-ttu-id="c751a-302">Sprawdź, czy klucze tajne zostały utworzone prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="c751a-302">Verify that secrets were created properly.</span></span>

    ```
    keiko@swarmm-master-13957614-0:/run# sudo docker secret ls
    ```

    ```
    ID                          NAME                CREATED             UPDATED
    j2fj153zxy91j8zbcitnjxjiv   WSID                43 minutes ago      43 minutes ago
    l9rh3n987g9c45zffuxdxetd9   KEY                 38 minutes ago      38 minutes ago
    ```

3. <span data-ttu-id="c751a-303">Witaj uruchom następujące polecenia toomount hello kluczy tajnych toohello konteneryzowanych Agent pakietu OMS.</span><span class="sxs-lookup"><span data-stu-id="c751a-303">Run hello following command toomount hello secrets toohello containerized OMS Agent.</span></span>

    ```
    sudo docker service create  --name omsagent --mode global  --mount type=bind,source=/var/run/docker.sock,destination=/var/run/docker.sock --secret source=WSID,target=WSID --secret source=KEY,target=KEY  -p 25225:25225 -p 25224:25224/udp --restart-condition=on-failure microsoft/oms
    ```

#### <a name="secure-secrets-for-kubernetes-with-yaml-files"></a><span data-ttu-id="c751a-304">Bezpiecznego hasła dla Kubernetes z plikami yaml programu</span><span class="sxs-lookup"><span data-stu-id="c751a-304">Secure secrets for Kubernetes with yaml files</span></span>

<span data-ttu-id="c751a-305">Dla Kubernetes możesz użyć pliku skryptu toogenerate hello kluczy tajnych yaml programu dla identyfikator i klucz podstawowy.</span><span class="sxs-lookup"><span data-stu-id="c751a-305">For Kubernetes, you use a script toogenerate hello secrets yaml file for your Workspace ID and Primary Key.</span></span> <span data-ttu-id="c751a-306">Na powitania [OMS Docker Kubernetes GitHub](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes) są dostępne pliki korzystające z lub bez tajnych informacji.</span><span class="sxs-lookup"><span data-stu-id="c751a-306">At hello [OMS Docker Kubernetes GitHub](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes) page, there are files that you can use with or without your secret information.</span></span>

- <span data-ttu-id="c751a-307">Witaj domyślne DaemonSet Agent pakietu OMS nie ma tajnych informacji (omsagent.yaml)</span><span class="sxs-lookup"><span data-stu-id="c751a-307">hello Default OMS Agent DaemonSet does not have secret information (omsagent.yaml)</span></span>
- <span data-ttu-id="c751a-308">Plik yaml programu DaemonSet Agent pakietu OMS Hello używa tajnych informacji (omsagent-ds-secrets.yaml) z tajny generowania skryptów toogenerate hello kluczy tajnych yaml programu (omsagentsecret.yaml) pliku.</span><span class="sxs-lookup"><span data-stu-id="c751a-308">hello OMS Agent DaemonSet yaml file uses secret information (omsagent-ds-secrets.yaml) with secret generation scripts toogenerate hello secrets yaml (omsagentsecret.yaml) file.</span></span>

<span data-ttu-id="c751a-309">Możesz wybrać omsagent toocreate DaemonSets z lub bez kluczy tajnych.</span><span class="sxs-lookup"><span data-stu-id="c751a-309">You can choose toocreate omsagent DaemonSets with or without secrets.</span></span>

##### <a name="default-omsagent-daemonset-yaml-file-without-secrets"></a><span data-ttu-id="c751a-310">Domyślny OMSagent DaemonSet yaml programu plik bez hasła</span><span class="sxs-lookup"><span data-stu-id="c751a-310">Default OMSagent DaemonSet yaml file without secrets</span></span>

- <span data-ttu-id="c751a-311">Hello domyślne DaemonSet Agent pakietu OMS yaml programu pliku, Zastąp hello `<WSID>` i `<KEY>` tooyour WSID i klucza.</span><span class="sxs-lookup"><span data-stu-id="c751a-311">For hello default OMS Agent DaemonSet yaml file, replace hello `<WSID>` and `<KEY>` tooyour WSID and KEY.</span></span> <span data-ttu-id="c751a-312">Skopiuj hello węzła głównego tooyour plików i hello wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="c751a-312">Copy hello file tooyour master node and run hello following:</span></span>

    ```
    sudo kubectl create -f omsagent.yaml
    ```

##### <a name="default-omsagent-daemonset-yaml-file-with-secrets"></a><span data-ttu-id="c751a-313">Domyślny OMSagent DaemonSet yaml programu plik z kluczy tajnych</span><span class="sxs-lookup"><span data-stu-id="c751a-313">Default OMSagent DaemonSet yaml file with secrets</span></span>

1. <span data-ttu-id="c751a-314">toouse DaemonSet Agent pakietu OMS przy użyciu tajnych informacji kluczy tajnych hello najpierw utworzyć.</span><span class="sxs-lookup"><span data-stu-id="c751a-314">toouse OMS Agent DaemonSet using secret information, create hello secrets first.</span></span>
    1. <span data-ttu-id="c751a-315">Skopiuj skrypt hello i tajne szablonu i upewnij się, że są one na powitania tego samego katalogu.</span><span class="sxs-lookup"><span data-stu-id="c751a-315">Copy hello script and secret template file and make sure they are on hello same directory.</span></span>
        - <span data-ttu-id="c751a-316">Generowanie skryptu - gen.sh klucz tajny klucz tajny</span><span class="sxs-lookup"><span data-stu-id="c751a-316">Secret generating script - secret-gen.sh</span></span>
        - <span data-ttu-id="c751a-317">Szablon tajne — template.yaml klucz tajny</span><span class="sxs-lookup"><span data-stu-id="c751a-317">secret template - secret-template.yaml</span></span>
    2. <span data-ttu-id="c751a-318">Uruchom skrypt hello, takich jak hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="c751a-318">Run hello script, like hello following example.</span></span> <span data-ttu-id="c751a-319">Hello wyświetleniu zapytania o hello OMS identyfikator i klucz podstawowy i po wprowadzeniu ich hello skrypt tworzy plik tajny yaml programu, dlatego może być uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="c751a-319">hello script asks for hello OMS Workspace ID and Primary Key and after you enter them, hello script creates a secret yaml file so you can run it.</span></span>   

        ```
        #> sudo bash ./secret-gen.sh
        ```

    3. <span data-ttu-id="c751a-320">Utwórz pod kluczy tajnych hello, uruchamiając następujące hello:</span><span class="sxs-lookup"><span data-stu-id="c751a-320">Create hello secrets pod by running hello following:</span></span>
        ```
        sudo kubectl create -f omsagentsecret.yaml
        ```

    4. <span data-ttu-id="c751a-321">tooverify, uruchom następujące hello:</span><span class="sxs-lookup"><span data-stu-id="c751a-321">tooverify, run hello following:</span></span>

        ```
        keiko@ubuntu16-13db:~# sudo kubectl get secrets
        ```

        <span data-ttu-id="c751a-322">Dane wyjściowe powinny wyglądać:</span><span class="sxs-lookup"><span data-stu-id="c751a-322">Output should resemble:</span></span>

        ```
        NAME                  TYPE                                  DATA      AGE
        default-token-gvl91   kubernetes.io/service-account-token   3         50d
        omsagent-secret       Opaque                                2         1d
        ```

        ```
        keiko@ubuntu16-13db:~# sudo kubectl describe secrets omsagent-secret
        ```

        <span data-ttu-id="c751a-323">Dane wyjściowe powinny wyglądać:</span><span class="sxs-lookup"><span data-stu-id="c751a-323">Output should resemble:</span></span>

        ```
        Name:           omsagent-secret
        Namespace:      default
        Labels:         <none>
        Annotations:    <none>

        Type:   Opaque

        Data
        ====
        WSID:   36 bytes
        KEY:    88 bytes
        ```

    5. <span data-ttu-id="c751a-324">Tworzenie sieci omsagent demon set, uruchamiając``` sudo kubectl create -f omsagent-ds-secrets.yaml ```</span><span class="sxs-lookup"><span data-stu-id="c751a-324">Create your omsagent daemon-set by running ``` sudo kubectl create -f omsagent-ds-secrets.yaml ```</span></span>

2. <span data-ttu-id="c751a-325">Sprawdź, że powitalne DaemonSet Agent pakietu OMS jest uruchomiona, podobne toohello po:</span><span class="sxs-lookup"><span data-stu-id="c751a-325">Verify that hello OMS Agent DaemonSet is running, similar toohello following:</span></span>

    ```
    keiko@ubuntu16-13db:~# sudo kubectl get ds omsagent
    ```

    ```
    NAME       DESIRED   CURRENT   NODE-SELECTOR   AGE
    omsagent   3         3         <none>          1h
    ```


<span data-ttu-id="c751a-326">Dla Kubernetes należy użyć pliku skryptu toogenerate hello kluczy tajnych yaml programu dla klucza podstawowego i identyfikator obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="c751a-326">For Kubernetes, use a script toogenerate hello secrets yaml file for Workspace ID and Primary Key.</span></span> <span data-ttu-id="c751a-327">Witaj Użyj następujących informacji w przykładzie z hello [pliku yaml programu omsagent](https://github.com/Microsoft/OMS-docker/blob/master/Kubernetes/omsagent.yaml) toosecure tajnych informacji.</span><span class="sxs-lookup"><span data-stu-id="c751a-327">Use hello following example information with hello [omsagent yaml file](https://github.com/Microsoft/OMS-docker/blob/master/Kubernetes/omsagent.yaml) toosecure your secret information.</span></span>

```
keiko@ubuntu16-13db:~# sudo kubectl describe secrets omsagent-secret
Name:           omsagent-secret
Namespace:      default
Labels:         <none>
Annotations:    <none>

Type:   Opaque

Data
====
WSID:   36 bytes
KEY:    88 bytes
```

## <a name="windows-container-hosts"></a><span data-ttu-id="c751a-328">Hosty kontenera systemu Windows</span><span class="sxs-lookup"><span data-stu-id="c751a-328">Windows container hosts</span></span>

### <a name="preparation-before-installing-windows-agents"></a><span data-ttu-id="c751a-329">Przygotowanie przed zainstalowaniem agentów systemu Windows</span><span class="sxs-lookup"><span data-stu-id="c751a-329">Preparation before installing Windows agents</span></span>

<span data-ttu-id="c751a-330">Aby zainstalować agentów na komputerach z systemem Windows, należy tooconfigure hello Docker usługi.</span><span class="sxs-lookup"><span data-stu-id="c751a-330">Before you install agents on computers running Windows, you need tooconfigure hello Docker service.</span></span> <span data-ttu-id="c751a-331">Konfiguracja Hello pozwala hello Windows agenta lub hello analizy dzienników maszyny wirtualnej rozszerzenia toouse hello gniazda Docker TCP, dzięki czemu agenci hello dostęp zdalnie demon Docker hello i toocapture danych monitorowania.</span><span class="sxs-lookup"><span data-stu-id="c751a-331">hello configuration allows hello Windows agent or hello Log Analytics virtual machine extension toouse hello Docker TCP socket so that hello agents can access hello Docker daemon remotely and toocapture data for monitoring.</span></span>

#### <a name="toostart-docker-and-verify-its-configuration"></a><span data-ttu-id="c751a-332">toostart Docker i sprawdzić jego konfigurację</span><span class="sxs-lookup"><span data-stu-id="c751a-332">toostart Docker and verify its configuration</span></span>

<span data-ttu-id="c751a-333">Istnieją tooset kroki niezbędne w górę TCP nazwany potok dla systemu Windows Server:</span><span class="sxs-lookup"><span data-stu-id="c751a-333">There are steps needed tooset up TCP named pipe for Windows Server:</span></span>

1. <span data-ttu-id="c751a-334">W programie Windows PowerShell umożliwiają potoku TCP i nazwanego potoku.</span><span class="sxs-lookup"><span data-stu-id="c751a-334">In Windows PowerShell, enable TCP pipe and named pipe.</span></span>

    ```
    Stop-Service docker
    dockerd --unregister-service
    dockerd --register-service -H npipe:// -H 0.0.0.0:2375  
    Start-Service docker
    ```

2. <span data-ttu-id="c751a-335">Konfigurowanie Docker z pliku konfiguracyjnego hello potoku TCP i nazwany potok.</span><span class="sxs-lookup"><span data-stu-id="c751a-335">Configure Docker with hello configuration file for TCP pipe and named pipe.</span></span> <span data-ttu-id="c751a-336">plik konfiguracji Hello znajduje się w C:\ProgramData\docker\config\daemon.json.</span><span class="sxs-lookup"><span data-stu-id="c751a-336">hello configuration file is located at C:\ProgramData\docker\config\daemon.json.</span></span>

    <span data-ttu-id="c751a-337">W pliku daemon.json hello potrzebne są następujące hello:</span><span class="sxs-lookup"><span data-stu-id="c751a-337">In hello daemon.json file, you will need hello following:</span></span>

    ```
    {
    "hosts": ["tcp://0.0.0.0:2375", "npipe://"]
    }
    ```

<span data-ttu-id="c751a-338">Aby uzyskać więcej informacji na temat konfiguracji demon Docker hello używane z kontenerami systemu Windows, temacie [aparatem platformy Docker w systemie Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon).</span><span class="sxs-lookup"><span data-stu-id="c751a-338">For more information about hello Docker daemon configuration used with Windows Containers, see [Docker Engine on Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon).</span></span>


### <a name="install-windows-agents"></a><span data-ttu-id="c751a-339">Zainstaluj agentów systemu Windows</span><span class="sxs-lookup"><span data-stu-id="c751a-339">Install Windows agents</span></span>

<span data-ttu-id="c751a-340">tooenable systemu Windows i kontener funkcji Hyper-V, monitorowanie, należy zainstalować hello Microsoft Monitoring Agent (MMA) na komputerach z systemem Windows, które są hostami kontenera.</span><span class="sxs-lookup"><span data-stu-id="c751a-340">tooenable Windows and Hyper-V container monitoring, install hello Microsoft Monitoring Agent (MMA) on Windows computers that are container hosts.</span></span> <span data-ttu-id="c751a-341">Na komputerach z systemem Windows w środowisku lokalnym, zobacz [tooLog komputerów Windows połączyć Analytics](log-analytics-windows-agents.md).</span><span class="sxs-lookup"><span data-stu-id="c751a-341">For computers running Windows in your on-premises environment, see [Connect Windows computers tooLog Analytics](log-analytics-windows-agents.md).</span></span> <span data-ttu-id="c751a-342">W przypadku maszyn wirtualnych działających na platformie Azure, podłącz je tooLog Analytics przy użyciu hello [rozszerzenie maszyny wirtualnej](log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="c751a-342">For virtual machines running in Azure, connect them tooLog Analytics using hello [virtual machine extension](log-analytics-azure-vm-extension.md).</span></span>

<span data-ttu-id="c751a-343">Można monitorować kontenery systemu Windows uruchomiona na sieć szkieletowa usług.</span><span class="sxs-lookup"><span data-stu-id="c751a-343">You can monitor Windows containers running on Service Fabric.</span></span> <span data-ttu-id="c751a-344">Jednak tylko [maszyn wirtualnych działających na platformie Azure](log-analytics-azure-vm-extension.md) i [komputery z systemem Windows w środowisku lokalnym](log-analytics-windows-agents.md) są obecnie obsługiwane dla sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="c751a-344">However, only [virtual machines running in Azure](log-analytics-azure-vm-extension.md) and [computers running Windows in your on-premises environment](log-analytics-windows-agents.md) are currently supported for Service Fabric.</span></span>

<span data-ttu-id="c751a-345">Możesz sprawdzić, czy ten hello rozwiązanie monitorowanie kontenera jest prawidłowo dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="c751a-345">You can verify that hello Container Monitoring solution is set correctly for Windows.</span></span> <span data-ttu-id="c751a-346">toocheck czy pakiet administracyjny hello pobierania został poprawnie, wyszukaj *ContainerManagement.xxx*.</span><span class="sxs-lookup"><span data-stu-id="c751a-346">toocheck whether hello management pack was download properly, look for *ContainerManagement.xxx*.</span></span> <span data-ttu-id="c751a-347">pliki Hello powinny być w folderze C:\Program Files\Microsoft Monitoring Agent\Agent\Health usługi State\Management pakietów hello.</span><span class="sxs-lookup"><span data-stu-id="c751a-347">hello files should be in hello C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs folder.</span></span>


## <a name="solution-components"></a><span data-ttu-id="c751a-348">Składniki rozwiązania</span><span class="sxs-lookup"><span data-stu-id="c751a-348">Solution components</span></span>

<span data-ttu-id="c751a-349">Jeśli korzystasz z agentów systemu Windows, następnie hello następujący pakiet administracyjny jest zainstalowany na każdym komputerze z agentem po dodaniu tego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="c751a-349">If you are using Windows agents, then hello following management pack is installed on each computer with an agent when you add this solution.</span></span> <span data-ttu-id="c751a-350">Jest niezbędny hello pakietu administracyjnego nie konfiguracji lub konserwacji.</span><span class="sxs-lookup"><span data-stu-id="c751a-350">No configuration or maintenance is required for hello management pack.</span></span>

- <span data-ttu-id="c751a-351">*ContainerManagement.xxx* zainstalowane w C:\Program Files\Microsoft Monitoring Agent\Agent\Health usługi State\Management pakietów</span><span class="sxs-lookup"><span data-stu-id="c751a-351">*ContainerManagement.xxx* installed in C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs</span></span>

## <a name="container-data-collection-details"></a><span data-ttu-id="c751a-352">Szczegóły pobierania danych kontenera</span><span class="sxs-lookup"><span data-stu-id="c751a-352">Container data collection details</span></span>
<span data-ttu-id="c751a-353">Hello rozwiązanie monitorowanie kontenera zbiera różne metryki i dziennika dane dotyczące wydajności z kontenera hostów i kontenerów przy użyciu agentów, które można włączyć.</span><span class="sxs-lookup"><span data-stu-id="c751a-353">hello Container Monitoring solution collects various performance metrics and log data from container hosts and containers using agents that you enable.</span></span>

<span data-ttu-id="c751a-354">Dane są gromadzone co 3 minuty przez hello następujące typy agenta.</span><span class="sxs-lookup"><span data-stu-id="c751a-354">Data is collected every three minutes by hello following agent types.</span></span>

- [<span data-ttu-id="c751a-355">Agent pakietu OMS dla systemu Linux</span><span class="sxs-lookup"><span data-stu-id="c751a-355">OMS Agent for Linux</span></span>](log-analytics-linux-agents.md)
- [<span data-ttu-id="c751a-356">Agent systemu Windows</span><span class="sxs-lookup"><span data-stu-id="c751a-356">Windows agent</span></span>](log-analytics-windows-agents.md)
- [<span data-ttu-id="c751a-357">Rozszerzenia maszyny Wirtualnej analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="c751a-357">Log Analytics VM extension</span></span>](log-analytics-azure-vm-extension.md)


### <a name="container-records"></a><span data-ttu-id="c751a-358">Rejestruje kontenera</span><span class="sxs-lookup"><span data-stu-id="c751a-358">Container records</span></span>

<span data-ttu-id="c751a-359">Witaj poniższej tabeli przedstawiono przykłady rekordów zebrane przez rozwiązanie monitorowanie kontenera hello i hello typów danych, które są wyświetlane w wynikach wyszukiwania dziennika.</span><span class="sxs-lookup"><span data-stu-id="c751a-359">hello following table shows examples of records collected by hello Container Monitoring solution and hello data types that appear in log search results.</span></span>

| <span data-ttu-id="c751a-360">Typ danych</span><span class="sxs-lookup"><span data-stu-id="c751a-360">Data type</span></span> | <span data-ttu-id="c751a-361">Typ danych w dzienniku wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="c751a-361">Data type in Log Search</span></span> | <span data-ttu-id="c751a-362">Pola</span><span class="sxs-lookup"><span data-stu-id="c751a-362">Fields</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c751a-363">Wydajność dla hostów i kontenerów</span><span class="sxs-lookup"><span data-stu-id="c751a-363">Performance for hosts and containers</span></span> | `Type=Perf` | <span data-ttu-id="c751a-364">Komputer, nazwa obiektu, CounterName &#40; czas procesora (%), dysk odczytuje MB, dysku zapisuje MB, użycie pamięć (MB), sieci odbieranie bajtów, sieci wysyłania w bajtach, procesor s użycia sieci &#41; równowartości, TimeGenerated, Ścieżka_licznika, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="c751a-364">Computer, ObjectName, CounterName &#40;%Processor Time, Disk Reads MB, Disk Writes MB, Memory Usage MB, Network Receive Bytes, Network Send Bytes, Processor Usage sec, Network&#41;, CounterValue,TimeGenerated, CounterPath, SourceSystem</span></span> |
| <span data-ttu-id="c751a-365">Kontener magazynu</span><span class="sxs-lookup"><span data-stu-id="c751a-365">Container inventory</span></span> | `Type=ContainerInventory` | <span data-ttu-id="c751a-366">TimeGenerated, komputera, nazwę kontenera, ContainerHostname, obraz, ImageTag, ContainerState, ExitCode, EnvironmentVar, polecenia, CreatedTime, StartedTime, FinishedTime, SourceSystem, identyfikatora kontenera, ImageID</span><span class="sxs-lookup"><span data-stu-id="c751a-366">TimeGenerated, Computer, container name, ContainerHostname, Image, ImageTag, ContainerState, ExitCode, EnvironmentVar, Command, CreatedTime, StartedTime, FinishedTime, SourceSystem, ContainerID, ImageID</span></span> |
| <span data-ttu-id="c751a-367">Kontener magazynu obrazu</span><span class="sxs-lookup"><span data-stu-id="c751a-367">Container image inventory</span></span> | `Type=ContainerImageInventory` | <span data-ttu-id="c751a-368">TimeGenerated, komputer, obraz, ImageTag, ImageSize, VirtualSize, działa wstrzymana, zatrzymana, nie powiodło się, SourceSystem, ImageID, TotalContainer</span><span class="sxs-lookup"><span data-stu-id="c751a-368">TimeGenerated, Computer, Image, ImageTag, ImageSize, VirtualSize, Running, Paused, Stopped, Failed, SourceSystem, ImageID, TotalContainer</span></span> |
| <span data-ttu-id="c751a-369">Kontener dziennika</span><span class="sxs-lookup"><span data-stu-id="c751a-369">Container log</span></span> | `Type=ContainerLog` | <span data-ttu-id="c751a-370">TimeGenerated, komputer, identyfikator obrazu, nazwy kontenera, LogEntrySource, LogEntry, SourceSystem, identyfikatora kontenera</span><span class="sxs-lookup"><span data-stu-id="c751a-370">TimeGenerated, Computer, image ID, container name, LogEntrySource, LogEntry, SourceSystem, ContainerID</span></span> |
| <span data-ttu-id="c751a-371">Dziennik usługi kontenera</span><span class="sxs-lookup"><span data-stu-id="c751a-371">Container service log</span></span> | `Type=ContainerServiceLog`  | <span data-ttu-id="c751a-372">TimeGenerated, komputer, TimeOfCommand, obraz, polecenia, SourceSystem, identyfikatora kontenera</span><span class="sxs-lookup"><span data-stu-id="c751a-372">TimeGenerated, Computer, TimeOfCommand, Image, Command, SourceSystem, ContainerID</span></span> |
| <span data-ttu-id="c751a-373">Kontener węzła magazynu</span><span class="sxs-lookup"><span data-stu-id="c751a-373">Container node inventory</span></span> | `Type=ContainerNodeInventory_CL`| <span data-ttu-id="c751a-374">TimeGenerated, komputer, ClassName_s, DockerVersion_s, OperatingSystem_s, Volume_s, Network_s, NodeRole_s, OrchestratorType_s, InstanceID_g, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="c751a-374">TimeGenerated, Computer, ClassName_s, DockerVersion_s, OperatingSystem_s, Volume_s, Network_s, NodeRole_s, OrchestratorType_s, InstanceID_g, SourceSystem</span></span>|
| <span data-ttu-id="c751a-375">Kubernetes spisu</span><span class="sxs-lookup"><span data-stu-id="c751a-375">Kubernetes inventory</span></span> | `Type=KubePodInventory_CL` | <span data-ttu-id="c751a-376">TimeGenerated, komputer, PodLabel_deployment_s, PodLabel_deploymentconfig_s, PodLabel_docker_registry_s, Name_s, Namespace_s, PodStatus_s, PodIp_s, PodUid_g, PodCreationTimeStamp_t, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="c751a-376">TimeGenerated, Computer, PodLabel_deployment_s, PodLabel_deploymentconfig_s, PodLabel_docker_registry_s, Name_s, Namespace_s, PodStatus_s, PodIp_s, PodUid_g, PodCreationTimeStamp_t, SourceSystem</span></span> |
| <span data-ttu-id="c751a-377">Proces kontenera</span><span class="sxs-lookup"><span data-stu-id="c751a-377">Container process</span></span> | `Type=ContainerProcess_CL` | <span data-ttu-id="c751a-378">TimeGenerated, komputer, Pod_s, Namespace_s, ClassName_s, InstanceID_s, Uid_s, PID_s, PPID_s, C_s, STIME_s, Tty_s, TIME_s, Cmd_s, Id_s, Name_s, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="c751a-378">TimeGenerated, Computer, Pod_s, Namespace_s, ClassName_s, InstanceID_s, Uid_s, PID_s, PPID_s, C_s, STIME_s, Tty_s, TIME_s, Cmd_s, Id_s, Name_s, SourceSystem</span></span> |
| <span data-ttu-id="c751a-379">Zdarzenia Kubernetes</span><span class="sxs-lookup"><span data-stu-id="c751a-379">Kubernetes events</span></span> | `Type=KubeEvents_CL` | <span data-ttu-id="c751a-380">TimeGenerated, komputer, Name_s, ObjectKind_s, Namespace_s, Reason_s, Type_s, SourceComponent_s, SourceSystem, komunikatów</span><span class="sxs-lookup"><span data-stu-id="c751a-380">TimeGenerated, Computer, Name_s, ObjectKind_s, Namespace_s, Reason_s, Type_s, SourceComponent_s, SourceSystem, Message</span></span> |

<span data-ttu-id="c751a-381">Etykiety dołączany zbyt*PodLabel* typy danych są etykiet niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="c751a-381">Labels appended too*PodLabel* data types are your own custom labels.</span></span> <span data-ttu-id="c751a-382">Witaj dołączany PodLabel etykiety tabelą hello znajdują się przykłady.</span><span class="sxs-lookup"><span data-stu-id="c751a-382">hello appended PodLabel labels shown in hello table are examples.</span></span> <span data-ttu-id="c751a-383">Tak `PodLabel_deployment_s`, `PodLabel_deploymentconfig_s`, `PodLabel_docker_registry_s` różnią się w zestawie danych w danym środowisku, a objęty przypominać `PodLabel_yourlabel_s`.</span><span class="sxs-lookup"><span data-stu-id="c751a-383">So, `PodLabel_deployment_s`, `PodLabel_deploymentconfig_s`, `PodLabel_docker_registry_s` will differ in your environment's data set and generically resemble `PodLabel_yourlabel_s`.</span></span>


## <a name="monitor-containers"></a><span data-ttu-id="c751a-384">Kontenery monitora</span><span class="sxs-lookup"><span data-stu-id="c751a-384">Monitor containers</span></span>
<span data-ttu-id="c751a-385">Po utworzeniu rozwiązania hello włączone w portalu OMS hello hello **kontenery** kafelka zawiera podsumowanie informacji o hostach kontenera i kontenery hello uruchomione na hostach.</span><span class="sxs-lookup"><span data-stu-id="c751a-385">After you have hello solution enabled in hello OMS portal, hello **Containers** tile shows summary information about your container hosts and hello containers running in hosts.</span></span>

![Kontenery kafelka](./media/log-analytics-containers/containers-title.png)

<span data-ttu-id="c751a-387">Kafelek Hello przedstawiono przegląd liczbę kontenerów masz w środowisku hello i czy jest nie, uruchamiania i zatrzymywana.</span><span class="sxs-lookup"><span data-stu-id="c751a-387">hello tile shows an overview of how many containers you have in hello environment and whether they're failed, running, or stopped.</span></span>

### <a name="using-hello-containers-dashboard"></a><span data-ttu-id="c751a-388">Przy użyciu pulpitu nawigacyjnego kontenery hello</span><span class="sxs-lookup"><span data-stu-id="c751a-388">Using hello Containers dashboard</span></span>
<span data-ttu-id="c751a-389">Kliknij przycisk hello **kontenery** kafelka.</span><span class="sxs-lookup"><span data-stu-id="c751a-389">Click hello **Containers** tile.</span></span> <span data-ttu-id="c751a-390">Z tego miejsca zobaczysz widoki uporządkowane według:</span><span class="sxs-lookup"><span data-stu-id="c751a-390">From there you'll see views organized by:</span></span>

- <span data-ttu-id="c751a-391">**Kontenery zdarzeń** -pokazuje stan kontenera i komputerów z kontenerami nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="c751a-391">**Container Events** - Shows container status and computers with failed containers.</span></span>
- <span data-ttu-id="c751a-392">**Dzienniki kontenera** — przedstawia wykres kontenera pliki dziennika wygenerowane przez czas i listę komputerów z hello największa liczba plików dziennika.</span><span class="sxs-lookup"><span data-stu-id="c751a-392">**Container Logs** - Shows a chart of container log files generated over time and a list of computers with hello highest number of log files.</span></span>
- <span data-ttu-id="c751a-393">**Zdarzenia Kubernetes** — przedstawia wykres Kubernetes zdarzenia generowane przez czas i listę przyczyn hello Dlaczego stanowiskami wygenerowany hello zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="c751a-393">**Kubernetes Events** - Shows a chart of Kubernetes events generated over time and a list of hello reasons why pods generated hello events.</span></span> <span data-ttu-id="c751a-394">*Ten zestaw danych jest używany tylko w środowiskach Linux.*</span><span class="sxs-lookup"><span data-stu-id="c751a-394">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="c751a-395">**Spis Namespace Kubernetes** — pokazuje liczbę hello obszary nazw i stanowiskami i przedstawiono ich hierarchii.</span><span class="sxs-lookup"><span data-stu-id="c751a-395">**Kubernetes Namespace Inventory** - Shows hello number of namespaces and pods and shows their hierarchy.</span></span> <span data-ttu-id="c751a-396">*Ten zestaw danych jest używany tylko w środowiskach Linux.*</span><span class="sxs-lookup"><span data-stu-id="c751a-396">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="c751a-397">**Kontener węzeł spisu** — pokazuje liczbę hello typów aranżacji używanych na hosty węzłów kontenera.</span><span class="sxs-lookup"><span data-stu-id="c751a-397">**Container Node Inventory** - Shows hello number of orchestration types used on container nodes/hosts.</span></span> <span data-ttu-id="c751a-398">hosty węzłów komputera Hello są również wyświetlane według hello liczbę kontenerów.</span><span class="sxs-lookup"><span data-stu-id="c751a-398">hello computer nodes/hosts are also listed by hello number of containers.</span></span> <span data-ttu-id="c751a-399">*Ten zestaw danych jest używany tylko w środowiskach Linux.*</span><span class="sxs-lookup"><span data-stu-id="c751a-399">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="c751a-400">**Kontener obrazów spisu** -pokazuje hello całkowita liczba kontenera obrazy używane oraz liczbę typów obrazów.</span><span class="sxs-lookup"><span data-stu-id="c751a-400">**Container Images Inventory** - Shows hello total number of container images used and number of image types.</span></span> <span data-ttu-id="c751a-401">Hello liczbę obrazów są również wyświetlane według hello tag obrazu.</span><span class="sxs-lookup"><span data-stu-id="c751a-401">hello number of images are also listed by hello image tag.</span></span>
- <span data-ttu-id="c751a-402">**Stan kontenery** — przedstawia hello łączna liczba kontenera Komputery węzłów/hosta uruchomionych kontenerów.</span><span class="sxs-lookup"><span data-stu-id="c751a-402">**Containers Status** - Shows hello total number of container nodes/host computers that have running containers.</span></span> <span data-ttu-id="c751a-403">Komputery są także wyświetlane według liczby hello systemem hostów.</span><span class="sxs-lookup"><span data-stu-id="c751a-403">Computers are also listed by hello number of running hosts.</span></span>
- <span data-ttu-id="c751a-404">**Proces kontenera** — przedstawia wykres liniowy procesów kontenera działających w czasie.</span><span class="sxs-lookup"><span data-stu-id="c751a-404">**Container Process** - Shows a line chart of container processes running over time.</span></span> <span data-ttu-id="c751a-405">Kontenery znajdują się przez uruchomienie polecenia procesu w kontenerach.</span><span class="sxs-lookup"><span data-stu-id="c751a-405">Containers are also listed by running command/process within containers.</span></span> <span data-ttu-id="c751a-406">*Ten zestaw danych jest używany tylko w środowiskach Linux.*</span><span class="sxs-lookup"><span data-stu-id="c751a-406">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="c751a-407">**Wydajność Procesora kontenera** — przedstawia wykres liniowy w hello średnie wykorzystanie procesora CPU wraz z upływem czasu hosty węzłów komputera.</span><span class="sxs-lookup"><span data-stu-id="c751a-407">**Container CPU Performance** - Shows a line chart of hello average CPU utilization over time for computer nodes/hosts.</span></span> <span data-ttu-id="c751a-408">Również komputera hello listy węzłów/hostów na podstawie średniego użycia Procesora.</span><span class="sxs-lookup"><span data-stu-id="c751a-408">Also lists hello computer nodes/hosts based on average CPU utilization.</span></span>
- <span data-ttu-id="c751a-409">**Kontener wydajności pamięci** — przedstawia wykres liniowy użycia pamięci w czasie.</span><span class="sxs-lookup"><span data-stu-id="c751a-409">**Container Memory Performance** - Shows a line chart of memory usage over time.</span></span> <span data-ttu-id="c751a-410">Zawiera także listę wykorzystania opartego na nazwie wystąpienia pamięci komputera.</span><span class="sxs-lookup"><span data-stu-id="c751a-410">Also lists computer memory utilization based on instance name.</span></span>
- <span data-ttu-id="c751a-411">**Wydajność komputera** — zawiera wykresy liniowe hello procent wydajności Procesora w czasie, procent użycia pamięci przez czas i megabajtów wolnego miejsca na dysku wraz z upływem czasu.</span><span class="sxs-lookup"><span data-stu-id="c751a-411">**Computer Performance** - Shows line charts of hello percent of CPU performance over time, percent of memory usage over time, and megabytes of free disk space over time.</span></span> <span data-ttu-id="c751a-412">Aktywuj przez dowolny wiersz tooview wykresu więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="c751a-412">You can hover over any line in a chart tooview more details.</span></span>


<span data-ttu-id="c751a-413">Każdy obszar pulpitu nawigacyjnego hello jest wizualną reprezentację wyszukiwania, które jest uruchamiane na zebranych danych.</span><span class="sxs-lookup"><span data-stu-id="c751a-413">Each area of hello dashboard is a visual representation of a search that is run on collected data.</span></span>

![Kontenery pulpitu nawigacyjnego](./media/log-analytics-containers/containers-dash01.png)

![Kontenery pulpitu nawigacyjnego](./media/log-analytics-containers/containers-dash02.png)

<span data-ttu-id="c751a-416">W hello **stan kontenera** obszarze kliknij górny obszar hello, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="c751a-416">In hello **Container Status** area, click hello top area, as shown below.</span></span>

![Stan kontenerów](./media/log-analytics-containers/containers-status.png)

<span data-ttu-id="c751a-418">Otwiera dziennik wyszukiwania, wyświetlania informacji o stanie hello kontenerów.</span><span class="sxs-lookup"><span data-stu-id="c751a-418">Log Search opens, displaying information about hello state of your containers.</span></span>

![Dziennik wyszukiwania dla kontenerów](./media/log-analytics-containers/containers-log-search.png)

<span data-ttu-id="c751a-420">W tym miejscu można edytować toomodify zapytania wyszukiwania hello go toofind hello określone informacje Cię interesują.</span><span class="sxs-lookup"><span data-stu-id="c751a-420">From here, you can edit hello search query toomodify it toofind hello specific information you're interested in.</span></span> <span data-ttu-id="c751a-421">Aby uzyskać więcej informacji na temat wyszukiwania dziennika, zobacz [Zaloguj wyszukiwania analizy dzienników](log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="c751a-421">For more information about Log Searches, see [Log searches in Log Analytics](log-analytics-log-searches.md).</span></span>

## <a name="troubleshoot-by-finding-a-failed-container"></a><span data-ttu-id="c751a-422">Rozwiązywanie problemów z znajdując kontenera nie powiodło się</span><span class="sxs-lookup"><span data-stu-id="c751a-422">Troubleshoot by finding a failed container</span></span>

<span data-ttu-id="c751a-423">Analiza dzienników oznacza kontener jako **nie powiodło się** Jeśli został zakończony z kodem zakończenia inną niż zero.</span><span class="sxs-lookup"><span data-stu-id="c751a-423">Log Analytics marks a container as **Failed** if it has exited with a non-zero exit code.</span></span> <span data-ttu-id="c751a-424">Można zapoznać się z omówieniem hello błędów i awarii w środowisku hello w hello **nie powiodło się kontenery** obszaru.</span><span class="sxs-lookup"><span data-stu-id="c751a-424">You can see an overview of hello errors and failures in hello environment in hello **Failed Containers** area.</span></span>

### <a name="toofind-failed-containers"></a><span data-ttu-id="c751a-425">kontenery toofind nie powiodło się</span><span class="sxs-lookup"><span data-stu-id="c751a-425">toofind failed containers</span></span>
1. <span data-ttu-id="c751a-426">Kliknij przycisk hello **stan kontenera** obszaru.</span><span class="sxs-lookup"><span data-stu-id="c751a-426">Click hello **Container Status** area.</span></span>  
   <span data-ttu-id="c751a-427">![Stan kontenerów](./media/log-analytics-containers/containers-status.png)</span><span class="sxs-lookup"><span data-stu-id="c751a-427">![containers status](./media/log-analytics-containers/containers-status.png)</span></span>
2. <span data-ttu-id="c751a-428">Dziennik wyszukiwania otwiera i wyświetla stan hello kontenerów, podobne toohello następujące.</span><span class="sxs-lookup"><span data-stu-id="c751a-428">Log Search opens and displays hello state of your containers, similar toohello following.</span></span>  
   ![Stan kontenerów](./media/log-analytics-containers/containers-log-search.png)
3. <span data-ttu-id="c751a-430">Następnie kliknij przycisk hello agregowane wartości dodatkowych informacji tooview kontenery nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="c751a-430">Next, click hello aggregated value of failed containers tooview additional information.</span></span> <span data-ttu-id="c751a-431">Rozwiń węzeł **Pokaż więcej** identyfikator tooview hello obrazu.</span><span class="sxs-lookup"><span data-stu-id="c751a-431">Expand **show more** tooview hello image ID.</span></span>  
   <span data-ttu-id="c751a-432">![kontenery nie powiodło się](./media/log-analytics-containers/containers-state-failed.png)</span><span class="sxs-lookup"><span data-stu-id="c751a-432">![failed containers](./media/log-analytics-containers/containers-state-failed.png)</span></span>  
4. <span data-ttu-id="c751a-433">Następnie wpisz następujące hello hello zapytania wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="c751a-433">Next, type hello following in hello search query.</span></span> <span data-ttu-id="c751a-434">`Type=ContainerInventory <ImageID>`Szczegóły toosee obraz powitania, takich jak rozmiar obrazu i Liczba obrazów zatrzymane, a nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="c751a-434">`Type=ContainerInventory <ImageID>` toosee details about hello image such as image size and number of stopped and failed images.</span></span>  
   <span data-ttu-id="c751a-435">![kontenery nie powiodło się](./media/log-analytics-containers/containers-failed04.png)</span><span class="sxs-lookup"><span data-stu-id="c751a-435">![failed containers](./media/log-analytics-containers/containers-failed04.png)</span></span>

## <a name="search-logs-for-container-data"></a><span data-ttu-id="c751a-436">Dzienniki wyszukiwania danych kontenera</span><span class="sxs-lookup"><span data-stu-id="c751a-436">Search logs for container data</span></span>
<span data-ttu-id="c751a-437">W przypadku Rozwiązywanie problemów z określonego błędu, ułatwia toosee, gdzie występuje w danym środowisku.</span><span class="sxs-lookup"><span data-stu-id="c751a-437">When you're troubleshooting a specific error, it can help toosee where it is occurring in your environment.</span></span> <span data-ttu-id="c751a-438">następujące typy dziennika Hello pomoże Ci tworzenie zapytań tooreturn hello informacje, które mają.</span><span class="sxs-lookup"><span data-stu-id="c751a-438">hello following log types will help you create queries tooreturn hello information you want.</span></span>


- <span data-ttu-id="c751a-439">**ContainerImageInventory** — Użyj tego typu, jeśli próbujesz informacji toofind uporządkowane według obrazu i tooview informacje obrazu, takie jak identyfikatorów obrazów lub rozmiary.</span><span class="sxs-lookup"><span data-stu-id="c751a-439">**ContainerImageInventory** – Use this type when you're trying toofind information organized by image and tooview image information such as image IDs or sizes.</span></span>
- <span data-ttu-id="c751a-440">**ContainerInventory** — tego typu należy używać informacji o lokalizację kontenera, ich nazwy są i jakie obrazy są na nich uruchomione.</span><span class="sxs-lookup"><span data-stu-id="c751a-440">**ContainerInventory** – Use this type when you want information about container location, what their names are, and what images they're running.</span></span>
- <span data-ttu-id="c751a-441">**ContainerLog** — tego typu należy używać toofind błędu dziennika informacji i zapisów.</span><span class="sxs-lookup"><span data-stu-id="c751a-441">**ContainerLog** – Use this type when you want toofind specific error log information and entries.</span></span>
- <span data-ttu-id="c751a-442">**ContainerNodeInventory_CL** tego typu należy używać hello informacji o hoście/węzła gdzie są znajdującej się kontenerów.</span><span class="sxs-lookup"><span data-stu-id="c751a-442">**ContainerNodeInventory_CL**  Use this type when you want hello information about host/node where containers are residing.</span></span> <span data-ttu-id="c751a-443">Umożliwia Docker wersji, typ aranżacji magazynu i informacje o sieci.</span><span class="sxs-lookup"><span data-stu-id="c751a-443">It provides you Docker version, orchestration type, storage, and network information.</span></span>
- <span data-ttu-id="c751a-444">**ContainerProcess_CL** proces hello uruchomiony w kontenerze hello Zobacz Użyj tooquickly tego typu.</span><span class="sxs-lookup"><span data-stu-id="c751a-444">**ContainerProcess_CL** Use this type tooquickly see hello process running within hello container.</span></span>
- <span data-ttu-id="c751a-445">**ContainerServiceLog** — Użyj tego typu, jeśli próbujesz toofind informacji o dzienniku inspekcji dla hello demona Docker, jak uruchamianie, zatrzymywanie, usunąć lub poleceń ściągnięcia.</span><span class="sxs-lookup"><span data-stu-id="c751a-445">**ContainerServiceLog** – Use this type when you're trying toofind audit trail information for hello Docker daemon, such as start, stop, delete, or pull commands.</span></span>
- <span data-ttu-id="c751a-446">**KubeEvents_CL** korzysta z tego typu toosee hello Kubernetes zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="c751a-446">**KubeEvents_CL**  Use this type toosee hello Kubernetes events.</span></span>
- <span data-ttu-id="c751a-447">**KubePodInventory_CL** tego typu należy używać toounderstand hello klastra hierarchii informacji.</span><span class="sxs-lookup"><span data-stu-id="c751a-447">**KubePodInventory_CL**  Use this type when you want toounderstand hello cluster hierarchy information.</span></span>


### <a name="toosearch-logs-for-container-data"></a><span data-ttu-id="c751a-448">toosearch dzienniki dla kontenera danych</span><span class="sxs-lookup"><span data-stu-id="c751a-448">toosearch logs for container data</span></span>
* <span data-ttu-id="c751a-449">Wybierz obraz, który ostatnio nie powiodło się i znaleźć hello w dzienniku błędów.</span><span class="sxs-lookup"><span data-stu-id="c751a-449">Choose an image that you know has failed recently and find hello error logs for it.</span></span> <span data-ttu-id="c751a-450">Uruchom znajdując nazwę kontenera, która działa obrazu z **ContainerInventory** wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="c751a-450">Start by finding a container name that is running that image with a **ContainerInventory** search.</span></span> <span data-ttu-id="c751a-451">Na przykład wyszukaj`Type=ContainerInventory ubuntu Failed`</span><span class="sxs-lookup"><span data-stu-id="c751a-451">For example, search for `Type=ContainerInventory ubuntu Failed`</span></span>  
    <span data-ttu-id="c751a-452">![Wyszukaj kontenery Ubuntu](./media/log-analytics-containers/search-ubuntu.png)</span><span class="sxs-lookup"><span data-stu-id="c751a-452">![Search for Ubuntu containers](./media/log-analytics-containers/search-ubuntu.png)</span></span>

  <span data-ttu-id="c751a-453">Witaj nazwa kontenera hello obok zbyt**nazwa**i poszukaj tych dzienników.</span><span class="sxs-lookup"><span data-stu-id="c751a-453">hello name of hello container next too**Name**, and search for those logs.</span></span> <span data-ttu-id="c751a-454">W tym przykładzie jest to `Type=ContainerLog cranky_stonebreaker`.</span><span class="sxs-lookup"><span data-stu-id="c751a-454">In this example, it is `Type=ContainerLog cranky_stonebreaker`.</span></span>

<span data-ttu-id="c751a-455">**Wyświetlanie informacji o wydajności**</span><span class="sxs-lookup"><span data-stu-id="c751a-455">**View performance information**</span></span>

<span data-ttu-id="c751a-456">Gdy jest począwszy od tooconstruct zapytania, może pomóc toosee co to jest możliwe najpierw.</span><span class="sxs-lookup"><span data-stu-id="c751a-456">When you're beginning tooconstruct queries, it can help toosee what's possible first.</span></span> <span data-ttu-id="c751a-457">Na przykład toosee, które przeszukiwać wszystkie dane dotyczące wydajności, spróbuj hello szerokie zapytania, wpisując następujące zapytanie.</span><span class="sxs-lookup"><span data-stu-id="c751a-457">For example, toosee all performance data, try a broad query by typing hello following search query.</span></span>

```
Type=Perf
```

![kontenery wydajności](./media/log-analytics-containers/containers-perf01.png)

<span data-ttu-id="c751a-459">Zakres danych wydajności hello występują tooa określonego kontenera, wpisując jej nazwę hello toohello prawo do zapytania można określić.</span><span class="sxs-lookup"><span data-stu-id="c751a-459">You can scope hello performance data you're seeing tooa specific container by typing hello name of it toohello right of your query.</span></span>

```
Type=Perf <containerName>
```

<span data-ttu-id="c751a-460">Który lista hello metryki wydajności, które są zbierane dla poszczególnych kontenera.</span><span class="sxs-lookup"><span data-stu-id="c751a-460">That shows hello list of performance metrics that are collected for an individual container.</span></span>

![kontenery wydajności](./media/log-analytics-containers/containers-perf03.png)

## <a name="example-log-search-queries"></a><span data-ttu-id="c751a-462">Przykładowe zapytania wyszukiwania dziennika</span><span class="sxs-lookup"><span data-stu-id="c751a-462">Example log search queries</span></span>
<span data-ttu-id="c751a-463">Toobuild często przydatne jego kwerendę rozpoczynające się przykładem lub dwóch i modyfikuje je po toofit środowiska.</span><span class="sxs-lookup"><span data-stu-id="c751a-463">It's often useful toobuild queries starting with an example or two and then modifying them toofit your environment.</span></span> <span data-ttu-id="c751a-464">Jako punkt początkowy, możesz eksperymentować z hello **przykładowe zapytania** toohelp obszaru tworzenie bardziej zaawansowanych zapytań.</span><span class="sxs-lookup"><span data-stu-id="c751a-464">As a starting point, you can experiment with hello **Sample Queries** area toohelp you build more advanced queries.</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Kontenery zapytań](./media/log-analytics-containers/containers-queries.png)


## <a name="saving-log-search-queries"></a><span data-ttu-id="c751a-466">Zapisywanie dziennika zapytania wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="c751a-466">Saving log search queries</span></span>
<span data-ttu-id="c751a-467">Zapisywanie zapytań jest standardowa funkcja Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="c751a-467">Saving queries is a standard feature in Log Analytics.</span></span> <span data-ttu-id="c751a-468">Zapisując je, należy te, które zostały znalezione przydatne przydatne do użytku w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="c751a-468">By saving them, you'll have those that you've found useful handy for future use.</span></span>

<span data-ttu-id="c751a-469">Po utworzeniu kwerendę, która jest użyteczna, zapisz go, klikając **ulubione** u góry strony wyszukiwania dziennika hello hello.</span><span class="sxs-lookup"><span data-stu-id="c751a-469">After you create a query that you find useful, save it by clicking **Favorites** at hello top of hello Log Search page.</span></span> <span data-ttu-id="c751a-470">Następnie możesz z łatwością później z hello **Mój pulpit nawigacyjny** strony.</span><span class="sxs-lookup"><span data-stu-id="c751a-470">Then you can easily access it later from hello **My Dashboard** page.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c751a-471">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c751a-471">Next steps</span></span>
* <span data-ttu-id="c751a-472">[Wyszukaj dzienniki](log-analytics-log-searches.md) tooview szczegółowe kontenera rekordów danych.</span><span class="sxs-lookup"><span data-stu-id="c751a-472">[Search logs](log-analytics-log-searches.md) tooview detailed container data records.</span></span>
