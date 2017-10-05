---
title: "Rozwiązania monitorowanie kontenera Azure Log Analytics | Dokumentacja firmy Microsoft"
description: "Rozwiązanie monitorowania kontenera w Log Analytics pomaga wyświetlać i zarządzać Docker i Windows hostów kontenera w jednym miejscu."
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
ms.openlocfilehash: b2e03531ee401f4552198e5dd50fbfe1d970f0e5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="container-monitoring-solution-in-log-analytics"></a><span data-ttu-id="6d5cb-103">Kontener rozwiązania monitorowanie analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="6d5cb-103">Container Monitoring solution in Log Analytics</span></span>

![Symbol kontenerów](./media/log-analytics-containers/containers-symbol.png)

<span data-ttu-id="6d5cb-105">W tym artykule opisano sposób konfigurowania i używania to rozwiązanie monitorowanie kontenera w analizy dzienników, która ułatwia wyświetlanie i zarządzanie Docker i Windows hostów kontenera w jednym miejscu.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-105">This article describes how to set up and use the Container Monitoring solution in Log Analytics, which helps you view and manage your Docker and Windows container hosts in a single location.</span></span> <span data-ttu-id="6d5cb-106">Docker to system wirtualizacji oprogramowania pozwala utworzyć kontenerów, które automatyzują wdrożenia oprogramowania na infrastruktury informatycznej.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-106">Docker is a software virtualization system used to create containers that automate software deployment to their IT infrastructure.</span></span>

<span data-ttu-id="6d5cb-107">Rozwiązanie zawiera kontenery, które są, obrazów kontenera nich uruchomiony uruchomiona, i gdy kontenery są.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-107">The solution shows which containers are running, what container image they’re running, and where containers are running.</span></span> <span data-ttu-id="6d5cb-108">Można wyświetlić szczegółowe informacje o inspekcji przedstawiający poleceń używanych przez kontenery.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-108">You can view detailed audit information showing commands used with containers.</span></span> <span data-ttu-id="6d5cb-109">I rozwiązywać kontenery wyświetlanie i wyszukując scentralizowane dzienniki bez konieczności zdalnie wyświetlić hostach Docker lub systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-109">And, you can troubleshoot containers by viewing and searching centralized logs without having to remotely view Docker or Windows hosts.</span></span> <span data-ttu-id="6d5cb-110">Można znaleźć kontenerów, które mogą być zakłócenia i spójniejsze nadmiarowe zasobów na hoście.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-110">You can find containers that may be noisy and consuming excess resources on a host.</span></span> <span data-ttu-id="6d5cb-111">I można wyświetlić scentralizowane procesora CPU, pamięci, magazynu i użycia i wydajności informacje o sieci dla kontenerów.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-111">And, you can view centralized CPU, memory, storage, and network usage and performance information for containers.</span></span> <span data-ttu-id="6d5cb-112">Na komputerach z systemem Windows, można scentralizować i porównaj dzienniki systemu Windows Server, Hyper-V i kontenery Docker.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-112">On computers running Windows, you can centralize and compare logs from Windows Server, Hyper-V, and Docker containers.</span></span> <span data-ttu-id="6d5cb-113">Rozwiązanie obsługuje następujące orchestrators kontenera:</span><span class="sxs-lookup"><span data-stu-id="6d5cb-113">The solution supports the following container orchestrators:</span></span>

- <span data-ttu-id="6d5cb-114">Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="6d5cb-114">Docker Swarm</span></span>
- <span data-ttu-id="6d5cb-115">DC/OS</span><span class="sxs-lookup"><span data-stu-id="6d5cb-115">DC/OS</span></span>
- <span data-ttu-id="6d5cb-116">Kubernetes</span><span class="sxs-lookup"><span data-stu-id="6d5cb-116">Kubernetes</span></span>
- <span data-ttu-id="6d5cb-117">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="6d5cb-117">Service Fabric</span></span>
- <span data-ttu-id="6d5cb-118">Red Hat OpenShift</span><span class="sxs-lookup"><span data-stu-id="6d5cb-118">Red Hat OpenShift</span></span>


<span data-ttu-id="6d5cb-119">Na poniższym diagramie przedstawiono relacje między różnych hostów kontenera i agentów z usługą OMS.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-119">The following diagram shows the relationships between various container hosts and agents with OMS.</span></span>

![Diagram kontenerów](./media/log-analytics-containers/containers-diagram.png)

## <a name="system-requirements"></a><span data-ttu-id="6d5cb-121">Wymagania systemowe</span><span class="sxs-lookup"><span data-stu-id="6d5cb-121">System requirements</span></span>

<span data-ttu-id="6d5cb-122">Przed rozpoczęciem należy przejrzeć następujące informacje, aby sprawdzić, czy zostały spełnione wymagania wstępne.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-122">Before starting, review the following details to verify you meet the prerequisites.</span></span>

### <a name="container-monitoring-solution-support-for-docker-orchestrator-and-os-platform"></a><span data-ttu-id="6d5cb-123">Rozwiązanie monitorowania kontener obsługuje platformy Docker Orchestrator i systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="6d5cb-123">Container monitoring solution support for Docker Orchestrator and OS platform</span></span>
<span data-ttu-id="6d5cb-124">W poniższej tabeli przedstawiono aranżacji Docker i monitorowania obsługę kontenera magazynu, wydajności i dzienniki z analizy dzienników systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-124">The following table outlines the Docker orchestration and operating system monitoring support of container inventory, performance, and logs with Log Analytics.</span></span>   

| | <span data-ttu-id="6d5cb-125">ACS</span><span class="sxs-lookup"><span data-stu-id="6d5cb-125">ACS</span></span> | <span data-ttu-id="6d5cb-126">Linux</span><span class="sxs-lookup"><span data-stu-id="6d5cb-126">Linux</span></span> | <span data-ttu-id="6d5cb-127">Windows</span><span class="sxs-lookup"><span data-stu-id="6d5cb-127">Windows</span></span> | <span data-ttu-id="6d5cb-128">Kontener</span><span class="sxs-lookup"><span data-stu-id="6d5cb-128">Container</span></span><br><span data-ttu-id="6d5cb-129">Spis</span><span class="sxs-lookup"><span data-stu-id="6d5cb-129">Inventory</span></span> | <span data-ttu-id="6d5cb-130">Image (Obraz)</span><span class="sxs-lookup"><span data-stu-id="6d5cb-130">Image</span></span><br><span data-ttu-id="6d5cb-131">Spis</span><span class="sxs-lookup"><span data-stu-id="6d5cb-131">Inventory</span></span> | <span data-ttu-id="6d5cb-132">Węzeł</span><span class="sxs-lookup"><span data-stu-id="6d5cb-132">Node</span></span><br><span data-ttu-id="6d5cb-133">Spis</span><span class="sxs-lookup"><span data-stu-id="6d5cb-133">Inventory</span></span> | <span data-ttu-id="6d5cb-134">Kontener</span><span class="sxs-lookup"><span data-stu-id="6d5cb-134">Container</span></span><br><span data-ttu-id="6d5cb-135">Wydajność</span><span class="sxs-lookup"><span data-stu-id="6d5cb-135">Performance</span></span> | <span data-ttu-id="6d5cb-136">Kontener</span><span class="sxs-lookup"><span data-stu-id="6d5cb-136">Container</span></span><br><span data-ttu-id="6d5cb-137">Wydarzenie</span><span class="sxs-lookup"><span data-stu-id="6d5cb-137">Event</span></span> | <span data-ttu-id="6d5cb-138">Wydarzenie</span><span class="sxs-lookup"><span data-stu-id="6d5cb-138">Event</span></span><br><span data-ttu-id="6d5cb-139">Log</span><span class="sxs-lookup"><span data-stu-id="6d5cb-139">Log</span></span> | <span data-ttu-id="6d5cb-140">Kontener</span><span class="sxs-lookup"><span data-stu-id="6d5cb-140">Container</span></span><br><span data-ttu-id="6d5cb-141">Log</span><span class="sxs-lookup"><span data-stu-id="6d5cb-141">Log</span></span> |
|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|
| <span data-ttu-id="6d5cb-142">Kubernetes</span><span class="sxs-lookup"><span data-stu-id="6d5cb-142">Kubernetes</span></span> | <span data-ttu-id="6d5cb-143">&#8226;</span><span class="sxs-lookup"><span data-stu-id="6d5cb-143">&#8226;</span></span> | <span data-ttu-id="6d5cb-144">&#8226;</span><span class="sxs-lookup"><span data-stu-id="6d5cb-144">&#8226;</span></span> | | <span data-ttu-id="6d5cb-145">&#8226;</span><span class="sxs-lookup"><span data-stu-id="6d5cb-145">&#8226;</span></span> | <span data-ttu-id="6d5cb-146">&#8226;</span><span class="sxs-lookup"><span data-stu-id="6d5cb-146">&#8226;</span></span> | <span data-ttu-id="6d5cb-147">&#8226;</span><span class="sxs-lookup"><span data-stu-id="6d5cb-147">&#8226;</span></span> | <span data-ttu-id="6d5cb-148">&#8226;</span><span class="sxs-lookup"><span data-stu-id="6d5cb-148">&#8226;</span></span> | <span data-ttu-id="6d5cb-149">&#8226;</span><span class="sxs-lookup"><span data-stu-id="6d5cb-149">&#8226;</span></span> | <span data-ttu-id="6d5cb-150">&#8226;</span><span class="sxs-lookup"><span data-stu-id="6d5cb-150">&#8226;</span></span> | <span data-ttu-id="6d5cb-151">&#8226;</span><span class="sxs-lookup"><span data-stu-id="6d5cb-151">&#8226;</span></span> |
| <span data-ttu-id="6d5cb-152">Mesosphere</span><span class="sxs-lookup"><span data-stu-id="6d5cb-152">Mesosphere</span></span><br><span data-ttu-id="6d5cb-153">DC/OS</span><span class="sxs-lookup"><span data-stu-id="6d5cb-153">DC/OS</span></span> | <span data-ttu-id="6d5cb-154">&#8226;</span><span class="sxs-lookup"><span data-stu-id="6d5cb-154">&#8226;</span></span> | <span data-ttu-id="6d5cb-155">&#8226;</span><span class="sxs-lookup"><span data-stu-id="6d5cb-155">&#8226;</span></span> | | <span data-ttu-id="6d5cb-156">&#8226;</span><span class="sxs-lookup"><span data-stu-id="6d5cb-156">&#8226;</span></span> | <span data-ttu-id="6d5cb-157">&#8226;</span><span class="sxs-lookup"><span data-stu-id="6d5cb-157">&#8226;</span></span> | <span data-ttu-id="6d5cb-158">&#8226;</span><span class="sxs-lookup"><span data-stu-id="6d5cb-158">&#8226;</span></span> | <span data-ttu-id="6d5cb-159">&#8226;</span><span class="sxs-lookup"><span data-stu-id="6d5cb-159">&#8226;</span></span>| <span data-ttu-id="6d5cb-160">&#8226;</span><span class="sxs-lookup"><span data-stu-id="6d5cb-160">&#8226;</span></span> | <span data-ttu-id="6d5cb-161">&#8226;</span><span class="sxs-lookup"><span data-stu-id="6d5cb-161">&#8226;</span></span> | <span data-ttu-id="6d5cb-162">&#8226;</span><span class="sxs-lookup"><span data-stu-id="6d5cb-162">&#8226;</span></span> |
| <span data-ttu-id="6d5cb-163">Docker</span><span class="sxs-lookup"><span data-stu-id="6d5cb-163">Docker</span></span><br><span data-ttu-id="6d5cb-164">Swarm</span><span class="sxs-lookup"><span data-stu-id="6d5cb-164">Swarm</span></span> | <span data-ttu-id="6d5cb-165">&#8226;</span><span class="sxs-lookup"><span data-stu-id="6d5cb-165">&#8226;</span></span> | <span data-ttu-id="6d5cb-166">&#8226;</span><span class="sxs-lookup"><span data-stu-id="6d5cb-166">&#8226;</span></span> | <span data-ttu-id="6d5cb-167">&#8226;</span><span class="sxs-lookup"><span data-stu-id="6d5cb-167">&#8226;</span></span> | <span data-ttu-id="6d5cb-168">&#8226;</span><span class="sxs-lookup"><span data-stu-id="6d5cb-168">&#8226;</span></span> | <span data-ttu-id="6d5cb-169">&#8226;</span><span class="sxs-lookup"><span data-stu-id="6d5cb-169">&#8226;</span></span> | <span data-ttu-id="6d5cb-170">&#8226;</span><span class="sxs-lookup"><span data-stu-id="6d5cb-170">&#8226;</span></span> | <span data-ttu-id="6d5cb-171">&#8226;</span><span class="sxs-lookup"><span data-stu-id="6d5cb-171">&#8226;</span></span> | <span data-ttu-id="6d5cb-172">&#8226;</span><span class="sxs-lookup"><span data-stu-id="6d5cb-172">&#8226;</span></span> | | <span data-ttu-id="6d5cb-173">&#8226;</span><span class="sxs-lookup"><span data-stu-id="6d5cb-173">&#8226;</span></span> |
| <span data-ttu-id="6d5cb-174">Usługa</span><span class="sxs-lookup"><span data-stu-id="6d5cb-174">Service</span></span><br><span data-ttu-id="6d5cb-175">Sieć szkieletowa</span><span class="sxs-lookup"><span data-stu-id="6d5cb-175">Fabric</span></span> | | | <span data-ttu-id="6d5cb-176">&#8226;</span><span class="sxs-lookup"><span data-stu-id="6d5cb-176">&#8226;</span></span> | <span data-ttu-id="6d5cb-177">&#8226;</span><span class="sxs-lookup"><span data-stu-id="6d5cb-177">&#8226;</span></span> | <span data-ttu-id="6d5cb-178">&#8226;</span><span class="sxs-lookup"><span data-stu-id="6d5cb-178">&#8226;</span></span> | <span data-ttu-id="6d5cb-179">&#8226;</span><span class="sxs-lookup"><span data-stu-id="6d5cb-179">&#8226;</span></span> | <span data-ttu-id="6d5cb-180">&#8226;</span><span class="sxs-lookup"><span data-stu-id="6d5cb-180">&#8226;</span></span> | <span data-ttu-id="6d5cb-181">&#8226;</span><span class="sxs-lookup"><span data-stu-id="6d5cb-181">&#8226;</span></span> | <span data-ttu-id="6d5cb-182">&#8226;</span><span class="sxs-lookup"><span data-stu-id="6d5cb-182">&#8226;</span></span> | <span data-ttu-id="6d5cb-183">&#8226;</span><span class="sxs-lookup"><span data-stu-id="6d5cb-183">&#8226;</span></span> |
| <span data-ttu-id="6d5cb-184">Red Hat Otwórz</span><span class="sxs-lookup"><span data-stu-id="6d5cb-184">Red Hat Open</span></span><br><span data-ttu-id="6d5cb-185">SHIFT</span><span class="sxs-lookup"><span data-stu-id="6d5cb-185">Shift</span></span> | | <span data-ttu-id="6d5cb-186">&#8226;</span><span class="sxs-lookup"><span data-stu-id="6d5cb-186">&#8226;</span></span> | | <span data-ttu-id="6d5cb-187">&#8226;</span><span class="sxs-lookup"><span data-stu-id="6d5cb-187">&#8226;</span></span> | <span data-ttu-id="6d5cb-188">&#8226;</span><span class="sxs-lookup"><span data-stu-id="6d5cb-188">&#8226;</span></span>| <span data-ttu-id="6d5cb-189">&#8226;</span><span class="sxs-lookup"><span data-stu-id="6d5cb-189">&#8226;</span></span> | <span data-ttu-id="6d5cb-190">&#8226;</span><span class="sxs-lookup"><span data-stu-id="6d5cb-190">&#8226;</span></span> | <span data-ttu-id="6d5cb-191">&#8226;</span><span class="sxs-lookup"><span data-stu-id="6d5cb-191">&#8226;</span></span> | | <span data-ttu-id="6d5cb-192">&#8226;</span><span class="sxs-lookup"><span data-stu-id="6d5cb-192">&#8226;</span></span> |
| <span data-ttu-id="6d5cb-193">Windows Server</span><span class="sxs-lookup"><span data-stu-id="6d5cb-193">Windows Server</span></span><br><span data-ttu-id="6d5cb-194">(autonomiczna)</span><span class="sxs-lookup"><span data-stu-id="6d5cb-194">(standalone)</span></span> | | | <span data-ttu-id="6d5cb-195">&#8226;</span><span class="sxs-lookup"><span data-stu-id="6d5cb-195">&#8226;</span></span> | <span data-ttu-id="6d5cb-196">&#8226;</span><span class="sxs-lookup"><span data-stu-id="6d5cb-196">&#8226;</span></span> | <span data-ttu-id="6d5cb-197">&#8226;</span><span class="sxs-lookup"><span data-stu-id="6d5cb-197">&#8226;</span></span> | <span data-ttu-id="6d5cb-198">&#8226;</span><span class="sxs-lookup"><span data-stu-id="6d5cb-198">&#8226;</span></span> | <span data-ttu-id="6d5cb-199">&#8226;</span><span class="sxs-lookup"><span data-stu-id="6d5cb-199">&#8226;</span></span> | <span data-ttu-id="6d5cb-200">&#8226;</span><span class="sxs-lookup"><span data-stu-id="6d5cb-200">&#8226;</span></span> | | <span data-ttu-id="6d5cb-201">&#8226;</span><span class="sxs-lookup"><span data-stu-id="6d5cb-201">&#8226;</span></span> |
| <span data-ttu-id="6d5cb-202">Serwer systemu Linux</span><span class="sxs-lookup"><span data-stu-id="6d5cb-202">Linux Server</span></span><br><span data-ttu-id="6d5cb-203">(autonomiczna)</span><span class="sxs-lookup"><span data-stu-id="6d5cb-203">(standalone)</span></span> | | <span data-ttu-id="6d5cb-204">&#8226;</span><span class="sxs-lookup"><span data-stu-id="6d5cb-204">&#8226;</span></span> | | <span data-ttu-id="6d5cb-205">&#8226;</span><span class="sxs-lookup"><span data-stu-id="6d5cb-205">&#8226;</span></span> | <span data-ttu-id="6d5cb-206">&#8226;</span><span class="sxs-lookup"><span data-stu-id="6d5cb-206">&#8226;</span></span> | <span data-ttu-id="6d5cb-207">&#8226;</span><span class="sxs-lookup"><span data-stu-id="6d5cb-207">&#8226;</span></span> | <span data-ttu-id="6d5cb-208">&#8226;</span><span class="sxs-lookup"><span data-stu-id="6d5cb-208">&#8226;</span></span> | <span data-ttu-id="6d5cb-209">&#8226;</span><span class="sxs-lookup"><span data-stu-id="6d5cb-209">&#8226;</span></span> | | <span data-ttu-id="6d5cb-210">&#8226;</span><span class="sxs-lookup"><span data-stu-id="6d5cb-210">&#8226;</span></span> |


### <a name="docker-versions-supported-on-linux"></a><span data-ttu-id="6d5cb-211">Wersje docker obsługiwane w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="6d5cb-211">Docker versions supported on Linux</span></span>

- <span data-ttu-id="6d5cb-212">Docker 1.11 do 1.13</span><span class="sxs-lookup"><span data-stu-id="6d5cb-212">Docker 1.11 to 1.13</span></span>
- <span data-ttu-id="6d5cb-213">V17.06 docker CE i EE</span><span class="sxs-lookup"><span data-stu-id="6d5cb-213">Docker CE and EE v17.06</span></span>

### <a name="x64-linux-distributions-supported-as-container-hosts"></a><span data-ttu-id="6d5cb-214">x64 dystrybucje systemu Linux obsługiwane jako hosty kontenera</span><span class="sxs-lookup"><span data-stu-id="6d5cb-214">x64 Linux distributions supported as container hosts</span></span>

- <span data-ttu-id="6d5cb-215">Ubuntu 14.04 LTS i 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="6d5cb-215">Ubuntu 14.04 LTS and 16.04 LTS</span></span>
- <span data-ttu-id="6d5cb-216">CoreOS(stable)</span><span class="sxs-lookup"><span data-stu-id="6d5cb-216">CoreOS(stable)</span></span>
- <span data-ttu-id="6d5cb-217">Amazon Linux 2016.09.0</span><span class="sxs-lookup"><span data-stu-id="6d5cb-217">Amazon Linux 2016.09.0</span></span>
- <span data-ttu-id="6d5cb-218">openSUSE 13.2</span><span class="sxs-lookup"><span data-stu-id="6d5cb-218">openSUSE 13.2</span></span>
- <span data-ttu-id="6d5cb-219">openSUSE LEAP 42.2</span><span class="sxs-lookup"><span data-stu-id="6d5cb-219">openSUSE LEAP 42.2</span></span>
- <span data-ttu-id="6d5cb-220">CentOS 7.2 i 7.3</span><span class="sxs-lookup"><span data-stu-id="6d5cb-220">CentOS 7.2 and 7.3</span></span>
- <span data-ttu-id="6d5cb-221">SLES 12</span><span class="sxs-lookup"><span data-stu-id="6d5cb-221">SLES 12</span></span>
- <span data-ttu-id="6d5cb-222">RHEL 7.2 i 7.3</span><span class="sxs-lookup"><span data-stu-id="6d5cb-222">RHEL 7.2 and 7.3</span></span>
- <span data-ttu-id="6d5cb-223">Red Hat OpenShift kontenera platformy (OCP) 3.4 i 3.5</span><span class="sxs-lookup"><span data-stu-id="6d5cb-223">Red Hat OpenShift Container Platform (OCP) 3.4 and 3.5</span></span>
- <span data-ttu-id="6d5cb-224">ACS Mesosphere DC/OS 1.7.3 do 1.8.8</span><span class="sxs-lookup"><span data-stu-id="6d5cb-224">ACS Mesosphere DC/OS 1.7.3 to 1.8.8</span></span>
- <span data-ttu-id="6d5cb-225">Usługi ACS Kubernetes 1.4.5 do wersji 1.6</span><span class="sxs-lookup"><span data-stu-id="6d5cb-225">ACS Kubernetes 1.4.5 to 1.6</span></span>
- <span data-ttu-id="6d5cb-226">Usługi ACS Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="6d5cb-226">ACS Docker Swarm</span></span>

### <a name="supported-windows-operating-system"></a><span data-ttu-id="6d5cb-227">Obsługiwany system operacyjny Windows</span><span class="sxs-lookup"><span data-stu-id="6d5cb-227">Supported Windows operating system</span></span>

- <span data-ttu-id="6d5cb-228">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="6d5cb-228">Windows Server 2016</span></span>
- <span data-ttu-id="6d5cb-229">Windows 10 Anniversary Edition (Professional lub Enterprise)</span><span class="sxs-lookup"><span data-stu-id="6d5cb-229">Windows 10 Anniversary Edition (Professional or Enterprise)</span></span>

### <a name="docker-versions-supported-on-windows"></a><span data-ttu-id="6d5cb-230">Wersje docker obsługiwane w systemie Windows</span><span class="sxs-lookup"><span data-stu-id="6d5cb-230">Docker versions supported on Windows</span></span>

- <span data-ttu-id="6d5cb-231">Docker 1.12 i 1.13</span><span class="sxs-lookup"><span data-stu-id="6d5cb-231">Docker 1.12 and 1.13</span></span>
- <span data-ttu-id="6d5cb-232">Docker 17.03.0 i nowsze</span><span class="sxs-lookup"><span data-stu-id="6d5cb-232">Docker 17.03.0 and later</span></span>

## <a name="installing-and-configuring-the-solution"></a><span data-ttu-id="6d5cb-233">Instalowanie i konfigurowanie rozwiązania</span><span class="sxs-lookup"><span data-stu-id="6d5cb-233">Installing and configuring the solution</span></span>
<span data-ttu-id="6d5cb-234">Skorzystaj z poniższych informacji, aby zainstalować i skonfigurować rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-234">Use the following information to install and configure the solution.</span></span>

1. <span data-ttu-id="6d5cb-235">Dodaj rozwiązanie monitorowanie kontenera na obszar roboczy OMS z [witrynę Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ContainersOMS?tab=Overview) lub przy użyciu procesu opisanego w [rozwiązań dodać analizy dzienników z galerii rozwiązań](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="6d5cb-235">Add the Container Monitoring solution to your OMS workspace from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ContainersOMS?tab=Overview) or by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>

2. <span data-ttu-id="6d5cb-236">Zainstalować i korzystać z agentem pakietu OMS Docker.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-236">Install and use Docker with an OMS agent.</span></span>  <span data-ttu-id="6d5cb-237">Oparte na systemie operacyjnym, możesz wybrać z następujących metod:</span><span class="sxs-lookup"><span data-stu-id="6d5cb-237">Based on your operating system, you can choose from the following methods:</span></span>

  * <span data-ttu-id="6d5cb-238">W obsługiwanych systemach operacyjnych Linux, zainstaluj i uruchom Docker, a następnie zainstaluj i skonfiguruj [Agent pakietu OMS Linux](log-analytics-agent-linux.md).</span><span class="sxs-lookup"><span data-stu-id="6d5cb-238">On supported Linux operating systems, install and run Docker and then install and configure the [OMS Agent for Linux](log-analytics-agent-linux.md).</span></span>  
  * <span data-ttu-id="6d5cb-239">Na CoreOS nie można uruchomić agenta pakietu OMS dla systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-239">On CoreOS, you cannot run the OMS Agent for Linux.</span></span> <span data-ttu-id="6d5cb-240">Zamiast tego należy uruchomić konteneryzowanych wersję agenta pakietu OMS dla systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-240">Instead, you run a containerized version of the OMS Agent for Linux.</span></span> <span data-ttu-id="6d5cb-241">Przegląd [hostów kontenera systemu Linux, w tym CoreOS](#for-all-linux-container-hosts-including-coreos) lub [hostów kontenera platformy Azure dla instytucji rządowych Linux, w tym CoreOS](#for-all-azure-government-linux-container-hosts-including-coreos) podczas pracy z kontenerami w chmurze Azure dla instytucji rządowych.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-241">Review [Linux container hosts including CoreOS](#for-all-linux-container-hosts-including-coreos) or [Azure Government Linux container hosts including CoreOS](#for-all-azure-government-linux-container-hosts-including-coreos) if you are working with containers in Azure Government Cloud.</span></span>
  * <span data-ttu-id="6d5cb-242">W systemie Windows Server 2016 i Windows 10 zainstalować aparatem platformy Docker i klienta, a następnie połącz agenta w celu zbierania informacji oraz wysyłać je do analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-242">On Windows Server 2016 and Windows 10, install the Docker Engine and client then connect an agent to gather information and send it to Log Analytics.</span></span>  

### <a name="container-services"></a><span data-ttu-id="6d5cb-243">Kontener usług</span><span class="sxs-lookup"><span data-stu-id="6d5cb-243">Container services</span></span>

- <span data-ttu-id="6d5cb-244">Jeśli masz środowisko Red Hat OpenShift przejrzeć [skonfigurować agenta pakietu OMS dla Red Hat OpenShift](#configure-an-oms-agent-for-red-hat-openshift).</span><span class="sxs-lookup"><span data-stu-id="6d5cb-244">If you have a Red Hat OpenShift environment, review [Configure an OMS agent for Red Hat OpenShift](#configure-an-oms-agent-for-red-hat-openshift).</span></span>
- <span data-ttu-id="6d5cb-245">Jeśli masz klaster Kubernetes za pomocą usługi kontenera platformy Azure, przejrzyj [monitorować klastra usługi kontenera platformy Azure z Microsoft Operations Management Suite (OMS)](../container-service/kubernetes/container-service-kubernetes-oms.md).</span><span class="sxs-lookup"><span data-stu-id="6d5cb-245">If you have a Kubernetes cluster using the Azure Container Service, review [Monitor an Azure Container Service cluster with Microsoft Operations Management Suite (OMS)](../container-service/kubernetes/container-service-kubernetes-oms.md).</span></span>
- <span data-ttu-id="6d5cb-246">W przypadku klastra usługi kontenera platformy Azure DC/OS więcej w [monitorować klastra usługi kontenera platformy Azure DC/OS w usłudze Operations Management Suite](../container-service/dcos-swarm/container-service-monitoring-oms.md).</span><span class="sxs-lookup"><span data-stu-id="6d5cb-246">If you have an Azure Container Service DC/OS cluster, learn more at [Monitor an Azure Container Service DC/OS cluster with Operations Management Suite](../container-service/dcos-swarm/container-service-monitoring-oms.md).</span></span>
- <span data-ttu-id="6d5cb-247">Jeśli masz środowisku trybu Docker Swarm, dowiedzieć się więcej o [skonfigurować agenta pakietu OMS dla rozwiązania Docker Swarm](#configure-an-oms-agent-for-docker-swarm).</span><span class="sxs-lookup"><span data-stu-id="6d5cb-247">If you have a Docker Swarm mode environment, learn more at [Configure an OMS agent for Docker Swarm](#configure-an-oms-agent-for-docker-swarm).</span></span>
- <span data-ttu-id="6d5cb-248">Jeśli używasz kontenery z sieci szkieletowej usług dowiedzieć się więcej na [Omówienie usługi Azure Service Fabric](../service-fabric/service-fabric-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6d5cb-248">If you use containers with Service Fabric, learn more at [Overview of Azure Service Fabric](../service-fabric/service-fabric-overview.md).</span></span>
- <span data-ttu-id="6d5cb-249">Przegląd [aparatem platformy Docker w systemie Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon) artykułu, aby uzyskać dodatkowe informacje o sposobie instalowania i konfigurowania silnik Docker na komputerach z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-249">Review the [Docker Engine on Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon) article for additional information about how to install and configure your Docker Engines on computers running Windows.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6d5cb-250">Musi być uruchomiona docker **przed** zainstalowaniu [Agent pakietu OMS Linux](log-analytics-agent-linux.md) na hostach kontenera.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-250">Docker must be running **before** you install the [OMS Agent for Linux](log-analytics-agent-linux.md) on your container hosts.</span></span> <span data-ttu-id="6d5cb-251">Jeśli agent został już zainstalowany przed zainstalowaniem Docker, należy ponownie zainstalować agenta pakietu OMS dla systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-251">If you've already installed the agent before installing Docker, you need to reinstall the OMS Agent for Linux.</span></span> <span data-ttu-id="6d5cb-252">Aby uzyskać więcej informacji na temat rozwiązania Docker, zobacz [Docker witryny sieci Web](https://www.docker.com).</span><span class="sxs-lookup"><span data-stu-id="6d5cb-252">For more information about Docker, see the [Docker website](https://www.docker.com).</span></span>


## <a name="linux-container-hosts"></a><span data-ttu-id="6d5cb-253">Hosty kontenera systemu Linux</span><span class="sxs-lookup"><span data-stu-id="6d5cb-253">Linux container hosts</span></span>

<span data-ttu-id="6d5cb-254">Po zainstalowaniu Docker Użyj następujących ustawień dla hosta kontenera, aby skonfigurować agenta do użycia z Docker.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-254">After you've installed Docker, use the following settings for your container host to configure the agent for use with Docker.</span></span> <span data-ttu-id="6d5cb-255">Najpierw należy OMS identyfikator i klucz, który można znaleźć w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-255">First you need your OMS workspace ID and key, which you can find in the Azure portal.</span></span> <span data-ttu-id="6d5cb-256">W obszarze roboczym, kliknij przycisk **Szybki Start** > **komputerów** do wyświetlania Twojego **identyfikator obszaru roboczego** i **klucz podstawowy**.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-256">In your workspace, click **Quick Start** > **Computers** to view your **Workspace ID** and **Primary Key**.</span></span>  <span data-ttu-id="6d5cb-257">Skopiuj i Wklej zarówno do Twojego ulubionego edytora.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-257">Copy and paste both into your favorite editor.</span></span>

### <a name="for-all-linux-container-hosts-except-coreos"></a><span data-ttu-id="6d5cb-258">Dla wszystkich hostów kontenera systemu Linux, z wyjątkiem CoreOS</span><span class="sxs-lookup"><span data-stu-id="6d5cb-258">For all Linux container hosts except CoreOS</span></span>

- <span data-ttu-id="6d5cb-259">Aby uzyskać więcej informacji i kroki dotyczące instalowania agenta pakietu OMS dla systemu Linux, zobacz [połączyć komputery Linux do Operations Management Suite (OMS)](log-analytics-agent-linux.md).</span><span class="sxs-lookup"><span data-stu-id="6d5cb-259">For more information and steps on how to install the OMS Agent for Linux, see [Connect your Linux Computers to Operations Management Suite (OMS)](log-analytics-agent-linux.md).</span></span>

### <a name="for-all-linux-container-hosts-including-coreos"></a><span data-ttu-id="6d5cb-260">Dla wszystkich hostów kontenera systemu Linux, łącznie z CoreOS</span><span class="sxs-lookup"><span data-stu-id="6d5cb-260">For all Linux container hosts including CoreOS</span></span>

<span data-ttu-id="6d5cb-261">Uruchom kontener OMS, który chcesz monitorować.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-261">Start the OMS container that you want to monitor.</span></span> <span data-ttu-id="6d5cb-262">Zmodyfikuj i skorzystaj z następującego przykładu:</span><span class="sxs-lookup"><span data-stu-id="6d5cb-262">Modify and use the following example:</span></span>

```
sudo docker run --privileged -d -v /var/run/docker.sock:/var/run/docker.sock -e WSID="your workspace id" -e KEY="your key" -h=`hostname` -p 127.0.0.1:25225:25225 --name="omsagent" --restart=always microsoft/oms
```

### <a name="for-all-azure-government-linux-container-hosts-including-coreos"></a><span data-ttu-id="6d5cb-263">Dla wszystkich hostów kontenera Azure dla instytucji rządowych Linux, łącznie z CoreOS</span><span class="sxs-lookup"><span data-stu-id="6d5cb-263">For all Azure Government Linux container hosts including CoreOS</span></span>

<span data-ttu-id="6d5cb-264">Uruchom kontener OMS, który chcesz monitorować.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-264">Start the OMS container that you want to monitor.</span></span> <span data-ttu-id="6d5cb-265">Zmodyfikuj i skorzystaj z następującego przykładu:</span><span class="sxs-lookup"><span data-stu-id="6d5cb-265">Modify and use the following example:</span></span>

```
sudo docker run --privileged -d -v /var/run/docker.sock:/var/run/docker.sock -v /var/log:/var/log -e WSID="your workspace id" -e KEY="your key" -e DOMAIN="opinsights.azure.us" -p 127.0.0.1:25225:25225 -p 127.0.0.1:25224:25224/udp --name="omsagent" -h=`hostname` --restart=always microsoft/oms
```

### <a name="switching-from-using-an-installed-linux-agent-to-one-in-a-container"></a><span data-ttu-id="6d5cb-266">Zmiana typu zapytania z przy użyciu zainstalowanych agentów systemu Linux na jedną w kontenerze</span><span class="sxs-lookup"><span data-stu-id="6d5cb-266">Switching from using an installed Linux agent to one in a container</span></span>
<span data-ttu-id="6d5cb-267">Jeśli wcześniej używana bezpośrednio zainstalować agenta i chcesz zamiast tego użyć agenta uruchomionego w kontenerze, należy najpierw usunąć agenta pakietu OMS dla systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-267">If you previously used the directly-installed agent and want to instead use an agent running in a container, you must first remove the OMS Agent for Linux.</span></span> <span data-ttu-id="6d5cb-268">Zobacz [odinstalowanie agenta pakietu OMS Linux](log-analytics-agent-linux.md#uninstalling-the-oms-agent-for-linux) zrozumienie, jak pomyślnie odinstalowania agenta.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-268">See [Uninstalling the OMS Agent for Linux](log-analytics-agent-linux.md#uninstalling-the-oms-agent-for-linux) to understand how to successfully uninstall the agent.</span></span>  

### <a name="configure-an-oms-agent-for-docker-swarm"></a><span data-ttu-id="6d5cb-269">Konfigurowanie agenta pakietu OMS dla rozwiązania Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="6d5cb-269">Configure an OMS agent for Docker Swarm</span></span>

<span data-ttu-id="6d5cb-270">Agent pakietu OMS można uruchomić jako usługę globalnej w rozwiązaniu Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-270">You can run the OMS Agent as a global service on Docker Swarm.</span></span> <span data-ttu-id="6d5cb-271">Skorzystaj z poniższych informacji, aby utworzyć usługę agenta pakietu OMS.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-271">Use the following information to create an OMS Agent service.</span></span> <span data-ttu-id="6d5cb-272">Należy wstawić OMS identyfikator i klucz podstawowy.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-272">You need to insert your OMS Workspace ID and Primary Key.</span></span>

- <span data-ttu-id="6d5cb-273">Uruchom następujące polecenie na węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-273">Run the following on the master node.</span></span>

    ```
    sudo docker service create  --name omsagent --mode global  --mount type=bind,source=/var/run/docker.sock,destination=/var/run/docker.sock  -e WSID="<WORKSPACE ID>" -e KEY="<PRIMARY KEY>" -p 25225:25225 -p 25224:25224/udp  --restart-condition=on-failure microsoft/oms
    ```

### <a name="configure-an-oms-agent-for-red-hat-openshift"></a><span data-ttu-id="6d5cb-274">Konfigurowanie agenta pakietu OMS dla OpenShift Red Hat</span><span class="sxs-lookup"><span data-stu-id="6d5cb-274">Configure an OMS Agent for Red Hat OpenShift</span></span>
<span data-ttu-id="6d5cb-275">Istnieją trzy sposoby dodawania Agent pakietu OMS do Red Hat OpenShift można uruchomić zbierania danych monitorowania kontenera.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-275">There are three ways to add the OMS Agent to Red Hat OpenShift to start collecting container monitoring data.</span></span>

* <span data-ttu-id="6d5cb-276">[Zainstaluj dla systemu Linux Agent pakietu OMS](log-analytics-agent-linux.md) bezpośrednio w każdym węźle OpenShift</span><span class="sxs-lookup"><span data-stu-id="6d5cb-276">[Install the OMS Agent for Linux](log-analytics-agent-linux.md) directly on each OpenShift node</span></span>  
* <span data-ttu-id="6d5cb-277">[Włączanie rozszerzenia maszyny Wirtualnej analizy dziennika](log-analytics-azure-vm-extension.md) w każdym węźle OpenShift znajdującej się na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="6d5cb-277">[Enable Log Analytics VM Extension](log-analytics-azure-vm-extension.md) on each OpenShift node residing in Azure</span></span>  
* <span data-ttu-id="6d5cb-278">Zainstaluj agenta pakietu OMS jako zestaw demon OpenShift</span><span class="sxs-lookup"><span data-stu-id="6d5cb-278">Install the OMS Agent as a OpenShift daemon-set</span></span>  

<span data-ttu-id="6d5cb-279">W tej sekcji możemy opisano kroki wymagane do zainstalowania agenta pakietu OMS jako zbiór demon OpenShift.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-279">In this section we cover the steps required to install the OMS Agent as an OpenShift daemon-set.</span></span>  

1. <span data-ttu-id="6d5cb-280">Zaloguj się do węzła głównego OpenShift, a następnie skopiuj plik yaml programu [ocp omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-omsagent.yaml) z serwisu GitHub, aby Twój główny węzeł i zmodyfikuj wartość za pomocą Identyfikatora obszar roboczy OMS i kluczem podstawowym.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-280">Sign on to the OpenShift master node and copy the yaml file [ocp-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-omsagent.yaml) from GitHub to your master node and modify the value with your OMS Workspace ID and with your Primary Key.</span></span>
2. <span data-ttu-id="6d5cb-281">Uruchom następujące polecenia, aby utworzyć projekt pakietu OMS i ustaw konto użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-281">Run the following commands to create a project for OMS and set the user account.</span></span>

    ```
    oadm new-project omslogging --node-selector='zone=default'
    oc project omslogging  
    oc create serviceaccount omsagent  
    oadm policy add-cluster-role-to-user cluster-reader   system:serviceaccount:omslogging:omsagent  
    oadm policy add-scc-to-user privileged system:serviceaccount:omslogging:omsagent  
    ```

4. <span data-ttu-id="6d5cb-282">Aby wdrożyć zestaw demon, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="6d5cb-282">To deploy the daemon-set, run the following:</span></span>

    `oc create -f ocp-omsagent.yaml`

5. <span data-ttu-id="6d5cb-283">Aby sprawdzić, czy jest on skonfigurowany i działa poprawnie, wpisz następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="6d5cb-283">To verify it is configured and working correctly, type the following:</span></span>

    `oc describe daemonset omsagent`  

    <span data-ttu-id="6d5cb-284">i powinien wyglądać dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="6d5cb-284">and the output should resemble:</span></span>

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

<span data-ttu-id="6d5cb-285">Jeśli chcesz zabezpieczyć OMS identyfikator i klucz podstawowy, korzystając z pliku zestawu demon yaml programu Agent pakietu OMS przy użyciu kluczy tajnych, wykonaj następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-285">If you want to use secrets to secure your OMS Workspace ID and Primary Key when using the OMS Agent daemon-set yaml file, perform the following steps.</span></span>

1. <span data-ttu-id="6d5cb-286">Zaloguj się do węzła głównego OpenShift, a następnie skopiuj plik yaml programu [ocp-ds-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-ds-omsagent.yaml) i klucz tajny Generowanie skryptu [ocp secretgen.sh](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-secretgen.sh) z usługi GitHub.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-286">Sign on to the OpenShift master node and copy the yaml file [ocp-ds-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-ds-omsagent.yaml) and secret generating script [ocp-secretgen.sh](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-secretgen.sh) from GitHub.</span></span>  <span data-ttu-id="6d5cb-287">Ten skrypt spowoduje wygenerowanie pliku yaml programu kluczy tajnych OMS identyfikator obszaru roboczego i klucz podstawowy zabezpieczyć Twoje secrete informacji.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-287">This script will generate the secrets yaml file for OMS Workspace ID and Primary Key to secure your secrete information.</span></span>  
2. <span data-ttu-id="6d5cb-288">Uruchom następujące polecenia, aby utworzyć projekt pakietu OMS i ustaw konto użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-288">Run the following commands to create a project for OMS and set the user account.</span></span> <span data-ttu-id="6d5cb-289">Klucz tajny Generowanie skryptu poprosi o podanie Identyfikatora obszar roboczy OMS <WSID> i klucz podstawowy <KEY> i po jego ukończeniu, tworzy plik ocp secret.yaml.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-289">The secret generating script asks for your OMS Workspace ID <WSID> and Primary Key <KEY> and upon completion, it creates the ocp-secret.yaml file.</span></span>  

    ```
    oadm new-project omslogging --node-selector='zone=default'  
    oc project omslogging  
    oc create serviceaccount omsagent  
    oadm policy add-cluster-role-to-user cluster-reader   system:serviceaccount:omslogging:omsagent  
    oadm policy add-scc-to-user privileged system:serviceaccount:omslogging:omsagent  
    ```

4. <span data-ttu-id="6d5cb-290">Wdróż plik za pomocą tajne, uruchamiając następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="6d5cb-290">Deploy the secret file by running the following:</span></span>

    `oc create -f ocp-secret.yaml`

5. <span data-ttu-id="6d5cb-291">Sprawdź wdrożenie, uruchamiając następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="6d5cb-291">Verify deployment by running the following:</span></span>

    `oc describe secret omsagent-secret`  

    <span data-ttu-id="6d5cb-292">i powinien wyglądać dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="6d5cb-292">and the  output should resemble:</span></span>  

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

6. <span data-ttu-id="6d5cb-293">Wdróż plik zestawu demon yaml programu Agent pakietu OMS, uruchamiając następujące:</span><span class="sxs-lookup"><span data-stu-id="6d5cb-293">Deploy the OMS Agent daemon-set yaml file by running the following:</span></span>

    `oc create -f ocp-ds-omsagent.yaml`  

7. <span data-ttu-id="6d5cb-294">Sprawdź wdrożenie, uruchamiając następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="6d5cb-294">Verify deployment by running the following:</span></span>

    `oc describe ds oms`

    <span data-ttu-id="6d5cb-295">i powinien wyglądać dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="6d5cb-295">and the output should resemble:</span></span>

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

### <a name="secure-your-secret-information-for-docker-swarm-and-kubernetes"></a><span data-ttu-id="6d5cb-296">Zabezpieczanie tajnych informacji o Docker Swarm i Kubernetes</span><span class="sxs-lookup"><span data-stu-id="6d5cb-296">Secure your secret information for Docker Swarm and Kubernetes</span></span>

<span data-ttu-id="6d5cb-297">Dla usługi kontenera Kubernetes i Docker Swarm można zabezpieczyć tajny identyfikator OMS i kluczy podstawowych.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-297">You can secure your secret OMS Workspace ID and Primary Keys for Docker Swarm and Kubernetes container services.</span></span>

#### <a name="secure-secrets-for-docker-swarm"></a><span data-ttu-id="6d5cb-298">Bezpiecznego hasła dla rozwiązania Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="6d5cb-298">Secure secrets for Docker Swarm</span></span>

<span data-ttu-id="6d5cb-299">Dla rozwiązania Docker Swarm po klucz tajny dla identyfikator i klucz podstawowy został utworzony, można uruchomić tworzenia usługi Docker dla OMSagent.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-299">For Docker Swarm, once the secret for Workspace ID and Primary Key is created, you can run the create the Docker service for OMSagent.</span></span> <span data-ttu-id="6d5cb-300">Skorzystaj z poniższych informacji, aby utworzyć dane poufne.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-300">Use the following information to create your secret information.</span></span>

1. <span data-ttu-id="6d5cb-301">Uruchom następujące polecenie na węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-301">Run the following on the master node.</span></span>

    ```
    echo "WSID" | docker secret create WSID -
    echo "KEY" | docker secret create KEY -
    ```

2. <span data-ttu-id="6d5cb-302">Sprawdź, czy klucze tajne zostały utworzone prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-302">Verify that secrets were created properly.</span></span>

    ```
    keiko@swarmm-master-13957614-0:/run# sudo docker secret ls
    ```

    ```
    ID                          NAME                CREATED             UPDATED
    j2fj153zxy91j8zbcitnjxjiv   WSID                43 minutes ago      43 minutes ago
    l9rh3n987g9c45zffuxdxetd9   KEY                 38 minutes ago      38 minutes ago
    ```

3. <span data-ttu-id="6d5cb-303">Uruchom następujące polecenie, aby zainstalować kluczy tajnych konteneryzowanych Agent pakietu OMS.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-303">Run the following command to mount the secrets to the containerized OMS Agent.</span></span>

    ```
    sudo docker service create  --name omsagent --mode global  --mount type=bind,source=/var/run/docker.sock,destination=/var/run/docker.sock --secret source=WSID,target=WSID --secret source=KEY,target=KEY  -p 25225:25225 -p 25224:25224/udp --restart-condition=on-failure microsoft/oms
    ```

#### <a name="secure-secrets-for-kubernetes-with-yaml-files"></a><span data-ttu-id="6d5cb-304">Bezpiecznego hasła dla Kubernetes z plikami yaml programu</span><span class="sxs-lookup"><span data-stu-id="6d5cb-304">Secure secrets for Kubernetes with yaml files</span></span>

<span data-ttu-id="6d5cb-305">Dla Kubernetes możesz użyć skryptu do generowania pliku yaml programu kluczy tajnych identyfikator i klucz podstawowy.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-305">For Kubernetes, you use a script to generate the secrets yaml file for your Workspace ID and Primary Key.</span></span> <span data-ttu-id="6d5cb-306">W [OMS Docker Kubernetes GitHub](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes) są dostępne pliki korzystające z lub bez tajnych informacji.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-306">At the [OMS Docker Kubernetes GitHub](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes) page, there are files that you can use with or without your secret information.</span></span>

- <span data-ttu-id="6d5cb-307">DaemonSet domyślne Agent pakietu OMS nie ma tajnych informacji (omsagent.yaml)</span><span class="sxs-lookup"><span data-stu-id="6d5cb-307">The Default OMS Agent DaemonSet does not have secret information (omsagent.yaml)</span></span>
- <span data-ttu-id="6d5cb-308">Plik yaml programu DaemonSet Agent pakietu OMS używa tajnych informacji (omsagent-ds-secrets.yaml) z tajny generowania skryptów do generowania kluczy tajnych pliku yaml programu (omsagentsecret.yaml).</span><span class="sxs-lookup"><span data-stu-id="6d5cb-308">The OMS Agent DaemonSet yaml file uses secret information (omsagent-ds-secrets.yaml) with secret generation scripts to generate the secrets yaml (omsagentsecret.yaml) file.</span></span>

<span data-ttu-id="6d5cb-309">Można utworzyć omsagent DaemonSets z lub bez kluczy tajnych.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-309">You can choose to create omsagent DaemonSets with or without secrets.</span></span>

##### <a name="default-omsagent-daemonset-yaml-file-without-secrets"></a><span data-ttu-id="6d5cb-310">Domyślny OMSagent DaemonSet yaml programu plik bez hasła</span><span class="sxs-lookup"><span data-stu-id="6d5cb-310">Default OMSagent DaemonSet yaml file without secrets</span></span>

- <span data-ttu-id="6d5cb-311">Dla domyślnego pliku yaml programu DaemonSet Agent pakietu OMS, Zastąp `<WSID>` i `<KEY>` WSID i klucza.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-311">For the default OMS Agent DaemonSet yaml file, replace the `<WSID>` and `<KEY>` to your WSID and KEY.</span></span> <span data-ttu-id="6d5cb-312">Skopiuj plik do główny węzeł i uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="6d5cb-312">Copy the file to your master node and run the following:</span></span>

    ```
    sudo kubectl create -f omsagent.yaml
    ```

##### <a name="default-omsagent-daemonset-yaml-file-with-secrets"></a><span data-ttu-id="6d5cb-313">Domyślny OMSagent DaemonSet yaml programu plik z kluczy tajnych</span><span class="sxs-lookup"><span data-stu-id="6d5cb-313">Default OMSagent DaemonSet yaml file with secrets</span></span>

1. <span data-ttu-id="6d5cb-314">Aby użyć DaemonSet Agent pakietu OMS przy użyciu poufne informacje, należy najpierw utworzyć kluczy tajnych.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-314">To use OMS Agent DaemonSet using secret information, create the secrets first.</span></span>
    1. <span data-ttu-id="6d5cb-315">Skopiuj skrypt i pliku szablonu tajne i upewnij się, że znajdują się w tym samym katalogu.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-315">Copy the script and secret template file and make sure they are on the same directory.</span></span>
        - <span data-ttu-id="6d5cb-316">Generowanie skryptu - gen.sh klucz tajny klucz tajny</span><span class="sxs-lookup"><span data-stu-id="6d5cb-316">Secret generating script - secret-gen.sh</span></span>
        - <span data-ttu-id="6d5cb-317">Szablon tajne — template.yaml klucz tajny</span><span class="sxs-lookup"><span data-stu-id="6d5cb-317">secret template - secret-template.yaml</span></span>
    2. <span data-ttu-id="6d5cb-318">Uruchom skrypt, jak w następującym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-318">Run the script, like the following example.</span></span> <span data-ttu-id="6d5cb-319">Wyświetleniu zapytania o OMS identyfikator i klucz podstawowy i po wprowadzeniu ich skrypt tworzy plik tajny yaml programu, dlatego może być uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-319">The script asks for the OMS Workspace ID and Primary Key and after you enter them, the script creates a secret yaml file so you can run it.</span></span>   

        ```
        #> sudo bash ./secret-gen.sh
        ```

    3. <span data-ttu-id="6d5cb-320">Utwórz pod kluczy tajnych, uruchamiając następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="6d5cb-320">Create the secrets pod by running the following:</span></span>
        ```
        sudo kubectl create -f omsagentsecret.yaml
        ```

    4. <span data-ttu-id="6d5cb-321">Aby sprawdzić, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="6d5cb-321">To verify, run the following:</span></span>

        ```
        keiko@ubuntu16-13db:~# sudo kubectl get secrets
        ```

        <span data-ttu-id="6d5cb-322">Dane wyjściowe powinny wyglądać:</span><span class="sxs-lookup"><span data-stu-id="6d5cb-322">Output should resemble:</span></span>

        ```
        NAME                  TYPE                                  DATA      AGE
        default-token-gvl91   kubernetes.io/service-account-token   3         50d
        omsagent-secret       Opaque                                2         1d
        ```

        ```
        keiko@ubuntu16-13db:~# sudo kubectl describe secrets omsagent-secret
        ```

        <span data-ttu-id="6d5cb-323">Dane wyjściowe powinny wyglądać:</span><span class="sxs-lookup"><span data-stu-id="6d5cb-323">Output should resemble:</span></span>

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

    5. <span data-ttu-id="6d5cb-324">Tworzenie sieci omsagent demon set, uruchamiając``` sudo kubectl create -f omsagent-ds-secrets.yaml ```</span><span class="sxs-lookup"><span data-stu-id="6d5cb-324">Create your omsagent daemon-set by running ``` sudo kubectl create -f omsagent-ds-secrets.yaml ```</span></span>

2. <span data-ttu-id="6d5cb-325">Sprawdź, czy DaemonSet Agent pakietu OMS jest uruchomiona, podobny do następującego:</span><span class="sxs-lookup"><span data-stu-id="6d5cb-325">Verify that the OMS Agent DaemonSet is running, similar to the following:</span></span>

    ```
    keiko@ubuntu16-13db:~# sudo kubectl get ds omsagent
    ```

    ```
    NAME       DESIRED   CURRENT   NODE-SELECTOR   AGE
    omsagent   3         3         <none>          1h
    ```


<span data-ttu-id="6d5cb-326">Aby wygenerować plik yaml programu klucze tajne dla identyfikator i klucz podstawowy dla Kubernetes, za pomocą skryptu.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-326">For Kubernetes, use a script to generate the secrets yaml file for Workspace ID and Primary Key.</span></span> <span data-ttu-id="6d5cb-327">Skorzystaj z poniższych informacji przykład z [pliku yaml programu omsagent](https://github.com/Microsoft/OMS-docker/blob/master/Kubernetes/omsagent.yaml) zabezpieczyć dane poufne.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-327">Use the following example information with the [omsagent yaml file](https://github.com/Microsoft/OMS-docker/blob/master/Kubernetes/omsagent.yaml) to secure your secret information.</span></span>

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

## <a name="windows-container-hosts"></a><span data-ttu-id="6d5cb-328">Hosty kontenera systemu Windows</span><span class="sxs-lookup"><span data-stu-id="6d5cb-328">Windows container hosts</span></span>

### <a name="preparation-before-installing-windows-agents"></a><span data-ttu-id="6d5cb-329">Przygotowanie przed zainstalowaniem agentów systemu Windows</span><span class="sxs-lookup"><span data-stu-id="6d5cb-329">Preparation before installing Windows agents</span></span>

<span data-ttu-id="6d5cb-330">Aby zainstalować agentów na komputerach z systemem Windows, należy skonfigurować usługę Docker.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-330">Before you install agents on computers running Windows, you need to configure the Docker service.</span></span> <span data-ttu-id="6d5cb-331">Konfiguracji umożliwia agent systemu Windows lub analizy dzienników rozszerzenie maszyny wirtualnej do używania gniazda Docker TCP, dzięki czemu agenci dostęp zdalnie demona Docker i przechwytywania danych monitorowania.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-331">The configuration allows the Windows agent or the Log Analytics virtual machine extension to use the Docker TCP socket so that the agents can access the Docker daemon remotely and to capture data for monitoring.</span></span>

#### <a name="to-start-docker-and-verify-its-configuration"></a><span data-ttu-id="6d5cb-332">Aby uruchomić Docker i sprawdzić jego konfigurację</span><span class="sxs-lookup"><span data-stu-id="6d5cb-332">To start Docker and verify its configuration</span></span>

<span data-ttu-id="6d5cb-333">Istnieją kroki niezbędne do skonfigurowania TCP nazwany potok dla systemu Windows Server:</span><span class="sxs-lookup"><span data-stu-id="6d5cb-333">There are steps needed to set up TCP named pipe for Windows Server:</span></span>

1. <span data-ttu-id="6d5cb-334">W programie Windows PowerShell umożliwiają potoku TCP i nazwanego potoku.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-334">In Windows PowerShell, enable TCP pipe and named pipe.</span></span>

    ```
    Stop-Service docker
    dockerd --unregister-service
    dockerd --register-service -H npipe:// -H 0.0.0.0:2375  
    Start-Service docker
    ```

2. <span data-ttu-id="6d5cb-335">Konfigurowanie Docker z pliku konfiguracji dla potoku TCP i nazwany potok.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-335">Configure Docker with the configuration file for TCP pipe and named pipe.</span></span> <span data-ttu-id="6d5cb-336">Plik konfiguracji znajduje się w C:\ProgramData\docker\config\daemon.json.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-336">The configuration file is located at C:\ProgramData\docker\config\daemon.json.</span></span>

    <span data-ttu-id="6d5cb-337">W pliku daemon.json potrzebne następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="6d5cb-337">In the daemon.json file, you will need the following:</span></span>

    ```
    {
    "hosts": ["tcp://0.0.0.0:2375", "npipe://"]
    }
    ```

<span data-ttu-id="6d5cb-338">Aby uzyskać więcej informacji na temat konfiguracji demon Docker używane z kontenerami systemu Windows, temacie [aparatem platformy Docker w systemie Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon).</span><span class="sxs-lookup"><span data-stu-id="6d5cb-338">For more information about the Docker daemon configuration used with Windows Containers, see [Docker Engine on Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon).</span></span>


### <a name="install-windows-agents"></a><span data-ttu-id="6d5cb-339">Zainstaluj agentów systemu Windows</span><span class="sxs-lookup"><span data-stu-id="6d5cb-339">Install Windows agents</span></span>

<span data-ttu-id="6d5cb-340">Aby włączyć monitorowania kontenera systemu Windows i funkcji Hyper-V, należy zainstalować program Microsoft Monitoring Agent (MMA) na komputerach z systemem Windows, które są hostami kontenera.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-340">To enable Windows and Hyper-V container monitoring, install the Microsoft Monitoring Agent (MMA) on Windows computers that are container hosts.</span></span> <span data-ttu-id="6d5cb-341">Na komputerach z systemem Windows w środowisku lokalnym, zobacz [połączyć komputery do analizy dzienników](log-analytics-windows-agents.md).</span><span class="sxs-lookup"><span data-stu-id="6d5cb-341">For computers running Windows in your on-premises environment, see [Connect Windows computers to Log Analytics](log-analytics-windows-agents.md).</span></span> <span data-ttu-id="6d5cb-342">W przypadku maszyn wirtualnych działających na platformie Azure, podłącz je do analizy dzienników przy użyciu [rozszerzenie maszyny wirtualnej](log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="6d5cb-342">For virtual machines running in Azure, connect them to Log Analytics using the [virtual machine extension](log-analytics-azure-vm-extension.md).</span></span>

<span data-ttu-id="6d5cb-343">Można monitorować kontenery systemu Windows uruchomiona na sieć szkieletowa usług.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-343">You can monitor Windows containers running on Service Fabric.</span></span> <span data-ttu-id="6d5cb-344">Jednak tylko [maszyn wirtualnych działających na platformie Azure](log-analytics-azure-vm-extension.md) i [komputery z systemem Windows w środowisku lokalnym](log-analytics-windows-agents.md) są obecnie obsługiwane dla sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-344">However, only [virtual machines running in Azure](log-analytics-azure-vm-extension.md) and [computers running Windows in your on-premises environment](log-analytics-windows-agents.md) are currently supported for Service Fabric.</span></span>

<span data-ttu-id="6d5cb-345">Możesz sprawdzić, czy to rozwiązanie monitorowanie kontenera jest prawidłowo dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-345">You can verify that the Container Monitoring solution is set correctly for Windows.</span></span> <span data-ttu-id="6d5cb-346">Aby sprawdzić, czy pakiet administracyjny został poprawnie pobierania, należy wyszukać *ContainerManagement.xxx*.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-346">To check whether the management pack was download properly, look for *ContainerManagement.xxx*.</span></span> <span data-ttu-id="6d5cb-347">Pliki powinny być w folderze C:\Program Files\Microsoft Monitoring Agent\Agent\Health usługi State\Management pakietów.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-347">The files should be in the C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs folder.</span></span>


## <a name="solution-components"></a><span data-ttu-id="6d5cb-348">Składniki rozwiązania</span><span class="sxs-lookup"><span data-stu-id="6d5cb-348">Solution components</span></span>

<span data-ttu-id="6d5cb-349">Jeśli korzystasz z agentów systemu Windows, następujące pakiet administracyjny jest zainstalowany na każdym komputerze z agentem po dodaniu tego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-349">If you are using Windows agents, then the following management pack is installed on each computer with an agent when you add this solution.</span></span> <span data-ttu-id="6d5cb-350">Nie konfiguracji lub konserwacji jest wymagany dla pakietu administracyjnego.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-350">No configuration or maintenance is required for the management pack.</span></span>

- <span data-ttu-id="6d5cb-351">*ContainerManagement.xxx* zainstalowane w C:\Program Files\Microsoft Monitoring Agent\Agent\Health usługi State\Management pakietów</span><span class="sxs-lookup"><span data-stu-id="6d5cb-351">*ContainerManagement.xxx* installed in C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs</span></span>

## <a name="container-data-collection-details"></a><span data-ttu-id="6d5cb-352">Szczegóły pobierania danych kontenera</span><span class="sxs-lookup"><span data-stu-id="6d5cb-352">Container data collection details</span></span>
<span data-ttu-id="6d5cb-353">To rozwiązanie monitorowanie kontenera zbiera różne metryki i dziennika dane dotyczące wydajności z kontenera hostów i kontenerów przy użyciu agentów, które można włączyć.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-353">The Container Monitoring solution collects various performance metrics and log data from container hosts and containers using agents that you enable.</span></span>

<span data-ttu-id="6d5cb-354">Dane są zbierane co 3 minuty przez następujące typy agenta.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-354">Data is collected every three minutes by the following agent types.</span></span>

- [<span data-ttu-id="6d5cb-355">Agent pakietu OMS dla systemu Linux</span><span class="sxs-lookup"><span data-stu-id="6d5cb-355">OMS Agent for Linux</span></span>](log-analytics-linux-agents.md)
- [<span data-ttu-id="6d5cb-356">Agent systemu Windows</span><span class="sxs-lookup"><span data-stu-id="6d5cb-356">Windows agent</span></span>](log-analytics-windows-agents.md)
- [<span data-ttu-id="6d5cb-357">Rozszerzenia maszyny Wirtualnej analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="6d5cb-357">Log Analytics VM extension</span></span>](log-analytics-azure-vm-extension.md)


### <a name="container-records"></a><span data-ttu-id="6d5cb-358">Rejestruje kontenera</span><span class="sxs-lookup"><span data-stu-id="6d5cb-358">Container records</span></span>

<span data-ttu-id="6d5cb-359">W poniższej tabeli przedstawiono przykłady rekordów zebrane przez rozwiązanie monitorowanie kontenera i typy danych, które są wyświetlane w wynikach wyszukiwania dziennika.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-359">The following table shows examples of records collected by the Container Monitoring solution and the data types that appear in log search results.</span></span>

| <span data-ttu-id="6d5cb-360">Typ danych</span><span class="sxs-lookup"><span data-stu-id="6d5cb-360">Data type</span></span> | <span data-ttu-id="6d5cb-361">Typ danych w dzienniku wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="6d5cb-361">Data type in Log Search</span></span> | <span data-ttu-id="6d5cb-362">Pola</span><span class="sxs-lookup"><span data-stu-id="6d5cb-362">Fields</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6d5cb-363">Wydajność dla hostów i kontenerów</span><span class="sxs-lookup"><span data-stu-id="6d5cb-363">Performance for hosts and containers</span></span> | `Type=Perf` | <span data-ttu-id="6d5cb-364">Komputer, nazwa obiektu, CounterName &#40; czas procesora (%), dysk odczytuje MB, dysku zapisuje MB, użycie pamięć (MB), sieci odbieranie bajtów, sieci wysyłania w bajtach, procesor s użycia sieci &#41; równowartości, TimeGenerated, Ścieżka_licznika, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="6d5cb-364">Computer, ObjectName, CounterName &#40;%Processor Time, Disk Reads MB, Disk Writes MB, Memory Usage MB, Network Receive Bytes, Network Send Bytes, Processor Usage sec, Network&#41;, CounterValue,TimeGenerated, CounterPath, SourceSystem</span></span> |
| <span data-ttu-id="6d5cb-365">Kontener magazynu</span><span class="sxs-lookup"><span data-stu-id="6d5cb-365">Container inventory</span></span> | `Type=ContainerInventory` | <span data-ttu-id="6d5cb-366">TimeGenerated, komputera, nazwę kontenera, ContainerHostname, obraz, ImageTag, ContainerState, ExitCode, EnvironmentVar, polecenia, CreatedTime, StartedTime, FinishedTime, SourceSystem, identyfikatora kontenera, ImageID</span><span class="sxs-lookup"><span data-stu-id="6d5cb-366">TimeGenerated, Computer, container name, ContainerHostname, Image, ImageTag, ContainerState, ExitCode, EnvironmentVar, Command, CreatedTime, StartedTime, FinishedTime, SourceSystem, ContainerID, ImageID</span></span> |
| <span data-ttu-id="6d5cb-367">Kontener magazynu obrazu</span><span class="sxs-lookup"><span data-stu-id="6d5cb-367">Container image inventory</span></span> | `Type=ContainerImageInventory` | <span data-ttu-id="6d5cb-368">TimeGenerated, komputer, obraz, ImageTag, ImageSize, VirtualSize, działa wstrzymana, zatrzymana, nie powiodło się, SourceSystem, ImageID, TotalContainer</span><span class="sxs-lookup"><span data-stu-id="6d5cb-368">TimeGenerated, Computer, Image, ImageTag, ImageSize, VirtualSize, Running, Paused, Stopped, Failed, SourceSystem, ImageID, TotalContainer</span></span> |
| <span data-ttu-id="6d5cb-369">Kontener dziennika</span><span class="sxs-lookup"><span data-stu-id="6d5cb-369">Container log</span></span> | `Type=ContainerLog` | <span data-ttu-id="6d5cb-370">TimeGenerated, komputer, identyfikator obrazu, nazwy kontenera, LogEntrySource, LogEntry, SourceSystem, identyfikatora kontenera</span><span class="sxs-lookup"><span data-stu-id="6d5cb-370">TimeGenerated, Computer, image ID, container name, LogEntrySource, LogEntry, SourceSystem, ContainerID</span></span> |
| <span data-ttu-id="6d5cb-371">Dziennik usługi kontenera</span><span class="sxs-lookup"><span data-stu-id="6d5cb-371">Container service log</span></span> | `Type=ContainerServiceLog`  | <span data-ttu-id="6d5cb-372">TimeGenerated, komputer, TimeOfCommand, obraz, polecenia, SourceSystem, identyfikatora kontenera</span><span class="sxs-lookup"><span data-stu-id="6d5cb-372">TimeGenerated, Computer, TimeOfCommand, Image, Command, SourceSystem, ContainerID</span></span> |
| <span data-ttu-id="6d5cb-373">Kontener węzła magazynu</span><span class="sxs-lookup"><span data-stu-id="6d5cb-373">Container node inventory</span></span> | `Type=ContainerNodeInventory_CL`| <span data-ttu-id="6d5cb-374">TimeGenerated, komputer, ClassName_s, DockerVersion_s, OperatingSystem_s, Volume_s, Network_s, NodeRole_s, OrchestratorType_s, InstanceID_g, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="6d5cb-374">TimeGenerated, Computer, ClassName_s, DockerVersion_s, OperatingSystem_s, Volume_s, Network_s, NodeRole_s, OrchestratorType_s, InstanceID_g, SourceSystem</span></span>|
| <span data-ttu-id="6d5cb-375">Kubernetes spisu</span><span class="sxs-lookup"><span data-stu-id="6d5cb-375">Kubernetes inventory</span></span> | `Type=KubePodInventory_CL` | <span data-ttu-id="6d5cb-376">TimeGenerated, komputer, PodLabel_deployment_s, PodLabel_deploymentconfig_s, PodLabel_docker_registry_s, Name_s, Namespace_s, PodStatus_s, PodIp_s, PodUid_g, PodCreationTimeStamp_t, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="6d5cb-376">TimeGenerated, Computer, PodLabel_deployment_s, PodLabel_deploymentconfig_s, PodLabel_docker_registry_s, Name_s, Namespace_s, PodStatus_s, PodIp_s, PodUid_g, PodCreationTimeStamp_t, SourceSystem</span></span> |
| <span data-ttu-id="6d5cb-377">Proces kontenera</span><span class="sxs-lookup"><span data-stu-id="6d5cb-377">Container process</span></span> | `Type=ContainerProcess_CL` | <span data-ttu-id="6d5cb-378">TimeGenerated, komputer, Pod_s, Namespace_s, ClassName_s, InstanceID_s, Uid_s, PID_s, PPID_s, C_s, STIME_s, Tty_s, TIME_s, Cmd_s, Id_s, Name_s, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="6d5cb-378">TimeGenerated, Computer, Pod_s, Namespace_s, ClassName_s, InstanceID_s, Uid_s, PID_s, PPID_s, C_s, STIME_s, Tty_s, TIME_s, Cmd_s, Id_s, Name_s, SourceSystem</span></span> |
| <span data-ttu-id="6d5cb-379">Zdarzenia Kubernetes</span><span class="sxs-lookup"><span data-stu-id="6d5cb-379">Kubernetes events</span></span> | `Type=KubeEvents_CL` | <span data-ttu-id="6d5cb-380">TimeGenerated, komputer, Name_s, ObjectKind_s, Namespace_s, Reason_s, Type_s, SourceComponent_s, SourceSystem, komunikatów</span><span class="sxs-lookup"><span data-stu-id="6d5cb-380">TimeGenerated, Computer, Name_s, ObjectKind_s, Namespace_s, Reason_s, Type_s, SourceComponent_s, SourceSystem, Message</span></span> |

<span data-ttu-id="6d5cb-381">Etykiety dołączany do *PodLabel* typy danych są etykiet niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-381">Labels appended to *PodLabel* data types are your own custom labels.</span></span> <span data-ttu-id="6d5cb-382">Dołączany etykiety PodLabel przedstawione w tabeli przedstawiono przykłady.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-382">The appended PodLabel labels shown in the table are examples.</span></span> <span data-ttu-id="6d5cb-383">Tak `PodLabel_deployment_s`, `PodLabel_deploymentconfig_s`, `PodLabel_docker_registry_s` różnią się w zestawie danych w danym środowisku, a objęty przypominać `PodLabel_yourlabel_s`.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-383">So, `PodLabel_deployment_s`, `PodLabel_deploymentconfig_s`, `PodLabel_docker_registry_s` will differ in your environment's data set and generically resemble `PodLabel_yourlabel_s`.</span></span>


## <a name="monitor-containers"></a><span data-ttu-id="6d5cb-384">Kontenery monitora</span><span class="sxs-lookup"><span data-stu-id="6d5cb-384">Monitor containers</span></span>
<span data-ttu-id="6d5cb-385">Po rozwiązaniu włączone w portalu OMS **kontenery** kafelka zawiera podsumowanie informacji o hostach kontenera i kontenery uruchomione na hostach.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-385">After you have the solution enabled in the OMS portal, the **Containers** tile shows summary information about your container hosts and the containers running in hosts.</span></span>

![Kontenery kafelka](./media/log-analytics-containers/containers-title.png)

<span data-ttu-id="6d5cb-387">Kafelek Wyświetla liczbę kontenerów masz w środowisku, czy jest nie, uruchamiania i zatrzymywana.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-387">The tile shows an overview of how many containers you have in the environment and whether they're failed, running, or stopped.</span></span>

### <a name="using-the-containers-dashboard"></a><span data-ttu-id="6d5cb-388">Przy użyciu pulpitu nawigacyjnego kontenerów</span><span class="sxs-lookup"><span data-stu-id="6d5cb-388">Using the Containers dashboard</span></span>
<span data-ttu-id="6d5cb-389">Kliknij przycisk **kontenery** kafelka.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-389">Click the **Containers** tile.</span></span> <span data-ttu-id="6d5cb-390">Z tego miejsca zobaczysz widoki uporządkowane według:</span><span class="sxs-lookup"><span data-stu-id="6d5cb-390">From there you'll see views organized by:</span></span>

- <span data-ttu-id="6d5cb-391">**Kontenery zdarzeń** -pokazuje stan kontenera i komputerów z kontenerami nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-391">**Container Events** - Shows container status and computers with failed containers.</span></span>
- <span data-ttu-id="6d5cb-392">**Dzienniki kontenera** — przedstawia wykres kontenera pliki dziennika wygenerowane przez czas i listę komputerów o najwyższym numerze plików dziennika.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-392">**Container Logs** - Shows a chart of container log files generated over time and a list of computers with the highest number of log files.</span></span>
- <span data-ttu-id="6d5cb-393">**Zdarzenia Kubernetes** — przedstawia wykres Kubernetes zdarzenia generowane przez czas i listę przyczyn, dlaczego stanowiskami wygenerowane zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-393">**Kubernetes Events** - Shows a chart of Kubernetes events generated over time and a list of the reasons why pods generated the events.</span></span> <span data-ttu-id="6d5cb-394">*Ten zestaw danych jest używany tylko w środowiskach Linux.*</span><span class="sxs-lookup"><span data-stu-id="6d5cb-394">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="6d5cb-395">**Spis Namespace Kubernetes** — pokazuje liczbę obszary nazw i stanowiskami i przedstawiono ich hierarchii.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-395">**Kubernetes Namespace Inventory** - Shows the number of namespaces and pods and shows their hierarchy.</span></span> <span data-ttu-id="6d5cb-396">*Ten zestaw danych jest używany tylko w środowiskach Linux.*</span><span class="sxs-lookup"><span data-stu-id="6d5cb-396">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="6d5cb-397">**Kontener węzeł spisu** — pokazuje liczbę typów aranżacji używanych na hosty węzłów kontenera.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-397">**Container Node Inventory** - Shows the number of orchestration types used on container nodes/hosts.</span></span> <span data-ttu-id="6d5cb-398">Węzły komputera/hostów są także wyświetlane przez liczbę kontenerów.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-398">The computer nodes/hosts are also listed by the number of containers.</span></span> <span data-ttu-id="6d5cb-399">*Ten zestaw danych jest używany tylko w środowiskach Linux.*</span><span class="sxs-lookup"><span data-stu-id="6d5cb-399">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="6d5cb-400">**Kontener obrazów spisu** -pokazuje całkowitą liczbę obrazów kontenera używane oraz liczbę typów obrazów.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-400">**Container Images Inventory** - Shows the total number of container images used and number of image types.</span></span> <span data-ttu-id="6d5cb-401">Liczba obrazów są także wyświetlane przez tag obrazu.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-401">The number of images are also listed by the image tag.</span></span>
- <span data-ttu-id="6d5cb-402">**Stan kontenery** — zawiera całkowitą liczbę kontenera Komputery węzłów/hosta uruchomionych kontenerów.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-402">**Containers Status** - Shows the total number of container nodes/host computers that have running containers.</span></span> <span data-ttu-id="6d5cb-403">Komputery są również wyświetlane według liczba uruchomionych na hostach.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-403">Computers are also listed by the number of running hosts.</span></span>
- <span data-ttu-id="6d5cb-404">**Proces kontenera** — przedstawia wykres liniowy procesów kontenera działających w czasie.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-404">**Container Process** - Shows a line chart of container processes running over time.</span></span> <span data-ttu-id="6d5cb-405">Kontenery znajdują się przez uruchomienie polecenia procesu w kontenerach.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-405">Containers are also listed by running command/process within containers.</span></span> <span data-ttu-id="6d5cb-406">*Ten zestaw danych jest używany tylko w środowiskach Linux.*</span><span class="sxs-lookup"><span data-stu-id="6d5cb-406">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="6d5cb-407">**Wydajność Procesora kontenera** — przedstawia wykres liniowy w średnie wykorzystanie procesora CPU, wraz z upływem czasu hosty węzłów komputera.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-407">**Container CPU Performance** - Shows a line chart of the average CPU utilization over time for computer nodes/hosts.</span></span> <span data-ttu-id="6d5cb-408">Również listy węzłów komputera/hostów na podstawie średniego użycia Procesora.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-408">Also lists the computer nodes/hosts based on average CPU utilization.</span></span>
- <span data-ttu-id="6d5cb-409">**Kontener wydajności pamięci** — przedstawia wykres liniowy użycia pamięci w czasie.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-409">**Container Memory Performance** - Shows a line chart of memory usage over time.</span></span> <span data-ttu-id="6d5cb-410">Zawiera także listę wykorzystania opartego na nazwie wystąpienia pamięci komputera.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-410">Also lists computer memory utilization based on instance name.</span></span>
- <span data-ttu-id="6d5cb-411">**Wydajność komputera** — zawiera wykresy liniowe procent wydajności Procesora w czasie, procent użycia pamięci przez czas i megabajtów wolnego miejsca na dysku wraz z upływem czasu.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-411">**Computer Performance** - Shows line charts of the percent of CPU performance over time, percent of memory usage over time, and megabytes of free disk space over time.</span></span> <span data-ttu-id="6d5cb-412">Można umieść kursor nad wiersza na wykresie, aby wyświetlić więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-412">You can hover over any line in a chart to view more details.</span></span>


<span data-ttu-id="6d5cb-413">Każdy obszar pulpitu nawigacyjnego jest wizualną reprezentację wyszukiwania, które jest uruchamiane na zebranych danych.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-413">Each area of the dashboard is a visual representation of a search that is run on collected data.</span></span>

![Kontenery pulpitu nawigacyjnego](./media/log-analytics-containers/containers-dash01.png)

![Kontenery pulpitu nawigacyjnego](./media/log-analytics-containers/containers-dash02.png)

<span data-ttu-id="6d5cb-416">W **stan kontenera** obszarze kliknij górny obszar, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-416">In the **Container Status** area, click the top area, as shown below.</span></span>

![Stan kontenerów](./media/log-analytics-containers/containers-status.png)

<span data-ttu-id="6d5cb-418">Otwiera dziennik wyszukiwania, wyświetlania informacji o stanie kontenerów.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-418">Log Search opens, displaying information about the state of your containers.</span></span>

![Dziennik wyszukiwania dla kontenerów](./media/log-analytics-containers/containers-log-search.png)

<span data-ttu-id="6d5cb-420">W tym miejscu można edytować zapytania wyszukiwania można zmodyfikować, aby znaleźć określone informacje, że jesteś zainteresowany.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-420">From here, you can edit the search query to modify it to find the specific information you're interested in.</span></span> <span data-ttu-id="6d5cb-421">Aby uzyskać więcej informacji na temat wyszukiwania dziennika, zobacz [Zaloguj wyszukiwania analizy dzienników](log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="6d5cb-421">For more information about Log Searches, see [Log searches in Log Analytics](log-analytics-log-searches.md).</span></span>

## <a name="troubleshoot-by-finding-a-failed-container"></a><span data-ttu-id="6d5cb-422">Rozwiązywanie problemów z znajdując kontenera nie powiodło się</span><span class="sxs-lookup"><span data-stu-id="6d5cb-422">Troubleshoot by finding a failed container</span></span>

<span data-ttu-id="6d5cb-423">Analiza dzienników oznacza kontener jako **nie powiodło się** Jeśli został zakończony z kodem zakończenia inną niż zero.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-423">Log Analytics marks a container as **Failed** if it has exited with a non-zero exit code.</span></span> <span data-ttu-id="6d5cb-424">Można zapoznać się z omówieniem błędów i awarii w środowisku w **nie powiodło się kontenery** obszaru.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-424">You can see an overview of the errors and failures in the environment in the **Failed Containers** area.</span></span>

### <a name="to-find-failed-containers"></a><span data-ttu-id="6d5cb-425">Aby znaleźć kontenery nie powiodło się</span><span class="sxs-lookup"><span data-stu-id="6d5cb-425">To find failed containers</span></span>
1. <span data-ttu-id="6d5cb-426">Kliknij przycisk **stan kontenera** obszaru.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-426">Click the **Container Status** area.</span></span>  
   <span data-ttu-id="6d5cb-427">![Stan kontenerów](./media/log-analytics-containers/containers-status.png)</span><span class="sxs-lookup"><span data-stu-id="6d5cb-427">![containers status](./media/log-analytics-containers/containers-status.png)</span></span>
2. <span data-ttu-id="6d5cb-428">Dziennik wyszukiwania otwiera i wyświetla stan kontenerów, podobny do następującego.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-428">Log Search opens and displays the state of your containers, similar to the following.</span></span>  
   ![Stan kontenerów](./media/log-analytics-containers/containers-log-search.png)
3. <span data-ttu-id="6d5cb-430">Następnie kliknij przycisk zagregowane wartości kontenery nie powiodło się, aby wyświetlić dodatkowe informacje.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-430">Next, click the aggregated value of failed containers to view additional information.</span></span> <span data-ttu-id="6d5cb-431">Rozwiń węzeł **Pokaż więcej** Aby wyświetlić identyfikator obrazu.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-431">Expand **show more** to view the image ID.</span></span>  
   <span data-ttu-id="6d5cb-432">![kontenery nie powiodło się](./media/log-analytics-containers/containers-state-failed.png)</span><span class="sxs-lookup"><span data-stu-id="6d5cb-432">![failed containers](./media/log-analytics-containers/containers-state-failed.png)</span></span>  
4. <span data-ttu-id="6d5cb-433">Następnie wpisz następujące polecenie w zapytaniu wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-433">Next, type the following in the search query.</span></span> <span data-ttu-id="6d5cb-434">`Type=ContainerInventory <ImageID>`Aby wyświetlić szczegóły dotyczące obrazu, takich jak rozmiar obrazu i Liczba obrazów zatrzymane, a nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-434">`Type=ContainerInventory <ImageID>` to see details about the image such as image size and number of stopped and failed images.</span></span>  
   <span data-ttu-id="6d5cb-435">![kontenery nie powiodło się](./media/log-analytics-containers/containers-failed04.png)</span><span class="sxs-lookup"><span data-stu-id="6d5cb-435">![failed containers](./media/log-analytics-containers/containers-failed04.png)</span></span>

## <a name="search-logs-for-container-data"></a><span data-ttu-id="6d5cb-436">Dzienniki wyszukiwania danych kontenera</span><span class="sxs-lookup"><span data-stu-id="6d5cb-436">Search logs for container data</span></span>
<span data-ttu-id="6d5cb-437">W przypadku Rozwiązywanie problemów z określonego błędu, ułatwia Zobacz, gdzie występuje w danym środowisku.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-437">When you're troubleshooting a specific error, it can help to see where it is occurring in your environment.</span></span> <span data-ttu-id="6d5cb-438">Następujące typy dziennika ułatwia tworzenie kwerend do zwracania informacji, które chcesz.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-438">The following log types will help you create queries to return the information you want.</span></span>


- <span data-ttu-id="6d5cb-439">**ContainerImageInventory** — Użyj tego typu, jeśli próbujesz można znaleźć informacje są zorganizowane według obrazu oraz wyświetlać informacje obrazu, takich jak obraz lub identyfikatory rozmiarów.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-439">**ContainerImageInventory** – Use this type when you're trying to find information organized by image and to view image information such as image IDs or sizes.</span></span>
- <span data-ttu-id="6d5cb-440">**ContainerInventory** — tego typu należy używać informacji o lokalizację kontenera, ich nazwy są i jakie obrazy są na nich uruchomione.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-440">**ContainerInventory** – Use this type when you want information about container location, what their names are, and what images they're running.</span></span>
- <span data-ttu-id="6d5cb-441">**ContainerLog** — Użyj tego typu można znaleźć informacje dziennika błędu i zapisów.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-441">**ContainerLog** – Use this type when you want to find specific error log information and entries.</span></span>
- <span data-ttu-id="6d5cb-442">**ContainerNodeInventory_CL** tego typu należy używać informacji o hoście/węzła gdzie są znajdującej się kontenerów.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-442">**ContainerNodeInventory_CL**  Use this type when you want the information about host/node where containers are residing.</span></span> <span data-ttu-id="6d5cb-443">Umożliwia Docker wersji, typ aranżacji magazynu i informacje o sieci.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-443">It provides you Docker version, orchestration type, storage, and network information.</span></span>
- <span data-ttu-id="6d5cb-444">**ContainerProcess_CL** użyć tego typu, aby szybko zapoznać się z procesem uruchomione w kontenerze.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-444">**ContainerProcess_CL** Use this type to quickly see the process running within the container.</span></span>
- <span data-ttu-id="6d5cb-445">**ContainerServiceLog** — Użyj tego typu, gdy użytkownik próbuje odnaleźć informacje dziennika inspekcji demona Docker jak uruchamianie, Zatrzymaj, usunąć lub poleceń ściągnięcia.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-445">**ContainerServiceLog** – Use this type when you're trying to find audit trail information for the Docker daemon, such as start, stop, delete, or pull commands.</span></span>
- <span data-ttu-id="6d5cb-446">**KubeEvents_CL** umożliwia wyświetlanie zdarzeń Kubernetes tego typu.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-446">**KubeEvents_CL**  Use this type to see the Kubernetes events.</span></span>
- <span data-ttu-id="6d5cb-447">**KubePodInventory_CL** użyć tego typu, jeśli chcesz poznać informacje o klastrze hierarchii.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-447">**KubePodInventory_CL**  Use this type when you want to understand the cluster hierarchy information.</span></span>


### <a name="to-search-logs-for-container-data"></a><span data-ttu-id="6d5cb-448">Do wyszukania w dziennikach dane w kontenerze</span><span class="sxs-lookup"><span data-stu-id="6d5cb-448">To search logs for container data</span></span>
* <span data-ttu-id="6d5cb-449">Wybierz obraz, który ostatnio nie powiodło się i znaleźć w dziennikach błędów.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-449">Choose an image that you know has failed recently and find the error logs for it.</span></span> <span data-ttu-id="6d5cb-450">Uruchom znajdując nazwę kontenera, która działa obrazu z **ContainerInventory** wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-450">Start by finding a container name that is running that image with a **ContainerInventory** search.</span></span> <span data-ttu-id="6d5cb-451">Na przykład wyszukaj`Type=ContainerInventory ubuntu Failed`</span><span class="sxs-lookup"><span data-stu-id="6d5cb-451">For example, search for `Type=ContainerInventory ubuntu Failed`</span></span>  
    <span data-ttu-id="6d5cb-452">![Wyszukaj kontenery Ubuntu](./media/log-analytics-containers/search-ubuntu.png)</span><span class="sxs-lookup"><span data-stu-id="6d5cb-452">![Search for Ubuntu containers](./media/log-analytics-containers/search-ubuntu.png)</span></span>

  <span data-ttu-id="6d5cb-453">Nazwa kontenera dalej, aby **nazwa**i poszukaj tych dzienników.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-453">The name of the container next to **Name**, and search for those logs.</span></span> <span data-ttu-id="6d5cb-454">W tym przykładzie jest to `Type=ContainerLog cranky_stonebreaker`.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-454">In this example, it is `Type=ContainerLog cranky_stonebreaker`.</span></span>

<span data-ttu-id="6d5cb-455">**Wyświetlanie informacji o wydajności**</span><span class="sxs-lookup"><span data-stu-id="6d5cb-455">**View performance information**</span></span>

<span data-ttu-id="6d5cb-456">W przypadku od tworzyć zapytania, ułatwia Zobacz, co jest możliwe najpierw.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-456">When you're beginning to construct queries, it can help to see what's possible first.</span></span> <span data-ttu-id="6d5cb-457">Na przykład aby wyświetlić wszystkie dane dotyczące wydajności, spróbuj szerokie zapytania, wpisując następujące zapytanie wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-457">For example, to see all performance data, try a broad query by typing the following search query.</span></span>

```
Type=Perf
```

![kontenery wydajności](./media/log-analytics-containers/containers-perf01.png)

<span data-ttu-id="6d5cb-459">Można określić zakres dane wydajności, które widać do określonego kontenera przez wpisanie nazwy tego zapytania z prawej strony.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-459">You can scope the performance data you're seeing to a specific container by typing the name of it to the right of your query.</span></span>

```
Type=Perf <containerName>
```

<span data-ttu-id="6d5cb-460">Które z listą metryki wydajności, które są zbierane dla poszczególnych kontenera.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-460">That shows the list of performance metrics that are collected for an individual container.</span></span>

![kontenery wydajności](./media/log-analytics-containers/containers-perf03.png)

## <a name="example-log-search-queries"></a><span data-ttu-id="6d5cb-462">Przykładowe zapytania wyszukiwania dziennika</span><span class="sxs-lookup"><span data-stu-id="6d5cb-462">Example log search queries</span></span>
<span data-ttu-id="6d5cb-463">Często jest przydatne do tworzenia zapytań w programie przykład lub dwóch, a następnie modyfikując je do środowiska.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-463">It's often useful to build queries starting with an example or two and then modifying them to fit your environment.</span></span> <span data-ttu-id="6d5cb-464">Jako punkt początkowy, możesz eksperymentować z **przykładowe zapytania** obszaru do tworzenia bardziej zaawansowanych zapytań.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-464">As a starting point, you can experiment with the **Sample Queries** area to help you build more advanced queries.</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Kontenery zapytań](./media/log-analytics-containers/containers-queries.png)


## <a name="saving-log-search-queries"></a><span data-ttu-id="6d5cb-466">Zapisywanie dziennika zapytania wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="6d5cb-466">Saving log search queries</span></span>
<span data-ttu-id="6d5cb-467">Zapisywanie zapytań jest standardowa funkcja Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-467">Saving queries is a standard feature in Log Analytics.</span></span> <span data-ttu-id="6d5cb-468">Zapisując je, należy te, które zostały znalezione przydatne przydatne do użytku w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-468">By saving them, you'll have those that you've found useful handy for future use.</span></span>

<span data-ttu-id="6d5cb-469">Po utworzeniu kwerendę, która jest użyteczna, zapisz go, klikając **ulubione** w górnej części strony wyszukiwania dziennika.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-469">After you create a query that you find useful, save it by clicking **Favorites** at the top of the Log Search page.</span></span> <span data-ttu-id="6d5cb-470">Następnie możesz z łatwością później z **Mój pulpit nawigacyjny** strony.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-470">Then you can easily access it later from the **My Dashboard** page.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d5cb-471">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6d5cb-471">Next steps</span></span>
* <span data-ttu-id="6d5cb-472">[Wyszukaj dzienniki](log-analytics-log-searches.md) Aby wyświetlić szczegółowe kontenera rekordów danych.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-472">[Search logs](log-analytics-log-searches.md) to view detailed container data records.</span></span>
