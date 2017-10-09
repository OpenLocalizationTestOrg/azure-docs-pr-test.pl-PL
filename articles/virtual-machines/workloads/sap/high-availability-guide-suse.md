---
title: "Maszyny wirtualne wysokiej dostępności dla programu SAP NetWeaver w systemie SUSE Linux Enterprise Server dla aplikacji SAP aaaAzure | Dokumentacja firmy Microsoft"
description: "Przewodnik wysokiej dostępności dla programu SAP NetWeaver w systemie SUSE Linux Enterprise Server dla programu SAP aplikacji"
services: virtual-machines-windows,virtual-network,storage
documentationcenter: saponazure
author: mssedusch
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 5e514964-c907-4324-b659-16dd825f6f87
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 04/27/2017
ms.author: sedusch
ms.openlocfilehash: e944103df92d5ffec9196189f138e25972bea79f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-for-sap-netweaver-on-azure-vms-on-suse-linux-enterprise-server-for-sap-applications"></a><span data-ttu-id="0749e-103">Wysoka dostępność dla programu SAP NetWeaver na maszynach wirtualnych Azure w systemie SUSE Linux Enterprise Server dla programu SAP aplikacji</span><span class="sxs-lookup"><span data-stu-id="0749e-103">High availability for SAP NetWeaver on Azure VMs on SUSE Linux Enterprise Server for SAP applications</span></span>

[dbms-guide]:dbms-guide.md
[deployment-guide]:deployment-guide.md
[planning-guide]:planning-guide.md

[2205917]:https://launchpad.support.sap.com/#/notes/2205917
[1944799]:https://launchpad.support.sap.com/#/notes/1944799
[1928533]:https://launchpad.support.sap.com/#/notes/1928533
[2015553]:https://launchpad.support.sap.com/#/notes/2015553
[2178632]:https://launchpad.support.sap.com/#/notes/2178632
[2191498]:https://launchpad.support.sap.com/#/notes/2191498
[2243692]:https://launchpad.support.sap.com/#/notes/2243692
[1984787]:https://launchpad.support.sap.com/#/notes/1984787
[1999351]:https://launchpad.support.sap.com/#/notes/1999351
[1410736]:https://launchpad.support.sap.com/#/notes/1410736

[sap-swcenter]:https://support.sap.com/en/my-support/software-downloads.html

[suse-hana-ha-guide]:https://www.suse.com/docrep/documents/ir8w88iwu7/suse_linux_enterprise_server_for_sap_applications_12_sp1.pdf
[suse-drbd-guide]:https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha_techguides/book_sleha_techguides.html

[template-multisid-xscs]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs-md%2Fazuredeploy.json
[template-converged]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-converged-md%2Fazuredeploy.json
[template-file-server]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-file-server-md%2Fazuredeploy.json

[sap-hana-ha]:sap-hana-high-availability.md

<span data-ttu-id="0749e-113">W tym artykule opisano, jak toodeploy hello maszyn wirtualnych, konfigurowanie maszyn wirtualnych hello, zainstaluj program hello framework klastra i zainstalować wysokiej dostępności systemu SAP NetWeaver 7.50.</span><span class="sxs-lookup"><span data-stu-id="0749e-113">This article describes how toodeploy hello virtual machines, configure hello virtual machines, install hello cluster framework and install a highly available SAP NetWeaver 7.50 system.</span></span>
<span data-ttu-id="0749e-114">W hello przykładowe konfiguracje polecenia instalacji itp. Liczby wystąpień ASCS 00, liczby wystąpień Wywołujących 02 i NWS identyfikator systemu SAP jest używany.</span><span class="sxs-lookup"><span data-stu-id="0749e-114">In hello example configurations, installation commands etc. ASCS instance number 00, ERS instance number 02 and SAP System ID NWS is used.</span></span> <span data-ttu-id="0749e-115">Hello nazw hello zasobów (na przykład maszyn wirtualnych, sieci wirtualne) w przykładzie hello założono użycie hello [zbieżność szablonu] [ template-converged] SAP systemu identyfikator NWS toocreate hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="0749e-115">hello names of hello resources (for example virtual machines, virtual networks) in hello example assume that you have used hello [converged template][template-converged] with SAP system ID NWS toocreate hello resources.</span></span>

<span data-ttu-id="0749e-116">Przeczytaj hello najpierw następujące uwagi SAP i dokumentów</span><span class="sxs-lookup"><span data-stu-id="0749e-116">Read hello following SAP Notes and papers first</span></span>

* <span data-ttu-id="0749e-117">Uwaga SAP [1928533], który zawiera:</span><span class="sxs-lookup"><span data-stu-id="0749e-117">SAP Note [1928533], which has:</span></span>
  * <span data-ttu-id="0749e-118">Lista rozmiarów maszyny Wirtualnej platformy Azure, które są obsługiwane dla hello wdrożenia oprogramowania SAP</span><span class="sxs-lookup"><span data-stu-id="0749e-118">List of Azure VM sizes that are supported for hello deployment of SAP software</span></span>
  * <span data-ttu-id="0749e-119">Informacje o rozmiary maszyn wirtualnych Azure ważne pojemności</span><span class="sxs-lookup"><span data-stu-id="0749e-119">Important capacity information for Azure VM sizes</span></span>
  * <span data-ttu-id="0749e-120">Obsługiwane oprogramowanie SAP i kombinacji bazy danych i systemu operacyjnego (OS)</span><span class="sxs-lookup"><span data-stu-id="0749e-120">Supported SAP software, and operating system (OS) and database combinations</span></span>
  * <span data-ttu-id="0749e-121">Wymagana wersja jądra SAP dla systemu Windows i Linux w systemie Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="0749e-121">Required SAP kernel version for Windows and Linux on Microsoft Azure</span></span>

* <span data-ttu-id="0749e-122">Uwaga SAP [2015553] wymieniono wymagania wstępne dotyczące wdrażania oprogramowania SAP SAP, obsługiwane na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="0749e-122">SAP Note [2015553] lists prerequisites for SAP-supported SAP software deployments in Azure.</span></span>
* <span data-ttu-id="0749e-123">Uwaga SAP [2205917] zawiera zalecane ustawienia systemu operacyjnego SUSE Linux Enterprise Server dla programu SAP aplikacji</span><span class="sxs-lookup"><span data-stu-id="0749e-123">SAP Note [2205917] has recommended OS settings for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="0749e-124">Uwaga SAP [1944799] ma SAP HANA wytyczne dla SUSE Linux Enterprise Server dla programu SAP aplikacji</span><span class="sxs-lookup"><span data-stu-id="0749e-124">SAP Note [1944799] has SAP HANA Guidelines for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="0749e-125">Uwaga SAP [2178632] zawiera szczegółowe informacje na temat wszystkie funkcje monitorowania metryki zgłoszone dla SAP na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="0749e-125">SAP Note [2178632] has detailed information about all monitoring metrics reported for SAP in Azure.</span></span>
* <span data-ttu-id="0749e-126">Uwaga SAP [2191498] hello wymaga wersji agenta hosta SAP dla systemu Linux na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="0749e-126">SAP Note [2191498] has hello required SAP Host Agent version for Linux in Azure.</span></span>
* <span data-ttu-id="0749e-127">Uwaga SAP [2243692] zawiera informacje o licencjonowaniu SAP w systemie Linux na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="0749e-127">SAP Note [2243692] has information about SAP licensing on Linux in Azure.</span></span>
* <span data-ttu-id="0749e-128">Uwaga SAP [1984787] zawiera ogólne informacje o systemie SUSE Linux Enterprise Server 12.</span><span class="sxs-lookup"><span data-stu-id="0749e-128">SAP Note [1984787] has general information about SUSE Linux Enterprise Server 12.</span></span>
* <span data-ttu-id="0749e-129">Uwaga SAP [1999351] zawiera dodatkowe informacje dotyczące rozwiązywania problemów hello Azure ulepszone rozszerzenie monitorowania dla programu SAP.</span><span class="sxs-lookup"><span data-stu-id="0749e-129">SAP Note [1999351] has additional troubleshooting information for hello Azure Enhanced Monitoring Extension for SAP.</span></span>
* <span data-ttu-id="0749e-130">[SAP społeczności WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) ma wszystkie wymagane informacje SAP dla systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="0749e-130">[SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) has all required SAP Notes for Linux.</span></span>
* <span data-ttu-id="0749e-131">[Azure maszyn wirtualnych, planowania i wdrażania dla SAP w systemie Linux][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="0749e-131">[Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide]</span></span>
* <span data-ttu-id="0749e-132">[Maszyny wirtualne Azure wdrożenie SAP w systemie Linux (w tym artykule)][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="0749e-132">[Azure Virtual Machines deployment for SAP on Linux (this article)][deployment-guide]</span></span>
* <span data-ttu-id="0749e-133">[Azure maszyn wirtualnych systemu DBMS wdrożenie SAP w systemie Linux][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="0749e-133">[Azure Virtual Machines DBMS deployment for SAP on Linux][dbms-guide]</span></span>
* <span data-ttu-id="0749e-134">[SAP HANA SR zoptymalizowana scenariusza][suse-hana-ha-guide]</span><span class="sxs-lookup"><span data-stu-id="0749e-134">[SAP HANA SR Performance Optimized Scenario][suse-hana-ha-guide]</span></span>  
  <span data-ttu-id="0749e-135">Przewodnik Hello zawiera wszystkie wymagane informacje tooset zapasowych replikacji systemu SAP HANA lokalnie.</span><span class="sxs-lookup"><span data-stu-id="0749e-135">hello guide contains all required information tooset up SAP HANA System Replication on-premises.</span></span> <span data-ttu-id="0749e-136">Użyj tego podręcznika, jako linii bazowej.</span><span class="sxs-lookup"><span data-stu-id="0749e-136">Use this guide as a baseline.</span></span>
* <span data-ttu-id="0749e-137">[Wysoce dostępny magazyn systemu plików NFS z DRBD i rozrusznik] [ suse-drbd-guide] hello przewodnik zawiera wszystkie wymagane informacje tooset wysokiej dostępności serwera systemu plików NFS.</span><span class="sxs-lookup"><span data-stu-id="0749e-137">[Highly Available NFS Storage with DRBD and Pacemaker][suse-drbd-guide] hello guide contains all required information tooset up a highly available NFS server.</span></span> <span data-ttu-id="0749e-138">Użyj tego podręcznika, jako linii bazowej.</span><span class="sxs-lookup"><span data-stu-id="0749e-138">Use this guide as a baseline.</span></span>


## <a name="overview"></a><span data-ttu-id="0749e-139">Omówienie</span><span class="sxs-lookup"><span data-stu-id="0749e-139">Overview</span></span>

<span data-ttu-id="0749e-140">tooachieve wysokiej dostępności, SAP NetWeaver wymaga, aby serwer systemu plików NFS.</span><span class="sxs-lookup"><span data-stu-id="0749e-140">tooachieve high availability, SAP NetWeaver requires an NFS server.</span></span> <span data-ttu-id="0749e-141">Serwer systemu plików NFS Hello jest skonfigurowany w osobnym klastrze i mogą być używane przez wiele systemów SAP.</span><span class="sxs-lookup"><span data-stu-id="0749e-141">hello NFS server is configured in a separate cluster and can be used by multiple SAP systems.</span></span>

![Informacje o SAP NetWeaver wysokiej dostępności](./media/high-availability-guide-suse/img_001.png)

<span data-ttu-id="0749e-143">powitania serwera NFS, SAP NetWeaver ASCS, SAP NetWeaver SCS SAP NetWeaver Wywołujących i bazy danych SAP HANA hello używać nazwy hosta wirtualnego i wirtualnych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="0749e-143">hello NFS server, SAP NetWeaver ASCS, SAP NetWeaver SCS, SAP NetWeaver ERS and hello SAP HANA database use virtual hostname and virtual IP addresses.</span></span> <span data-ttu-id="0749e-144">Na platformie Azure usługi równoważenia obciążenia jest wymagany toouse wirtualnego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="0749e-144">On Azure, a load balancer is required toouse a virtual IP address.</span></span> <span data-ttu-id="0749e-145">Witaj Poniższa lista zawiera hello konfiguracji usługi równoważenia obciążenia hello.</span><span class="sxs-lookup"><span data-stu-id="0749e-145">hello following list shows hello configuration of hello load balancer.</span></span>

### <a name="nfs-server"></a><span data-ttu-id="0749e-146">Serwer systemu plików NFS</span><span class="sxs-lookup"><span data-stu-id="0749e-146">NFS Server</span></span>
* <span data-ttu-id="0749e-147">Konfiguracja serwera sieci Web</span><span class="sxs-lookup"><span data-stu-id="0749e-147">Frontend configuration</span></span>
  * <span data-ttu-id="0749e-148">Adres IP 10.0.0.4</span><span class="sxs-lookup"><span data-stu-id="0749e-148">IP address 10.0.0.4</span></span>
* <span data-ttu-id="0749e-149">Konfiguracja zaplecza</span><span class="sxs-lookup"><span data-stu-id="0749e-149">Backend configuration</span></span>
  * <span data-ttu-id="0749e-150">Połączone tooprimary interfejsy sieciowe wszystkich maszyn wirtualnych, które powinny być częścią klastra systemu plików NFS hello</span><span class="sxs-lookup"><span data-stu-id="0749e-150">Connected tooprimary network interfaces of all virtual machines that should be part of hello NFS cluster</span></span>
* <span data-ttu-id="0749e-151">Port sondy</span><span class="sxs-lookup"><span data-stu-id="0749e-151">Probe Port</span></span>
  * <span data-ttu-id="0749e-152">Port 61000</span><span class="sxs-lookup"><span data-stu-id="0749e-152">Port 61000</span></span>
* <span data-ttu-id="0749e-153">Reguły obciążenia</span><span class="sxs-lookup"><span data-stu-id="0749e-153">Loadbalancing rules</span></span>
  * <span data-ttu-id="0749e-154">2049 TCP</span><span class="sxs-lookup"><span data-stu-id="0749e-154">2049 TCP</span></span> 
  * <span data-ttu-id="0749e-155">2049 UDP</span><span class="sxs-lookup"><span data-stu-id="0749e-155">2049 UDP</span></span>

### <a name="ascs"></a><span data-ttu-id="0749e-156">(A) SCS</span><span class="sxs-lookup"><span data-stu-id="0749e-156">(A)SCS</span></span>
* <span data-ttu-id="0749e-157">Konfiguracja serwera sieci Web</span><span class="sxs-lookup"><span data-stu-id="0749e-157">Frontend configuration</span></span>
  * <span data-ttu-id="0749e-158">Adres IP 10.0.0.10</span><span class="sxs-lookup"><span data-stu-id="0749e-158">IP address 10.0.0.10</span></span>
* <span data-ttu-id="0749e-159">Konfiguracja zaplecza</span><span class="sxs-lookup"><span data-stu-id="0749e-159">Backend configuration</span></span>
  * <span data-ttu-id="0749e-160">Interfejsów sieciowych podłączonych tooprimary wszystkich maszyn wirtualnych, które powinny być częścią klastra SCS/Wywołujących hello (A)</span><span class="sxs-lookup"><span data-stu-id="0749e-160">Connected tooprimary network interfaces of all virtual machines that should be part of hello (A)SCS/ERS cluster</span></span>
* <span data-ttu-id="0749e-161">Port sondy</span><span class="sxs-lookup"><span data-stu-id="0749e-161">Probe Port</span></span>
  * <span data-ttu-id="0749e-162">Port 620**&lt;nr&gt;**</span><span class="sxs-lookup"><span data-stu-id="0749e-162">Port 620**&lt;nr&gt;**</span></span>
* <span data-ttu-id="0749e-163">Reguły obciążenia</span><span class="sxs-lookup"><span data-stu-id="0749e-163">Loadbalancing rules</span></span>
  * <span data-ttu-id="0749e-164">32**&lt;nr&gt;**  TCP</span><span class="sxs-lookup"><span data-stu-id="0749e-164">32**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="0749e-165">36**&lt;nr&gt;**  TCP</span><span class="sxs-lookup"><span data-stu-id="0749e-165">36**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="0749e-166">39**&lt;nr&gt;**  TCP</span><span class="sxs-lookup"><span data-stu-id="0749e-166">39**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="0749e-167">81**&lt;nr&gt;**  TCP</span><span class="sxs-lookup"><span data-stu-id="0749e-167">81**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="0749e-168">5**&lt;nr&gt;**13 TCP</span><span class="sxs-lookup"><span data-stu-id="0749e-168">5**&lt;nr&gt;**13 TCP</span></span>
  * <span data-ttu-id="0749e-169">5**&lt;nr&gt;**14 TCP</span><span class="sxs-lookup"><span data-stu-id="0749e-169">5**&lt;nr&gt;**14 TCP</span></span>
  * <span data-ttu-id="0749e-170">5**&lt;nr&gt;**16 TCP</span><span class="sxs-lookup"><span data-stu-id="0749e-170">5**&lt;nr&gt;**16 TCP</span></span>

### <a name="ers"></a><span data-ttu-id="0749e-171">WYWOŁUJĄCYCH</span><span class="sxs-lookup"><span data-stu-id="0749e-171">ERS</span></span>
* <span data-ttu-id="0749e-172">Konfiguracja serwera sieci Web</span><span class="sxs-lookup"><span data-stu-id="0749e-172">Frontend configuration</span></span>
  * <span data-ttu-id="0749e-173">Adres IP 10.0.0.11</span><span class="sxs-lookup"><span data-stu-id="0749e-173">IP address 10.0.0.11</span></span>
* <span data-ttu-id="0749e-174">Konfiguracja zaplecza</span><span class="sxs-lookup"><span data-stu-id="0749e-174">Backend configuration</span></span>
  * <span data-ttu-id="0749e-175">Interfejsów sieciowych podłączonych tooprimary wszystkich maszyn wirtualnych, które powinny być częścią klastra SCS/Wywołujących hello (A)</span><span class="sxs-lookup"><span data-stu-id="0749e-175">Connected tooprimary network interfaces of all virtual machines that should be part of hello (A)SCS/ERS cluster</span></span>
* <span data-ttu-id="0749e-176">Port sondy</span><span class="sxs-lookup"><span data-stu-id="0749e-176">Probe Port</span></span>
  * <span data-ttu-id="0749e-177">Port 621**&lt;nr&gt;**</span><span class="sxs-lookup"><span data-stu-id="0749e-177">Port 621**&lt;nr&gt;**</span></span>
* <span data-ttu-id="0749e-178">Reguły obciążenia</span><span class="sxs-lookup"><span data-stu-id="0749e-178">Loadbalancing rules</span></span>
  * <span data-ttu-id="0749e-179">33**&lt;nr&gt;**  TCP</span><span class="sxs-lookup"><span data-stu-id="0749e-179">33**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="0749e-180">5**&lt;nr&gt;**13 TCP</span><span class="sxs-lookup"><span data-stu-id="0749e-180">5**&lt;nr&gt;**13 TCP</span></span>
  * <span data-ttu-id="0749e-181">5**&lt;nr&gt;**14 TCP</span><span class="sxs-lookup"><span data-stu-id="0749e-181">5**&lt;nr&gt;**14 TCP</span></span>
  * <span data-ttu-id="0749e-182">5**&lt;nr&gt;**16 TCP</span><span class="sxs-lookup"><span data-stu-id="0749e-182">5**&lt;nr&gt;**16 TCP</span></span>

### <a name="sap-hana"></a><span data-ttu-id="0749e-183">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="0749e-183">SAP HANA</span></span>
* <span data-ttu-id="0749e-184">Konfiguracja serwera sieci Web</span><span class="sxs-lookup"><span data-stu-id="0749e-184">Frontend configuration</span></span>
  * <span data-ttu-id="0749e-185">Adres IP 10.0.0.12</span><span class="sxs-lookup"><span data-stu-id="0749e-185">IP address 10.0.0.12</span></span>
* <span data-ttu-id="0749e-186">Konfiguracja zaplecza</span><span class="sxs-lookup"><span data-stu-id="0749e-186">Backend configuration</span></span>
  * <span data-ttu-id="0749e-187">Połączone tooprimary interfejsy sieciowe wszystkich maszyn wirtualnych, które powinny być częścią hello HANA klastra</span><span class="sxs-lookup"><span data-stu-id="0749e-187">Connected tooprimary network interfaces of all virtual machines that should be part of hello HANA cluster</span></span>
* <span data-ttu-id="0749e-188">Port sondy</span><span class="sxs-lookup"><span data-stu-id="0749e-188">Probe Port</span></span>
  * <span data-ttu-id="0749e-189">Port 625**&lt;nr&gt;**</span><span class="sxs-lookup"><span data-stu-id="0749e-189">Port 625**&lt;nr&gt;**</span></span>
* <span data-ttu-id="0749e-190">Reguły obciążenia</span><span class="sxs-lookup"><span data-stu-id="0749e-190">Loadbalancing rules</span></span>
  * <span data-ttu-id="0749e-191">3**&lt;nr&gt;**15 TCP</span><span class="sxs-lookup"><span data-stu-id="0749e-191">3**&lt;nr&gt;**15 TCP</span></span>
  * <span data-ttu-id="0749e-192">3**&lt;nr&gt;**17 TCP</span><span class="sxs-lookup"><span data-stu-id="0749e-192">3**&lt;nr&gt;**17 TCP</span></span>

## <a name="setting-up-a-highly-available-nfs-server"></a><span data-ttu-id="0749e-193">Konfigurowanie serwera systemu plików NFS o wysokiej dostępności</span><span class="sxs-lookup"><span data-stu-id="0749e-193">Setting up a highly available NFS server</span></span>

### <a name="deploying-linux"></a><span data-ttu-id="0749e-194">Wdrażanie systemu Linux</span><span class="sxs-lookup"><span data-stu-id="0749e-194">Deploying Linux</span></span>

<span data-ttu-id="0749e-195">Hello Azure Marketplace zawiera obraz systemu SUSE Linux Enterprise Server dla 12 aplikacje SAP służy toodeploy nowych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="0749e-195">hello Azure Marketplace contains an image for SUSE Linux Enterprise Server for SAP Applications 12 that you can use toodeploy new virtual machines.</span></span>
<span data-ttu-id="0749e-196">Możesz użyć jednego z szablonów szybki start hello w github toodeploy wszystkich wymaganych zasobów.</span><span class="sxs-lookup"><span data-stu-id="0749e-196">You can use one of hello quick start templates on github toodeploy all required resources.</span></span> <span data-ttu-id="0749e-197">Szablon Hello wdraża hello maszyn wirtualnych, usługi równoważenia obciążenia hello, itp zestawu dostępności. Wykonaj te kroki toodeploy hello szablonu:</span><span class="sxs-lookup"><span data-stu-id="0749e-197">hello template deploys hello virtual machines, hello load balancer, availability set etc. Follow these steps toodeploy hello template:</span></span>

1. <span data-ttu-id="0749e-198">Otwórz hello [szablon serwera SAP pliku] [ template-file-server] w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="0749e-198">Open hello [SAP file server template][template-file-server] in hello Azure portal</span></span>   
1. <span data-ttu-id="0749e-199">Wprowadź następujące parametry hello</span><span class="sxs-lookup"><span data-stu-id="0749e-199">Enter hello following parameters</span></span>
   1. <span data-ttu-id="0749e-200">Prefiks zasobów</span><span class="sxs-lookup"><span data-stu-id="0749e-200">Resource Prefix</span></span>  
      <span data-ttu-id="0749e-201">Wprowadź prefiks hello ma toouse.</span><span class="sxs-lookup"><span data-stu-id="0749e-201">Enter hello prefix you want toouse.</span></span> <span data-ttu-id="0749e-202">wartość Hello jest używany jako prefiksu hello zasobów, które zostały wdrożone.</span><span class="sxs-lookup"><span data-stu-id="0749e-202">hello value is used as a prefix for hello resources that are deployed.</span></span>
   2. <span data-ttu-id="0749e-203">Typ systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="0749e-203">Os Type</span></span>  
      <span data-ttu-id="0749e-204">Wybierz jedną z hello dystrybucje systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="0749e-204">Select one of hello Linux distributions.</span></span> <span data-ttu-id="0749e-205">Na przykład wybierz SLES 12.</span><span class="sxs-lookup"><span data-stu-id="0749e-205">For this example, select SLES 12</span></span>
   3. <span data-ttu-id="0749e-206">Nazwa użytkownika i hasło administratora</span><span class="sxs-lookup"><span data-stu-id="0749e-206">Admin Username and Admin Password</span></span>  
      <span data-ttu-id="0749e-207">Tworzony jest nowy użytkownik, który może być używane toolog toohello maszyny.</span><span class="sxs-lookup"><span data-stu-id="0749e-207">A new user is created that can be used toolog on toohello machine.</span></span>
   4. <span data-ttu-id="0749e-208">Identyfikator podsieci</span><span class="sxs-lookup"><span data-stu-id="0749e-208">Subnet Id</span></span>  
      <span data-ttu-id="0749e-209">Identyfikator Hello maszyn wirtualnych hello hello podsieci toowhich powinny być podłączone do.</span><span class="sxs-lookup"><span data-stu-id="0749e-209">hello ID of hello subnet toowhich hello virtual machines should be connected to.</span></span> <span data-ttu-id="0749e-210">Jeśli toocreate nową sieć wirtualną lub wybierz podsieć hello VPN Express Route sieci wirtualnej tooconnect hello maszyny wirtualnej tooyour lokalnej sieci lub pozostać puste.</span><span class="sxs-lookup"><span data-stu-id="0749e-210">Leave empty if you want toocreate a new virtual network or select hello subnet of your VPN or Express Route virtual network tooconnect hello virtual machine tooyour on-premises network.</span></span> <span data-ttu-id="0749e-211">Identyfikator Hello zwykle wygląda /subscriptions/**&lt;identyfikator subskrypcji&gt;**/resourceGroups/**&lt;Nazwa grupy zasobów&gt;**/providers/ Microsoft.Network/virtualNetworks/**&lt;wirtualnej nazwy sieciowej&gt;**/subnets/**&lt;nazwy podsieci&gt;**</span><span class="sxs-lookup"><span data-stu-id="0749e-211">hello ID usually looks like /subscriptions/**&lt;subscription id&gt;**/resourceGroups/**&lt;resource group name&gt;**/providers/Microsoft.Network/virtualNetworks/**&lt;virtual network name&gt;**/subnets/**&lt;subnet name&gt;**</span></span>

### <a name="installation"></a><span data-ttu-id="0749e-212">Instalacja</span><span class="sxs-lookup"><span data-stu-id="0749e-212">Installation</span></span>

<span data-ttu-id="0749e-213">Hello następujące elementy są poprzedzane prefiksem albo **[A]** -węzłów dotyczy tooall **[1]** -tylko odpowiednie toonode 1 lub **[2]** -tylko odpowiednie toonode 2.</span><span class="sxs-lookup"><span data-stu-id="0749e-213">hello following items are prefixed with either **[A]** - applicable tooall nodes, **[1]** - only applicable toonode 1 or **[2]** - only applicable toonode 2.</span></span>

1. <span data-ttu-id="0749e-214">**[A]**  Zaktualizować SLES</span><span class="sxs-lookup"><span data-stu-id="0749e-214">**[A]** Update SLES</span></span>

   <pre><code>
   sudo zypper update
   </code></pre>

1. <span data-ttu-id="0749e-215">**[1]**  Dostęp ssh</span><span class="sxs-lookup"><span data-stu-id="0749e-215">**[1]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

2. <span data-ttu-id="0749e-216">**[2]**  Dostęp ssh</span><span class="sxs-lookup"><span data-stu-id="0749e-216">**[2]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa

   # insert hello public key you copied in hello last step into hello authorized keys file on hello second server
   sudo vi /root/.ssh/authorized_keys
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key   
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

1. <span data-ttu-id="0749e-217">**[1]**  Dostęp ssh</span><span class="sxs-lookup"><span data-stu-id="0749e-217">**[1]** Enable ssh access</span></span>

   <pre><code>
   # insert hello public key you copied in hello last step into hello authorized keys file on hello first server
   sudo vi /root/.ssh/authorized_keys
   </code></pre>

1. <span data-ttu-id="0749e-218">**[A]**  Zainstalować HA rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="0749e-218">**[A]** Install HA extension</span></span>
   
   <pre><code>
   sudo zypper install sle-ha-release fence-agents
   </code></pre>

1. <span data-ttu-id="0749e-219">**[A]**  Instalatora rozpoznawania nazwy hosta</span><span class="sxs-lookup"><span data-stu-id="0749e-219">**[A]** Setup host name resolution</span></span>   

   <span data-ttu-id="0749e-220">Można użyć serwera DNS lub zmodyfikować hello/etc/hosts na wszystkich węzłach.</span><span class="sxs-lookup"><span data-stu-id="0749e-220">You can either use a DNS server or modify hello /etc/hosts on all nodes.</span></span> <span data-ttu-id="0749e-221">Ten przykład przedstawia, jak toouse hello plik/etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="0749e-221">This example shows how toouse hello /etc/hosts file.</span></span>
   <span data-ttu-id="0749e-222">Zastąpienie hello adresu IP i nazwy hosta hello w hello następujące polecenia</span><span class="sxs-lookup"><span data-stu-id="0749e-222">Replace hello IP address and hello hostname in hello following commands</span></span>

   <pre><code>
   sudo vi /etc/hosts
   </code></pre>
   
   <span data-ttu-id="0749e-223">Wstaw hello następujące wiersze zbyt/etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="0749e-223">Insert hello following lines too/etc/hosts.</span></span> <span data-ttu-id="0749e-224">Zmień toomatch adres i nazwę hosta IP hello środowiska</span><span class="sxs-lookup"><span data-stu-id="0749e-224">Change hello IP address and hostname toomatch your environment</span></span>   
   
   <pre><code>
   # IP address of hello load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   </code></pre>

1. <span data-ttu-id="0749e-225">**[1]**  Instalacji klastra</span><span class="sxs-lookup"><span data-stu-id="0749e-225">**[1]** Install Cluster</span></span>
   
   <pre><code>
   sudo ha-cluster-init
   
   # Do you want toocontinue anyway? [y/N] -> y
   # Network address toobind too(for example: 192.168.1.0) [10.79.227.0] -> ENTER
   # Multicast address (for example: 239.x.x.x) [239.174.218.125] -> ENTER
   # Multicast port [5405] -> ENTER
   # Do you wish toouse SBD? [y/N] -> N
   # Do you wish tooconfigure an administration IP? [y/N] -> N
   </code></pre>

1. <span data-ttu-id="0749e-226">**[2]**  Dodaj toocluster węzła</span><span class="sxs-lookup"><span data-stu-id="0749e-226">**[2]** Add node toocluster</span></span>
   
   <pre><code> 
   sudo ha-cluster-join

   # WARNING: NTP is not configured toostart at system boot.
   # WARNING: No watchdog device found. If SBD is used, hello cluster will be unable toostart without a watchdog.
   # Do you want toocontinue anyway? [y/N] -> y
   # IP address or hostname of existing node (for example: 192.168.1.1) [] -> IP address of node 1 for example 10.0.0.10
   # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
   </code></pre>

1. <span data-ttu-id="0749e-227">**[A]**  Toohello hasło hacluster zmiany tego samego hasła</span><span class="sxs-lookup"><span data-stu-id="0749e-227">**[A]** Change hacluster password toohello same password</span></span>

   <pre><code> 
   sudo passwd hacluster
   </code></pre>

1. <span data-ttu-id="0749e-228">**[A]**  Skonfigurować corosync toouse innych transportu i Dodaj wstawienia.</span><span class="sxs-lookup"><span data-stu-id="0749e-228">**[A]** Configure corosync toouse other transport and add nodelist.</span></span> <span data-ttu-id="0749e-229">Klaster nie będą działać inaczej.</span><span class="sxs-lookup"><span data-stu-id="0749e-229">Cluster will not work otherwise.</span></span>
   
   <pre><code> 
   sudo vi /etc/corosync/corosync.conf   
   </code></pre>

   <span data-ttu-id="0749e-230">Dodaj powitania po bold toohello zawartości pliku.</span><span class="sxs-lookup"><span data-stu-id="0749e-230">Add hello following bold content toohello file.</span></span>
   
   <pre><code> 
   [...]
     interface { 
        [...] 
     }
     <b>transport:      udpu</b>
   } 
   <b>nodelist {
     node {
      # IP address of <b>prod-nfs-0</b>
      ring0_addr:10.0.0.5
     }
     node {
      # IP address of <b>prod-nfs-1</b>
      ring0_addr:10.0.0.6
     } 
   }</b>
   logging {
     [...]
   </code></pre>

   <span data-ttu-id="0749e-231">Następnie uruchom ponownie usługę corosync hello</span><span class="sxs-lookup"><span data-stu-id="0749e-231">Then restart hello corosync service</span></span>

   <pre><code>
   sudo service corosync restart
   </code></pre>

1. <span data-ttu-id="0749e-232">**[A]**  Zainstalować składniki drbd</span><span class="sxs-lookup"><span data-stu-id="0749e-232">**[A]** Install drbd components</span></span>

   <pre><code>
   sudo zypper install drbd drbd-kmp-default drbd-utils
   </code></pre>

1. <span data-ttu-id="0749e-233">**[A]**  Utworzyć partycję hello drbd urządzenia</span><span class="sxs-lookup"><span data-stu-id="0749e-233">**[A]** Create a partition for hello drbd device</span></span>

   <pre><code>
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdc'
   </code></pre>

1. <span data-ttu-id="0749e-234">**[A]**  LVM Tworzenie konfiguracji</span><span class="sxs-lookup"><span data-stu-id="0749e-234">**[A]** Create LVM configurations</span></span>

   <pre><code>
   sudo pvcreate /dev/sdc1   
   sudo vgcreate vg_NFS /dev/sdc1
   sudo lvcreate -l 100%FREE -n <b>NWS</b> vg_NFS
   </code></pre>

1. <span data-ttu-id="0749e-235">**[A]**  Utwórz hello NFS drbd urządzenia</span><span class="sxs-lookup"><span data-stu-id="0749e-235">**[A]** Create hello NFS drbd device</span></span>

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_nfs.res
   </code></pre>

   <span data-ttu-id="0749e-236">Wstaw hello konfiguracji dla nowego urządzenia drbd hello i zakończenia</span><span class="sxs-lookup"><span data-stu-id="0749e-236">Insert hello configuration for hello new drbd device and exit</span></span>

   <pre><code>
   resource <b>NWS</b>_nfs {
      protocol     C;
      disk {
         on-io-error       pass_on;
      }
      on <b>prod-nfs-0</b> {
         address   <b>10.0.0.5</b>:7790;
         device    /dev/drbd0;
         disk      /dev/vg_NFS/NWS;
         meta-disk internal;
      }
      on <b>prod-nfs-1</b> {
         address   <b>10.0.0.6</b>:7790;
         device    /dev/drbd0;
         disk      /dev/vg_NFS/NWS;
         meta-disk internal;
      }
   }
   </code></pre>

   <span data-ttu-id="0749e-237">Utwórz urządzenie drbd hello i uruchom ją</span><span class="sxs-lookup"><span data-stu-id="0749e-237">Create hello drbd device and start it</span></span>

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_nfs
   sudo drbdadm up <b>NWS</b>_nfs
   </code></pre>

1. <span data-ttu-id="0749e-238">**[1]**  Pominąć synchronizacji początkowej</span><span class="sxs-lookup"><span data-stu-id="0749e-238">**[1]** Skip initial synchronization</span></span>

   <pre><code>
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_nfs
   </code></pre>

1. <span data-ttu-id="0749e-239">**[1]**  Węzła podstawowego hello zestawu</span><span class="sxs-lookup"><span data-stu-id="0749e-239">**[1]** Set hello primary node</span></span>

   <pre><code>
   sudo drbdadm primary --force <b>NWS</b>_nfs
   </code></pre>

1. <span data-ttu-id="0749e-240">**[1]**  Poczekaj, aż nowych urządzeń drbd hello są zsynchronizowane.</span><span class="sxs-lookup"><span data-stu-id="0749e-240">**[1]** Wait until hello new drbd devices are synchronized</span></span>

   <pre><code>
   sudo cat /proc/drbd

   # version: 8.4.6 (api:1/proto:86-101)
   # GIT-hash: 833d830e0152d1e457fa7856e71e11248ccf3f70 build by abuild@sheep14, 2016-05-09 23:14:56
   # 0: cs:Connected ro:Primary/Secondary ds:UpToDate/UpToDate C r-----
   #    ns:0 nr:0 dw:0 dr:912 al:8 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   </code></pre>

1. <span data-ttu-id="0749e-241">**[1]**  Utworzyć systemy plików na powitania drbd urządzeń</span><span class="sxs-lookup"><span data-stu-id="0749e-241">**[1]** Create file systems on hello drbd devices</span></span>

   <pre><code>
   sudo mkfs.xfs /dev/drbd0
   </code></pre>


### <a name="configure-cluster-framework"></a><span data-ttu-id="0749e-242">Konfigurowanie klastra Framework</span><span class="sxs-lookup"><span data-stu-id="0749e-242">Configure Cluster Framework</span></span>

1. <span data-ttu-id="0749e-243">**[1]**  Zmiany ustawień domyślnych hello</span><span class="sxs-lookup"><span data-stu-id="0749e-243">**[1]** Change hello default settings</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# rsc_defaults resource-stickiness="1"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="0749e-244">**[1]**  Konfiguracji klastra toohello urządzenia drbd Dodaj hello systemu plików NFS</span><span class="sxs-lookup"><span data-stu-id="0749e-244">**[1]** Add hello NFS drbd device toohello cluster configuration</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive drbd_<b>NWS</b>_nfs \
     ocf:linbit:drbd \
     params drbd_resource="<b>NWS</b>_nfs" \
     op monitor interval="15" role="Master" \
     op monitor interval="30" role="Slave"

   crm(live)configure# ms ms-drbd_<b>NWS</b>_nfs drbd_<b>NWS</b>_nfs \
     meta master-max="1" master-node-max="1" clone-max="2" \
     clone-node-max="1" notify="true" interleave="true"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="0749e-245">**[1]**  Serwer NFS hello Utwórz</span><span class="sxs-lookup"><span data-stu-id="0749e-245">**[1]** Create hello NFS server</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive nfsserver \
     systemd:nfs-server \
     op monitor interval="30s"

   crm(live)configure# clone cl-nfsserver nfsserver interleave="true"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="0749e-246">**[1]**  Utworzyć hello zasobów systemu plików NFS</span><span class="sxs-lookup"><span data-stu-id="0749e-246">**[1]** Create hello NFS File System resources</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive fs_<b>NWS</b>_sapmnt \
     ocf:heartbeat:Filesystem \
     params device=/dev/drbd0 \
     directory=/srv/nfs/<b>NWS</b>  \
     fstype=xfs \
     op monitor interval="10s"

   crm(live)configure# group g-<b>NWS</b>_nfs fs_<b>NWS</b>_sapmnt

   crm(live)configure# order o-<b>NWS</b>_drbd_before_nfs inf: \
     ms-drbd_<b>NWS</b>_nfs:promote g-<b>NWS</b>_nfs:start
   
   crm(live)configure# colocation col-<b>NWS</b>_nfs_on_drbd inf: \
     g-<b>NWS</b>_nfs ms-drbd_<b>NWS</b>_nfs:Master

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="0749e-247">**[1]**  Utworzyć hello eksportu systemu plików NFS</span><span class="sxs-lookup"><span data-stu-id="0749e-247">**[1]** Create hello NFS exports</span></span>

   <pre><code>
   sudo mkdir /srv/nfs/<b>NWS</b>/sidsys
   sudo mkdir /srv/nfs/<b>NWS</b>/sapmntsid
   sudo mkdir /srv/nfs/<b>NWS</b>/trans

   sudo crm configure

   crm(live)configure# primitive exportfs_<b>NWS</b> \
     ocf:heartbeat:exportfs \
     params directory="/srv/nfs/<b>NWS</b>" \
     options="rw,no_root_squash" \
     clientspec="*" fsid=0 \
     wait_for_leasetime_on_stop=true \
     op monitor interval="30s"

   crm(live)configure# modgroup g-<b>NWS</b>_nfs add exportfs_<b>NWS</b>

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="0749e-248">**[1]**  Tworzenie wirtualnego adresu IP zasobu i sondy kondycji dla hello wewnętrznego modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="0749e-248">**[1]** Create a virtual IP resource and health-probe for hello internal load balancer</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive vip_<b>NWS</b>_nfs IPaddr2 \
     params ip=<b>10.0.0.4</b> cidr_netmask=24 \
     op monitor interval=10 timeout=20

   crm(live)configure# primitive nc_<b>NWS</b>_nfs anything \
     params binfile="/usr/bin/nc" cmdline_options="-l -k 610<b>00</b>" \
     op monitor timeout=20s interval=10 depth=0

   crm(live)configure# modgroup g-<b>NWS</b>_nfs add nc_<b>NWS</b>_nfs
   crm(live)configure# modgroup g-<b>NWS</b>_nfs add vip_<b>NWS</b>_nfs

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

### <a name="create-stonith-device"></a><span data-ttu-id="0749e-249">Utwórz urządzenie STONITH</span><span class="sxs-lookup"><span data-stu-id="0749e-249">Create STONITH device</span></span>

<span data-ttu-id="0749e-250">Witaj STONITH urządzenie używa nazwy głównej usługi tooauthorize przed Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="0749e-250">hello STONITH device uses a Service Principal tooauthorize against Microsoft Azure.</span></span> <span data-ttu-id="0749e-251">Wykonaj te kroki toocreate nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="0749e-251">Follow these steps toocreate a Service Principal.</span></span>

1. <span data-ttu-id="0749e-252">Przejdź do zbyt<https://portal.azure.com></span><span class="sxs-lookup"><span data-stu-id="0749e-252">Go too<https://portal.azure.com></span></span>
1. <span data-ttu-id="0749e-253">Otwórz hello bloku usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0749e-253">Open hello Azure Active Directory blade</span></span>  
   <span data-ttu-id="0749e-254">Przejdź tooProperties i zanotuj hello identyfikator katalogu. Jest to hello **identyfikator dzierżawcy**.</span><span class="sxs-lookup"><span data-stu-id="0749e-254">Go tooProperties and write down hello Directory Id. This is hello **tenant id**.</span></span>
1. <span data-ttu-id="0749e-255">Kliknij przycisk rejestracji aplikacji</span><span class="sxs-lookup"><span data-stu-id="0749e-255">Click App registrations</span></span>
1. <span data-ttu-id="0749e-256">Kliknij pozycję Dodaj.</span><span class="sxs-lookup"><span data-stu-id="0749e-256">Click Add</span></span>
1. <span data-ttu-id="0749e-257">Wprowadź nazwę, wybierz typ aplikacji "Aplikacja/interfejs API sieci Web", wprowadź adres URL logowania (np. http://localhost) i kliknij przycisk Utwórz</span><span class="sxs-lookup"><span data-stu-id="0749e-257">Enter a Name, select Application Type "Web app/API", enter a sign-on URL (for example http://localhost) and click Create</span></span>
1. <span data-ttu-id="0749e-258">Witaj adres URL logowania nie jest używany i może być dowolny prawidłowy adres URL</span><span class="sxs-lookup"><span data-stu-id="0749e-258">hello sign-on URL is not used and can be any valid URL</span></span>
1. <span data-ttu-id="0749e-259">Wybierz hello nowej aplikacji i kliknij na karcie Ustawienia hello</span><span class="sxs-lookup"><span data-stu-id="0749e-259">Select hello new App and click Keys in hello Settings tab</span></span>
1. <span data-ttu-id="0749e-260">Wprowadź opis nowego klucza, wybierz pozycję "Nigdy nie wygasa" i kliknij przycisk Zapisz</span><span class="sxs-lookup"><span data-stu-id="0749e-260">Enter a description for a new key, select "Never expires" and click Save</span></span>
1. <span data-ttu-id="0749e-261">Zapisz hello wartość.</span><span class="sxs-lookup"><span data-stu-id="0749e-261">Write down hello Value.</span></span> <span data-ttu-id="0749e-262">Jest on używany jako hello **hasło** dla hello nazwy głównej usługi</span><span class="sxs-lookup"><span data-stu-id="0749e-262">It is used as hello **password** for hello Service Principal</span></span>
1. <span data-ttu-id="0749e-263">Zapisz hello identyfikator aplikacji. Jest używany jako hello username (**identyfikatora** w poniższych krokach hello) z hello nazwy głównej usługi</span><span class="sxs-lookup"><span data-stu-id="0749e-263">Write down hello Application Id. It is used as hello username (**login id** in hello steps below) of hello Service Principal</span></span>

<span data-ttu-id="0749e-264">Witaj nazwy głównej usługi nie ma uprawnienia tooaccess zasobów platformy Azure domyślnie.</span><span class="sxs-lookup"><span data-stu-id="0749e-264">hello Service Principal does not have permissions tooaccess your Azure resources by default.</span></span> <span data-ttu-id="0749e-265">Należy toogive hello nazwy głównej usługi uprawnienia toostart i Zatrzymaj (deallocate) wszystkich maszyn wirtualnych klastra hello.</span><span class="sxs-lookup"><span data-stu-id="0749e-265">You need toogive hello Service Principal permissions toostart and stop (deallocate) all virtual machines of hello cluster.</span></span>

1. <span data-ttu-id="0749e-266">Przejdź toohttps://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="0749e-266">Go toohttps://portal.azure.com</span></span>
1. <span data-ttu-id="0749e-267">Otwórz hello wszystkich bloku zasobów</span><span class="sxs-lookup"><span data-stu-id="0749e-267">Open hello All resources blade</span></span>
1. <span data-ttu-id="0749e-268">Wybierz maszynę wirtualną hello</span><span class="sxs-lookup"><span data-stu-id="0749e-268">Select hello virtual machine</span></span>
1. <span data-ttu-id="0749e-269">Kliknij przycisk kontroli dostępu (IAM)</span><span class="sxs-lookup"><span data-stu-id="0749e-269">Click Access control (IAM)</span></span>
1. <span data-ttu-id="0749e-270">Kliknij pozycję Dodaj.</span><span class="sxs-lookup"><span data-stu-id="0749e-270">Click Add</span></span>
1. <span data-ttu-id="0749e-271">Wybierz rolę hello właściciela</span><span class="sxs-lookup"><span data-stu-id="0749e-271">Select hello role Owner</span></span>
1. <span data-ttu-id="0749e-272">Wprowadź nazwę hello aplikacji hello utworzone powyżej</span><span class="sxs-lookup"><span data-stu-id="0749e-272">Enter hello name of hello application you created above</span></span>
1. <span data-ttu-id="0749e-273">Kliknij przycisk OK</span><span class="sxs-lookup"><span data-stu-id="0749e-273">Click OK</span></span>

#### <a name="1-create-hello-stonith-devices"></a><span data-ttu-id="0749e-274">**[1]**  Utworzyć hello STONITH urządzeń</span><span class="sxs-lookup"><span data-stu-id="0749e-274">**[1]** Create hello STONITH devices</span></span>

<span data-ttu-id="0749e-275">Po edytować uprawnienia hello hello maszyn wirtualnych, możesz skonfigurować urządzenia STONITH hello hello klastra.</span><span class="sxs-lookup"><span data-stu-id="0749e-275">After you edited hello permissions for hello virtual machines, you can configure hello STONITH devices in hello cluster.</span></span>

<pre><code>
sudo crm configure

# replace hello bold string with your subscription id, resource group, tenant id, service principal id and password

crm(live)configure# primitive rsc_st_azure_1 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# primitive rsc_st_azure_2 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started

crm(live)configure# commit
crm(live)configure# exit
</code></pre>

#### <a name="1-enable-hello-use-of-a-stonith-device"></a><span data-ttu-id="0749e-276">**[1]**  Zezwalaj na używanie hello urządzenia STONITH</span><span class="sxs-lookup"><span data-stu-id="0749e-276">**[1]** Enable hello use of a STONITH device</span></span>

<pre><code>
sudo crm configure property stonith-enabled=true 
</code></pre>

## <a name="setting-up-ascs"></a><span data-ttu-id="0749e-277">Konfigurowanie SCS ()</span><span class="sxs-lookup"><span data-stu-id="0749e-277">Setting up (A)SCS</span></span>

### <a name="deploying-linux"></a><span data-ttu-id="0749e-278">Wdrażanie systemu Linux</span><span class="sxs-lookup"><span data-stu-id="0749e-278">Deploying Linux</span></span>

<span data-ttu-id="0749e-279">Hello Azure Marketplace zawiera obraz systemu SUSE Linux Enterprise Server dla 12 aplikacje SAP służy toodeploy nowych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="0749e-279">hello Azure Marketplace contains an image for SUSE Linux Enterprise Server for SAP Applications 12 that you can use toodeploy new virtual machines.</span></span> <span data-ttu-id="0749e-280">Witaj obrazu z witryny marketplace zawiera hello zasobów agenta dla programu SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="0749e-280">hello marketplace image contains hello resource agent for SAP NetWeaver.</span></span>

<span data-ttu-id="0749e-281">Możesz użyć jednego z szablonów szybki start hello w github toodeploy wszystkich wymaganych zasobów.</span><span class="sxs-lookup"><span data-stu-id="0749e-281">You can use one of hello quick start templates on github toodeploy all required resources.</span></span> <span data-ttu-id="0749e-282">Szablon Hello wdraża hello maszyn wirtualnych, usługi równoważenia obciążenia hello, itp zestawu dostępności. Wykonaj te kroki toodeploy hello szablonu:</span><span class="sxs-lookup"><span data-stu-id="0749e-282">hello template deploys hello virtual machines, hello load balancer, availability set etc. Follow these steps toodeploy hello template:</span></span>

1. <span data-ttu-id="0749e-283">Otwórz hello [szablon identyfikatora SID Multi ASCS/SCS] [ template-multisid-xscs] lub hello [zbieżność szablonu] [ template-converged] w szablonie ASCS/SCS hello portalu Azure hello tylko Tworzy hello równoważenia obciążenia reguły hello SAP NetWeaver ASCS/SCS i wystąpień Wywołujących (tylko w systemie Linux), dlatego szablon konwergentnej hello tworzy również hello reguły równoważenia obciążenia dla bazy danych (na przykład Microsoft SQL Server lub SAP HANA).</span><span class="sxs-lookup"><span data-stu-id="0749e-283">Open hello [ASCS/SCS Multi SID template][template-multisid-xscs] or hello [converged template][template-converged] on hello Azure portal hello ASCS/SCS template only creates hello load-balancing rules for hello SAP NetWeaver ASCS/SCS and ERS (Linux only) instances whereas hello converged template also creates hello load-balancing rules for a database (for example Microsoft SQL Server or SAP HANA).</span></span> <span data-ttu-id="0749e-284">Jeśli planujesz tooinstall systemu SAP NetWeaver na podstawie i ma bazy danych hello tooinstall na hello tych komputerów, użyj hello [zbieżność szablonu][template-converged].</span><span class="sxs-lookup"><span data-stu-id="0749e-284">If you plan tooinstall an SAP NetWeaver based system and you also want tooinstall hello database on hello same machines, use hello [converged template][template-converged].</span></span>
1. <span data-ttu-id="0749e-285">Wprowadź następujące parametry hello</span><span class="sxs-lookup"><span data-stu-id="0749e-285">Enter hello following parameters</span></span>
   1. <span data-ttu-id="0749e-286">Prefiks zasobów (tylko szablon identyfikatora SID Multi ASCS/SCS)</span><span class="sxs-lookup"><span data-stu-id="0749e-286">Resource Prefix (ASCS/SCS Multi SID template only)</span></span>  
      <span data-ttu-id="0749e-287">Wprowadź prefiks hello ma toouse.</span><span class="sxs-lookup"><span data-stu-id="0749e-287">Enter hello prefix you want toouse.</span></span> <span data-ttu-id="0749e-288">wartość Hello jest używany jako prefiksu hello zasobów, które zostały wdrożone.</span><span class="sxs-lookup"><span data-stu-id="0749e-288">hello value is used as a prefix for hello resources that are deployed.</span></span>
   3. <span data-ttu-id="0749e-289">Identyfikator systemu SAP (tylko szablon konwergentnej)</span><span class="sxs-lookup"><span data-stu-id="0749e-289">Sap System Id (converged template only)</span></span>  
      <span data-ttu-id="0749e-290">Wprowadź systemu SAP hello identyfikator hello ma tooinstall systemu SAP.</span><span class="sxs-lookup"><span data-stu-id="0749e-290">Enter hello SAP system Id of hello SAP system you want tooinstall.</span></span> <span data-ttu-id="0749e-291">Witaj identyfikator jest używany jako prefiksu hello zasobów, które zostały wdrożone.</span><span class="sxs-lookup"><span data-stu-id="0749e-291">hello Id is used as a prefix for hello resources that are deployed.</span></span>
   4. <span data-ttu-id="0749e-292">Typ stosu</span><span class="sxs-lookup"><span data-stu-id="0749e-292">Stack Type</span></span>  
      <span data-ttu-id="0749e-293">Wybierz typ stosu SAP NetWeaver hello</span><span class="sxs-lookup"><span data-stu-id="0749e-293">Select hello SAP NetWeaver stack type</span></span>
   5. <span data-ttu-id="0749e-294">Typ systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="0749e-294">Os Type</span></span>  
      <span data-ttu-id="0749e-295">Wybierz jedną z hello dystrybucje systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="0749e-295">Select one of hello Linux distributions.</span></span> <span data-ttu-id="0749e-296">Na przykład wybierz SLES 12 BYOS</span><span class="sxs-lookup"><span data-stu-id="0749e-296">For this example, select SLES 12 BYOS</span></span>
   6. <span data-ttu-id="0749e-297">Typ bazy danych</span><span class="sxs-lookup"><span data-stu-id="0749e-297">Db Type</span></span>  
      <span data-ttu-id="0749e-298">Wybierz HANA</span><span class="sxs-lookup"><span data-stu-id="0749e-298">Select HANA</span></span>
   7. <span data-ttu-id="0749e-299">Rozmiar systemu SAP</span><span class="sxs-lookup"><span data-stu-id="0749e-299">Sap System Size</span></span>  
      <span data-ttu-id="0749e-300">udostępnia Hello ilość protokoły SAP hello nowy system.</span><span class="sxs-lookup"><span data-stu-id="0749e-300">hello amount of SAPS hello new system provides.</span></span> <span data-ttu-id="0749e-301">Jeśli nie masz pewności, ile system hello protokoły SAP wymaga, należy skontaktować się z partnerem technologii SAP lub Integrator systemu</span><span class="sxs-lookup"><span data-stu-id="0749e-301">If you are not sure how many SAPS hello system requires, please ask your SAP Technology Partner or System Integrator</span></span>
   8. <span data-ttu-id="0749e-302">Dostępność systemu</span><span class="sxs-lookup"><span data-stu-id="0749e-302">System Availability</span></span>  
      <span data-ttu-id="0749e-303">Wybierz opcję wysokiej dostępności</span><span class="sxs-lookup"><span data-stu-id="0749e-303">Select HA</span></span>
   9. <span data-ttu-id="0749e-304">Nazwa użytkownika i hasło administratora</span><span class="sxs-lookup"><span data-stu-id="0749e-304">Admin Username and Admin Password</span></span>  
      <span data-ttu-id="0749e-305">Tworzony jest nowy użytkownik, który może być używane toolog toohello maszyny.</span><span class="sxs-lookup"><span data-stu-id="0749e-305">A new user is created that can be used toolog on toohello machine.</span></span>
   10. <span data-ttu-id="0749e-306">Identyfikator podsieci</span><span class="sxs-lookup"><span data-stu-id="0749e-306">Subnet Id</span></span>  
   <span data-ttu-id="0749e-307">Identyfikator Hello maszyn wirtualnych hello hello podsieci toowhich powinny być podłączone do.</span><span class="sxs-lookup"><span data-stu-id="0749e-307">hello ID of hello subnet toowhich hello virtual machines should be connected to.</span></span>  <span data-ttu-id="0749e-308">Jeśli chcesz toocreate nową sieć wirtualną lub wybierz hello tej samej podsieci, która używane lub tworzone w ramach wdrażania serwera systemu plików NFS hello może pozostać puste.</span><span class="sxs-lookup"><span data-stu-id="0749e-308">Leave empty if you want toocreate a new virtual network or select hello same subnet that you used or created as part of hello NFS server deployment.</span></span> <span data-ttu-id="0749e-309">Identyfikator Hello zwykle wygląda /subscriptions/**&lt;identyfikator subskrypcji&gt;**/resourceGroups/**&lt;Nazwa grupy zasobów&gt;**/providers/ Microsoft.Network/virtualNetworks/**&lt;wirtualnej nazwy sieciowej&gt;**/subnets/**&lt;nazwy podsieci&gt;**</span><span class="sxs-lookup"><span data-stu-id="0749e-309">hello ID usually looks like /subscriptions/**&lt;subscription id&gt;**/resourceGroups/**&lt;resource group name&gt;**/providers/Microsoft.Network/virtualNetworks/**&lt;virtual network name&gt;**/subnets/**&lt;subnet name&gt;**</span></span>

### <a name="installation"></a><span data-ttu-id="0749e-310">Instalacja</span><span class="sxs-lookup"><span data-stu-id="0749e-310">Installation</span></span>

<span data-ttu-id="0749e-311">Hello następujące elementy są poprzedzane prefiksem albo **[A]** -węzłów dotyczy tooall **[1]** -tylko odpowiednie toonode 1 lub **[2]** -tylko odpowiednie toonode 2.</span><span class="sxs-lookup"><span data-stu-id="0749e-311">hello following items are prefixed with either **[A]** - applicable tooall nodes, **[1]** - only applicable toonode 1 or **[2]** - only applicable toonode 2.</span></span>

1. <span data-ttu-id="0749e-312">**[A]**  Zaktualizować SLES</span><span class="sxs-lookup"><span data-stu-id="0749e-312">**[A]** Update SLES</span></span>

   <pre><code>
   sudo zypper update
   </code></pre>

1. <span data-ttu-id="0749e-313">**[1]**  Dostęp ssh</span><span class="sxs-lookup"><span data-stu-id="0749e-313">**[1]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

2. <span data-ttu-id="0749e-314">**[2]**  Dostęp ssh</span><span class="sxs-lookup"><span data-stu-id="0749e-314">**[2]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa

   # insert hello public key you copied in hello last step into hello authorized keys file on hello second server
   sudo vi /root/.ssh/authorized_keys
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key   
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

1. <span data-ttu-id="0749e-315">**[1]**  Dostęp ssh</span><span class="sxs-lookup"><span data-stu-id="0749e-315">**[1]** Enable ssh access</span></span>

   <pre><code>
   # insert hello public key you copied in hello last step into hello authorized keys file on hello first server
   sudo vi /root/.ssh/authorized_keys
   </code></pre>

1. <span data-ttu-id="0749e-316">**[A]**  Zainstalować HA rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="0749e-316">**[A]** Install HA extension</span></span>
   
   <pre><code>
   sudo zypper install sle-ha-release fence-agents
   </code></pre>

1. <span data-ttu-id="0749e-317">**[A]**  SAP aktualizacji zasobów agentów</span><span class="sxs-lookup"><span data-stu-id="0749e-317">**[A]** Update SAP resource agents</span></span>  
   
   <span data-ttu-id="0749e-318">Poprawka dla pakietu zasobów agentów hello jest wymagana toouse hello nowej konfiguracji opisanej w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="0749e-318">A patch for hello resource-agents package is required toouse hello new configuration, that is described in this article.</span></span> <span data-ttu-id="0749e-319">Można sprawdzić, czy hello poprawka jest już zainstalowana hello następujące polecenie</span><span class="sxs-lookup"><span data-stu-id="0749e-319">You can check, if hello patch is already installed with hello following command</span></span>

   <pre><code>
   sudo grep 'parameter name="IS_ERS"' /usr/lib/ocf/resource.d/heartbeat/SAPInstance
   </code></pre>

   <span data-ttu-id="0749e-320">dane wyjściowe Hello powinna być podobna do</span><span class="sxs-lookup"><span data-stu-id="0749e-320">hello output should be similar to</span></span>

   <pre><code>
   &lt;parameter name="IS_ERS" unique="0" required="0"&gt;
   </code></pre>

   <span data-ttu-id="0749e-321">Polecenie grep hello nie może znaleźć parametr IS_ERS hello, konieczne będzie tooinstall hello poprawki wymienione na [hello SUSE stronę pobierania](https://download.suse.com/patch/finder/#bu=suse&familyId=&productId=&dateRange=&startDate=&endDate=&priority=&architecture=&keywords=resource-agents)</span><span class="sxs-lookup"><span data-stu-id="0749e-321">If hello grep command does not find hello IS_ERS parameter, you need tooinstall hello patch listed on [hello SUSE download page](https://download.suse.com/patch/finder/#bu=suse&familyId=&productId=&dateRange=&startDate=&endDate=&priority=&architecture=&keywords=resource-agents)</span></span>

   <pre><code>
   # example for patch for SLES 12 SP1
   sudo zypper in -t patch SUSE-SLE-HA-12-SP1-2017-885=1
   # example for patch for SLES 12 SP2
   sudo zypper in -t patch SUSE-SLE-HA-12-SP2-2017-886=1
   </code></pre>

1. <span data-ttu-id="0749e-322">**[A]**  Instalatora rozpoznawania nazwy hosta</span><span class="sxs-lookup"><span data-stu-id="0749e-322">**[A]** Setup host name resolution</span></span>   

   <span data-ttu-id="0749e-323">Można użyć serwera DNS lub zmodyfikować hello/etc/hosts na wszystkich węzłach.</span><span class="sxs-lookup"><span data-stu-id="0749e-323">You can either use a DNS server or modify hello /etc/hosts on all nodes.</span></span> <span data-ttu-id="0749e-324">Ten przykład przedstawia, jak toouse hello plik/etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="0749e-324">This example shows how toouse hello /etc/hosts file.</span></span>
   <span data-ttu-id="0749e-325">Zastąpienie hello adresu IP i nazwy hosta hello w hello następujące polecenia</span><span class="sxs-lookup"><span data-stu-id="0749e-325">Replace hello IP address and hello hostname in hello following commands</span></span>

   <pre><code>
   sudo vi /etc/hosts
   </code></pre>
   
   <span data-ttu-id="0749e-326">Wstaw hello następujące wiersze zbyt/etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="0749e-326">Insert hello following lines too/etc/hosts.</span></span> <span data-ttu-id="0749e-327">Zmień toomatch adres i nazwę hosta IP hello środowiska</span><span class="sxs-lookup"><span data-stu-id="0749e-327">Change hello IP address and hostname toomatch your environment</span></span>   
   
   <pre><code>
   # IP address of hello load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ASCS/SCS
   <b>10.0.0.10 nws-ascs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ERS
   <b>10.0.0.11 nws-ers</b>
   # IP address of hello load balancer frontend configuration for database
   <b>10.0.0.12 nws-db</b>
   </code></pre>

1. <span data-ttu-id="0749e-328">**[1]**  Instalacji klastra</span><span class="sxs-lookup"><span data-stu-id="0749e-328">**[1]** Install Cluster</span></span>
   
   <pre><code>
   sudo ha-cluster-init
   
   # Do you want toocontinue anyway? [y/N] -> y
   # Network address toobind too(for example: 192.168.1.0) [10.79.227.0] -> ENTER
   # Multicast address (for example: 239.x.x.x) [239.174.218.125] -> ENTER
   # Multicast port [5405] -> ENTER
   # Do you wish toouse SBD? [y/N] -> N
   # Do you wish tooconfigure an administration IP? [y/N] -> N
   </code></pre>

1. <span data-ttu-id="0749e-329">**[2]**  Dodaj toocluster węzła</span><span class="sxs-lookup"><span data-stu-id="0749e-329">**[2]** Add node toocluster</span></span>
   
   <pre><code> 
   sudo ha-cluster-join

   # WARNING: NTP is not configured toostart at system boot.
   # WARNING: No watchdog device found. If SBD is used, hello cluster will be unable toostart without a watchdog.
   # Do you want toocontinue anyway? [y/N] -> y
   # IP address or hostname of existing node (for example: 192.168.1.1) [] -> IP address of node 1 for example 10.0.0.10
   # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
   </code></pre>

1. <span data-ttu-id="0749e-330">**[A]**  Toohello hasło hacluster zmiany tego samego hasła</span><span class="sxs-lookup"><span data-stu-id="0749e-330">**[A]** Change hacluster password toohello same password</span></span>

   <pre><code> 
   sudo passwd hacluster
   </code></pre>

1. <span data-ttu-id="0749e-331">**[A]**  Skonfigurować corosync toouse innych transportu i Dodaj wstawienia.</span><span class="sxs-lookup"><span data-stu-id="0749e-331">**[A]** Configure corosync toouse other transport and add nodelist.</span></span> <span data-ttu-id="0749e-332">Klaster nie będą działać inaczej.</span><span class="sxs-lookup"><span data-stu-id="0749e-332">Cluster will not work otherwise.</span></span>
   
   <pre><code> 
   sudo vi /etc/corosync/corosync.conf   
   </code></pre>

   <span data-ttu-id="0749e-333">Dodaj powitania po bold toohello zawartości pliku.</span><span class="sxs-lookup"><span data-stu-id="0749e-333">Add hello following bold content toohello file.</span></span>
   
   <pre><code> 
   [...]
     interface { 
        [...] 
     }
     <b>transport:      udpu</b>
   } 
   <b>nodelist {
     node {
      # IP address of <b>nws-cl-0</b>
      ring0_addr:     10.0.0.14
     }
     node {
      # IP address of <b>nws-cl-1</b>
      ring0_addr:     10.0.0.13
     } 
   }</b>
   logging {
     [...]
   </code></pre>

   <span data-ttu-id="0749e-334">Następnie uruchom ponownie usługę corosync hello</span><span class="sxs-lookup"><span data-stu-id="0749e-334">Then restart hello corosync service</span></span>

   <pre><code>
   sudo service corosync restart
   </code></pre>

1. <span data-ttu-id="0749e-335">**[A]**  Zainstalować składniki drbd</span><span class="sxs-lookup"><span data-stu-id="0749e-335">**[A]** Install drbd components</span></span>

   <pre><code>
   sudo zypper install drbd drbd-kmp-default drbd-utils
   </code></pre>

1. <span data-ttu-id="0749e-336">**[A]**  Utworzyć partycję hello drbd urządzenia</span><span class="sxs-lookup"><span data-stu-id="0749e-336">**[A]** Create a partition for hello drbd device</span></span>

   <pre><code>
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdc'
   </code></pre>

1. <span data-ttu-id="0749e-337">**[A]**  LVM Tworzenie konfiguracji</span><span class="sxs-lookup"><span data-stu-id="0749e-337">**[A]** Create LVM configurations</span></span>

   <pre><code>
   sudo pvcreate /dev/sdc1   
   sudo vgcreate vg_<b>NWS</b> /dev/sdc1
   sudo lvcreate -l 50%FREE -n <b>NWS</b>_ASCS vg_<b>NWS</b>
   sudo lvcreate -l 50%FREE -n <b>NWS</b>_ERS vg_<b>NWS</b>
   </code></pre>

1. <span data-ttu-id="0749e-338">**[A]**  Utwórz hello SCS drbd urządzenia</span><span class="sxs-lookup"><span data-stu-id="0749e-338">**[A]** Create hello SCS drbd device</span></span>

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_ascs.res
   </code></pre>

   <span data-ttu-id="0749e-339">Wstaw hello konfiguracji dla nowego urządzenia drbd hello i zakończenia</span><span class="sxs-lookup"><span data-stu-id="0749e-339">Insert hello configuration for hello new drbd device and exit</span></span>

   <pre><code>
   resource <b>NWS</b>_ascs {
      protocol     C;
      disk {
         on-io-error       pass_on;
      }
      on <b>nws-cl-0</b> {
         address   <b>10.0.0.14</b>:7791;
         device    /dev/drbd0;
         disk      /dev/vg_NWS/NWS_ASCS;
         meta-disk internal;
      }
      on <b>nws-cl-1</b> {
         address   <b>10.0.0.13</b>:7791;
         device    /dev/drbd0;
         disk      /dev/vg_NWS/NWS_ASCS;
         meta-disk internal;
      }
   }
   </code></pre>

   <span data-ttu-id="0749e-340">Utwórz urządzenie drbd hello i uruchom ją</span><span class="sxs-lookup"><span data-stu-id="0749e-340">Create hello drbd device and start it</span></span>

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_ascs
   sudo drbdadm up <b>NWS</b>_ascs
   </code></pre>

1. <span data-ttu-id="0749e-341">**[A]**  Utwórz hello Wywołujących drbd urządzenia</span><span class="sxs-lookup"><span data-stu-id="0749e-341">**[A]** Create hello ERS drbd device</span></span>

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_ers.res
   </code></pre>

   <span data-ttu-id="0749e-342">Wstaw hello konfiguracji dla nowego urządzenia drbd hello i zakończenia</span><span class="sxs-lookup"><span data-stu-id="0749e-342">Insert hello configuration for hello new drbd device and exit</span></span>

   <pre><code>
   resource <b>NWS</b>_ers {
      protocol     C;
      disk {
         on-io-error       pass_on;
      }
      on <b>nws-cl-0</b> {
         address   <b>10.0.0.14</b>:7792;
         device    /dev/drbd1;
         disk      /dev/vg_NWS/NWS_ERS;
         meta-disk internal;
      }
      on <b>nws-cl-1</b> {
         address   <b>10.0.0.13</b>:7792;
         device    /dev/drbd1;
         disk      /dev/vg_NWS/NWS_ERS;
         meta-disk internal;
      }
   }
   </code></pre>

   <span data-ttu-id="0749e-343">Utwórz urządzenie drbd hello i uruchom ją</span><span class="sxs-lookup"><span data-stu-id="0749e-343">Create hello drbd device and start it</span></span>

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_ers
   sudo drbdadm up <b>NWS</b>_ers
   </code></pre>

1. <span data-ttu-id="0749e-344">**[1]**  Pominąć synchronizacji początkowej</span><span class="sxs-lookup"><span data-stu-id="0749e-344">**[1]** Skip initial synchronization</span></span>

   <pre><code>
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_ascs
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_ers
   </code></pre>

1. <span data-ttu-id="0749e-345">**[1]**  Węzła podstawowego hello zestawu</span><span class="sxs-lookup"><span data-stu-id="0749e-345">**[1]** Set hello primary node</span></span>

   <pre><code>
   sudo drbdadm primary --force <b>NWS</b>_ascs
   sudo drbdadm primary --force <b>NWS</b>_ers
   </code></pre>

1. <span data-ttu-id="0749e-346">**[1]**  Poczekaj, aż nowych urządzeń drbd hello są zsynchronizowane.</span><span class="sxs-lookup"><span data-stu-id="0749e-346">**[1]** Wait until hello new drbd devices are synchronized</span></span>

   <pre><code>
   sudo cat /proc/drbd

   # version: 8.4.6 (api:1/proto:86-101)
   # GIT-hash: 833d830e0152d1e457fa7856e71e11248ccf3f70 build by abuild@sheep14, 2016-05-09 23:14:56
   # 0: cs:<b>Connected</b> ro:Primary/Secondary ds:<b>UpToDate/UpToDate</b> C r-----
   #     ns:93991268 nr:0 dw:93991268 dr:93944920 al:383 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   # 1: cs:<b>Connected</b> ro:Primary/Secondary ds:<b>UpToDate/UpToDate</b> C r-----
   #     ns:6047920 nr:0 dw:6047920 dr:6039112 al:34 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   # 2: cs:<b>Connected</b> ro:Primary/Secondary ds:<b>UpToDate/UpToDate</b> C r-----
   #     ns:5142732 nr:0 dw:5142732 dr:5133924 al:30 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   </code></pre>

1. <span data-ttu-id="0749e-347">**[1]**  Utworzyć systemy plików na powitania drbd urządzeń</span><span class="sxs-lookup"><span data-stu-id="0749e-347">**[1]** Create file systems on hello drbd devices</span></span>

   <pre><code>
   sudo mkfs.xfs /dev/drbd0
   sudo mkfs.xfs /dev/drbd1
   </code></pre>


### <a name="configure-cluster-framework"></a><span data-ttu-id="0749e-348">Konfigurowanie klastra Framework</span><span class="sxs-lookup"><span data-stu-id="0749e-348">Configure Cluster Framework</span></span>

<span data-ttu-id="0749e-349">**[1]**  Zmiany ustawień domyślnych hello</span><span class="sxs-lookup"><span data-stu-id="0749e-349">**[1]** Change hello default settings</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# rsc_defaults resource-stickiness="1"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

## <a name="prepare-for-sap-netweaver-installation"></a><span data-ttu-id="0749e-350">Przygotowanie do instalacji programu SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="0749e-350">Prepare for SAP NetWeaver installation</span></span>

1. <span data-ttu-id="0749e-351">**[A]**  Hello Utwórz udostępnionych katalogów</span><span class="sxs-lookup"><span data-stu-id="0749e-351">**[A]** Create hello shared directories</span></span>

   <pre><code>
   sudo mkdir -p /sapmnt/<b>NWS</b>
   sudo mkdir -p /usr/sap/trans
   sudo mkdir -p /usr/sap/<b>NWS</b>/SYS

   sudo chattr +i /sapmnt/<b>NWS</b>
   sudo chattr +i /usr/sap/trans
   sudo chattr +i /usr/sap/<b>NWS</b>/SYS
   </code></pre>

1. <span data-ttu-id="0749e-352">**[A]**  Skonfigurować autofs</span><span class="sxs-lookup"><span data-stu-id="0749e-352">**[A]** Configure autofs</span></span>
 
   <pre><code>
   sudo vi /etc/auto.master

   # Add hello following line toohello file, save and exit
   +auto.master
   /- /etc/auto.direct
   </code></pre>

   <span data-ttu-id="0749e-353">Utwórz plik o</span><span class="sxs-lookup"><span data-stu-id="0749e-353">Create a file with</span></span>

   <pre><code>
   sudo vi /etc/auto.direct

   # Add hello following lines toohello file, save and exit
   /sapmnt/<b>NWS</b> -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sapmntsid
   /usr/sap/trans -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/trans
   /usr/sap/<b>NWS</b>/SYS -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sidsys
   </code></pre>

   <span data-ttu-id="0749e-354">Uruchom ponownie autofs toomount hello nowe udziały</span><span class="sxs-lookup"><span data-stu-id="0749e-354">Restart autofs toomount hello new shares</span></span>

   <pre><code>
   sudo systemctl enable autofs
   sudo service autofs restart
   </code></pre>

1. <span data-ttu-id="0749e-355">**[A]**  Skonfigurować wymiany plików</span><span class="sxs-lookup"><span data-stu-id="0749e-355">**[A]** Configure SWAP file</span></span>
 
   <pre><code>
   sudo vi /etc/waagent.conf

   # Set hello property ResourceDisk.EnableSwap tooy
   # Create and use swapfile on resource disk.
   ResourceDisk.EnableSwap=<b>y</b>

   # Set hello size of hello SWAP file with property ResourceDisk.SwapSizeMB
   # hello free space of resource disk varies by virtual machine size. Make sure that you do not set a value that is too big. You can check hello SWAP space with command swapon
   # Size of hello swapfile.
   ResourceDisk.SwapSizeMB=<b>2000</b>
   </code></pre>

   <span data-ttu-id="0749e-356">Uruchom ponownie hello agenta tooactivate hello zmiany</span><span class="sxs-lookup"><span data-stu-id="0749e-356">Restart hello Agent tooactivate hello change</span></span>

   <pre><code>
   sudo service waagent restart
   </code></pre>

### <a name="installing-sap-netweaver-ascsers"></a><span data-ttu-id="0749e-357">Instalowanie programu SAP NetWeaver ASCS/Wywołujących</span><span class="sxs-lookup"><span data-stu-id="0749e-357">Installing SAP NetWeaver ASCS/ERS</span></span>

1. <span data-ttu-id="0749e-358">**[1]**  Tworzenie wirtualnego adresu IP zasobu i sondy kondycji dla hello wewnętrznego modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="0749e-358">**[1]** Create a virtual IP resource and health-probe for hello internal load balancer</span></span>

   <pre><code>
   sudo crm node standby <b>nws-cl-1</b>
   sudo crm configure

   crm(live)configure# primitive drbd_<b>NWS</b>_ASCS \
     ocf:linbit:drbd \
     params drbd_resource="<b>NWS</b>_ascs" \
     op monitor interval="15" role="Master" \
     op monitor interval="30" role="Slave"

   crm(live)configure# ms ms-drbd_<b>NWS</b>_ASCS drbd_<b>NWS</b>_ASCS \
     meta master-max="1" master-node-max="1" clone-max="2" \
     clone-node-max="1" notify="true"

   crm(live)configure# primitive fs_<b>NWS</b>_ASCS \
     ocf:heartbeat:Filesystem \
     params device=/dev/drbd0 \
     directory=/usr/sap/<b>NWS</b>/ASCS<b>00</b>  \
     fstype=xfs \
     op monitor interval="10s"

   crm(live)configure# primitive vip_<b>NWS</b>_ASCS IPaddr2 \
     params ip=<b>10.0.0.10</b> cidr_netmask=24 \
     op monitor interval=10 timeout=20

   crm(live)configure# primitive nc_<b>NWS</b>_ASCS anything \
     params binfile="/usr/bin/nc" cmdline_options="-l -k 620<b>00</b>" \
     op monitor timeout=20s interval=10 depth=0
   
   crm(live)configure# group g-<b>NWS</b>_ASCS nc_<b>NWS</b>_ASCS vip_<b>NWS</b>_ASCS fs_<b>NWS</b>_ASCS \
      meta resource-stickiness=3000

   crm(live)configure# order o-<b>NWS</b>_drbd_before_ASCS inf: \
     ms-drbd_<b>NWS</b>_ASCS:promote g-<b>NWS</b>_ASCS:start
   
   crm(live)configure# colocation col-<b>NWS</b>_ASCS_on_drbd inf: \
     ms-drbd_<b>NWS</b>_ASCS:Master g-<b>NWS</b>_ASCS
   
   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

   <span data-ttu-id="0749e-359">Upewnij się, że stan klastra hello jest prawidłowy i czy wszystkie zasoby są uruchomione.</span><span class="sxs-lookup"><span data-stu-id="0749e-359">Make sure that hello cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="0749e-360">Nie jest ważna zasobów hello węzeł, do których są uruchomione.</span><span class="sxs-lookup"><span data-stu-id="0749e-360">It is not important on which node hello resources are running.</span></span>

   <pre><code>
   sudo crm_mon -r

   # Node nws-cl-1: standby
   # <b>Online: [ nws-cl-0 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      Stopped: [ nws-cl-1 ]
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-0</b>
   </code></pre>

1. <span data-ttu-id="0749e-361">**[1]**  Zainstalować SAP NetWeaver ASCS</span><span class="sxs-lookup"><span data-stu-id="0749e-361">**[1]** Install SAP NetWeaver ASCS</span></span>  

   <span data-ttu-id="0749e-362">Instalowanie programu SAP NetWeaver ASCS jako główny na pierwszym węźle hello przy użyciu wirtualnego nazwy hosta, na przykład mapująca adres IP toohello hello konfiguracji frontonu modułu równoważenia obciążenia dla hello ASCS <b>nws ascs</b>, <b>10.0.0.10</b>i numer wystąpienia hello używanej hello sondę modułu równoważenia obciążenia hello na przykład <b>00</b>.</span><span class="sxs-lookup"><span data-stu-id="0749e-362">Install SAP NetWeaver ASCS as root on hello first node using a virtual hostname that maps toohello IP address of hello load balancer frontend configuration for hello ASCS for example <b>nws-ascs</b>, <b>10.0.0.10</b> and hello instance number that you used for hello probe of hello load balancer for example <b>00</b>.</span></span>

   <span data-ttu-id="0749e-363">Można użyć hello sapinst parametru SAPINST_REMOTE_ACCESS_USER tooallow toosapinst tooconnect użytkownika z systemem innym niż root.</span><span class="sxs-lookup"><span data-stu-id="0749e-363">You can use hello sapinst parameter SAPINST_REMOTE_ACCESS_USER tooallow a non-root user tooconnect toosapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

1. <span data-ttu-id="0749e-364">**[1]**  Tworzenie wirtualnego adresu IP zasobu i sondy kondycji dla hello wewnętrznego modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="0749e-364">**[1]** Create a virtual IP resource and health-probe for hello internal load balancer</span></span>

   <pre><code>
   sudo crm node standby <b>nws-cl-0</b>
   sudo crm node online <b>nws-cl-1</b>
   sudo crm configure

   crm(live)configure# primitive drbd_<b>NWS</b>_ERS \
     ocf:linbit:drbd \
     params drbd_resource="<b>NWS</b>_ers" \
     op monitor interval="15" role="Master" \
     op monitor interval="30" role="Slave"

   crm(live)configure# ms ms-drbd_<b>NWS</b>_ERS drbd_<b>NWS</b>_ERS \
     meta master-max="1" master-node-max="1" clone-max="2" \
     clone-node-max="1" notify="true"

   crm(live)configure# primitive fs_<b>NWS</b>_ERS \
     ocf:heartbeat:Filesystem \
     params device=/dev/drbd1 \
     directory=/usr/sap/<b>NWS</b>/ERS<b>02</b>  \
     fstype=xfs \
     op monitor interval="10s"

   crm(live)configure# primitive vip_<b>NWS</b>_ERS IPaddr2 \
     params ip=<b>10.0.0.11</b> cidr_netmask=24 \
     op monitor interval=10 timeout=20

   crm(live)configure# primitive nc_<b>NWS</b>_ERS anything \
    params binfile="/usr/bin/nc" cmdline_options="-l -k 621<b>02</b>" \
    op monitor timeout=20s interval=10 depth=0

   crm(live)configure# group g-<b>NWS</b>_ERS nc_<b>NWS</b>_ERS vip_<b>NWS</b>_ERS fs_<b>NWS</b>_ERS

   crm(live)configure# order o-<b>NWS</b>_drbd_before_ERS inf: \
     ms-drbd_<b>NWS</b>_ERS:promote g-<b>NWS</b>_ERS:start
   
   crm(live)configure# colocation col-<b>NWS</b>_ERS_on_drbd inf: \
     ms-drbd_<b>NWS</b>_ERS:Master g-<b>NWS</b>_ERS
   
   crm(live)configure# commit
   # WARNING: Resources nc_NWS_ASCS,nc_NWS_ERS,nc_NWS_nfs violate uniqueness for parameter "binfile": "/usr/bin/nc"
   # Do you still want toocommit (y/n)? y

   crm(live)configure# exit
   
   </code></pre>
 
   <span data-ttu-id="0749e-365">Upewnij się, że stan klastra hello jest prawidłowy i czy wszystkie zasoby są uruchomione.</span><span class="sxs-lookup"><span data-stu-id="0749e-365">Make sure that hello cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="0749e-366">Nie jest ważna zasobów hello węzeł, do których są uruchomione.</span><span class="sxs-lookup"><span data-stu-id="0749e-366">It is not important on which node hello resources are running.</span></span>

   <pre><code>
   sudo crm_mon -r

   # Node <b>nws-cl-0: standby</b>
   # <b>Online: [ nws-cl-1 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      Stopped: [ nws-cl-0 ]
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   #  Master/Slave Set: ms-drbd_NWS_ERS [drbd_NWS_ERS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      Stopped: [ nws-cl-0 ]
   #  Resource Group: g-NWS_ERS
   #      nc_NWS_ERS (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ERS        (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ERS (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   </code></pre>

1. <span data-ttu-id="0749e-367">**[2]**  Zainstalować SAP NetWeaver Wywołujących</span><span class="sxs-lookup"><span data-stu-id="0749e-367">**[2]** Install SAP NetWeaver ERS</span></span>  

   <span data-ttu-id="0749e-368">Instalowanie programu SAP NetWeaver Wywołujących jako główny na powitania drugiego węzła przy użyciu wirtualnego nazwy hosta, na przykład mapująca adres IP toohello hello konfiguracji frontonu modułu równoważenia obciążenia dla hello Wywołujących <b>wywołujących nws</b>, <b>10.0.0.11</b> i numer wystąpienia hello używanej hello sondę modułu równoważenia obciążenia hello na przykład <b>02</b>.</span><span class="sxs-lookup"><span data-stu-id="0749e-368">Install SAP NetWeaver ERS as root on hello second node using a virtual hostname that maps toohello IP address of hello load balancer frontend configuration for hello ERS for example <b>nws-ers</b>, <b>10.0.0.11</b> and hello instance number that you used for hello probe of hello load balancer for example <b>02</b>.</span></span>

   <span data-ttu-id="0749e-369">Można użyć hello sapinst parametru SAPINST_REMOTE_ACCESS_USER tooallow toosapinst tooconnect użytkownika z systemem innym niż root.</span><span class="sxs-lookup"><span data-stu-id="0749e-369">You can use hello sapinst parameter SAPINST_REMOTE_ACCESS_USER tooallow a non-root user tooconnect toosapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

   > [!NOTE]
   > <span data-ttu-id="0749e-370">Użyj PL SP 20 SWPM 05 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="0749e-370">Please use SWPM SP 20 PL 05 or higher.</span></span> <span data-ttu-id="0749e-371">Niższych wersjach nie należy ustawiać uprawnienia hello poprawnie i hello instalacja zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="0749e-371">Lower versions do not set hello permissions correctly and hello installation will fail.</span></span>
   > 

1. <span data-ttu-id="0749e-372">**[1]**  Dostosowanie profile hello ASCS/SCS i Wywołujących wystąpienia</span><span class="sxs-lookup"><span data-stu-id="0749e-372">**[1]** Adapt hello ASCS/SCS and ERS instance profiles</span></span>
 
   * <span data-ttu-id="0749e-373">ASCS/SCS profilu</span><span class="sxs-lookup"><span data-stu-id="0749e-373">ASCS/SCS profile</span></span>

   <pre><code> 
   sudo vi /sapmnt/<b>NWS</b>/profile/<b>NWS</b>_<b>ASCS00</b>_<b>nws-ascs</b>

   # Change hello restart command tooa start command
   #Restart_Program_01 = local $(_EN) pf=$(_PF)
   Start_Program_01 = local $(_EN) pf=$(_PF)

   # Add hello following lines
   service/halib = $(DIR_CT_RUN)/saphascriptco.so
   service/halib_cluster_connector = /usr/bin/sap_suse_cluster_connector

   # Add hello keep alive parameter
   enque/encni/set_so_keepalive = true
   </code></pre>

   * <span data-ttu-id="0749e-374">Profil Wywołujących</span><span class="sxs-lookup"><span data-stu-id="0749e-374">ERS profile</span></span>

   <pre><code> 
   sudo vi /sapmnt/<b>NWS</b>/profile/<b>NWS</b>_ERS<b>02</b>_<b>nws-ers</b>

   # Add hello following lines
   service/halib = $(DIR_CT_RUN)/saphascriptco.so
   service/halib_cluster_connector = /usr/bin/sap_suse_cluster_connector
   </code></pre>


1. <span data-ttu-id="0749e-375">**[A]**  Skonfigurować podtrzymanie aktywności</span><span class="sxs-lookup"><span data-stu-id="0749e-375">**[A]** Configure Keep Alive</span></span>

   <span data-ttu-id="0749e-376">Witaj komunikacji między serwera aplikacji hello SAP NetWeaver i hello ASCS/SCS jest kierowany przez programowy moduł równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="0749e-376">hello communication between hello SAP NetWeaver application server and hello ASCS/SCS is routed through a software load balancer.</span></span> <span data-ttu-id="0749e-377">usługi równoważenia obciążenia Hello rozłącza nieaktywne połączenia po upływie limitu czasu w można skonfigurować.</span><span class="sxs-lookup"><span data-stu-id="0749e-377">hello load balancer disconnects inactive connections after a configurable timeout.</span></span> <span data-ttu-id="0749e-378">tooprevent to należy tooset parametru w hello SAP NetWeaver ASCS/SCS profilu i zmiany ustawień systemu Linux hello.</span><span class="sxs-lookup"><span data-stu-id="0749e-378">tooprevent this you need tooset a parameter in hello SAP NetWeaver ASCS/SCS profile and change hello Linux system settings.</span></span> <span data-ttu-id="0749e-379">Przeczytaj [1410736 Uwaga SAP] [ 1410736] Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="0749e-379">Please read [SAP Note 1410736][1410736] for more information.</span></span>
   
   <span data-ttu-id="0749e-380">Witaj ASCS/SCS profilu parametru umieścić/encni/set_so_keepalive został już dodany w ostatnim kroku hello.</span><span class="sxs-lookup"><span data-stu-id="0749e-380">hello ASCS/SCS profile parameter enque/encni/set_so_keepalive was already added in hello last step.</span></span>

   <pre><code> 
   # Change hello Linux system configuration
   sudo sysctl net.ipv4.tcp_keepalive_time=120
   </code></pre>

1. <span data-ttu-id="0749e-381">**[A]**  Po instalacji hello skonfigurować hello SAP użytkowników</span><span class="sxs-lookup"><span data-stu-id="0749e-381">**[A]** Configure hello SAP users after hello installation</span></span>
 
   <pre><code>
   # Add sidadm toohello haclient group
   sudo usermod -aG haclient <b>nws</b>adm   
   </code></pre>

1. <span data-ttu-id="0749e-382">**[1]**  Dodaj hello ASCS i SAP Wywołujących toohello sapservice pliku usług</span><span class="sxs-lookup"><span data-stu-id="0749e-382">**[1]** Add hello ASCS and ERS SAP services toohello sapservice file</span></span>

   <span data-ttu-id="0749e-383">Dodaj hello ASCS usługi wpis toohello drugiego węzła i kopiowania hello Wywołujących wpis toohello pierwszego węzła usługi.</span><span class="sxs-lookup"><span data-stu-id="0749e-383">Add hello ASCS service entry toohello second node and copy hello ERS service entry toohello first node.</span></span>

   <pre><code>
   cat /usr/sap/sapservices | grep ASCS<b>00</b> | sudo ssh <b>nws-cl-1</b> "cat >>/usr/sap/sapservices"
   sudo ssh <b>nws-cl-1</b> "cat /usr/sap/sapservices" | grep ERS<b>02</b> | sudo tee -a /usr/sap/sapservices
   </code></pre>

1. <span data-ttu-id="0749e-384">**[1]**  Utworzenie zasobów klastra SAP hello</span><span class="sxs-lookup"><span data-stu-id="0749e-384">**[1]** Create hello SAP cluster resources</span></span>

   <pre><code>
   sudo crm configure property maintenance-mode="true"

   sudo crm configure

   crm(live)configure# primitive rsc_sap_<b>NWS</b>_ASCS<b>00</b> SAPInstance \
    operations $id=rsc_sap_<b>NWS</b>_ASCS<b>00</b>-operations \
    op monitor interval=11 timeout=60 on_fail=restart \
    params InstanceName=<b>NWS</b>_ASCS<b>00</b>_<b>nws-ascs</b> START_PROFILE="/sapmnt/<b>NWS</b>/profile/<b>NWS</b>_ASCS<b>00</b>_<b>nws-ascs</b>" \
    AUTOMATIC_RECOVER=false \
    meta resource-stickiness=5000 failure-timeout=60 migration-threshold=1 priority=10

   crm(live)configure# primitive rsc_sap_<b>NWS</b>_ERS<b>02</b> SAPInstance \
    operations $id=rsc_sap_<b>NWS</b>_ERS<b>02</b>-operations \
    op monitor interval=11 timeout=60 on_fail=restart \
    params InstanceName=<b>NWS</b>_ERS<b>02</b>_<b>nws-ers</b> START_PROFILE="/sapmnt/<b>NWS</b>/profile/<b>NWS</b>_ERS<b>02</b>_<b>nws-ers</b>" AUTOMATIC_RECOVER=false IS_ERS=true \
    meta priority=1000

   crm(live)configure# modgroup g-<b>NWS</b>_ASCS add rsc_sap_<b>NWS</b>_ASCS<b>00</b>
   crm(live)configure# modgroup g-<b>NWS</b>_ERS add rsc_sap_<b>NWS</b>_ERS<b>02</b>

   crm(live)configure# colocation col_sap_<b>NWS</b>_no_both -5000: g-<b>NWS</b>_ERS g-<b>NWS</b>_ASCS
   crm(live)configure# location loc_sap_<b>NWS</b>_failover_to_ers rsc_sap_<b>NWS</b>_ASCS<b>00</b> rule 2000: runs_ers_<b>NWS</b> eq 1
   crm(live)configure# order ord_sap_<b>NWS</b>_first_start_ascs Optional: rsc_sap_<b>NWS</b>_ASCS<b>00</b>:start rsc_sap_<b>NWS</b>_ERS<b>02</b>:stop symmetrical=false

   crm(live)configure# commit
   crm(live)configure# exit

   sudo crm configure property maintenance-mode="false"
   sudo crm node online <b>nws-cl-0</b>
   </code></pre>

   <span data-ttu-id="0749e-385">Upewnij się, że stan klastra hello jest prawidłowy i czy wszystkie zasoby są uruchomione.</span><span class="sxs-lookup"><span data-stu-id="0749e-385">Make sure that hello cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="0749e-386">Nie jest ważna zasobów hello węzeł, do których są uruchomione.</span><span class="sxs-lookup"><span data-stu-id="0749e-386">It is not important on which node hello resources are running.</span></span>

   <pre><code>
   sudo crm_mon -r

   # Online: <b>[ nws-cl-0 nws-cl-1 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      <b>Slaves: [ nws-cl-1 ]</b>
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-0</b>
   #      rsc_sap_NWS_ASCS00 (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-0</b>
   #  Master/Slave Set: ms-drbd_NWS_ERS [drbd_NWS_ERS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      <b>Slaves: [ nws-cl-0 ]</b>
   #  Resource Group: g-NWS_ERS
   #      nc_NWS_ERS (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ERS        (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ERS (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   #      rsc_sap_NWS_ERS02  (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-1</b>
   </code></pre>

### <a name="create-stonith-device"></a><span data-ttu-id="0749e-387">Utwórz urządzenie STONITH</span><span class="sxs-lookup"><span data-stu-id="0749e-387">Create STONITH device</span></span>

<span data-ttu-id="0749e-388">Witaj STONITH urządzenie używa nazwy głównej usługi tooauthorize przed Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="0749e-388">hello STONITH device uses a Service Principal tooauthorize against Microsoft Azure.</span></span> <span data-ttu-id="0749e-389">Wykonaj te kroki toocreate nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="0749e-389">Follow these steps toocreate a Service Principal.</span></span>

1. <span data-ttu-id="0749e-390">Przejdź do zbyt<https://portal.azure.com></span><span class="sxs-lookup"><span data-stu-id="0749e-390">Go too<https://portal.azure.com></span></span>
1. <span data-ttu-id="0749e-391">Otwórz hello bloku usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0749e-391">Open hello Azure Active Directory blade</span></span>  
   <span data-ttu-id="0749e-392">Przejdź tooProperties i zanotuj hello identyfikator katalogu. Jest to hello **identyfikator dzierżawcy**.</span><span class="sxs-lookup"><span data-stu-id="0749e-392">Go tooProperties and write down hello Directory Id. This is hello **tenant id**.</span></span>
1. <span data-ttu-id="0749e-393">Kliknij przycisk rejestracji aplikacji</span><span class="sxs-lookup"><span data-stu-id="0749e-393">Click App registrations</span></span>
1. <span data-ttu-id="0749e-394">Kliknij pozycję Dodaj.</span><span class="sxs-lookup"><span data-stu-id="0749e-394">Click Add</span></span>
1. <span data-ttu-id="0749e-395">Wprowadź nazwę, wybierz typ aplikacji "Aplikacja/interfejs API sieci Web", wprowadź adres URL logowania (np. http://localhost) i kliknij przycisk Utwórz</span><span class="sxs-lookup"><span data-stu-id="0749e-395">Enter a Name, select Application Type "Web app/API", enter a sign-on URL (for example http://localhost) and click Create</span></span>
1. <span data-ttu-id="0749e-396">Witaj adres URL logowania nie jest używany i może być dowolny prawidłowy adres URL</span><span class="sxs-lookup"><span data-stu-id="0749e-396">hello sign-on URL is not used and can be any valid URL</span></span>
1. <span data-ttu-id="0749e-397">Wybierz hello nowej aplikacji i kliknij na karcie Ustawienia hello</span><span class="sxs-lookup"><span data-stu-id="0749e-397">Select hello new App and click Keys in hello Settings tab</span></span>
1. <span data-ttu-id="0749e-398">Wprowadź opis nowego klucza, wybierz pozycję "Nigdy nie wygasa" i kliknij przycisk Zapisz</span><span class="sxs-lookup"><span data-stu-id="0749e-398">Enter a description for a new key, select "Never expires" and click Save</span></span>
1. <span data-ttu-id="0749e-399">Zapisz hello wartość.</span><span class="sxs-lookup"><span data-stu-id="0749e-399">Write down hello Value.</span></span> <span data-ttu-id="0749e-400">Jest on używany jako hello **hasło** dla hello nazwy głównej usługi</span><span class="sxs-lookup"><span data-stu-id="0749e-400">It is used as hello **password** for hello Service Principal</span></span>
1. <span data-ttu-id="0749e-401">Zapisz hello identyfikator aplikacji. Jest używany jako hello username (**identyfikatora** w poniższych krokach hello) z hello nazwy głównej usługi</span><span class="sxs-lookup"><span data-stu-id="0749e-401">Write down hello Application Id. It is used as hello username (**login id** in hello steps below) of hello Service Principal</span></span>

<span data-ttu-id="0749e-402">Witaj nazwy głównej usługi nie ma uprawnienia tooaccess zasobów platformy Azure domyślnie.</span><span class="sxs-lookup"><span data-stu-id="0749e-402">hello Service Principal does not have permissions tooaccess your Azure resources by default.</span></span> <span data-ttu-id="0749e-403">Należy toogive hello nazwy głównej usługi uprawnienia toostart i Zatrzymaj (deallocate) wszystkich maszyn wirtualnych klastra hello.</span><span class="sxs-lookup"><span data-stu-id="0749e-403">You need toogive hello Service Principal permissions toostart and stop (deallocate) all virtual machines of hello cluster.</span></span>

1. <span data-ttu-id="0749e-404">Przejdź toohttps://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="0749e-404">Go toohttps://portal.azure.com</span></span>
1. <span data-ttu-id="0749e-405">Otwórz hello wszystkich bloku zasobów</span><span class="sxs-lookup"><span data-stu-id="0749e-405">Open hello All resources blade</span></span>
1. <span data-ttu-id="0749e-406">Wybierz maszynę wirtualną hello</span><span class="sxs-lookup"><span data-stu-id="0749e-406">Select hello virtual machine</span></span>
1. <span data-ttu-id="0749e-407">Kliknij przycisk kontroli dostępu (IAM)</span><span class="sxs-lookup"><span data-stu-id="0749e-407">Click Access control (IAM)</span></span>
1. <span data-ttu-id="0749e-408">Kliknij pozycję Dodaj.</span><span class="sxs-lookup"><span data-stu-id="0749e-408">Click Add</span></span>
1. <span data-ttu-id="0749e-409">Wybierz rolę hello właściciela</span><span class="sxs-lookup"><span data-stu-id="0749e-409">Select hello role Owner</span></span>
1. <span data-ttu-id="0749e-410">Wprowadź nazwę hello aplikacji hello utworzone powyżej</span><span class="sxs-lookup"><span data-stu-id="0749e-410">Enter hello name of hello application you created above</span></span>
1. <span data-ttu-id="0749e-411">Kliknij przycisk OK</span><span class="sxs-lookup"><span data-stu-id="0749e-411">Click OK</span></span>

#### <a name="1-create-hello-stonith-devices"></a><span data-ttu-id="0749e-412">**[1]**  Utworzyć hello STONITH urządzeń</span><span class="sxs-lookup"><span data-stu-id="0749e-412">**[1]** Create hello STONITH devices</span></span>

<span data-ttu-id="0749e-413">Po edytować uprawnienia hello hello maszyn wirtualnych, możesz skonfigurować urządzenia STONITH hello hello klastra.</span><span class="sxs-lookup"><span data-stu-id="0749e-413">After you edited hello permissions for hello virtual machines, you can configure hello STONITH devices in hello cluster.</span></span>

<pre><code>
sudo crm configure

# replace hello bold string with your subscription id, resource group, tenant id, service principal id and password

crm(live)configure# primitive rsc_st_azure_1 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# primitive rsc_st_azure_2 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started

crm(live)configure# commit
crm(live)configure# exit
</code></pre>

#### <a name="1-enable-hello-use-of-a-stonith-device"></a><span data-ttu-id="0749e-414">**[1]**  Zezwalaj na używanie hello urządzenia STONITH</span><span class="sxs-lookup"><span data-stu-id="0749e-414">**[1]** Enable hello use of a STONITH device</span></span>

<span data-ttu-id="0749e-415">Zezwalaj na używanie hello urządzenia STONITH</span><span class="sxs-lookup"><span data-stu-id="0749e-415">Enable hello use of a STONITH device</span></span>

<pre><code>
sudo crm configure property stonith-enabled=true 
</code></pre>

## <a name="install-database"></a><span data-ttu-id="0749e-416">Instalowanie bazy danych</span><span class="sxs-lookup"><span data-stu-id="0749e-416">Install database</span></span>

<span data-ttu-id="0749e-417">W tym przykładzie replikacji systemu SAP HANA jest zainstalowana i skonfigurowana.</span><span class="sxs-lookup"><span data-stu-id="0749e-417">In this example an SAP HANA System Replication is installed and configured.</span></span> <span data-ttu-id="0749e-418">SAP HANA będą uruchamiane w hello sam klastra jako hello SAP NetWeaver ASCS/SCS i Wywołujących.</span><span class="sxs-lookup"><span data-stu-id="0749e-418">SAP HANA will run in hello same cluster as hello SAP NetWeaver ASCS/SCS and ERS.</span></span> <span data-ttu-id="0749e-419">W dedykowanym klastrze, można także zainstalować SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="0749e-419">You can also install SAP HANA on a dedicated cluster.</span></span> <span data-ttu-id="0749e-420">Zobacz [dostępności wysokiej programu SAP HANA na maszynach wirtualnych Azure (VM)] [ sap-hana-ha] Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="0749e-420">See [High Availability of SAP HANA on Azure Virtual Machines (VMs)][sap-hana-ha] for more information.</span></span>

### <a name="prepare-for-sap-hana-installation"></a><span data-ttu-id="0749e-421">Przygotowanie do instalacji SAP HANA</span><span class="sxs-lookup"><span data-stu-id="0749e-421">Prepare for SAP HANA installation</span></span>

<span data-ttu-id="0749e-422">Ogólnie zaleca LVM dla woluminów, które przechowują dane i pliki dziennika.</span><span class="sxs-lookup"><span data-stu-id="0749e-422">We generally recommend using LVM for volumes that store data and log files.</span></span> <span data-ttu-id="0749e-423">Do celów testowych można również toostore pliku danych i dziennika hello bezpośrednio na niezaszyfrowanym dysku.</span><span class="sxs-lookup"><span data-stu-id="0749e-423">For testing purposes, you can also choose toostore hello data and log file directly on a plain disk.</span></span>

1. <span data-ttu-id="0749e-424">**[A]**  LVM</span><span class="sxs-lookup"><span data-stu-id="0749e-424">**[A]** LVM</span></span>  
   <span data-ttu-id="0749e-425">w poniższym przykładzie Hello założenia, że maszyny wirtualne hello czterech dyskach danych dołączonych, które powinny być używane toocreate dwa woluminy.</span><span class="sxs-lookup"><span data-stu-id="0749e-425">hello example below assumes that hello virtual machines have four data disks attached that should be used toocreate two volumes.</span></span>
   
   <span data-ttu-id="0749e-426">Utwórz woluminy fizyczne dla wszystkich dysków, które mają toouse.</span><span class="sxs-lookup"><span data-stu-id="0749e-426">Create physical volumes for all disks that you want toouse.</span></span>
   
   <pre><code>
   sudo pvcreate /dev/sdd
   sudo pvcreate /dev/sde
   sudo pvcreate /dev/sdf
   sudo pvcreate /dev/sdg
   </code></pre>
   
   <span data-ttu-id="0749e-427">Utwórz grupę woluminu hello plików danych, jedna grupa woluminu dla plików dziennika hello i jeden dla udostępnionego katalogu hello SAP HANA</span><span class="sxs-lookup"><span data-stu-id="0749e-427">Create a volume group for hello data files, one volume group for hello log files and one for hello shared directory of SAP HANA</span></span>
   
   <pre><code>
   sudo vgcreate vg_hana_data /dev/sdd /dev/sde
   sudo vgcreate vg_hana_log /dev/sdf
   sudo vgcreate vg_hana_shared /dev/sdg
   </code></pre>
   
   <span data-ttu-id="0749e-428">Utwórz hello woluminy logiczne</span><span class="sxs-lookup"><span data-stu-id="0749e-428">Create hello logical volumes</span></span>
   
   <pre><code>
   sudo lvcreate -l 100%FREE -n hana_data vg_hana_data
   sudo lvcreate -l 100%FREE -n hana_log vg_hana_log
   sudo lvcreate -l 100%FREE -n hana_shared vg_hana_shared
   sudo mkfs.xfs /dev/vg_hana_data/hana_data
   sudo mkfs.xfs /dev/vg_hana_log/hana_log
   sudo mkfs.xfs /dev/vg_hana_shared/hana_shared
   </code></pre>
   
   <span data-ttu-id="0749e-429">Utwórz katalogi instalacji hello i skopiuj hello UUID wszystkich woluminów logicznych</span><span class="sxs-lookup"><span data-stu-id="0749e-429">Create hello mount directories and copy hello UUID of all logical volumes</span></span>
   
   <pre><code>
   sudo mkdir -p /hana/data
   sudo mkdir -p /hana/log
   sudo mkdir -p /hana/shared
   sudo chattr +i /hana/data
   sudo chattr +i /hana/log
   sudo chattr +i /hana/shared
   # write down hello id of /dev/vg_hana_data/hana_data, /dev/vg_hana_log/hana_log and /dev/vg_hana_shared/hana_shared
   sudo blkid
   </code></pre>
   
   <span data-ttu-id="0749e-430">Utwórz wpisy autofs hello trzy logiczne woluminy</span><span class="sxs-lookup"><span data-stu-id="0749e-430">Create autofs entries for hello three logical volumes</span></span>
   
   <pre><code>
   sudo vi /etc/auto.direct
   </code></pre>
   
   <span data-ttu-id="0749e-431">Wstaw ten wiersz toosudo vi /etc/auto.direct</span><span class="sxs-lookup"><span data-stu-id="0749e-431">Insert this line toosudo vi /etc/auto.direct</span></span>
   
   <pre><code>
   /hana/data -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_data/hana_data&gt;</b>
   /hana/log -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_log/hana_log&gt;</b>
   /hana/shared -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_shared/hana_shared&gt;</b>
   </code></pre>
   
   <span data-ttu-id="0749e-432">Zainstaluj nowe woluminy hello</span><span class="sxs-lookup"><span data-stu-id="0749e-432">Mount hello new volumes</span></span>
   
   <pre><code>
   sudo service autofs restart 
   </code></pre>

1. <span data-ttu-id="0749e-433">**[A]**  Zwykłych dysków</span><span class="sxs-lookup"><span data-stu-id="0749e-433">**[A]** Plain Disks</span></span>  

   <span data-ttu-id="0749e-434">Dla małych lub demonstracyjnych systemów, możesz umieścić HANA plików danych i dziennika na jednym dysku.</span><span class="sxs-lookup"><span data-stu-id="0749e-434">For small or demo systems, you can place your HANA data and log files on one disk.</span></span> <span data-ttu-id="0749e-435">Witaj następujące polecenia utworzyć partycję na /dev/sdc i sformatuj go przy xfs.</span><span class="sxs-lookup"><span data-stu-id="0749e-435">hello following commands create a partition on /dev/sdc and format it with xfs.</span></span>
   ```bash
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdd'
   sudo mkfs.xfs /dev/sdd1
   
   # write down hello id of /dev/sdd1
   sudo /sbin/blkid
   sudo vi /etc/auto.direct
   ```
   
   <span data-ttu-id="0749e-436">Wstaw ten too/etc/auto.direct wiersza</span><span class="sxs-lookup"><span data-stu-id="0749e-436">Insert this line too/etc/auto.direct</span></span>
   <pre><code>
   /hana -fstype=xfs :UUID=<b>&lt;UUID&gt;</b>
   </code></pre>
   
   <span data-ttu-id="0749e-437">Utwórz katalog docelowy hello i zainstalować dysk hello.</span><span class="sxs-lookup"><span data-stu-id="0749e-437">Create hello target directory and mount hello disk.</span></span>
   
   <pre><code>
   sudo mkdir /hana
   sudo chattr +i /hana
   sudo service autofs restart
   </code></pre>

### <a name="installing-sap-hana"></a><span data-ttu-id="0749e-438">Instalowanie programu SAP HANA</span><span class="sxs-lookup"><span data-stu-id="0749e-438">Installing SAP HANA</span></span>

<span data-ttu-id="0749e-439">Witaj poniższe kroki są oparte na rozdział 4 hello [przewodnik SAP HANA SR wydajności zoptymalizowanych pod kątem scenariusza] [ suse-hana-ha-guide] tooinstall replikacji systemu SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="0749e-439">hello following steps are based on chapter 4 of hello [SAP HANA SR Performance Optimized Scenario guide][suse-hana-ha-guide] tooinstall SAP HANA System Replication.</span></span> <span data-ttu-id="0749e-440">Przeczytaj go przed kontynuowaniem instalacji hello.</span><span class="sxs-lookup"><span data-stu-id="0749e-440">Please read it before you continue hello installation.</span></span>

1. <span data-ttu-id="0749e-441">**[A]**  Uruchom hdblcm z hello HANA DVD</span><span class="sxs-lookup"><span data-stu-id="0749e-441">**[A]** Run hdblcm from hello HANA DVD</span></span>
   
   <pre><code>
   sudo hdblcm --sid=<b>HDB</b> --number=<b>03</b> --action=install --batch --password=<b>&lt;password&gt;</b> --system_user_password=<b>&lt;password for system user&gt;</b>

   sudo /hana/shared/<b>HDB</b>/hdblcm/hdblcm --action=configure_internal_network --listen_interface=internal --internal_network=<b>10.0.0/24</b> --password=<b>&lt;password for system user&gt;</b> --batch
   </code></pre>

1. <span data-ttu-id="0749e-442">**[A]**  Uaktualnij agenta hosta SAP</span><span class="sxs-lookup"><span data-stu-id="0749e-442">**[A]** Upgrade SAP Host Agent</span></span>

   <span data-ttu-id="0749e-443">Pobierz najnowsze archiwum Agent hosta SAP hello z hello [SAP Softwarecenter] [ sap-swcenter] i uruchom hello następujące polecenia tooupgrade hello agenta.</span><span class="sxs-lookup"><span data-stu-id="0749e-443">Download hello latest SAP Host Agent archive from hello [SAP Softwarecenter][sap-swcenter] and run hello following command tooupgrade hello agent.</span></span> <span data-ttu-id="0749e-444">Zastąp hello ścieżki toohello archiwum toopoint toohello pobranego pliku.</span><span class="sxs-lookup"><span data-stu-id="0749e-444">Replace hello path toohello archive toopoint toohello file you downloaded.</span></span>
   <pre><code>
   sudo /usr/sap/hostctrl/exe/saphostexec -upgrade -archive <b>&lt;path tooSAP Host Agent SAR&gt;</b> 
   </code></pre>

1. <span data-ttu-id="0749e-445">**[1]**  Utworzyć HANA replikacji (jako główny)</span><span class="sxs-lookup"><span data-stu-id="0749e-445">**[1]** Create HANA replication (as root)</span></span>  

   <span data-ttu-id="0749e-446">Uruchom następujące polecenie hello.</span><span class="sxs-lookup"><span data-stu-id="0749e-446">Run hello following command.</span></span> <span data-ttu-id="0749e-447">Upewnij się, że tooreplace bold ciągów (HANA systemu identyfikator HDB i numer wystąpienia 03) wartościami hello instalacji SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="0749e-447">Make sure tooreplace bold strings (HANA System ID HDB and instance number 03) with hello values of your SAP HANA installation.</span></span>
   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbsql -u system -i <b>03</b> 'CREATE USER <b>hdb</b>hasync PASSWORD "<b>passwd</b>"' 
   hdbsql -u system -i <b>03</b> 'GRANT DATA ADMIN too<b>hdb</b>hasync' 
   hdbsql -u system -i <b>03</b> 'ALTER USER <b>hdb</b>hasync DISABLE PASSWORD LIFETIME' 
   </code></pre>

1. <span data-ttu-id="0749e-448">**[A]**  Tworzenie magazynu kluczy wpis (root)</span><span class="sxs-lookup"><span data-stu-id="0749e-448">**[A]** Create keystore entry (as root)</span></span>

   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbuserstore SET <b>hdb</b>haloc localhost:3<b>03</b>15 <b>hdb</b>hasync <b>&lt;passwd&gt;</b>
   </code></pre>

1. <span data-ttu-id="0749e-449">**[1]**  Kopii zapasowej bazy danych (root)</span><span class="sxs-lookup"><span data-stu-id="0749e-449">**[1]** Backup database (as root)</span></span>

   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbsql -u system -i <b>03</b> "BACKUP DATA USING FILE ('<b>initialbackup</b>')" 
   </code></pre>

1. <span data-ttu-id="0749e-450">**[1]**  Przełącz użytkownika sapsid HANA toohello i utworzyć hello lokacji głównej.</span><span class="sxs-lookup"><span data-stu-id="0749e-450">**[1]** Switch toohello HANA sapsid user and create hello primary site.</span></span>

   <pre><code>
   su - <b>hdb</b>adm
   hdbnsutil -sr_enable –-name=<b>SITE1</b>
   </code></pre>

1. <span data-ttu-id="0749e-451">**[2]**  Przełącz użytkownika sapsid HANA toohello i utworzyć lokację dodatkową hello.</span><span class="sxs-lookup"><span data-stu-id="0749e-451">**[2]** Switch toohello HANA sapsid user and create hello secondary site.</span></span>

   <pre><code>
   su - <b>hdb</b>adm
   sapcontrol -nr <b>03</b> -function StopWait 600 10
   hdbnsutil -sr_register --remoteHost=<b>nws-cl-0</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE2</b> 
   </code></pre>

1. <span data-ttu-id="0749e-452">**[1]**  Utworzyć SAP HANA zasobów klastra</span><span class="sxs-lookup"><span data-stu-id="0749e-452">**[1]** Create SAP HANA cluster resources</span></span>

   <span data-ttu-id="0749e-453">Najpierw utwórz hello topologii.</span><span class="sxs-lookup"><span data-stu-id="0749e-453">First, create hello topology.</span></span>
   
   <pre><code>
   sudo crm configure

   # replace hello bold string with your instance number and HANA system id
   
   crm(live)configure# primitive rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b>   ocf:suse:SAPHanaTopology \
     operations $id="rsc_sap2_<b>HDB</b>_HDB<b>03</b>-operations" \
     op monitor interval="10" timeout="600" \
     op start interval="0" timeout="600" \
     op stop interval="0" timeout="300" \
     params SID="<b>HDB</b>" InstanceNumber="<b>03</b>"
    
   crm(live)configure# clone cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \
     meta is-managed="true" clone-node-max="1" target-role="Started" interleave="true"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>
   
   <span data-ttu-id="0749e-454">Następnie należy utworzyć hello HANA zasobów</span><span class="sxs-lookup"><span data-stu-id="0749e-454">Next, create hello HANA resources</span></span>
   
   <pre><code>
   sudo crm configure

   # replace hello bold string with your instance number, HANA system id and hello frontend IP address of hello Azure load balancer. 
    
   crm(live)configure# primitive rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> ocf:suse:SAPHana \
     operations $id="rsc_sap_<b>HDB</b>_HDB<b>03</b>-operations" \
     op start interval="0" timeout="3600" \
     op stop interval="0" timeout="3600" \
     op promote interval="0" timeout="3600" \
     op monitor interval="60" role="Master" timeout="700" \
     op monitor interval="61" role="Slave" timeout="700" \
     params SID="<b>HDB</b>" InstanceNumber="<b>03</b>" PREFER_SITE_TAKEOVER="true" \
     DUPLICATE_PRIMARY_TIMEOUT="7200" AUTOMATED_REGISTER="false"
    
   crm(live)configure# ms msl_SAPHana_<b>HDB</b>_HDB<b>03</b> rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> \
     meta is-managed="true" notify="true" clone-max="2" clone-node-max="1" \
     target-role="Started" interleave="true"
    
   crm(live)configure# primitive rsc_ip_<b>HDB</b>_HDB<b>03</b> ocf:heartbeat:IPaddr2 \ 
     meta target-role="Started" is-managed="true" \ 
     operations $id="rsc_ip_<b>HDB</b>_HDB<b>03</b>-operations" \ 
     op monitor interval="10s" timeout="20s" \ 
     params ip="<b>10.0.0.12</b>" 

   crm(live)configure# primitive rsc_nc_<b>HDB</b>_HDB<b>03</b> anything \ 
     params binfile="/usr/bin/nc" cmdline_options="-l -k 625<b>03</b>" \ 
     op monitor timeout=20s interval=10 depth=0 

   crm(live)configure# group g_ip_<b>HDB</b>_HDB<b>03</b> rsc_ip_<b>HDB</b>_HDB<b>03</b> rsc_nc_<b>HDB</b>_HDB<b>03</b>
    
   crm(live)configure# colocation col_saphana_ip_<b>HDB</b>_HDB<b>03</b> 2000: g_ip_<b>HDB</b>_HDB<b>03</b>:Started \ 
     msl_SAPHana_<b>HDB</b>_HDB<b>03</b>:Master  

   crm(live)configure# order ord_SAPHana_<b>HDB</b>_HDB<b>03</b> 2000: cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \ 
     msl_SAPHana_<b>HDB</b>_HDB<b>03</b>
    
   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

   <span data-ttu-id="0749e-455">Upewnij się, że stan klastra hello jest prawidłowy i czy wszystkie zasoby są uruchomione.</span><span class="sxs-lookup"><span data-stu-id="0749e-455">Make sure that hello cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="0749e-456">Nie jest ważna zasobów hello węzeł, do których są uruchomione.</span><span class="sxs-lookup"><span data-stu-id="0749e-456">It is not important on which node hello resources are running.</span></span>

   <pre><code>
   sudo crm_mon -r

   # <b>Online: [ nws-cl-0 nws-cl-1 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      <b>Slaves: [ nws-cl-0 ]</b>
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   #      rsc_sap_NWS_ASCS00 (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-1</b>
   #  Master/Slave Set: ms-drbd_NWS_ERS [drbd_NWS_ERS]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      <b>Slaves: [ nws-cl-1 ]</b>
   #  Resource Group: g-NWS_ERS
   #      nc_NWS_ERS (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   #      vip_NWS_ERS        (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      fs_NWS_ERS (ocf::heartbeat:Filesystem):    <b>Started nws-cl-0</b>
   #      rsc_sap_NWS_ERS02  (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-0</b>
   #  Clone Set: cln_SAPHanaTopology_HDB_HDB03 [rsc_SAPHanaTopology_HDB_HDB03]
   #      <b>Started: [ nws-cl-0 nws-cl-1 ]</b>
   #  Master/Slave Set: msl_SAPHana_HDB_HDB03 [rsc_SAPHana_HDB_HDB03]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      <b>Slaves: [ nws-cl-1 ]</b>
   #  Resource Group: g_ip_HDB_HDB03
   #      rsc_ip_HDB_HDB03   (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      rsc_nc_HDB_HDB03   (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   # rsc_st_azure_1  (stonith:fence_azure_arm):      <b>Started nws-cl-0</b>
   # rsc_st_azure_2  (stonith:fence_azure_arm):      <b>Started nws-cl-1</b>
   </code></pre>

1. <span data-ttu-id="0749e-457">**[1]**  Wystąpienie bazy danych SAP NetWeaver hello instalacji</span><span class="sxs-lookup"><span data-stu-id="0749e-457">**[1]** Install hello SAP NetWeaver database instance</span></span>

   <span data-ttu-id="0749e-458">Wystąpienie bazy danych SAP NetWeaver hello instalacji jako główny przy użyciu wirtualnego nazwy hosta, na przykład mapująca adres IP toohello konfiguracji frontonu modułu równoważenia obciążenia hello hello bazy danych <b>nws-db</b> i <b>10.0.0.12</b>.</span><span class="sxs-lookup"><span data-stu-id="0749e-458">Install hello SAP NetWeaver database instance as root using a virtual hostname that maps toohello IP address of hello load balancer frontend configuration for hello database for example <b>nws-db</b> and <b>10.0.0.12</b>.</span></span>

   <span data-ttu-id="0749e-459">Można użyć hello sapinst parametru SAPINST_REMOTE_ACCESS_USER tooallow toosapinst tooconnect użytkownika z systemem innym niż root.</span><span class="sxs-lookup"><span data-stu-id="0749e-459">You can use hello sapinst parameter SAPINST_REMOTE_ACCESS_USER tooallow a non-root user tooconnect toosapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

## <a name="sap-netweaver-application-server-installation"></a><span data-ttu-id="0749e-460">Instalacja serwera programu SAP NetWeaver aplikacji</span><span class="sxs-lookup"><span data-stu-id="0749e-460">SAP NetWeaver application server installation</span></span>

<span data-ttu-id="0749e-461">Wykonaj te kroki tooinstall SAP serwera aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0749e-461">Follow these steps tooinstall an SAP application server.</span></span> <span data-ttu-id="0749e-462">Hello poniższych kroków założono, zainstalowanie serwera aplikacji hello na serwerze innym niż hello ASCS/SCS i serwery HANA.</span><span class="sxs-lookup"><span data-stu-id="0749e-462">hello steps bellow assume that you install hello application server on a server different from hello ASCS/SCS and HANA servers.</span></span> <span data-ttu-id="0749e-463">W przeciwnym razie niektóre kroki hello poniżej (np. Konfigurowanie rozpoznawania nazwy hosta) nie są wymagane.</span><span class="sxs-lookup"><span data-stu-id="0749e-463">Otherwise some of hello steps below (like configuring host name resolution) are not needed.</span></span>

1. <span data-ttu-id="0749e-464">Ustawienia rozpoznawania nazwy hosta</span><span class="sxs-lookup"><span data-stu-id="0749e-464">Setup host name resolution</span></span>    
   <span data-ttu-id="0749e-465">Można użyć serwera DNS lub zmodyfikować hello/etc/hosts na wszystkich węzłach.</span><span class="sxs-lookup"><span data-stu-id="0749e-465">You can either use a DNS server or modify hello /etc/hosts on all nodes.</span></span> <span data-ttu-id="0749e-466">Ten przykład przedstawia, jak toouse hello plik/etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="0749e-466">This example shows how toouse hello /etc/hosts file.</span></span>
   <span data-ttu-id="0749e-467">Zastąpienie hello adresu IP i nazwy hosta hello w hello następujące polecenia</span><span class="sxs-lookup"><span data-stu-id="0749e-467">Replace hello IP address and hello hostname in hello following commands</span></span>
   ```bash
   sudo vi /etc/hosts
   ```
   <span data-ttu-id="0749e-468">Wstaw hello następujące wiersze zbyt/etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="0749e-468">Insert hello following lines too/etc/hosts.</span></span> <span data-ttu-id="0749e-469">Zmień toomatch adres i nazwę hosta IP hello środowiska</span><span class="sxs-lookup"><span data-stu-id="0749e-469">Change hello IP address and hostname toomatch your environment</span></span>    
    
   <pre><code>
   # IP address of hello load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ASCS/SCS
   <b>10.0.0.10 nws-ascs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ERS
   <b>10.0.0.11 nws-ers</b>
   # IP address of hello load balancer frontend configuration for database
   <b>10.0.0.12 nws-db</b>
   # IP address of hello application server
   <b>10.0.0.8 nws-di-0</b>
   </code></pre>

1. <span data-ttu-id="0749e-470">Utwórz katalog sapmnt hello</span><span class="sxs-lookup"><span data-stu-id="0749e-470">Create hello sapmnt directory</span></span>

   <pre><code>
   sudo mkdir -p /sapmnt/<b>NWS</b>
   sudo mkdir -p /usr/sap/trans

   sudo chattr +i /sapmnt/<b>NWS</b>
   sudo chattr +i /usr/sap/trans
   </code></pre>

1. <span data-ttu-id="0749e-471">Skonfiguruj autofs</span><span class="sxs-lookup"><span data-stu-id="0749e-471">Configure autofs</span></span>
 
   <pre><code>
   sudo vi /etc/auto.master

   # Add hello following line toohello file, save and exit
   +auto.master
   /- /etc/auto.direct
   </code></pre>

   <span data-ttu-id="0749e-472">Utwórz nowy plik o</span><span class="sxs-lookup"><span data-stu-id="0749e-472">Create a new file with</span></span>

   <pre><code>
   sudo vi /etc/auto.direct

   # Add hello following lines toohello file, save and exit
   /sapmnt/<b>NWS</b> -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sapmntsid
   /usr/sap/trans -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/trans
   </code></pre>

   <span data-ttu-id="0749e-473">Uruchom ponownie autofs toomount hello nowe udziały</span><span class="sxs-lookup"><span data-stu-id="0749e-473">Restart autofs toomount hello new shares</span></span>

   <pre><code>
   sudo systemctl enable autofs
   sudo service autofs restart
   </code></pre>

1. <span data-ttu-id="0749e-474">Konfigurowanie pliku wymiany</span><span class="sxs-lookup"><span data-stu-id="0749e-474">Configure SWAP file</span></span>
 
   <pre><code>
   sudo vi /etc/waagent.conf

   # Set hello property ResourceDisk.EnableSwap tooy
   # Create and use swapfile on resource disk.
   ResourceDisk.EnableSwap=<b>y</b>

   # Set hello size of hello SWAP file with property ResourceDisk.SwapSizeMB
   # hello free space of resource disk varies by virtual machine size. Make sure that you do not set a value that is too big. You can check hello SWAP space with command swapon
   # Size of hello swapfile.
   ResourceDisk.SwapSizeMB=<b>2000</b>
   </code></pre>

   <span data-ttu-id="0749e-475">Uruchom ponownie hello agenta tooactivate hello zmiany</span><span class="sxs-lookup"><span data-stu-id="0749e-475">Restart hello Agent tooactivate hello change</span></span>

   <pre><code>
   sudo service waagent restart
   </code></pre>

1. <span data-ttu-id="0749e-476">Instalowanie programu SAP NetWeaver serwera aplikacji</span><span class="sxs-lookup"><span data-stu-id="0749e-476">Install SAP NetWeaver application server</span></span>

   <span data-ttu-id="0749e-477">Zainstaluj serwer aplikacje SAP NetWeaver podstawowej lub dodatkowej.</span><span class="sxs-lookup"><span data-stu-id="0749e-477">Install a primary or additional SAP NetWeaver applications server.</span></span>

   <span data-ttu-id="0749e-478">Można użyć hello sapinst parametru SAPINST_REMOTE_ACCESS_USER tooallow toosapinst tooconnect użytkownika z systemem innym niż root.</span><span class="sxs-lookup"><span data-stu-id="0749e-478">You can use hello sapinst parameter SAPINST_REMOTE_ACCESS_USER tooallow a non-root user tooconnect toosapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

1. <span data-ttu-id="0749e-479">Aktualizacja SAP HANA bezpiecznego magazynu</span><span class="sxs-lookup"><span data-stu-id="0749e-479">Update SAP HANA secure store</span></span>

   <span data-ttu-id="0749e-480">Hello aktualizacji SAP HANA bezpiecznego magazynu toopoint toohello wirtualnego nazwa hello ustawień replikacji systemu SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="0749e-480">Update hello SAP HANA secure store toopoint toohello virtual name of hello SAP HANA System Replication setup.</span></span>
   <pre><code>
   su - <b>nws</b>adm
   hdbuserstore SET DEFAULT <b>nws-db</b>:3<b>03</b>15 <b>SAPABAP1</b> <b>&lt;password of ABAP schema&gt;</b>
   </code></pre>

## <a name="next-steps"></a><span data-ttu-id="0749e-481">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0749e-481">Next steps</span></span>
* <span data-ttu-id="0749e-482">[Azure maszyn wirtualnych, planowania i wdrażania dla programu SAP][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="0749e-482">[Azure Virtual Machines planning and implementation for SAP][planning-guide]</span></span>
* <span data-ttu-id="0749e-483">[Maszyny wirtualne Azure wdrożenia SAP][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="0749e-483">[Azure Virtual Machines deployment for SAP][deployment-guide]</span></span>
* <span data-ttu-id="0749e-484">[Wdrożenia usługi Azure DBMS maszyny wirtualnej dla programu SAP][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="0749e-484">[Azure Virtual Machines DBMS deployment for SAP][dbms-guide]</span></span>
* <span data-ttu-id="0749e-485">toolearn jak tooestablish wysokiej dostępności i planu odzyskiwania po awarii programu SAP HANA na platformie Azure (wystąpienia duże), zobacz [SAP HANA (duże wystąpień) wysokiej dostępności i odzyskiwania po awarii na platformie Azure](hana-overview-high-availability-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="0749e-485">toolearn how tooestablish high availability and plan for disaster recovery of SAP HANA on Azure (large instances), see [SAP HANA (large instances) high availability and disaster recovery on Azure](hana-overview-high-availability-disaster-recovery.md).</span></span>
* <span data-ttu-id="0749e-486">jak tooestablish wysokiej dostępności i planu odzyskiwania po awarii programu SAP HANA na maszynach wirtualnych Azure, zobacz toolearn [dostępności wysokiej programu SAP HANA na maszynach wirtualnych Azure (VM)][sap-hana-ha]</span><span class="sxs-lookup"><span data-stu-id="0749e-486">toolearn how tooestablish high availability and plan for disaster recovery of SAP HANA on Azure VMs, see [High Availability of SAP HANA on Azure Virtual Machines (VMs)][sap-hana-ha]</span></span>
