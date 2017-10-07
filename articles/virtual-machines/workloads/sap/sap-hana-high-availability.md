---
title: "aaaHigh dostępności programu SAP HANA na maszynach wirtualnych Azure (VM) | Dokumentacja firmy Microsoft"
description: "Ustanów wysokiej dostępności SAP HANA na maszynach wirtualnych platformy Azure (VM)."
services: virtual-machines-linux
documentationcenter: 
author: MSSedusch
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 04/25/2017
ms.author: sedusch
ms.openlocfilehash: dcb9bb70594f9d97f8a888cec76300bcbe0bf1ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-of-sap-hana-on-azure-virtual-machines-vms"></a><span data-ttu-id="9efb0-103">Wysoka dostępność SAP HANA na maszynach wirtualnych platformy Azure (VM)</span><span class="sxs-lookup"><span data-stu-id="9efb0-103">High Availability of SAP HANA on Azure Virtual Machines (VMs)</span></span>

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

[hana-ha-guide-replication]:sap-hana-high-availability.md#14c19f65-b5aa-4856-9594-b81c7e4df73d
[hana-ha-guide-shared-storage]:sap-hana-high-availability.md#498de331-fa04-490b-997c-b078de457c9d

[suse-hana-ha-guide]:https://www.suse.com/docrep/documents/ir8w88iwu7/suse_linux_enterprise_server_for_sap_applications_12_sp1.pdf
[sap-swcenter]:https://launchpad.support.sap.com/#/softwarecenter
[template-multisid-db]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db%2Fazuredeploy.json
[template-converged]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-converged%2Fazuredeploy.json

<span data-ttu-id="9efb0-113">W infrastrukturze lokalnej, możesz użyć albo HANA replikacji systemu lub magazynu udostępnionego tooestablish wysokiej dostępności dla SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="9efb0-113">On-premises, you can use either HANA System Replication or use shared storage tooestablish high availability for SAP HANA.</span></span>
<span data-ttu-id="9efb0-114">Aktualnie obsługiwany jest tylko skonfigurowanie HANA replikacji systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="9efb0-114">We currently only support setting up HANA System Replication on Azure.</span></span> <span data-ttu-id="9efb0-115">SAP HANA replikacji składa się z jednego węzła głównego i co najmniej jeden podrzędny węzła.</span><span class="sxs-lookup"><span data-stu-id="9efb0-115">SAP HANA Replication consists of one master node and at least one slave node.</span></span> <span data-ttu-id="9efb0-116">Toohello zmiany, danych w węźle głównym hello są replikowane węzłów podrzędnych toohello synchronicznie lub asynchronicznie.</span><span class="sxs-lookup"><span data-stu-id="9efb0-116">Changes toohello data on hello master node are replicated toohello slave nodes synchronously or asynchronously.</span></span>

<span data-ttu-id="9efb0-117">W tym artykule opisano sposób toodeploy hello maszyn wirtualnych, konfigurowanie maszyn wirtualnych hello, zainstaluj program hello framework klastra, zainstalować i skonfigurować replikacji systemu SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="9efb0-117">This article describes how toodeploy hello virtual machines, configure hello virtual machines, install hello cluster framework, install and configure SAP HANA System Replication.</span></span>
<span data-ttu-id="9efb0-118">W hello przykładowe konfiguracje instalacja poleceń itp. liczby wystąpień 03 i HANA systemu identyfikator HDB jest używany.</span><span class="sxs-lookup"><span data-stu-id="9efb0-118">In hello example configurations, installation commands etc. instance number 03 and HANA System ID HDB is used.</span></span>

<span data-ttu-id="9efb0-119">Przeczytaj hello najpierw następujące uwagi SAP i dokumentów</span><span class="sxs-lookup"><span data-stu-id="9efb0-119">Read hello following SAP Notes and papers first</span></span>

* <span data-ttu-id="9efb0-120">Uwaga SAP [1928533], który zawiera:</span><span class="sxs-lookup"><span data-stu-id="9efb0-120">SAP Note [1928533], which has:</span></span>
  * <span data-ttu-id="9efb0-121">Lista rozmiarów maszyny Wirtualnej platformy Azure, które są obsługiwane dla hello wdrożenia oprogramowania SAP</span><span class="sxs-lookup"><span data-stu-id="9efb0-121">List of Azure VM sizes that are supported for hello deployment of SAP software</span></span>
  * <span data-ttu-id="9efb0-122">Informacje o rozmiary maszyn wirtualnych Azure ważne pojemności</span><span class="sxs-lookup"><span data-stu-id="9efb0-122">Important capacity information for Azure VM sizes</span></span>
  * <span data-ttu-id="9efb0-123">Obsługiwane oprogramowanie SAP i kombinacji bazy danych i systemu operacyjnego (OS)</span><span class="sxs-lookup"><span data-stu-id="9efb0-123">Supported SAP software, and operating system (OS) and database combinations</span></span>
  * <span data-ttu-id="9efb0-124">Wymagana wersja jądra SAP dla systemu Windows i Linux w systemie Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="9efb0-124">Required SAP kernel version for Windows and Linux on Microsoft Azure</span></span>
* <span data-ttu-id="9efb0-125">Uwaga SAP [2015553] wymieniono wymagania wstępne dotyczące wdrażania oprogramowania SAP SAP, obsługiwane na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="9efb0-125">SAP Note [2015553] lists prerequisites for SAP-supported SAP software deployments in Azure.</span></span>
* <span data-ttu-id="9efb0-126">Uwaga SAP [2205917] zawiera zalecane ustawienia systemu operacyjnego SUSE Linux Enterprise Server dla programu SAP aplikacji</span><span class="sxs-lookup"><span data-stu-id="9efb0-126">SAP Note [2205917] has recommended OS settings for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="9efb0-127">Uwaga SAP [1944799] ma SAP HANA wytyczne dla SUSE Linux Enterprise Server dla programu SAP aplikacji</span><span class="sxs-lookup"><span data-stu-id="9efb0-127">SAP Note [1944799] has SAP HANA Guidelines for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="9efb0-128">Uwaga SAP [2178632] zawiera szczegółowe informacje na temat wszystkie funkcje monitorowania metryki zgłoszone dla SAP na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="9efb0-128">SAP Note [2178632] has detailed information about all monitoring metrics reported for SAP in Azure.</span></span>
* <span data-ttu-id="9efb0-129">Uwaga SAP [2191498] hello wymaga wersji agenta hosta SAP dla systemu Linux na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="9efb0-129">SAP Note [2191498] has hello required SAP Host Agent version for Linux in Azure.</span></span>
* <span data-ttu-id="9efb0-130">Uwaga SAP [2243692] zawiera informacje o licencjonowaniu SAP w systemie Linux na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="9efb0-130">SAP Note [2243692] has information about SAP licensing on Linux in Azure.</span></span>
* <span data-ttu-id="9efb0-131">Uwaga SAP [1984787] zawiera ogólne informacje o systemie SUSE Linux Enterprise Server 12.</span><span class="sxs-lookup"><span data-stu-id="9efb0-131">SAP Note [1984787] has general information about SUSE Linux Enterprise Server 12.</span></span>
* <span data-ttu-id="9efb0-132">Uwaga SAP [1999351] zawiera dodatkowe informacje dotyczące rozwiązywania problemów hello Azure ulepszone rozszerzenie monitorowania dla programu SAP.</span><span class="sxs-lookup"><span data-stu-id="9efb0-132">SAP Note [1999351] has additional troubleshooting information for hello Azure Enhanced Monitoring Extension for SAP.</span></span>
* <span data-ttu-id="9efb0-133">[SAP społeczności WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) ma wszystkie wymagane informacje SAP dla systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="9efb0-133">[SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) has all required SAP Notes for Linux.</span></span>
* <span data-ttu-id="9efb0-134">[Azure maszyn wirtualnych, planowania i wdrażania dla SAP w systemie Linux][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="9efb0-134">[Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide]</span></span>
* <span data-ttu-id="9efb0-135">[Maszyny wirtualne Azure wdrożenie SAP w systemie Linux (w tym artykule)][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="9efb0-135">[Azure Virtual Machines deployment for SAP on Linux (this article)][deployment-guide]</span></span>
* <span data-ttu-id="9efb0-136">[Azure maszyn wirtualnych systemu DBMS wdrożenie SAP w systemie Linux][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="9efb0-136">[Azure Virtual Machines DBMS deployment for SAP on Linux][dbms-guide]</span></span>
* <span data-ttu-id="9efb0-137">[SAP HANA SR wydajności zoptymalizowanych pod kątem scenariusza] [ suse-hana-ha-guide] hello przewodnik zawiera wszystkie wymagane informacje tooset zapasowych replikacji systemu SAP HANA lokalnie.</span><span class="sxs-lookup"><span data-stu-id="9efb0-137">[SAP HANA SR Performance Optimized Scenario][suse-hana-ha-guide] hello guide contains all required information tooset up SAP HANA System Replication on-premises.</span></span> <span data-ttu-id="9efb0-138">Użyj tego podręcznika, jako linii bazowej.</span><span class="sxs-lookup"><span data-stu-id="9efb0-138">Use this guide as a baseline.</span></span>

## <a name="deploying-linux"></a><span data-ttu-id="9efb0-139">Wdrażanie systemu Linux</span><span class="sxs-lookup"><span data-stu-id="9efb0-139">Deploying Linux</span></span>

<span data-ttu-id="9efb0-140">Hello agenta zasobów dla SAP HANA znajduje się w systemie SUSE Linux Enterprise Server aplikacje SAP.</span><span class="sxs-lookup"><span data-stu-id="9efb0-140">hello resource agent for SAP HANA is included in SUSE Linux Enterprise Server for SAP Applications.</span></span>
<span data-ttu-id="9efb0-141">Hello Azure Marketplace zawiera obraz systemu SUSE Linux Enterprise Server dla programu SAP 12 aplikacji z użyciem nowych maszyn wirtualnych toodeploy BYOS (Bring Your własnej subskrypcji).</span><span class="sxs-lookup"><span data-stu-id="9efb0-141">hello Azure Marketplace contains an image for SUSE Linux Enterprise Server for SAP Applications 12 with BYOS (Bring Your Own Subscription) that you can use toodeploy new virtual machines.</span></span>

### <a name="manual-deployment"></a><span data-ttu-id="9efb0-142">Ręczne wdrażanie</span><span class="sxs-lookup"><span data-stu-id="9efb0-142">Manual Deployment</span></span>

1. <span data-ttu-id="9efb0-143">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="9efb0-143">Create a Resource Group</span></span>
1. <span data-ttu-id="9efb0-144">Tworzenie sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="9efb0-144">Create a Virtual Network</span></span>
1. <span data-ttu-id="9efb0-145">Utwórz dwa konta magazynu</span><span class="sxs-lookup"><span data-stu-id="9efb0-145">Create two Storage Accounts</span></span>
1. <span data-ttu-id="9efb0-146">Tworzenie zestawu dostępności</span><span class="sxs-lookup"><span data-stu-id="9efb0-146">Create an Availability Set</span></span>  
   <span data-ttu-id="9efb0-147">Zestaw aktualizacji max domeny</span><span class="sxs-lookup"><span data-stu-id="9efb0-147">Set max update domain</span></span>
1. <span data-ttu-id="9efb0-148">Tworzenie modułu równoważenia obciążenia (wewnętrzny)</span><span class="sxs-lookup"><span data-stu-id="9efb0-148">Create a Load Balancer (internal)</span></span>  
   <span data-ttu-id="9efb0-149">Wybierz sieć Wirtualną w kroku powyżej</span><span class="sxs-lookup"><span data-stu-id="9efb0-149">Select VNET of step above</span></span>
1. <span data-ttu-id="9efb0-150">Utwórz maszynę wirtualną 1</span><span class="sxs-lookup"><span data-stu-id="9efb0-150">Create Virtual Machine 1</span></span>  
   <span data-ttu-id="9efb0-151">https://Portal.Azure.com/#Create/SUSE-byos.SLES-for-SAP-byos12-SP1</span><span class="sxs-lookup"><span data-stu-id="9efb0-151">https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1</span></span>  
   <span data-ttu-id="9efb0-152">SLES 12 aplikacje SAP z dodatkiem SP1 (BYOS)</span><span class="sxs-lookup"><span data-stu-id="9efb0-152">SLES For SAP Applications 12 SP1 (BYOS)</span></span>  
   <span data-ttu-id="9efb0-153">Wybierz konto magazynu 1</span><span class="sxs-lookup"><span data-stu-id="9efb0-153">Select Storage Account 1</span></span>  
   <span data-ttu-id="9efb0-154">Wybierz zestaw dostępności</span><span class="sxs-lookup"><span data-stu-id="9efb0-154">Select Availability Set</span></span>  
1. <span data-ttu-id="9efb0-155">Tworzenie maszyny wirtualnej 2</span><span class="sxs-lookup"><span data-stu-id="9efb0-155">Create Virtual Machine 2</span></span>  
   <span data-ttu-id="9efb0-156">https://Portal.Azure.com/#Create/SUSE-byos.SLES-for-SAP-byos12-SP1</span><span class="sxs-lookup"><span data-stu-id="9efb0-156">https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1</span></span>  
   <span data-ttu-id="9efb0-157">SLES 12 aplikacje SAP z dodatkiem SP1 (BYOS)</span><span class="sxs-lookup"><span data-stu-id="9efb0-157">SLES For SAP Applications 12 SP1 (BYOS)</span></span>  
   <span data-ttu-id="9efb0-158">Wybierz konto magazynu 2</span><span class="sxs-lookup"><span data-stu-id="9efb0-158">Select Storage Account 2</span></span>   
   <span data-ttu-id="9efb0-159">Wybierz zestaw dostępności</span><span class="sxs-lookup"><span data-stu-id="9efb0-159">Select Availability Set</span></span>  
1. <span data-ttu-id="9efb0-160">Dodawanie dysków z danymi</span><span class="sxs-lookup"><span data-stu-id="9efb0-160">Add Data Disks</span></span>
1. <span data-ttu-id="9efb0-161">Konfigurowanie równoważenia obciążenia hello</span><span class="sxs-lookup"><span data-stu-id="9efb0-161">Configure hello load balancer</span></span>
    1. <span data-ttu-id="9efb0-162">Utwórz pulę IP frontonu</span><span class="sxs-lookup"><span data-stu-id="9efb0-162">Create a frontend IP pool</span></span>
        1. <span data-ttu-id="9efb0-163">Otwórz moduł równoważenia obciążenia hello, wybierz puli adresów IP frontonu i kliknij przycisk Dodaj</span><span class="sxs-lookup"><span data-stu-id="9efb0-163">Open hello load balancer, select frontend IP pool and click Add</span></span>
        1. <span data-ttu-id="9efb0-164">Wprowadź nazwę hello puli hello do adresów IP nowego serwera sieci Web (na przykład frontonu hana)</span><span class="sxs-lookup"><span data-stu-id="9efb0-164">Enter hello name of hello new frontend IP pool (for example hana-frontend)</span></span>
       1. <span data-ttu-id="9efb0-165">Kliknij przycisk OK</span><span class="sxs-lookup"><span data-stu-id="9efb0-165">Click OK</span></span>
        1. <span data-ttu-id="9efb0-166">Po utworzeniu hello nowa pula IP frontonu, zanotuj jego adresu IP</span><span class="sxs-lookup"><span data-stu-id="9efb0-166">After hello new frontend IP pool is created, write down its IP address</span></span>
    1. <span data-ttu-id="9efb0-167">Tworzenie puli wewnętrznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="9efb0-167">Create a backend pool</span></span>
        1. <span data-ttu-id="9efb0-168">Otwórz moduł równoważenia obciążenia hello, wybierz pul zaplecza i kliknij przycisk Dodaj</span><span class="sxs-lookup"><span data-stu-id="9efb0-168">Open hello load balancer, select backend pools and click Add</span></span>
        1. <span data-ttu-id="9efb0-169">Wprowadź nazwę hello hello nowej puli wewnętrznej bazy danych (na przykład zaplecze hana)</span><span class="sxs-lookup"><span data-stu-id="9efb0-169">Enter hello name of hello new backend pool (for example hana-backend)</span></span>
        1. <span data-ttu-id="9efb0-170">Kliknij przycisk Dodaj maszynę wirtualną</span><span class="sxs-lookup"><span data-stu-id="9efb0-170">Click Add a virtual machine</span></span>
        1. <span data-ttu-id="9efb0-171">Wybierz hello utworzoną wcześniej zestawu dostępności</span><span class="sxs-lookup"><span data-stu-id="9efb0-171">Select hello Availability Set you created earlier</span></span>
        1. <span data-ttu-id="9efb0-172">Wybierz maszyny wirtualne hello hello SAP HANA klastra</span><span class="sxs-lookup"><span data-stu-id="9efb0-172">Select hello virtual machines of hello SAP HANA cluster</span></span>
        1. <span data-ttu-id="9efb0-173">Kliknij przycisk OK</span><span class="sxs-lookup"><span data-stu-id="9efb0-173">Click OK</span></span>
    1. <span data-ttu-id="9efb0-174">Utworzyć sondy kondycji</span><span class="sxs-lookup"><span data-stu-id="9efb0-174">Create a health probe</span></span>
       1. <span data-ttu-id="9efb0-175">Otwórz moduł równoważenia obciążenia hello, wybierz sond kondycji i kliknij przycisk Dodaj</span><span class="sxs-lookup"><span data-stu-id="9efb0-175">Open hello load balancer, select health probes and click Add</span></span>
        1. <span data-ttu-id="9efb0-176">Wprowadź nazwę hello hello nowe sondy kondycji (na przykład hp hana)</span><span class="sxs-lookup"><span data-stu-id="9efb0-176">Enter hello name of hello new health probe (for example hana-hp)</span></span>
        1. <span data-ttu-id="9efb0-177">Wybierz protokół, port 625 TCP**03**, interwał 5 i próg złej kondycji 2</span><span class="sxs-lookup"><span data-stu-id="9efb0-177">Select TCP as protocol, port 625**03**, keep Interval 5 and Unhealthy threshold 2</span></span>
        1. <span data-ttu-id="9efb0-178">Kliknij przycisk OK</span><span class="sxs-lookup"><span data-stu-id="9efb0-178">Click OK</span></span>
    1. <span data-ttu-id="9efb0-179">Tworzenie reguł równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="9efb0-179">Create load balancing rules</span></span>
        1. <span data-ttu-id="9efb0-180">Otwórz moduł równoważenia obciążenia hello, wybierz reguły równoważenia obciążenia i kliknij przycisk Dodaj</span><span class="sxs-lookup"><span data-stu-id="9efb0-180">Open hello load balancer, select load balancing rules and click Add</span></span>
        1. <span data-ttu-id="9efb0-181">Wprowadź nazwę hello hello nowej reguły modułu równoważenia obciążenia (na przykład hana-lb-3**03**15)</span><span class="sxs-lookup"><span data-stu-id="9efb0-181">Enter hello name of hello new load balancer rule (for example hana-lb-3**03**15)</span></span>
        1. <span data-ttu-id="9efb0-182">Adres IP frontonu wybierz hello, puli wewnętrznej bazy danych i kondycji sondowania utworzonego wcześniej (na przykład frontonu hana)</span><span class="sxs-lookup"><span data-stu-id="9efb0-182">Select hello frontend IP address, backend pool and health probe you created earlier (for example hana-frontend)</span></span>
        1. <span data-ttu-id="9efb0-183">Zachowaj protokołu TCP, wprowadź port 3**03**15</span><span class="sxs-lookup"><span data-stu-id="9efb0-183">Keep protocol TCP, enter port 3**03**15</span></span>
        1. <span data-ttu-id="9efb0-184">Zwiększ limit czasu bezczynności too30 minut</span><span class="sxs-lookup"><span data-stu-id="9efb0-184">Increase idle timeout too30 minutes</span></span>
       1. <span data-ttu-id="9efb0-185">**Upewnij się, że tooenable pływającego adresu IP**</span><span class="sxs-lookup"><span data-stu-id="9efb0-185">**Make sure tooenable Floating IP**</span></span>
        1. <span data-ttu-id="9efb0-186">Kliknij przycisk OK</span><span class="sxs-lookup"><span data-stu-id="9efb0-186">Click OK</span></span>
        1. <span data-ttu-id="9efb0-187">Powtórz powyższe kroki hello portu 3**03**17</span><span class="sxs-lookup"><span data-stu-id="9efb0-187">Repeat hello steps above for port 3**03**17</span></span>

### <a name="deploy-with-template"></a><span data-ttu-id="9efb0-188">Wdrażanie za pomocą szablonu</span><span class="sxs-lookup"><span data-stu-id="9efb0-188">Deploy with template</span></span>
<span data-ttu-id="9efb0-189">Możesz użyć jednego z szablonów szybki start hello w github toodeploy wszystkich wymaganych zasobów.</span><span class="sxs-lookup"><span data-stu-id="9efb0-189">You can use one of hello quick start templates on github toodeploy all required resources.</span></span> <span data-ttu-id="9efb0-190">Szablon Hello wdraża hello maszyn wirtualnych, usługi równoważenia obciążenia hello, itp zestawu dostępności. Wykonaj te kroki toodeploy hello szablonu:</span><span class="sxs-lookup"><span data-stu-id="9efb0-190">hello template deploys hello virtual machines, hello load balancer, availability set etc. Follow these steps toodeploy hello template:</span></span>

1. <span data-ttu-id="9efb0-191">Otwórz hello [szablonu bazy danych] [ template-multisid-db] lub hello [zbieżność szablonu] [ template-converged] w portalu Azure hello hello szablonu bazy danych tylko tworzy hello reguły równoważenia obciążenia dla bazy danych należy szablon konwergentnej hello również tworzy tekst hello reguły równoważenia obciążenia ASCS/SCS i wystąpienia Wywołujących (tylko w systemie Linux).</span><span class="sxs-lookup"><span data-stu-id="9efb0-191">Open hello [database template][template-multisid-db] or hello [converged template][template-converged] on hello Azure Portal hello database template only creates hello load-balancing rules for a database whereas hello converged template also creates hello load-balancing rules for an ASCS/SCS and ERS (Linux only) instance.</span></span> <span data-ttu-id="9efb0-192">Jeśli planujesz tooinstall systemu SAP NetWeaver na podstawie i ma tooinstall hello ASCS/SCS wystąpienia na powitania sam maszyny, użyj hello [zbieżność szablonu][template-converged].</span><span class="sxs-lookup"><span data-stu-id="9efb0-192">If you plan tooinstall an SAP NetWeaver based system and you also want tooinstall hello ASCS/SCS instance on hello same machines, use hello [converged template][template-converged].</span></span>
1. <span data-ttu-id="9efb0-193">Wprowadź następujące parametry hello</span><span class="sxs-lookup"><span data-stu-id="9efb0-193">Enter hello following parameters</span></span>
    1. <span data-ttu-id="9efb0-194">Identyfikator systemu SAP</span><span class="sxs-lookup"><span data-stu-id="9efb0-194">Sap System Id</span></span>  
       <span data-ttu-id="9efb0-195">Wprowadź systemu SAP hello identyfikator hello ma tooinstall systemu SAP.</span><span class="sxs-lookup"><span data-stu-id="9efb0-195">Enter hello SAP system Id of hello SAP system you want tooinstall.</span></span> <span data-ttu-id="9efb0-196">Witaj identyfikator będzie służyć jako prefiks hello zasobów, które zostały wdrożone.</span><span class="sxs-lookup"><span data-stu-id="9efb0-196">hello Id will be used as a prefix for hello resources that are deployed.</span></span>
    1. <span data-ttu-id="9efb0-197">Typ stosu (dotyczy tylko jeśli używasz szablonu konwergentnej hello)</span><span class="sxs-lookup"><span data-stu-id="9efb0-197">Stack Type (only applicable if you use hello converged template)</span></span>  
       <span data-ttu-id="9efb0-198">Wybierz typ stosu SAP NetWeaver hello</span><span class="sxs-lookup"><span data-stu-id="9efb0-198">Select hello SAP NetWeaver stack type</span></span>
    1. <span data-ttu-id="9efb0-199">Typ systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="9efb0-199">Os Type</span></span>  
       <span data-ttu-id="9efb0-200">Wybierz jedną z hello dystrybucje systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="9efb0-200">Select one of hello Linux distributions.</span></span> <span data-ttu-id="9efb0-201">Na przykład wybierz SLES 12 BYOS</span><span class="sxs-lookup"><span data-stu-id="9efb0-201">For this example, select SLES 12 BYOS</span></span>
    1. <span data-ttu-id="9efb0-202">Typ bazy danych</span><span class="sxs-lookup"><span data-stu-id="9efb0-202">Db Type</span></span>  
       <span data-ttu-id="9efb0-203">Wybierz HANA</span><span class="sxs-lookup"><span data-stu-id="9efb0-203">Select HANA</span></span>
    1. <span data-ttu-id="9efb0-204">Rozmiar systemu SAP</span><span class="sxs-lookup"><span data-stu-id="9efb0-204">Sap System Size</span></span>  
       <span data-ttu-id="9efb0-205">zapewni Hello ilość protokoły SAP hello nowy system.</span><span class="sxs-lookup"><span data-stu-id="9efb0-205">hello amount of SAPS hello new system will provide.</span></span> <span data-ttu-id="9efb0-206">Jeśli nie masz pewności, ile protokoły SAP hello system będzie wymagać, należy skontaktować się z partnerem technologii SAP lub Integrator systemu</span><span class="sxs-lookup"><span data-stu-id="9efb0-206">If you are not sure how many SAPS hello system will require, please ask your SAP Technology Partner or System Integrator</span></span>
    1. <span data-ttu-id="9efb0-207">Dostępność systemu</span><span class="sxs-lookup"><span data-stu-id="9efb0-207">System Availability</span></span>  
       <span data-ttu-id="9efb0-208">Wybierz opcję wysokiej dostępności</span><span class="sxs-lookup"><span data-stu-id="9efb0-208">Select HA</span></span>
    1. <span data-ttu-id="9efb0-209">Nazwa użytkownika i hasło administratora</span><span class="sxs-lookup"><span data-stu-id="9efb0-209">Admin Username and Admin Password</span></span>  
       <span data-ttu-id="9efb0-210">Tworzony jest nowy użytkownik, który może być używane toolog toohello maszyny.</span><span class="sxs-lookup"><span data-stu-id="9efb0-210">A new user is created that can be used toolog on toohello machine.</span></span>
    1. <span data-ttu-id="9efb0-211">Nowy lub istniejący podsieci</span><span class="sxs-lookup"><span data-stu-id="9efb0-211">New Or Existing Subnet</span></span>  
       <span data-ttu-id="9efb0-212">Określa, czy należy utworzyć nową sieć wirtualną i podsieć lub istniejącą podsieć powinna być używana.</span><span class="sxs-lookup"><span data-stu-id="9efb0-212">Determines whether a new virtual network and subnet should be created or an existing subnet should be used.</span></span> <span data-ttu-id="9efb0-213">Jeśli masz już sieć wirtualną tooyour połączonych sieci lokalnej, wybierz istniejącą.</span><span class="sxs-lookup"><span data-stu-id="9efb0-213">If you already have a virtual network that is connected tooyour on-premises network, select existing.</span></span>
    1. <span data-ttu-id="9efb0-214">Identyfikator podsieci</span><span class="sxs-lookup"><span data-stu-id="9efb0-214">Subnet Id</span></span>  
    <span data-ttu-id="9efb0-215">Identyfikator Hello maszyn wirtualnych hello hello podsieci toowhich powinny być podłączone do.</span><span class="sxs-lookup"><span data-stu-id="9efb0-215">hello ID of hello subnet toowhich hello virtual machines should be connected to.</span></span> <span data-ttu-id="9efb0-216">Wybierz podsieć hello sieci VPN lub usługi Express Route sieci wirtualnej tooconnect hello maszyny wirtualnej tooyour w sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="9efb0-216">Select hello subnet of your VPN or Express Route virtual network tooconnect hello virtual machine tooyour on-premises network.</span></span> <span data-ttu-id="9efb0-217">Identyfikator Hello zwykle wygląda /subscriptions/`<subscription id`> /resourceGroups/`<resource group name`> /providers/Microsoft.Network/virtualNetworks/`<virtual network name`> /subnets/`<subnet name`></span><span class="sxs-lookup"><span data-stu-id="9efb0-217">hello ID usually looks like /subscriptions/`<subscription id`>/resourceGroups/`<resource group name`>/providers/Microsoft.Network/virtualNetworks/`<virtual network name`>/subnets/`<subnet name`></span></span>

## <a name="setting-up-linux-ha"></a><span data-ttu-id="9efb0-218">Konfigurowanie HA systemu Linux</span><span class="sxs-lookup"><span data-stu-id="9efb0-218">Setting up Linux HA</span></span>

<span data-ttu-id="9efb0-219">Witaj, następujące elementy są poprzedzane prefiksem albo [A] - tooall odpowiednich węzłów, toonode przeznaczone wyłącznie [1] - toonode stosuje się tylko 1 lub [2] - 2.</span><span class="sxs-lookup"><span data-stu-id="9efb0-219">hello following items are prefixed with either [A] - applicable tooall nodes, [1] - only applicable toonode 1 or [2] - only applicable toonode 2.</span></span>

1. <span data-ttu-id="9efb0-220">[A] SLES dla SAP BYOS tylko - zarejestrować SLES toobe toouse stanie hello repozytoria</span><span class="sxs-lookup"><span data-stu-id="9efb0-220">[A] SLES for SAP BYOS only - Register SLES toobe able toouse hello repositories</span></span>
1. <span data-ttu-id="9efb0-221">[A] SLES dla SAP BYOS tylko — Dodaj moduł chmury publicznej</span><span class="sxs-lookup"><span data-stu-id="9efb0-221">[A] SLES for SAP BYOS only - Add public-cloud module</span></span>
1. <span data-ttu-id="9efb0-222">[A] Aktualizacja SLES</span><span class="sxs-lookup"><span data-stu-id="9efb0-222">[A] Update SLES</span></span>
    ```bash
    sudo zypper update

    ```

1. <span data-ttu-id="9efb0-223">[1] dostęp ssh</span><span class="sxs-lookup"><span data-stu-id="9efb0-223">[1] Enable ssh access</span></span>
    ```bash
    sudo ssh-keygen -tdsa
    
    # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
    # Enter passphrase (empty for no passphrase): -> ENTER
    # Enter same passphrase again: -> ENTER
    
    # copy hello public key
    sudo cat /root/.ssh/id_dsa.pub
    ```

2. <span data-ttu-id="9efb0-224">[2] dostęp ssh</span><span class="sxs-lookup"><span data-stu-id="9efb0-224">[2] Enable ssh access</span></span>
    ```bash
    sudo ssh-keygen -tdsa

    # insert hello public key you copied in hello last step into hello authorized keys file on hello second server
    sudo vi /root/.ssh/authorized_keys
    
    # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
    # Enter passphrase (empty for no passphrase): -> ENTER
    # Enter same passphrase again: -> ENTER
    
    # copy hello public key    
    sudo cat /root/.ssh/id_dsa.pub
    ```

1. <span data-ttu-id="9efb0-225">[1] dostęp ssh</span><span class="sxs-lookup"><span data-stu-id="9efb0-225">[1] Enable ssh access</span></span>
    ```bash
    # insert hello public key you copied in hello last step into hello authorized keys file on hello first server
    sudo vi /root/.ssh/authorized_keys
    
    ```

1. <span data-ttu-id="9efb0-226">[A] należy zainstalować rozszerzenie wysokiej dostępności</span><span class="sxs-lookup"><span data-stu-id="9efb0-226">[A] Install HA extension</span></span>
    ```bash
    sudo zypper install sle-ha-release fence-agents
    
    ```

1. <span data-ttu-id="9efb0-227">[A] układ dysku instalacji</span><span class="sxs-lookup"><span data-stu-id="9efb0-227">[A] Setup disk layout</span></span>
    1. <span data-ttu-id="9efb0-228">LVM</span><span class="sxs-lookup"><span data-stu-id="9efb0-228">LVM</span></span>  
    <span data-ttu-id="9efb0-229">Ogólnie zaleca toouse LVM dla woluminów, które przechowują dane i pliki dziennika.</span><span class="sxs-lookup"><span data-stu-id="9efb0-229">We generally recommend toouse LVM for volumes that store data and log files.</span></span> <span data-ttu-id="9efb0-230">w poniższym przykładzie Hello założenia, że maszyny wirtualne hello czterech dyskach danych dołączonych, które powinny być używane toocreate dwa woluminy.</span><span class="sxs-lookup"><span data-stu-id="9efb0-230">hello example below assumes that hello virtual machines have four data disks attached that should be used toocreate two volumes.</span></span>
        * <span data-ttu-id="9efb0-231">Utwórz woluminy fizyczne dla wszystkich dysków, które mają toouse.</span><span class="sxs-lookup"><span data-stu-id="9efb0-231">Create physical volumes for all disks that you want toouse.</span></span>
    <pre><code>
    sudo pvcreate /dev/sdc
    sudo pvcreate /dev/sdd
    sudo pvcreate /dev/sde
    sudo pvcreate /dev/sdf
    </code></pre>
        * <span data-ttu-id="9efb0-232">Utwórz grupę woluminu hello plików danych, jedna grupa woluminu dla plików dziennika hello i jeden dla udostępnionego katalogu hello SAP HANA</span><span class="sxs-lookup"><span data-stu-id="9efb0-232">Create a volume group for hello data files, one volume group for hello log files and one for hello shared directory of SAP HANA</span></span>
    <pre><code>
    sudo vgcreate vg_hana_data /dev/sdc /dev/sdd
    sudo vgcreate vg_hana_log /dev/sde
    sudo vgcreate vg_hana_shared /dev/sdf
    </code></pre>
        * <span data-ttu-id="9efb0-233">Utwórz hello woluminy logiczne</span><span class="sxs-lookup"><span data-stu-id="9efb0-233">Create hello logical volumes</span></span>
    <pre><code>
    sudo lvcreate -l 100%FREE -n hana_data vg_hana_data
    sudo lvcreate -l 100%FREE -n hana_log vg_hana_log
    sudo lvcreate -l 100%FREE -n hana_shared vg_hana_shared
    sudo mkfs.xfs /dev/vg_hana_data/hana_data
    sudo mkfs.xfs /dev/vg_hana_log/hana_log
    sudo mkfs.xfs /dev/vg_hana_shared/hana_shared
    </code></pre>
        * <span data-ttu-id="9efb0-234">Utwórz katalogi instalacji hello i skopiuj hello UUID wszystkich woluminów logicznych</span><span class="sxs-lookup"><span data-stu-id="9efb0-234">Create hello mount directories and copy hello UUID of all logical volumes</span></span>
    <pre><code>
    sudo mkdir -p /hana/data
    sudo mkdir -p /hana/log
    sudo mkdir -p /hana/shared
    # write down hello id of /dev/vg_hana_data/hana_data, /dev/vg_hana_log/hana_log and /dev/vg_hana_shared/hana_shared
    sudo blkid
    </code></pre>
        * <span data-ttu-id="9efb0-235">Utwórz wpisy fstab hello trzy logiczne woluminy</span><span class="sxs-lookup"><span data-stu-id="9efb0-235">Create fstab entries for hello three logical volumes</span></span>
    <pre><code>
    sudo vi /etc/fstab
    </code></pre>
    <span data-ttu-id="9efb0-236">Wstaw ten wiersz zbyt/etc/fstab</span><span class="sxs-lookup"><span data-stu-id="9efb0-236">Insert this line too/etc/fstab</span></span>
    <pre><code>
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_data/hana_data&gt;</b> /hana/data xfs  defaults,nofail  0  2
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_log/hana_log&gt;</b> /hana/log xfs  defaults,nofail  0  2
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_shared/hana_shared&gt;</b> /hana/shared xfs  defaults,nofail  0  2
    </code></pre>
        * <span data-ttu-id="9efb0-237">Zainstaluj nowe woluminy hello</span><span class="sxs-lookup"><span data-stu-id="9efb0-237">Mount hello new volumes</span></span>
    <pre><code>
    sudo mount -a
    </code></pre>
    1. <span data-ttu-id="9efb0-238">Zwykły dysków</span><span class="sxs-lookup"><span data-stu-id="9efb0-238">Plain Disks</span></span>  
       <span data-ttu-id="9efb0-239">Dla małych lub demonstracyjnych systemów, możesz umieścić HANA plików danych i dziennika na jednym dysku.</span><span class="sxs-lookup"><span data-stu-id="9efb0-239">For small or demo systems, you can place your HANA data and log files on one disk.</span></span> <span data-ttu-id="9efb0-240">Witaj następujące polecenia utworzyć partycję na /dev/sdc i sformatuj go przy xfs.</span><span class="sxs-lookup"><span data-stu-id="9efb0-240">hello following commands create a partition on /dev/sdc and format it with xfs.</span></span>
    ```bash
    sudo fdisk /dev/sdc
    sudo mkfs.xfs /dev/sdc1
    
    # <a name="write-down-hello-id-of-devsdc1"></a><span data-ttu-id="9efb0-241">Zanotuj identyfikator hello /dev/sdc1</span><span class="sxs-lookup"><span data-stu-id="9efb0-241">write down hello id of /dev/sdc1</span></span>
    <span data-ttu-id="9efb0-242">sudo/sbin/blkid sudo vi/etc/fstab</span><span class="sxs-lookup"><span data-stu-id="9efb0-242">sudo /sbin/blkid  sudo vi /etc/fstab</span></span>
    ```

    Insert this line too/etc/fstab
    <pre><code>
    /dev/disk/by-uuid/<b>&lt;UUID&gt;</b> /hana xfs  defaults,nofail  0  2
    </code></pre>

    Create hello target directory and mount hello disk.

    ```bash
    sudo mkdir /hana
    sudo mount -a
    ```

1. <span data-ttu-id="9efb0-243">[A] ustawień rozpoznawania nazwy hosta dla wszystkich hostów</span><span class="sxs-lookup"><span data-stu-id="9efb0-243">[A] Setup host name resolution for all hosts</span></span>  
    <span data-ttu-id="9efb0-244">Można użyć serwera DNS lub zmodyfikować hello/etc/hosts na wszystkich węzłach.</span><span class="sxs-lookup"><span data-stu-id="9efb0-244">You can either use a DNS server or modify hello /etc/hosts on all nodes.</span></span> <span data-ttu-id="9efb0-245">Ten przykład przedstawia, jak toouse hello plik/etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="9efb0-245">This example shows how toouse hello /etc/hosts file.</span></span>
   <span data-ttu-id="9efb0-246">Zastąpienie hello adresu IP i nazwy hosta hello w hello następujące polecenia</span><span class="sxs-lookup"><span data-stu-id="9efb0-246">Replace hello IP address and hello hostname in hello following commands</span></span>
    ```bash
    sudo vi /etc/hosts
    ```
    <span data-ttu-id="9efb0-247">Wstaw hello następujące wiersze zbyt/etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="9efb0-247">Insert hello following lines too/etc/hosts.</span></span> <span data-ttu-id="9efb0-248">Zmień toomatch adres i nazwę hosta IP hello środowiska</span><span class="sxs-lookup"><span data-stu-id="9efb0-248">Change hello IP address and hostname toomatch your environment</span></span>    
    
    <pre><code>
    <b>&lt;IP address of host 1&gt; &lt;hostname of host 1&gt;</b>
    <b>&lt;IP address of host 2&gt; &lt;hostname of host 2&gt;</b>
    </code></pre>

1. <span data-ttu-id="9efb0-249">[1] instalacji klastra</span><span class="sxs-lookup"><span data-stu-id="9efb0-249">[1] Install Cluster</span></span>
    ```bash
    sudo ha-cluster-init
    
    # Do you want toocontinue anyway? [y/N] -> y
    # Network address toobind too(e.g.: 192.168.1.0) [10.79.227.0] -> ENTER
    # Multicast address (e.g.: 239.x.x.x) [239.174.218.125] -> ENTER
    # Multicast port [5405] -> ENTER
    # Do you wish toouse SBD? [y/N] -> N
    # Do you wish tooconfigure an administration IP? [y/N] -> N
    ```
        
1. <span data-ttu-id="9efb0-250">[2] dodać toocluster węzła</span><span class="sxs-lookup"><span data-stu-id="9efb0-250">[2] Add node toocluster</span></span>
    ```bash
    sudo ha-cluster-join
        
    # WARNING: NTP is not configured toostart at system boot.
    # WARNING: No watchdog device found. If SBD is used, hello cluster will be unable toostart without a watchdog.
    # Do you want toocontinue anyway? [y/N] -> y
    # IP address or hostname of existing node (e.g.: 192.168.1.1) [] -> IP address of node 1 e.g. 10.0.0.5
    # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
    ```

1. <span data-ttu-id="9efb0-251">[A] zmiany hacluster hasło toohello tego samego hasła</span><span class="sxs-lookup"><span data-stu-id="9efb0-251">[A] Change hacluster password toohello same password</span></span>
    ```bash
    sudo passwd hacluster
    
    ```

1. <span data-ttu-id="9efb0-252">[A] skonfiguruj corosync toouse innych transportu i dodać do wstawienia.</span><span class="sxs-lookup"><span data-stu-id="9efb0-252">[A] Configure corosync toouse other transport and add nodelist.</span></span> <span data-ttu-id="9efb0-253">Klaster nie będą działać inaczej.</span><span class="sxs-lookup"><span data-stu-id="9efb0-253">Cluster will not work otherwise.</span></span>
    ```bash
    sudo vi /etc/corosync/corosync.conf    
    
    ```

    <span data-ttu-id="9efb0-254">Dodaj powitania po bold toohello zawartości pliku.</span><span class="sxs-lookup"><span data-stu-id="9efb0-254">Add hello following bold content toohello file.</span></span>
    
    <pre><code> 
    [...]
      interface { 
          [...] 
      }
      <b>transport:      udpu</b>
    } 
    <b>nodelist {
      node {
        ring0_addr:     < ip address of node 1 >
      }
      node {
        ring0_addr:     < ip address of node 2 > 
      } 
    }</b>
    logging {
      [...]
    </code></pre>

    <span data-ttu-id="9efb0-255">Następnie uruchom ponownie usługę corosync hello</span><span class="sxs-lookup"><span data-stu-id="9efb0-255">Then restart hello corosync service</span></span>

    ```bash
    sudo service corosync restart
    
    ```

1. <span data-ttu-id="9efb0-256">[A] zainstalować pakiety HANA HA</span><span class="sxs-lookup"><span data-stu-id="9efb0-256">[A] Install HANA HA packages</span></span>  
    ```bash
    sudo zypper install SAPHanaSR
    
    ```

## <a name="installing-sap-hana"></a><span data-ttu-id="9efb0-257">Instalowanie programu SAP HANA</span><span class="sxs-lookup"><span data-stu-id="9efb0-257">Installing SAP HANA</span></span>

<span data-ttu-id="9efb0-258">Wykonaj rozdział 4 hello [przewodnik SAP HANA SR wydajności zoptymalizowanych pod kątem scenariusza] [ suse-hana-ha-guide] tooinstall replikacji systemu SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="9efb0-258">Follow chapter 4 of hello [SAP HANA SR Performance Optimized Scenario guide][suse-hana-ha-guide] tooinstall SAP HANA System Replication.</span></span>

1. <span data-ttu-id="9efb0-259">[A] uruchamiania hdblcm z hello HANA DVD</span><span class="sxs-lookup"><span data-stu-id="9efb0-259">[A] Run hdblcm from hello HANA DVD</span></span>
    * <span data-ttu-id="9efb0-260">Wybierz opcję instalacji -> 1</span><span class="sxs-lookup"><span data-stu-id="9efb0-260">Choose installation -> 1</span></span>
    * <span data-ttu-id="9efb0-261">1 -> Wybierz dodatkowe składniki do instalacji</span><span class="sxs-lookup"><span data-stu-id="9efb0-261">Select additional components for installation -> 1</span></span>
    * <span data-ttu-id="9efb0-262">Wprowadź ścieżkę instalacji [/ hana/udostępnione]: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="9efb0-262">Enter Installation Path [/hana/shared]: -> ENTER</span></span>
    * <span data-ttu-id="9efb0-263">Wprowadź nazwę hosta lokalnego [.]: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="9efb0-263">Enter Local Host Name [..]: -> ENTER</span></span>
    * <span data-ttu-id="9efb0-264">Czy chcesz, aby system toohello dodatkowych hostów tooadd?</span><span class="sxs-lookup"><span data-stu-id="9efb0-264">Do you want tooadd additional hosts toohello system?</span></span> <span data-ttu-id="9efb0-265">(t/n) [[n]: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="9efb0-265">(y/n) [n]: -> ENTER</span></span>
    * <span data-ttu-id="9efb0-266">Wprowadź identyfikator systemu SAP HANA:<SID of HANA e.g. HDB></span><span class="sxs-lookup"><span data-stu-id="9efb0-266">Enter SAP HANA System ID: <SID of HANA e.g. HDB></span></span>
    * <span data-ttu-id="9efb0-267">Wprowadź liczby wystąpień [00]:</span><span class="sxs-lookup"><span data-stu-id="9efb0-267">Enter Instance Number [00]:</span></span>   
  <span data-ttu-id="9efb0-268">Liczby wystąpień HANA.</span><span class="sxs-lookup"><span data-stu-id="9efb0-268">HANA Instance number.</span></span> <span data-ttu-id="9efb0-269">Użyj 03, jeśli używany szablon Azure hello i stosować w powyższym przykładzie hello</span><span class="sxs-lookup"><span data-stu-id="9efb0-269">Use 03 if you used hello Azure Template or followed hello example above</span></span>
    * <span data-ttu-id="9efb0-270">Wybierz tryb bazy danych / wprowadź indeks [1]: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="9efb0-270">Select Database Mode / Enter Index [1]: -> ENTER</span></span>
    * <span data-ttu-id="9efb0-271">Użycie systemu wybierz / Wprowadź indeks [4]:</span><span class="sxs-lookup"><span data-stu-id="9efb0-271">Select System Usage / Enter Index [4]:</span></span>  
  <span data-ttu-id="9efb0-272">Wybierz system hello użycia</span><span class="sxs-lookup"><span data-stu-id="9efb0-272">Select hello system Usage</span></span>
    * <span data-ttu-id="9efb0-273">Wprowadź lokalizację woluminów danych [/ hana/data/HDB]: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="9efb0-273">Enter Location of Data Volumes [/hana/data/HDB]: -> ENTER</span></span>
    * <span data-ttu-id="9efb0-274">Wprowadź lokalizację woluminy dziennika [/ HDB-hana/dziennika]: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="9efb0-274">Enter Location of Log Volumes [/hana/log/HDB]: -> ENTER</span></span>
    * <span data-ttu-id="9efb0-275">Ogranicz maksymalną wielkość pamięci alokacji?</span><span class="sxs-lookup"><span data-stu-id="9efb0-275">Restrict maximum memory allocation?</span></span> <span data-ttu-id="9efb0-276">[[n]: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="9efb0-276">[n]: -> ENTER</span></span>
    * <span data-ttu-id="9efb0-277">Wprowadź nazwę hosta certyfikat dla hosta "..." [...]: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="9efb0-277">Enter Certificate Host Name For Host '...' [...]: -> ENTER</span></span>
    * <span data-ttu-id="9efb0-278">Wprowadź nazwę użytkownika agenta hosta SAP (sapadm) hasło:</span><span class="sxs-lookup"><span data-stu-id="9efb0-278">Enter SAP Host Agent User (sapadm) Password:</span></span>
    * <span data-ttu-id="9efb0-279">Upewnij się, SAP hosta Agent użytkownika (sapadm) hasło:</span><span class="sxs-lookup"><span data-stu-id="9efb0-279">Confirm SAP Host Agent User (sapadm) Password:</span></span>
    * <span data-ttu-id="9efb0-280">Wprowadź administratora systemu (hdbadm) hasło:</span><span class="sxs-lookup"><span data-stu-id="9efb0-280">Enter System Administrator (hdbadm) Password:</span></span>
    * <span data-ttu-id="9efb0-281">Upewnij się, Administrator systemu (hdbadm) hasło:</span><span class="sxs-lookup"><span data-stu-id="9efb0-281">Confirm System Administrator (hdbadm) Password:</span></span>
    * <span data-ttu-id="9efb0-282">Wprowadź katalog macierzysty administratora systemu [/ usr/sap/HDB/głównej]: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="9efb0-282">Enter System Administrator Home Directory [/usr/sap/HDB/home]: -> ENTER</span></span>
    * <span data-ttu-id="9efb0-283">Wprowadź powłoka logowania administratora systemu [/ bin/sh]: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="9efb0-283">Enter System Administrator Login Shell [/bin/sh]: -> ENTER</span></span>
    * <span data-ttu-id="9efb0-284">Wprowadź identyfikator użytkownika administratora [1001]: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="9efb0-284">Enter System Administrator User ID [1001]: -> ENTER</span></span>
    * <span data-ttu-id="9efb0-285">Wprowadź identyfikator użytkownika grupy (sapsys) [79]: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="9efb0-285">Enter ID of User Group (sapsys) [79]: -> ENTER</span></span>
    * <span data-ttu-id="9efb0-286">Wprowadź hasło użytkownika (SYSTEM) bazy danych:</span><span class="sxs-lookup"><span data-stu-id="9efb0-286">Enter Database User (SYSTEM) Password:</span></span>
    * <span data-ttu-id="9efb0-287">Potwierdź hasło użytkownika (SYSTEM) bazy danych:</span><span class="sxs-lookup"><span data-stu-id="9efb0-287">Confirm Database User (SYSTEM) Password:</span></span>
    * <span data-ttu-id="9efb0-288">Uruchom ponownie system po ponownym uruchomieniu komputera?</span><span class="sxs-lookup"><span data-stu-id="9efb0-288">Restart system after machine reboot?</span></span> <span data-ttu-id="9efb0-289">[[n]: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="9efb0-289">[n]: -> ENTER</span></span>
    * <span data-ttu-id="9efb0-290">Czy chcesz toocontinue?</span><span class="sxs-lookup"><span data-stu-id="9efb0-290">Do you want toocontinue?</span></span> <span data-ttu-id="9efb0-291">(t/n):</span><span class="sxs-lookup"><span data-stu-id="9efb0-291">(y/n):</span></span>  
  <span data-ttu-id="9efb0-292">Sprawdź poprawność hello podsumowania, a następnie wprowadź y toocontinue</span><span class="sxs-lookup"><span data-stu-id="9efb0-292">Validate hello summary and enter y toocontinue</span></span>
1. <span data-ttu-id="9efb0-293">[A] Agent hosta uaktualnienia SAP</span><span class="sxs-lookup"><span data-stu-id="9efb0-293">[A] Upgrade SAP Host Agent</span></span>  
  <span data-ttu-id="9efb0-294">Pobierz najnowsze archiwum Agent hosta SAP hello z hello [SAP Softwarecenter] [ sap-swcenter] i uruchom hello następujące polecenia tooupgrade hello agenta.</span><span class="sxs-lookup"><span data-stu-id="9efb0-294">Download hello latest SAP Host Agent archive from hello [SAP Softwarecenter][sap-swcenter] and run hello following command tooupgrade hello agent.</span></span> <span data-ttu-id="9efb0-295">Zastąp hello ścieżki toohello archiwum toopoint toohello pobranego pliku.</span><span class="sxs-lookup"><span data-stu-id="9efb0-295">Replace hello path toohello archive toopoint toohello file you downloaded.</span></span>
    ```bash
    sudo /usr/sap/hostctrl/exe/saphostexec -upgrade -archive <path tooSAP Host Agent SAR>
    ```

1. <span data-ttu-id="9efb0-296">[1] utworzyć HANA replikacji (jako główny)</span><span class="sxs-lookup"><span data-stu-id="9efb0-296">[1] Create HANA replication (as root)</span></span>  
    <span data-ttu-id="9efb0-297">Uruchom następujące polecenie hello.</span><span class="sxs-lookup"><span data-stu-id="9efb0-297">Run hello following command.</span></span> <span data-ttu-id="9efb0-298">Upewnij się, że tooreplace bold ciągów (HANA systemu identyfikator HDB i numer wystąpienia 03) wartościami hello instalacji SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="9efb0-298">Make sure tooreplace bold strings (HANA System ID HDB and instance number 03) with hello values of your SAP HANA installation.</span></span>
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbsql -u system -i <b>03</b> 'CREATE USER <b>hdb</b>hasync PASSWORD "<b>passwd</b>"' 
    hdbsql -u system -i <b>03</b> 'GRANT DATA ADMIN too<b>hdb</b>hasync' 
    hdbsql -u system -i <b>03</b> 'ALTER USER <b>hdb</b>hasync DISABLE PASSWORD LIFETIME' 
    </code></pre>

1. <span data-ttu-id="9efb0-299">[A] utworzenia wpisu magazynu kluczy (jako główny)</span><span class="sxs-lookup"><span data-stu-id="9efb0-299">[A] Create keystore entry (as root)</span></span>
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbuserstore SET <b>hdb</b>haloc localhost:3<b>03</b>15 <b>hdb</b>hasync <b>passwd</b>
    </code></pre>
1. <span data-ttu-id="9efb0-300">[1] kopii zapasowej bazy danych (jako główny)</span><span class="sxs-lookup"><span data-stu-id="9efb0-300">[1] Backup database (as root)</span></span>
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbsql -u system -i <b>03</b> "BACKUP DATA USING FILE ('<b>initialbackup</b>')" 
    </code></pre>
1. <span data-ttu-id="9efb0-301">[1] Przełącz toohello sapsid użytkownika (na przykład hdbadm) i utworzyć hello lokacji głównej.</span><span class="sxs-lookup"><span data-stu-id="9efb0-301">[1] Switch toohello sapsid user (for example hdbadm) and create hello primary site.</span></span>
    <pre><code>
    su - <b>hdb</b>adm
    hdbnsutil -sr_enable –-name=<b>SITE1</b>
    </code></pre>
1. <span data-ttu-id="9efb0-302">[2] Przełącz toohello sapsid użytkownika (na przykład hdbadm) i utworzyć lokację dodatkową hello.</span><span class="sxs-lookup"><span data-stu-id="9efb0-302">[2] Switch toohello sapsid user (for example hdbadm) and create hello secondary site.</span></span>
    <pre><code>
    su - <b>hdb</b>adm
    sapcontrol -nr <b>03</b> -function StopWait 600 10
    hdbnsutil -sr_register --remoteHost=<b>saphanavm1</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE2</b> 
    </code></pre>

## <a name="configure-cluster-framework"></a><span data-ttu-id="9efb0-303">Konfigurowanie klastra Framework</span><span class="sxs-lookup"><span data-stu-id="9efb0-303">Configure Cluster Framework</span></span>

<span data-ttu-id="9efb0-304">Zmień ustawienia domyślne hello</span><span class="sxs-lookup"><span data-stu-id="9efb0-304">Change hello default settings</span></span>

<pre>
sudo vi crm-defaults.txt
# enter hello following toocrm-defaults.txt
<code>
property $id="cib-bootstrap-options" \
  no-quorum-policy="ignore" \
  stonith-enabled="true" \
  stonith-action="reboot" \
  stonith-timeout="150s"
rsc_defaults $id="rsc-options" \
  resource-stickiness="1000" \
  migration-threshold="5000"
op_defaults $id="op-options" \
  timeout="600"
</code>

# <a name="now-we-load-hello-file-toohello-cluster"></a><span data-ttu-id="9efb0-305">Teraz możemy załadować hello pliku toohello klastra</span><span class="sxs-lookup"><span data-stu-id="9efb0-305">now we load hello file toohello cluster</span></span>
<span data-ttu-id="9efb0-306">sudo crm Konfigurowanie aktualizacji obciążenia crm-defaults.txt</span><span class="sxs-lookup"><span data-stu-id="9efb0-306">sudo crm configure load update crm-defaults.txt</span></span>
</pre>

### <a name="create-stonith-device"></a><span data-ttu-id="9efb0-307">Utwórz urządzenie STONITH</span><span class="sxs-lookup"><span data-stu-id="9efb0-307">Create STONITH device</span></span>

<span data-ttu-id="9efb0-308">Witaj STONITH urządzenie używa nazwy głównej usługi tooauthorize przed Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="9efb0-308">hello STONITH device uses a Service Principal tooauthorize against Microsoft Azure.</span></span> <span data-ttu-id="9efb0-309">Wykonaj te kroki toocreate nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="9efb0-309">Please follow these steps toocreate a Service Principal.</span></span>

1. <span data-ttu-id="9efb0-310">Przejdź do zbyt<https://portal.azure.com></span><span class="sxs-lookup"><span data-stu-id="9efb0-310">Go too<https://portal.azure.com></span></span>
1. <span data-ttu-id="9efb0-311">Otwórz hello bloku usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9efb0-311">Open hello Azure Active Directory blade</span></span>  
   <span data-ttu-id="9efb0-312">Przejdź tooProperties i zanotuj hello identyfikator katalogu. Jest to hello **identyfikator dzierżawcy**.</span><span class="sxs-lookup"><span data-stu-id="9efb0-312">Go tooProperties and write down hello Directory Id. This is hello **tenant id**.</span></span>
1. <span data-ttu-id="9efb0-313">Kliknij przycisk rejestracji aplikacji</span><span class="sxs-lookup"><span data-stu-id="9efb0-313">Click App registrations</span></span>
1. <span data-ttu-id="9efb0-314">Kliknij pozycję Dodaj.</span><span class="sxs-lookup"><span data-stu-id="9efb0-314">Click Add</span></span>
1. <span data-ttu-id="9efb0-315">Wprowadź nazwę, wybierz typ aplikacji "Aplikacja/interfejs API sieci Web", wprowadź adres URL logowania (np. http://localhost) i kliknij przycisk Utwórz</span><span class="sxs-lookup"><span data-stu-id="9efb0-315">Enter a Name, select Application Type "Web app/API", enter a sign-on URL (for example http://localhost) and click Create</span></span>
1. <span data-ttu-id="9efb0-316">Witaj adres URL logowania nie jest używany i może być dowolny prawidłowy adres URL</span><span class="sxs-lookup"><span data-stu-id="9efb0-316">hello sign-on URL is not used and can be any valid URL</span></span>
1. <span data-ttu-id="9efb0-317">Wybierz hello nowej aplikacji i kliknij na karcie Ustawienia hello</span><span class="sxs-lookup"><span data-stu-id="9efb0-317">Select hello new App and click Keys in hello Settings tab</span></span>
1. <span data-ttu-id="9efb0-318">Wprowadź opis nowego klucza, wybierz pozycję "Nigdy nie wygasa" i kliknij przycisk Zapisz</span><span class="sxs-lookup"><span data-stu-id="9efb0-318">Enter a description for a new key, select "Never expires" and click Save</span></span>
1. <span data-ttu-id="9efb0-319">Zapisz hello wartość.</span><span class="sxs-lookup"><span data-stu-id="9efb0-319">Write down hello Value.</span></span> <span data-ttu-id="9efb0-320">Jest on używany jako hello **hasło** dla hello nazwy głównej usługi</span><span class="sxs-lookup"><span data-stu-id="9efb0-320">It is used as hello **password** for hello Service Principal</span></span>
1. <span data-ttu-id="9efb0-321">Zapisz hello identyfikator aplikacji. Jest używany jako hello username (**identyfikatora** w poniższych krokach hello) z hello nazwy głównej usługi</span><span class="sxs-lookup"><span data-stu-id="9efb0-321">Write down hello Application Id. It is used as hello username (**login id** in hello steps below) of hello Service Principal</span></span>

<span data-ttu-id="9efb0-322">Witaj nazwy głównej usługi nie ma uprawnienia tooaccess zasobów platformy Azure domyślnie.</span><span class="sxs-lookup"><span data-stu-id="9efb0-322">hello Service Principal does not have permissions tooaccess your Azure resources by default.</span></span> <span data-ttu-id="9efb0-323">Należy toogive hello nazwy głównej usługi uprawnienia toostart i Zatrzymaj (deallocate) wszystkich maszyn wirtualnych klastra hello.</span><span class="sxs-lookup"><span data-stu-id="9efb0-323">You need toogive hello Service Principal permissions toostart and stop (deallocate) all virtual machines of hello cluster.</span></span>

1. <span data-ttu-id="9efb0-324">Przejdź toohttps://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="9efb0-324">Go toohttps://portal.azure.com</span></span>
1. <span data-ttu-id="9efb0-325">Otwórz hello wszystkich bloku zasobów</span><span class="sxs-lookup"><span data-stu-id="9efb0-325">Open hello All resources blade</span></span>
1. <span data-ttu-id="9efb0-326">Wybierz maszynę wirtualną hello</span><span class="sxs-lookup"><span data-stu-id="9efb0-326">Select hello virtual machine</span></span>
1. <span data-ttu-id="9efb0-327">Kliknij przycisk kontroli dostępu (IAM)</span><span class="sxs-lookup"><span data-stu-id="9efb0-327">Click Access control (IAM)</span></span>
1. <span data-ttu-id="9efb0-328">Kliknij pozycję Dodaj.</span><span class="sxs-lookup"><span data-stu-id="9efb0-328">Click Add</span></span>
1. <span data-ttu-id="9efb0-329">Wybierz rolę hello właściciela</span><span class="sxs-lookup"><span data-stu-id="9efb0-329">Select hello role Owner</span></span>
1. <span data-ttu-id="9efb0-330">Wprowadź nazwę hello aplikacji hello utworzone powyżej</span><span class="sxs-lookup"><span data-stu-id="9efb0-330">Enter hello name of hello application you created above</span></span>
1. <span data-ttu-id="9efb0-331">Kliknij przycisk OK</span><span class="sxs-lookup"><span data-stu-id="9efb0-331">Click OK</span></span>

<span data-ttu-id="9efb0-332">Po edytować uprawnienia hello hello maszyn wirtualnych, możesz skonfigurować urządzenia STONITH hello hello klastra.</span><span class="sxs-lookup"><span data-stu-id="9efb0-332">After you edited hello permissions for hello virtual machines, you can configure hello STONITH devices in hello cluster.</span></span>

<pre>
sudo vi crm-fencing.txt
# enter hello following toocrm-fencing.txt
# replace hello bold string with your subscription id, resource group, tenant id, service principal id and password
<code>
primitive rsc_st_azure_1 stonith:fence_azure_arm \
    params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

primitive rsc_st_azure_2 stonith:fence_azure_arm \
    params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started
</code>

# <a name="now-we-load-hello-file-toohello-cluster"></a><span data-ttu-id="9efb0-333">Teraz możemy załadować hello pliku toohello klastra</span><span class="sxs-lookup"><span data-stu-id="9efb0-333">now we load hello file toohello cluster</span></span>
<span data-ttu-id="9efb0-334">sudo crm Konfigurowanie aktualizacji obciążenia crm-fencing.txt</span><span class="sxs-lookup"><span data-stu-id="9efb0-334">sudo crm configure load update crm-fencing.txt</span></span>
</pre>

### <a name="create-sap-hana-resources"></a><span data-ttu-id="9efb0-335">Utwórz zasoby SAP HANA</span><span class="sxs-lookup"><span data-stu-id="9efb0-335">Create SAP HANA resources</span></span>

<pre>
sudo vi crm-saphanatop.txt
# enter hello following toocrm-saphana.txt
# replace hello bold string with your instance number and HANA system id
<code>
primitive rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> ocf:suse:SAPHanaTopology \
    operations $id="rsc_sap2_<b>HDB</b>_HDB<b>03</b>-operations" \
    op monitor interval="10" timeout="600" \
    op start interval="0" timeout="600" \
    op stop interval="0" timeout="300" \
    params SID="<b>HDB</b>" InstanceNumber="<b>03</b>"

clone cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \
    meta is-managed="true" clone-node-max="1" target-role="Started" interleave="true"
</code>

# <a name="now-we-load-hello-file-toohello-cluster"></a><span data-ttu-id="9efb0-336">Teraz możemy załadować hello pliku toohello klastra</span><span class="sxs-lookup"><span data-stu-id="9efb0-336">now we load hello file toohello cluster</span></span>
<span data-ttu-id="9efb0-337">sudo crm Konfigurowanie aktualizacji obciążenia crm-saphanatop.txt</span><span class="sxs-lookup"><span data-stu-id="9efb0-337">sudo crm configure load update crm-saphanatop.txt</span></span>
</pre>

<pre>
sudo vi crm-saphana.txt
# enter hello following toocrm-saphana.txt
# replace hello bold string with your instance number, HANA system id and hello frontend IP address of hello Azure load balancer. 
<code>
primitive rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> ocf:suse:SAPHana \
    operations $id="rsc_sap_<b>HDB</b>_HDB<b>03</b>-operations" \
    op start interval="0" timeout="3600" \
    op stop interval="0" timeout="3600" \
    op promote interval="0" timeout="3600" \
    op monitor interval="60" role="Master" timeout="700" \
    op monitor interval="61" role="Slave" timeout="700" \
    params SID="<b>HDB</b>" InstanceNumber="<b>03</b>" PREFER_SITE_TAKEOVER="true" \
    DUPLICATE_PRIMARY_TIMEOUT="7200" AUTOMATED_REGISTER="false"

ms msl_SAPHana_<b>HDB</b>_HDB<b>03</b> rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> \
    meta is-managed="true" notify="true" clone-max="2" clone-node-max="1" \
    target-role="Started" interleave="true"

primitive rsc_ip_<b>HDB</b>_HDB<b>03</b> ocf:heartbeat:IPaddr2 \ 
    meta target-role="Started" is-managed="true" \ 
    operations $id="rsc_ip_<b>HDB</b>_HDB<b>03</b>-operations" \ 
    op monitor interval="10s" timeout="20s" \ 
    params ip="<b>10.0.0.21</b>" 
primitive rsc_nc_<b>HDB</b>_HDB<b>03</b> anything \ 
    params binfile="/usr/bin/nc" cmdline_options="-l -k 625<b>03</b>" \ 
    op monitor timeout=20s interval=10 depth=0 
group g_ip_<b>HDB</b>_HDB<b>03</b> rsc_ip_<b>HDB</b>_HDB<b>03</b> rsc_nc_<b>HDB</b>_HDB<b>03</b>
 
colocation col_saphana_ip_<b>HDB</b>_HDB<b>03</b> 2000: g_ip_<b>HDB</b>_HDB<b>03</b>:Started \ 
    msl_SAPHana_<b>HDB</b>_HDB<b>03</b>:Master  
order ord_SAPHana_<b>HDB</b>_HDB<b>03</b> 2000: cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \ 
    msl_SAPHana_<b>HDB</b>_HDB<b>03</b>
</code>

# <a name="now-we-load-hello-file-toohello-cluster"></a><span data-ttu-id="9efb0-338">Teraz możemy załadować hello pliku toohello klastra</span><span class="sxs-lookup"><span data-stu-id="9efb0-338">now we load hello file toohello cluster</span></span>
<span data-ttu-id="9efb0-339">sudo crm Konfigurowanie aktualizacji obciążenia crm-saphana.txt</span><span class="sxs-lookup"><span data-stu-id="9efb0-339">sudo crm configure load update crm-saphana.txt</span></span>
</pre>

### <a name="test-cluster-setup"></a><span data-ttu-id="9efb0-340">Konfiguracja klastra testu</span><span class="sxs-lookup"><span data-stu-id="9efb0-340">Test cluster setup</span></span>
<span data-ttu-id="9efb0-341">powitania po rozdziale opisano, jak można przetestować konfigurację.</span><span class="sxs-lookup"><span data-stu-id="9efb0-341">hello following chapter describe how you can test your setup.</span></span> <span data-ttu-id="9efb0-342">Każdy test założono, że są głównymi i wzorzec SAP HANA hello jest uruchomiona na powitania saphanavm1 maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9efb0-342">Every test assumes that you are root and hello SAP HANA master is running on hello virtual machine saphanavm1.</span></span>

#### <a name="fencing-test"></a><span data-ttu-id="9efb0-343">Test ogrodzenia</span><span class="sxs-lookup"><span data-stu-id="9efb0-343">Fencing Test</span></span>

<span data-ttu-id="9efb0-344">Instalator hello hello ogrodzenia agenta można przetestować wyłączając hello interfejs sieciowy na saphanavm1 węzła.</span><span class="sxs-lookup"><span data-stu-id="9efb0-344">You can test hello setup of hello fencing agent by disabling hello network interface on node saphanavm1.</span></span>

<pre><code>
sudo ifdown eth0
</code></pre>

<span data-ttu-id="9efb0-345">teraz Pobierz ponownie uruchomiona lub zatrzymana w zależności od konfiguracji klastra Hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9efb0-345">hello virtual machine should now get restarted or stopped depending on your cluster configuration.</span></span>
<span data-ttu-id="9efb0-346">Jeśli ustawisz toooff akcji stonith hello hello maszyny wirtualnej zostanie zatrzymana i zasoby hello są migrowane toohello uruchomienie maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9efb0-346">If you set hello stonith-action toooff, hello virtual machine will be stopped and hello resources are migrated toohello running virtual machine.</span></span>

<span data-ttu-id="9efb0-347">Po ponownym uruchomieniu maszyny wirtualnej hello hello zasobów SAP HANA zakończy się niepowodzeniem toostart pomocniczym po ustawieniu AUTOMATED_REGISTER = "false".</span><span class="sxs-lookup"><span data-stu-id="9efb0-347">Once you start hello virtual machine again, hello SAP HANA resource will fail toostart as secondary if you set AUTOMATED_REGISTER="false".</span></span> <span data-ttu-id="9efb0-348">W takim przypadku należy tooconfigure hello HANA wystąpienia jako dodatkowej, wykonując następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="9efb0-348">In this case, you need tooconfigure hello HANA instance as secondary by executing hello following command:</span></span>

<pre><code>
su - <b>hdb</b>adm

# Stop hello HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b>

# switch back tooroot and cleanup hello failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

#### <a name="testing-a-manual-failover"></a><span data-ttu-id="9efb0-349">Testowania ręcznego przełączania trybu failover</span><span class="sxs-lookup"><span data-stu-id="9efb0-349">Testing a manual failover</span></span>

<span data-ttu-id="9efb0-350">Zatrzymywanie usługi rozrusznik hello na węzeł saphanavm1 możesz przetestować ręcznego przełączania trybu failover.</span><span class="sxs-lookup"><span data-stu-id="9efb0-350">You can test a manual failover by stopping hello pacemaker service on node saphanavm1.</span></span>
<pre><code>
service pacemaker stop
</code></pre>

<span data-ttu-id="9efb0-351">Po hello w tryb failover można ponownie uruchomić usługę hello.</span><span class="sxs-lookup"><span data-stu-id="9efb0-351">After hello failover, you can start hello service again.</span></span> <span data-ttu-id="9efb0-352">Witaj SAP HANA zasobu na saphanavm1 zakończy się niepowodzeniem toostart pomocniczym po ustawieniu AUTOMATED_REGISTER = "false".</span><span class="sxs-lookup"><span data-stu-id="9efb0-352">hello SAP HANA resource on saphanavm1 will fail toostart as secondary if you set AUTOMATED_REGISTER="false".</span></span> <span data-ttu-id="9efb0-353">W takim przypadku należy tooconfigure hello HANA wystąpienia jako dodatkowej, wykonując następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="9efb0-353">In this case, you need tooconfigure hello HANA instance as secondary by executing hello following command:</span></span>

<pre><code>
service pacemaker start
su - <b>hdb</b>adm

# Stop hello HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b> 


# switch back tooroot and cleanup hello failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

#### <a name="testing-a-migration"></a><span data-ttu-id="9efb0-354">Testowanie migracji</span><span class="sxs-lookup"><span data-stu-id="9efb0-354">Testing a migration</span></span>

<span data-ttu-id="9efb0-355">Węzeł główny SAP HANA hello można migrować, wykonując następujące polecenia hello</span><span class="sxs-lookup"><span data-stu-id="9efb0-355">You can migrate hello SAP HANA master node by executing hello following command</span></span>
<pre><code>
crm resource migrate msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm2</b>
crm resource migrate g_ip_<b>HDB</b>_HDB<b>03</b> <b>saphanavm2</b>
</code></pre>

<span data-ttu-id="9efb0-356">To należy zmigrować węzła głównego SAP HANA hello i hello grupy, która zawiera hello toosaphanavm2 w wirtualnego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="9efb0-356">This should migrate hello SAP HANA master node and hello group that contains hello virtual IP address toosaphanavm2.</span></span>
<span data-ttu-id="9efb0-357">Witaj SAP HANA zasobu na saphanavm1 zakończy się niepowodzeniem toostart pomocniczym po ustawieniu AUTOMATED_REGISTER = "false".</span><span class="sxs-lookup"><span data-stu-id="9efb0-357">hello SAP HANA resource on saphanavm1 will fail toostart as secondary if you set AUTOMATED_REGISTER="false".</span></span> <span data-ttu-id="9efb0-358">W takim przypadku należy tooconfigure hello HANA wystąpienia jako dodatkowej, wykonując następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="9efb0-358">In this case, you need tooconfigure hello HANA instance as secondary by executing hello following command:</span></span>

<pre><code>
su - <b>hdb</b>adm

# Stop hello HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b> 
</code></pre>

<span data-ttu-id="9efb0-359">Migracja Hello tworzy ograniczenia lokalizacji, w których należy ponownie usunąć toobe.</span><span class="sxs-lookup"><span data-stu-id="9efb0-359">hello migration creates location contraints that need toobe deleted again.</span></span>

<pre><code>
crm configure edited

# delete location contraints that are named like hello following contraint. You should have two contraints, one for hello SAP HANA resource and one for hello IP address group.
location cli-prefer-g_ip_<b>HDB</b>_HDB<b>03</b> g_ip_<b>HDB</b>_HDB<b>03</b> role=Started inf: <b>saphanavm2</b>
</code></pre>

<span data-ttu-id="9efb0-360">Należy również toocleanup hello stanu zasobu węzła pomocniczego hello</span><span class="sxs-lookup"><span data-stu-id="9efb0-360">You also need toocleanup hello state of hello secondary node resource</span></span>

<pre><code>
# switch back tooroot and cleanup hello failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

## <a name="next-steps"></a><span data-ttu-id="9efb0-361">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9efb0-361">Next steps</span></span>
* <span data-ttu-id="9efb0-362">[Azure maszyn wirtualnych, planowania i wdrażania dla programu SAP][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="9efb0-362">[Azure Virtual Machines planning and implementation for SAP][planning-guide]</span></span>
* <span data-ttu-id="9efb0-363">[Maszyny wirtualne Azure wdrożenia SAP][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="9efb0-363">[Azure Virtual Machines deployment for SAP][deployment-guide]</span></span>
* <span data-ttu-id="9efb0-364">[Wdrożenia usługi Azure DBMS maszyny wirtualnej dla programu SAP][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="9efb0-364">[Azure Virtual Machines DBMS deployment for SAP][dbms-guide]</span></span>
* <span data-ttu-id="9efb0-365">toolearn jak tooestablish wysokiej dostępności i planu odzyskiwania po awarii programu SAP HANA na platformie Azure (wystąpienia duże), zobacz [SAP HANA (duże wystąpień) wysokiej dostępności i odzyskiwania po awarii na platformie Azure](hana-overview-high-availability-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="9efb0-365">toolearn how tooestablish high availability and plan for disaster recovery of SAP HANA on Azure (large instances), see [SAP HANA (large instances) high availability and disaster recovery on Azure](hana-overview-high-availability-disaster-recovery.md).</span></span> 
