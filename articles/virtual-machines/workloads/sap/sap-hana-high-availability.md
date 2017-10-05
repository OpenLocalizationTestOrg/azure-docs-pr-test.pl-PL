---
title: "Wysoka dostępność SAP HANA na maszynach wirtualnych platformy Azure (VM) | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 951150e621d21037b0adde7287b9f985290d8d11
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="high-availability-of-sap-hana-on-azure-virtual-machines-vms"></a><span data-ttu-id="cd48a-103">Wysoka dostępność SAP HANA na maszynach wirtualnych platformy Azure (VM)</span><span class="sxs-lookup"><span data-stu-id="cd48a-103">High Availability of SAP HANA on Azure Virtual Machines (VMs)</span></span>

[dbms-guide]:dbms-guide.md
[deployment-guide]:deployment-guide.md
[planning-guide]:planning-guide.md

<span data-ttu-id="cd48a-104">[2205917]:https://launchpad.support.sap.com/#/notes/2205917</span><span class="sxs-lookup"><span data-stu-id="cd48a-104">[2205917]:https://launchpad.support.sap.com/#/notes/2205917</span></span>
<span data-ttu-id="cd48a-105">[1944799]:https://launchpad.support.sap.com/#/notes/1944799</span><span class="sxs-lookup"><span data-stu-id="cd48a-105">[1944799]:https://launchpad.support.sap.com/#/notes/1944799</span></span>
<span data-ttu-id="cd48a-106">[1928533]:https://launchpad.support.sap.com/#/notes/1928533</span><span class="sxs-lookup"><span data-stu-id="cd48a-106">[1928533]:https://launchpad.support.sap.com/#/notes/1928533</span></span>
<span data-ttu-id="cd48a-107">[2015553]:https://launchpad.support.sap.com/#/notes/2015553</span><span class="sxs-lookup"><span data-stu-id="cd48a-107">[2015553]:https://launchpad.support.sap.com/#/notes/2015553</span></span>
<span data-ttu-id="cd48a-108">[2178632]:https://launchpad.support.sap.com/#/notes/2178632</span><span class="sxs-lookup"><span data-stu-id="cd48a-108">[2178632]:https://launchpad.support.sap.com/#/notes/2178632</span></span>
<span data-ttu-id="cd48a-109">[2191498]:https://launchpad.support.sap.com/#/notes/2191498</span><span class="sxs-lookup"><span data-stu-id="cd48a-109">[2191498]:https://launchpad.support.sap.com/#/notes/2191498</span></span>
<span data-ttu-id="cd48a-110">[2243692]:https://launchpad.support.sap.com/#/notes/2243692</span><span class="sxs-lookup"><span data-stu-id="cd48a-110">[2243692]:https://launchpad.support.sap.com/#/notes/2243692</span></span>
<span data-ttu-id="cd48a-111">[1984787]:https://launchpad.support.sap.com/#/notes/1984787</span><span class="sxs-lookup"><span data-stu-id="cd48a-111">[1984787]:https://launchpad.support.sap.com/#/notes/1984787</span></span>
<span data-ttu-id="cd48a-112">[1999351]:https://launchpad.support.sap.com/#/notes/1999351</span><span class="sxs-lookup"><span data-stu-id="cd48a-112">[1999351]:https://launchpad.support.sap.com/#/notes/1999351</span></span>

[hana-ha-guide-replication]:sap-hana-high-availability.md#14c19f65-b5aa-4856-9594-b81c7e4df73d
[hana-ha-guide-shared-storage]:sap-hana-high-availability.md#498de331-fa04-490b-997c-b078de457c9d

[suse-hana-ha-guide]:https://www.suse.com/docrep/documents/ir8w88iwu7/suse_linux_enterprise_server_for_sap_applications_12_sp1.pdf
[sap-swcenter]:https://launchpad.support.sap.com/#/softwarecenter
[template-multisid-db]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db%2Fazuredeploy.json
[template-converged]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-converged%2Fazuredeploy.json

<span data-ttu-id="cd48a-113">W infrastrukturze lokalnej, możesz użyć albo HANA replikacji systemu lub magazynu udostępnionego ustanowienie wysoką dostępność dla programu SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="cd48a-113">On-premises, you can use either HANA System Replication or use shared storage to establish high availability for SAP HANA.</span></span>
<span data-ttu-id="cd48a-114">Aktualnie obsługiwany jest tylko skonfigurowanie HANA replikacji systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="cd48a-114">We currently only support setting up HANA System Replication on Azure.</span></span> <span data-ttu-id="cd48a-115">SAP HANA replikacji składa się z jednego węzła głównego i co najmniej jeden podrzędny węzła.</span><span class="sxs-lookup"><span data-stu-id="cd48a-115">SAP HANA Replication consists of one master node and at least one slave node.</span></span> <span data-ttu-id="cd48a-116">Węzły podrzędne zmiany danych w węźle głównym są replikowane synchronicznie lub asynchronicznie.</span><span class="sxs-lookup"><span data-stu-id="cd48a-116">Changes to the data on the master node are replicated to the slave nodes synchronously or asynchronously.</span></span>

<span data-ttu-id="cd48a-117">W tym artykule opisano sposób wdrażania maszyn wirtualnych, konfigurowanie maszyn wirtualnych, zainstaluj platformę klaster, zainstalować i skonfigurować replikacji systemu SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="cd48a-117">This article describes how to deploy the virtual machines, configure the virtual machines, install the cluster framework, install and configure SAP HANA System Replication.</span></span>
<span data-ttu-id="cd48a-118">W konfiguracji przykład instalacji poleceń itp. liczby wystąpień 03 i HANA systemu identyfikator HDB jest używany.</span><span class="sxs-lookup"><span data-stu-id="cd48a-118">In the example configurations, installation commands etc. instance number 03 and HANA System ID HDB is used.</span></span>

<span data-ttu-id="cd48a-119">Przeczytaj następujące uwagi SAP i dokumenty najpierw</span><span class="sxs-lookup"><span data-stu-id="cd48a-119">Read the following SAP Notes and papers first</span></span>

* <span data-ttu-id="cd48a-120">Uwaga SAP [1928533], który zawiera:</span><span class="sxs-lookup"><span data-stu-id="cd48a-120">SAP Note [1928533], which has:</span></span>
  * <span data-ttu-id="cd48a-121">Lista rozmiary maszyn wirtualnych Azure, które są obsługiwane w przypadku wdrażania oprogramowania SAP</span><span class="sxs-lookup"><span data-stu-id="cd48a-121">List of Azure VM sizes that are supported for the deployment of SAP software</span></span>
  * <span data-ttu-id="cd48a-122">Informacje o rozmiary maszyn wirtualnych Azure ważne pojemności</span><span class="sxs-lookup"><span data-stu-id="cd48a-122">Important capacity information for Azure VM sizes</span></span>
  * <span data-ttu-id="cd48a-123">Obsługiwane oprogramowanie SAP i kombinacji bazy danych i systemu operacyjnego (OS)</span><span class="sxs-lookup"><span data-stu-id="cd48a-123">Supported SAP software, and operating system (OS) and database combinations</span></span>
  * <span data-ttu-id="cd48a-124">Wymagana wersja jądra SAP dla systemu Windows i Linux w systemie Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="cd48a-124">Required SAP kernel version for Windows and Linux on Microsoft Azure</span></span>
* <span data-ttu-id="cd48a-125">Uwaga SAP [2015553] wymieniono wymagania wstępne dotyczące wdrażania oprogramowania SAP SAP, obsługiwane na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="cd48a-125">SAP Note [2015553] lists prerequisites for SAP-supported SAP software deployments in Azure.</span></span>
* <span data-ttu-id="cd48a-126">Uwaga SAP [2205917] zawiera zalecane ustawienia systemu operacyjnego SUSE Linux Enterprise Server dla programu SAP aplikacji</span><span class="sxs-lookup"><span data-stu-id="cd48a-126">SAP Note [2205917] has recommended OS settings for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="cd48a-127">Uwaga SAP [1944799] ma SAP HANA wytyczne dla SUSE Linux Enterprise Server dla programu SAP aplikacji</span><span class="sxs-lookup"><span data-stu-id="cd48a-127">SAP Note [1944799] has SAP HANA Guidelines for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="cd48a-128">Uwaga SAP [2178632] zawiera szczegółowe informacje na temat wszystkie funkcje monitorowania metryki zgłoszone dla SAP na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="cd48a-128">SAP Note [2178632] has detailed information about all monitoring metrics reported for SAP in Azure.</span></span>
* <span data-ttu-id="cd48a-129">Uwaga SAP [2191498] ma wymaganą wersję agenta hosta SAP dla systemu Linux na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="cd48a-129">SAP Note [2191498] has the required SAP Host Agent version for Linux in Azure.</span></span>
* <span data-ttu-id="cd48a-130">Uwaga SAP [2243692] zawiera informacje o licencjonowaniu SAP w systemie Linux na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="cd48a-130">SAP Note [2243692] has information about SAP licensing on Linux in Azure.</span></span>
* <span data-ttu-id="cd48a-131">Uwaga SAP [1984787] zawiera ogólne informacje o systemie SUSE Linux Enterprise Server 12.</span><span class="sxs-lookup"><span data-stu-id="cd48a-131">SAP Note [1984787] has general information about SUSE Linux Enterprise Server 12.</span></span>
* <span data-ttu-id="cd48a-132">Uwaga SAP [1999351] zawiera dodatkowe informacje dotyczące rozwiązywania problemów Azure rozszerzone monitorowanie rozszerzenia dla programu SAP.</span><span class="sxs-lookup"><span data-stu-id="cd48a-132">SAP Note [1999351] has additional troubleshooting information for the Azure Enhanced Monitoring Extension for SAP.</span></span>
* <span data-ttu-id="cd48a-133">[SAP społeczności WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) ma wszystkie wymagane informacje SAP dla systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="cd48a-133">[SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) has all required SAP Notes for Linux.</span></span>
* <span data-ttu-id="cd48a-134">[Azure maszyn wirtualnych, planowania i wdrażania dla SAP w systemie Linux][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="cd48a-134">[Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide]</span></span>
* <span data-ttu-id="cd48a-135">[Maszyny wirtualne Azure wdrożenie SAP w systemie Linux (w tym artykule)][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="cd48a-135">[Azure Virtual Machines deployment for SAP on Linux (this article)][deployment-guide]</span></span>
* <span data-ttu-id="cd48a-136">[Azure maszyn wirtualnych systemu DBMS wdrożenie SAP w systemie Linux][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="cd48a-136">[Azure Virtual Machines DBMS deployment for SAP on Linux][dbms-guide]</span></span>
* <span data-ttu-id="cd48a-137">[SAP HANA SR wydajności zoptymalizowanych pod kątem scenariusza] [ suse-hana-ha-guide] zawiera wszystkie wymagane informacje, aby skonfigurować lokalne replikacji systemu SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="cd48a-137">[SAP HANA SR Performance Optimized Scenario][suse-hana-ha-guide] The guide contains all required information to set up SAP HANA System Replication on-premises.</span></span> <span data-ttu-id="cd48a-138">Użyj tego podręcznika, jako linii bazowej.</span><span class="sxs-lookup"><span data-stu-id="cd48a-138">Use this guide as a baseline.</span></span>

## <a name="deploying-linux"></a><span data-ttu-id="cd48a-139">Wdrażanie systemu Linux</span><span class="sxs-lookup"><span data-stu-id="cd48a-139">Deploying Linux</span></span>

<span data-ttu-id="cd48a-140">Agent zasobów dla SAP HANA znajduje się w systemie SUSE Linux Enterprise Server aplikacje SAP.</span><span class="sxs-lookup"><span data-stu-id="cd48a-140">The resource agent for SAP HANA is included in SUSE Linux Enterprise Server for SAP Applications.</span></span>
<span data-ttu-id="cd48a-141">Portalu Azure Marketplace zawiera obraz systemu SUSE Linux Enterprise Server dla programu SAP 12 aplikacji z BYOS (Bring Your własnej subskrypcji), który służy do wdrażania nowych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="cd48a-141">The Azure Marketplace contains an image for SUSE Linux Enterprise Server for SAP Applications 12 with BYOS (Bring Your Own Subscription) that you can use to deploy new virtual machines.</span></span>

### <a name="manual-deployment"></a><span data-ttu-id="cd48a-142">Ręczne wdrażanie</span><span class="sxs-lookup"><span data-stu-id="cd48a-142">Manual Deployment</span></span>

1. <span data-ttu-id="cd48a-143">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="cd48a-143">Create a Resource Group</span></span>
1. <span data-ttu-id="cd48a-144">Tworzenie sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="cd48a-144">Create a Virtual Network</span></span>
1. <span data-ttu-id="cd48a-145">Utwórz dwa konta magazynu</span><span class="sxs-lookup"><span data-stu-id="cd48a-145">Create two Storage Accounts</span></span>
1. <span data-ttu-id="cd48a-146">Tworzenie zestawu dostępności</span><span class="sxs-lookup"><span data-stu-id="cd48a-146">Create an Availability Set</span></span>  
   <span data-ttu-id="cd48a-147">Zestaw aktualizacji max domeny</span><span class="sxs-lookup"><span data-stu-id="cd48a-147">Set max update domain</span></span>
1. <span data-ttu-id="cd48a-148">Tworzenie modułu równoważenia obciążenia (wewnętrzny)</span><span class="sxs-lookup"><span data-stu-id="cd48a-148">Create a Load Balancer (internal)</span></span>  
   <span data-ttu-id="cd48a-149">Wybierz sieć Wirtualną w kroku powyżej</span><span class="sxs-lookup"><span data-stu-id="cd48a-149">Select VNET of step above</span></span>
1. <span data-ttu-id="cd48a-150">Utwórz maszynę wirtualną 1</span><span class="sxs-lookup"><span data-stu-id="cd48a-150">Create Virtual Machine 1</span></span>  
   <span data-ttu-id="cd48a-151">https://Portal.Azure.com/#Create/SUSE-byos.SLES-for-SAP-byos12-SP1</span><span class="sxs-lookup"><span data-stu-id="cd48a-151">https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1</span></span>  
   <span data-ttu-id="cd48a-152">SLES 12 aplikacje SAP z dodatkiem SP1 (BYOS)</span><span class="sxs-lookup"><span data-stu-id="cd48a-152">SLES For SAP Applications 12 SP1 (BYOS)</span></span>  
   <span data-ttu-id="cd48a-153">Wybierz konto magazynu 1</span><span class="sxs-lookup"><span data-stu-id="cd48a-153">Select Storage Account 1</span></span>  
   <span data-ttu-id="cd48a-154">Wybierz zestaw dostępności</span><span class="sxs-lookup"><span data-stu-id="cd48a-154">Select Availability Set</span></span>  
1. <span data-ttu-id="cd48a-155">Tworzenie maszyny wirtualnej 2</span><span class="sxs-lookup"><span data-stu-id="cd48a-155">Create Virtual Machine 2</span></span>  
   <span data-ttu-id="cd48a-156">https://Portal.Azure.com/#Create/SUSE-byos.SLES-for-SAP-byos12-SP1</span><span class="sxs-lookup"><span data-stu-id="cd48a-156">https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1</span></span>  
   <span data-ttu-id="cd48a-157">SLES 12 aplikacje SAP z dodatkiem SP1 (BYOS)</span><span class="sxs-lookup"><span data-stu-id="cd48a-157">SLES For SAP Applications 12 SP1 (BYOS)</span></span>  
   <span data-ttu-id="cd48a-158">Wybierz konto magazynu 2</span><span class="sxs-lookup"><span data-stu-id="cd48a-158">Select Storage Account 2</span></span>   
   <span data-ttu-id="cd48a-159">Wybierz zestaw dostępności</span><span class="sxs-lookup"><span data-stu-id="cd48a-159">Select Availability Set</span></span>  
1. <span data-ttu-id="cd48a-160">Dodawanie dysków z danymi</span><span class="sxs-lookup"><span data-stu-id="cd48a-160">Add Data Disks</span></span>
1. <span data-ttu-id="cd48a-161">Konfigurowanie usługi równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="cd48a-161">Configure the load balancer</span></span>
    1. <span data-ttu-id="cd48a-162">Utwórz pulę IP frontonu</span><span class="sxs-lookup"><span data-stu-id="cd48a-162">Create a frontend IP pool</span></span>
        1. <span data-ttu-id="cd48a-163">Otwórz moduł równoważenia obciążenia, wybierz puli adresów IP frontonu i kliknij przycisk Dodaj</span><span class="sxs-lookup"><span data-stu-id="cd48a-163">Open the load balancer, select frontend IP pool and click Add</span></span>
        1. <span data-ttu-id="cd48a-164">Wprowadź nazwę puli adresów IP nowego serwera sieci Web (na przykład frontonu hana)</span><span class="sxs-lookup"><span data-stu-id="cd48a-164">Enter the name of the new frontend IP pool (for example hana-frontend)</span></span>
       1. <span data-ttu-id="cd48a-165">Kliknij przycisk OK</span><span class="sxs-lookup"><span data-stu-id="cd48a-165">Click OK</span></span>
        1. <span data-ttu-id="cd48a-166">Po utworzeniu puli adresów IP frontonu, zanotuj jego adresu IP</span><span class="sxs-lookup"><span data-stu-id="cd48a-166">After the new frontend IP pool is created, write down its IP address</span></span>
    1. <span data-ttu-id="cd48a-167">Tworzenie puli wewnętrznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="cd48a-167">Create a backend pool</span></span>
        1. <span data-ttu-id="cd48a-168">Otwórz moduł równoważenia obciążenia, wybierz pul zaplecza i kliknij przycisk Dodaj</span><span class="sxs-lookup"><span data-stu-id="cd48a-168">Open the load balancer, select backend pools and click Add</span></span>
        1. <span data-ttu-id="cd48a-169">Wprowadź nazwę dla nowej puli wewnętrznej bazy danych (na przykład zaplecze hana)</span><span class="sxs-lookup"><span data-stu-id="cd48a-169">Enter the name of the new backend pool (for example hana-backend)</span></span>
        1. <span data-ttu-id="cd48a-170">Kliknij przycisk Dodaj maszynę wirtualną</span><span class="sxs-lookup"><span data-stu-id="cd48a-170">Click Add a virtual machine</span></span>
        1. <span data-ttu-id="cd48a-171">Wybierz zestaw dostępności utworzoną wcześniej</span><span class="sxs-lookup"><span data-stu-id="cd48a-171">Select the Availability Set you created earlier</span></span>
        1. <span data-ttu-id="cd48a-172">Wybierz maszyny wirtualne klastra SAP HANA</span><span class="sxs-lookup"><span data-stu-id="cd48a-172">Select the virtual machines of the SAP HANA cluster</span></span>
        1. <span data-ttu-id="cd48a-173">Kliknij przycisk OK</span><span class="sxs-lookup"><span data-stu-id="cd48a-173">Click OK</span></span>
    1. <span data-ttu-id="cd48a-174">Utworzyć sondy kondycji</span><span class="sxs-lookup"><span data-stu-id="cd48a-174">Create a health probe</span></span>
       1. <span data-ttu-id="cd48a-175">Otwórz moduł równoważenia obciążenia, wybierz sond kondycji i kliknij przycisk Dodaj</span><span class="sxs-lookup"><span data-stu-id="cd48a-175">Open the load balancer, select health probes and click Add</span></span>
        1. <span data-ttu-id="cd48a-176">Wprowadź nazwę nowego sondy kondycji (na przykład hp hana)</span><span class="sxs-lookup"><span data-stu-id="cd48a-176">Enter the name of the new health probe (for example hana-hp)</span></span>
        1. <span data-ttu-id="cd48a-177">Wybierz protokół, port 625 TCP**03**, interwał 5 i próg złej kondycji 2</span><span class="sxs-lookup"><span data-stu-id="cd48a-177">Select TCP as protocol, port 625**03**, keep Interval 5 and Unhealthy threshold 2</span></span>
        1. <span data-ttu-id="cd48a-178">Kliknij przycisk OK</span><span class="sxs-lookup"><span data-stu-id="cd48a-178">Click OK</span></span>
    1. <span data-ttu-id="cd48a-179">Tworzenie reguł równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="cd48a-179">Create load balancing rules</span></span>
        1. <span data-ttu-id="cd48a-180">Otwórz moduł równoważenia obciążenia, wybierz reguły równoważenia obciążenia i kliknij przycisk Dodaj</span><span class="sxs-lookup"><span data-stu-id="cd48a-180">Open the load balancer, select load balancing rules and click Add</span></span>
        1. <span data-ttu-id="cd48a-181">Wprowadź nazwę nowej reguły modułu równoważenia obciążenia (na przykład hana-lb-3**03**15)</span><span class="sxs-lookup"><span data-stu-id="cd48a-181">Enter the name of the new load balancer rule (for example hana-lb-3**03**15)</span></span>
        1. <span data-ttu-id="cd48a-182">Wybierz adres IP frontonu, puli wewnętrznej bazy danych i kondycji sondowania utworzonego wcześniej (na przykład frontonu hana)</span><span class="sxs-lookup"><span data-stu-id="cd48a-182">Select the frontend IP address, backend pool and health probe you created earlier (for example hana-frontend)</span></span>
        1. <span data-ttu-id="cd48a-183">Zachowaj protokołu TCP, wprowadź port 3**03**15</span><span class="sxs-lookup"><span data-stu-id="cd48a-183">Keep protocol TCP, enter port 3**03**15</span></span>
        1. <span data-ttu-id="cd48a-184">Zwiększ limit czasu bezczynności do 30 minut</span><span class="sxs-lookup"><span data-stu-id="cd48a-184">Increase idle timeout to 30 minutes</span></span>
       1. <span data-ttu-id="cd48a-185">**Upewnij się, że można włączyć pływającego adresu IP**</span><span class="sxs-lookup"><span data-stu-id="cd48a-185">**Make sure to enable Floating IP**</span></span>
        1. <span data-ttu-id="cd48a-186">Kliknij przycisk OK</span><span class="sxs-lookup"><span data-stu-id="cd48a-186">Click OK</span></span>
        1. <span data-ttu-id="cd48a-187">Powtórz powyższe kroki dla portu 3**03**17</span><span class="sxs-lookup"><span data-stu-id="cd48a-187">Repeat the steps above for port 3**03**17</span></span>

### <a name="deploy-with-template"></a><span data-ttu-id="cd48a-188">Wdrażanie za pomocą szablonu</span><span class="sxs-lookup"><span data-stu-id="cd48a-188">Deploy with template</span></span>
<span data-ttu-id="cd48a-189">Umożliwia jednego z szablonów szybki start w serwisie github wdrożenie wszystkich wymaganych zasobów.</span><span class="sxs-lookup"><span data-stu-id="cd48a-189">You can use one of the quick start templates on github to deploy all required resources.</span></span> <span data-ttu-id="cd48a-190">Szablon wdraża maszyny wirtualne, usługi równoważenia obciążenia, dostępność ustawić itd. Wykonaj następujące kroki, aby wdrożyć szablon:</span><span class="sxs-lookup"><span data-stu-id="cd48a-190">The template deploys the virtual machines, the load balancer, availability set etc. Follow these steps to deploy the template:</span></span>

1. <span data-ttu-id="cd48a-191">Otwórz [szablonu bazy danych] [ template-multisid-db] lub [zbieżność szablonu] [ template-converged] w portalu Azure, jedynie tworzy szablon bazy danych Równoważenie obciążenia zasady dla bazy danych, natomiast konwergentnej szablon tworzy także reguły równoważenia obciążenia ASCS/SCS i wystąpienia Wywołujących (tylko w systemie Linux).</span><span class="sxs-lookup"><span data-stu-id="cd48a-191">Open the [database template][template-multisid-db] or the [converged template][template-converged] on the Azure Portal The database template only creates the load-balancing rules for a database whereas the converged template also creates the load-balancing rules for an ASCS/SCS and ERS (Linux only) instance.</span></span> <span data-ttu-id="cd48a-192">Jeśli planujesz zainstalowanie systemu SAP NetWeaver na podstawie i również chcesz zainstalować wystąpienie ASCS/SCS na tej samej maszyny, użyj [zbieżność szablonu][template-converged].</span><span class="sxs-lookup"><span data-stu-id="cd48a-192">If you plan to install an SAP NetWeaver based system and you also want to install the ASCS/SCS instance on the same machines, use the [converged template][template-converged].</span></span>
1. <span data-ttu-id="cd48a-193">Wprowadź następujące parametry</span><span class="sxs-lookup"><span data-stu-id="cd48a-193">Enter the following parameters</span></span>
    1. <span data-ttu-id="cd48a-194">Identyfikator systemu SAP</span><span class="sxs-lookup"><span data-stu-id="cd48a-194">Sap System Id</span></span>  
       <span data-ttu-id="cd48a-195">Wprowadź systemu SAP identyfikator systemu SAP, które chcesz zainstalować.</span><span class="sxs-lookup"><span data-stu-id="cd48a-195">Enter the SAP system Id of the SAP system you want to install.</span></span> <span data-ttu-id="cd48a-196">Identyfikator będzie służyć jako prefiks dla zasobów, które zostały wdrożone.</span><span class="sxs-lookup"><span data-stu-id="cd48a-196">The Id will be used as a prefix for the resources that are deployed.</span></span>
    1. <span data-ttu-id="cd48a-197">Typ stosu (dotyczy tylko jeśli używasz szablonu konwergentnej)</span><span class="sxs-lookup"><span data-stu-id="cd48a-197">Stack Type (only applicable if you use the converged template)</span></span>  
       <span data-ttu-id="cd48a-198">Wybierz typ SAP NetWeaver stosu</span><span class="sxs-lookup"><span data-stu-id="cd48a-198">Select the SAP NetWeaver stack type</span></span>
    1. <span data-ttu-id="cd48a-199">Typ systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="cd48a-199">Os Type</span></span>  
       <span data-ttu-id="cd48a-200">Wybierz jedną z dystrybucje systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="cd48a-200">Select one of the Linux distributions.</span></span> <span data-ttu-id="cd48a-201">Na przykład wybierz SLES 12 BYOS</span><span class="sxs-lookup"><span data-stu-id="cd48a-201">For this example, select SLES 12 BYOS</span></span>
    1. <span data-ttu-id="cd48a-202">Typ bazy danych</span><span class="sxs-lookup"><span data-stu-id="cd48a-202">Db Type</span></span>  
       <span data-ttu-id="cd48a-203">Wybierz HANA</span><span class="sxs-lookup"><span data-stu-id="cd48a-203">Select HANA</span></span>
    1. <span data-ttu-id="cd48a-204">Rozmiar systemu SAP</span><span class="sxs-lookup"><span data-stu-id="cd48a-204">Sap System Size</span></span>  
       <span data-ttu-id="cd48a-205">Ilość protokoły SAP zapewnia nowy system.</span><span class="sxs-lookup"><span data-stu-id="cd48a-205">The amount of SAPS the new system will provide.</span></span> <span data-ttu-id="cd48a-206">Jeśli nie wiadomo jak wiele protokoły SAP wymaga systemu, należy skontaktować się z partnerem technologii SAP lub Integrator systemu</span><span class="sxs-lookup"><span data-stu-id="cd48a-206">If you are not sure how many SAPS the system will require, please ask your SAP Technology Partner or System Integrator</span></span>
    1. <span data-ttu-id="cd48a-207">Dostępność systemu</span><span class="sxs-lookup"><span data-stu-id="cd48a-207">System Availability</span></span>  
       <span data-ttu-id="cd48a-208">Wybierz opcję wysokiej dostępności</span><span class="sxs-lookup"><span data-stu-id="cd48a-208">Select HA</span></span>
    1. <span data-ttu-id="cd48a-209">Nazwa użytkownika i hasło administratora</span><span class="sxs-lookup"><span data-stu-id="cd48a-209">Admin Username and Admin Password</span></span>  
       <span data-ttu-id="cd48a-210">Tworzony jest nowy użytkownik, który może służyć do logowania się do komputera.</span><span class="sxs-lookup"><span data-stu-id="cd48a-210">A new user is created that can be used to log on to the machine.</span></span>
    1. <span data-ttu-id="cd48a-211">Nowy lub istniejący podsieci</span><span class="sxs-lookup"><span data-stu-id="cd48a-211">New Or Existing Subnet</span></span>  
       <span data-ttu-id="cd48a-212">Określa, czy należy utworzyć nową sieć wirtualną i podsieć lub istniejącą podsieć powinna być używana.</span><span class="sxs-lookup"><span data-stu-id="cd48a-212">Determines whether a new virtual network and subnet should be created or an existing subnet should be used.</span></span> <span data-ttu-id="cd48a-213">Jeśli masz już sieć wirtualną, która jest połączona z siecią lokalną, wybierz istniejącą.</span><span class="sxs-lookup"><span data-stu-id="cd48a-213">If you already have a virtual network that is connected to your on-premises network, select existing.</span></span>
    1. <span data-ttu-id="cd48a-214">Identyfikator podsieci</span><span class="sxs-lookup"><span data-stu-id="cd48a-214">Subnet Id</span></span>  
    <span data-ttu-id="cd48a-215">Identyfikator podsieci, do której maszyny wirtualne powinny być podłączone do.</span><span class="sxs-lookup"><span data-stu-id="cd48a-215">The ID of the subnet to which the virtual machines should be connected to.</span></span> <span data-ttu-id="cd48a-216">Wybierz podsieć sieci VPN lub usługi Express Route wirtualnej sieci lokalnej nawiązać połączenia z maszyną wirtualną.</span><span class="sxs-lookup"><span data-stu-id="cd48a-216">Select the subnet of your VPN or Express Route virtual network to connect the virtual machine to your on-premises network.</span></span> <span data-ttu-id="cd48a-217">Identyfikator zwykle wygląda /subscriptions/`<subscription id`> /resourceGroups/`<resource group name`> /providers/Microsoft.Network/virtualNetworks/`<virtual network name`> /subnets/`<subnet name`></span><span class="sxs-lookup"><span data-stu-id="cd48a-217">The ID usually looks like /subscriptions/`<subscription id`>/resourceGroups/`<resource group name`>/providers/Microsoft.Network/virtualNetworks/`<virtual network name`>/subnets/`<subnet name`></span></span>

## <a name="setting-up-linux-ha"></a><span data-ttu-id="cd48a-218">Konfigurowanie HA systemu Linux</span><span class="sxs-lookup"><span data-stu-id="cd48a-218">Setting up Linux HA</span></span>

<span data-ttu-id="cd48a-219">Następujące elementy są poprzedzane prefiksem [A] - mają zastosowanie do wszystkich węzłów [1] — dotyczy to tylko węzeł 1 lub [2] — dotyczy to tylko węzeł 2.</span><span class="sxs-lookup"><span data-stu-id="cd48a-219">The following items are prefixed with either [A] - applicable to all nodes, [1] - only applicable to node 1 or [2] - only applicable to node 2.</span></span>

1. <span data-ttu-id="cd48a-220">[A] SLES dla SAP BYOS tylko - zarejestrować SLES, aby można było użyć repozytoria</span><span class="sxs-lookup"><span data-stu-id="cd48a-220">[A] SLES for SAP BYOS only - Register SLES to be able to use the repositories</span></span>
1. <span data-ttu-id="cd48a-221">[A] SLES dla SAP BYOS tylko — Dodaj moduł chmury publicznej</span><span class="sxs-lookup"><span data-stu-id="cd48a-221">[A] SLES for SAP BYOS only - Add public-cloud module</span></span>
1. <span data-ttu-id="cd48a-222">[A] Aktualizacja SLES</span><span class="sxs-lookup"><span data-stu-id="cd48a-222">[A] Update SLES</span></span>
    ```bash
    sudo zypper update

    ```

1. <span data-ttu-id="cd48a-223">[1] dostęp ssh</span><span class="sxs-lookup"><span data-stu-id="cd48a-223">[1] Enable ssh access</span></span>
    ```bash
    sudo ssh-keygen -tdsa
    
    # Enter file in which to save the key (/root/.ssh/id_dsa): -> ENTER
    # Enter passphrase (empty for no passphrase): -> ENTER
    # Enter same passphrase again: -> ENTER
    
    # copy the public key
    sudo cat /root/.ssh/id_dsa.pub
    ```

2. <span data-ttu-id="cd48a-224">[2] dostęp ssh</span><span class="sxs-lookup"><span data-stu-id="cd48a-224">[2] Enable ssh access</span></span>
    ```bash
    sudo ssh-keygen -tdsa

    # insert the public key you copied in the last step into the authorized keys file on the second server
    sudo vi /root/.ssh/authorized_keys
    
    # Enter file in which to save the key (/root/.ssh/id_dsa): -> ENTER
    # Enter passphrase (empty for no passphrase): -> ENTER
    # Enter same passphrase again: -> ENTER
    
    # copy the public key    
    sudo cat /root/.ssh/id_dsa.pub
    ```

1. <span data-ttu-id="cd48a-225">[1] dostęp ssh</span><span class="sxs-lookup"><span data-stu-id="cd48a-225">[1] Enable ssh access</span></span>
    ```bash
    # insert the public key you copied in the last step into the authorized keys file on the first server
    sudo vi /root/.ssh/authorized_keys
    
    ```

1. <span data-ttu-id="cd48a-226">[A] należy zainstalować rozszerzenie wysokiej dostępności</span><span class="sxs-lookup"><span data-stu-id="cd48a-226">[A] Install HA extension</span></span>
    ```bash
    sudo zypper install sle-ha-release fence-agents
    
    ```

1. <span data-ttu-id="cd48a-227">[A] układ dysku instalacji</span><span class="sxs-lookup"><span data-stu-id="cd48a-227">[A] Setup disk layout</span></span>
    1. <span data-ttu-id="cd48a-228">LVM</span><span class="sxs-lookup"><span data-stu-id="cd48a-228">LVM</span></span>  
    <span data-ttu-id="cd48a-229">Ogólnie zaleca się używania LVM dla woluminów, które przechowują dane i pliki dziennika.</span><span class="sxs-lookup"><span data-stu-id="cd48a-229">We generally recommend to use LVM for volumes that store data and log files.</span></span> <span data-ttu-id="cd48a-230">W poniższym przykładzie założenia, że maszyny wirtualne czterech dyskach danych dołączonych, które powinny być używane do tworzenia dwa woluminy.</span><span class="sxs-lookup"><span data-stu-id="cd48a-230">The example below assumes that the virtual machines have four data disks attached that should be used to create two volumes.</span></span>
        * <span data-ttu-id="cd48a-231">Utwórz woluminy fizyczne dla wszystkich dysków, które chcesz użyć.</span><span class="sxs-lookup"><span data-stu-id="cd48a-231">Create physical volumes for all disks that you want to use.</span></span>
    <pre><code>
    sudo pvcreate /dev/sdc
    sudo pvcreate /dev/sdd
    sudo pvcreate /dev/sde
    sudo pvcreate /dev/sdf
    </code></pre>
        * <span data-ttu-id="cd48a-232">Utwórz grupę woluminu plików danych, jedna grupa woluminu dla plików dziennika i jeden do udostępnionego katalogu SAP HANA</span><span class="sxs-lookup"><span data-stu-id="cd48a-232">Create a volume group for the data files, one volume group for the log files and one for the shared directory of SAP HANA</span></span>
    <pre><code>
    sudo vgcreate vg_hana_data /dev/sdc /dev/sdd
    sudo vgcreate vg_hana_log /dev/sde
    sudo vgcreate vg_hana_shared /dev/sdf
    </code></pre>
        * <span data-ttu-id="cd48a-233">Utwórz woluminy logiczne</span><span class="sxs-lookup"><span data-stu-id="cd48a-233">Create the logical volumes</span></span>
    <pre><code>
    sudo lvcreate -l 100%FREE -n hana_data vg_hana_data
    sudo lvcreate -l 100%FREE -n hana_log vg_hana_log
    sudo lvcreate -l 100%FREE -n hana_shared vg_hana_shared
    sudo mkfs.xfs /dev/vg_hana_data/hana_data
    sudo mkfs.xfs /dev/vg_hana_log/hana_log
    sudo mkfs.xfs /dev/vg_hana_shared/hana_shared
    </code></pre>
        * <span data-ttu-id="cd48a-234">Utwórz katalogi instalacji i skopiuj identyfikator UUID wszystkie woluminy logiczne</span><span class="sxs-lookup"><span data-stu-id="cd48a-234">Create the mount directories and copy the UUID of all logical volumes</span></span>
    <pre><code>
    sudo mkdir -p /hana/data
    sudo mkdir -p /hana/log
    sudo mkdir -p /hana/shared
    # write down the id of /dev/vg_hana_data/hana_data, /dev/vg_hana_log/hana_log and /dev/vg_hana_shared/hana_shared
    sudo blkid
    </code></pre>
        * <span data-ttu-id="cd48a-235">Tworzenie wpisów fstab trzy logiczne woluminów</span><span class="sxs-lookup"><span data-stu-id="cd48a-235">Create fstab entries for the three logical volumes</span></span>
    <pre><code>
    sudo vi /etc/fstab
    </code></pre>
    <span data-ttu-id="cd48a-236">Wstaw ten wiersz, aby /etc/fstab</span><span class="sxs-lookup"><span data-stu-id="cd48a-236">Insert this line to /etc/fstab</span></span>
    <pre><code>
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_data/hana_data&gt;</b> /hana/data xfs  defaults,nofail  0  2
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_log/hana_log&gt;</b> /hana/log xfs  defaults,nofail  0  2
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_shared/hana_shared&gt;</b> /hana/shared xfs  defaults,nofail  0  2
    </code></pre>
        * <span data-ttu-id="cd48a-237">Zainstaluj nowe woluminy</span><span class="sxs-lookup"><span data-stu-id="cd48a-237">Mount the new volumes</span></span>
    <pre><code>
    sudo mount -a
    </code></pre>
    1. <span data-ttu-id="cd48a-238">Zwykły dysków</span><span class="sxs-lookup"><span data-stu-id="cd48a-238">Plain Disks</span></span>  
       <span data-ttu-id="cd48a-239">Dla małych lub demonstracyjnych systemów, możesz umieścić HANA plików danych i dziennika na jednym dysku.</span><span class="sxs-lookup"><span data-stu-id="cd48a-239">For small or demo systems, you can place your HANA data and log files on one disk.</span></span> <span data-ttu-id="cd48a-240">Poniższe polecenia utworzyć partycję na /dev/sdc i sformatuj go przy xfs.</span><span class="sxs-lookup"><span data-stu-id="cd48a-240">The following commands create a partition on /dev/sdc and format it with xfs.</span></span>
    ```bash
    sudo fdisk /dev/sdc
    sudo mkfs.xfs /dev/sdc1
    
    # <a name="write-down-the-id-of-devsdc1"></a><span data-ttu-id="cd48a-241">Zanotuj identyfikator /dev/sdc1</span><span class="sxs-lookup"><span data-stu-id="cd48a-241">write down the id of /dev/sdc1</span></span>
    <span data-ttu-id="cd48a-242">sudo/sbin/blkid sudo vi/etc/fstab</span><span class="sxs-lookup"><span data-stu-id="cd48a-242">sudo /sbin/blkid  sudo vi /etc/fstab</span></span>
    ```

    Insert this line to /etc/fstab
    <pre><code>
    /dev/disk/by-uuid/<b>&lt;UUID&gt;</b> /hana xfs  defaults,nofail  0  2
    </code></pre>

    Create the target directory and mount the disk.

    ```bash
    sudo mkdir /hana
    sudo mount -a
    ```

1. <span data-ttu-id="cd48a-243">[A] ustawień rozpoznawania nazwy hosta dla wszystkich hostów</span><span class="sxs-lookup"><span data-stu-id="cd48a-243">[A] Setup host name resolution for all hosts</span></span>  
    <span data-ttu-id="cd48a-244">Można użyć serwera DNS lub zmodyfikować/etc/hosts na wszystkich węzłach.</span><span class="sxs-lookup"><span data-stu-id="cd48a-244">You can either use a DNS server or modify the /etc/hosts on all nodes.</span></span> <span data-ttu-id="cd48a-245">Ten przykład przedstawia sposób użycia pliku/etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="cd48a-245">This example shows how to use the /etc/hosts file.</span></span>
   <span data-ttu-id="cd48a-246">Zastąp adres IP i nazwy hosta w poniższych poleceniach</span><span class="sxs-lookup"><span data-stu-id="cd48a-246">Replace the IP address and the hostname in the following commands</span></span>
    ```bash
    sudo vi /etc/hosts
    ```
    <span data-ttu-id="cd48a-247">Wstaw następujące wiersze do/etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="cd48a-247">Insert the following lines to /etc/hosts.</span></span> <span data-ttu-id="cd48a-248">Zmienianie adresu IP i nazwy hosta do danego środowiska</span><span class="sxs-lookup"><span data-stu-id="cd48a-248">Change the IP address and hostname to match your environment</span></span>    
    
    <pre><code>
    <b>&lt;IP address of host 1&gt; &lt;hostname of host 1&gt;</b>
    <b>&lt;IP address of host 2&gt; &lt;hostname of host 2&gt;</b>
    </code></pre>

1. <span data-ttu-id="cd48a-249">[1] instalacji klastra</span><span class="sxs-lookup"><span data-stu-id="cd48a-249">[1] Install Cluster</span></span>
    ```bash
    sudo ha-cluster-init
    
    # Do you want to continue anyway? [y/N] -> y
    # Network address to bind to (e.g.: 192.168.1.0) [10.79.227.0] -> ENTER
    # Multicast address (e.g.: 239.x.x.x) [239.174.218.125] -> ENTER
    # Multicast port [5405] -> ENTER
    # Do you wish to use SBD? [y/N] -> N
    # Do you wish to configure an administration IP? [y/N] -> N
    ```
        
1. <span data-ttu-id="cd48a-250">[2] dodać węzeł do klastra</span><span class="sxs-lookup"><span data-stu-id="cd48a-250">[2] Add node to cluster</span></span>
    ```bash
    sudo ha-cluster-join
        
    # WARNING: NTP is not configured to start at system boot.
    # WARNING: No watchdog device found. If SBD is used, the cluster will be unable to start without a watchdog.
    # Do you want to continue anyway? [y/N] -> y
    # IP address or hostname of existing node (e.g.: 192.168.1.1) [] -> IP address of node 1 e.g. 10.0.0.5
    # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
    ```

1. <span data-ttu-id="cd48a-251">[A] Zmień hacluster hasło do tego samego hasła</span><span class="sxs-lookup"><span data-stu-id="cd48a-251">[A] Change hacluster password to the same password</span></span>
    ```bash
    sudo passwd hacluster
    
    ```

1. <span data-ttu-id="cd48a-252">[A] skonfiguruj corosync Użyj innego transportu, a następnie dodaj wstawienia.</span><span class="sxs-lookup"><span data-stu-id="cd48a-252">[A] Configure corosync to use other transport and add nodelist.</span></span> <span data-ttu-id="cd48a-253">Klaster nie będą działać inaczej.</span><span class="sxs-lookup"><span data-stu-id="cd48a-253">Cluster will not work otherwise.</span></span>
    ```bash
    sudo vi /etc/corosync/corosync.conf    
    
    ```

    <span data-ttu-id="cd48a-254">Dodaj następującą zawartość pogrubienie do pliku.</span><span class="sxs-lookup"><span data-stu-id="cd48a-254">Add the following bold content to the file.</span></span>
    
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

    <span data-ttu-id="cd48a-255">Następnie uruchom ponownie usługę corosync</span><span class="sxs-lookup"><span data-stu-id="cd48a-255">Then restart the corosync service</span></span>

    ```bash
    sudo service corosync restart
    
    ```

1. <span data-ttu-id="cd48a-256">[A] zainstalować pakiety HANA HA</span><span class="sxs-lookup"><span data-stu-id="cd48a-256">[A] Install HANA HA packages</span></span>  
    ```bash
    sudo zypper install SAPHanaSR
    
    ```

## <a name="installing-sap-hana"></a><span data-ttu-id="cd48a-257">Instalowanie programu SAP HANA</span><span class="sxs-lookup"><span data-stu-id="cd48a-257">Installing SAP HANA</span></span>

<span data-ttu-id="cd48a-258">Wykonaj rozdziału 4 [przewodnik SAP HANA SR wydajności zoptymalizowanych pod kątem scenariusza] [ suse-hana-ha-guide] do zainstalowania replikacji systemu SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="cd48a-258">Follow chapter 4 of the [SAP HANA SR Performance Optimized Scenario guide][suse-hana-ha-guide] to install SAP HANA System Replication.</span></span>

1. <span data-ttu-id="cd48a-259">[A] uruchamiania z dysku DVD HANA hdblcm</span><span class="sxs-lookup"><span data-stu-id="cd48a-259">[A] Run hdblcm from the HANA DVD</span></span>
    * <span data-ttu-id="cd48a-260">Wybierz opcję instalacji -> 1</span><span class="sxs-lookup"><span data-stu-id="cd48a-260">Choose installation -> 1</span></span>
    * <span data-ttu-id="cd48a-261">1 -> Wybierz dodatkowe składniki do instalacji</span><span class="sxs-lookup"><span data-stu-id="cd48a-261">Select additional components for installation -> 1</span></span>
    * <span data-ttu-id="cd48a-262">Wprowadź ścieżkę instalacji [/ hana/udostępnione]: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="cd48a-262">Enter Installation Path [/hana/shared]: -> ENTER</span></span>
    * <span data-ttu-id="cd48a-263">Wprowadź nazwę hosta lokalnego [.]: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="cd48a-263">Enter Local Host Name [..]: -> ENTER</span></span>
    * <span data-ttu-id="cd48a-264">Czy chcesz dodać dodatkowe hosty systemu?</span><span class="sxs-lookup"><span data-stu-id="cd48a-264">Do you want to add additional hosts to the system?</span></span> <span data-ttu-id="cd48a-265">(t/n) [[n]: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="cd48a-265">(y/n) [n]: -> ENTER</span></span>
    * <span data-ttu-id="cd48a-266">Wprowadź identyfikator systemu SAP HANA:<SID of HANA e.g. HDB></span><span class="sxs-lookup"><span data-stu-id="cd48a-266">Enter SAP HANA System ID: <SID of HANA e.g. HDB></span></span>
    * <span data-ttu-id="cd48a-267">Wprowadź liczby wystąpień [00]:</span><span class="sxs-lookup"><span data-stu-id="cd48a-267">Enter Instance Number [00]:</span></span>   
  <span data-ttu-id="cd48a-268">Liczby wystąpień HANA.</span><span class="sxs-lookup"><span data-stu-id="cd48a-268">HANA Instance number.</span></span> <span data-ttu-id="cd48a-269">Użyj 03, jeśli używany szablon Azure i stosować w powyższym przykładzie</span><span class="sxs-lookup"><span data-stu-id="cd48a-269">Use 03 if you used the Azure Template or followed the example above</span></span>
    * <span data-ttu-id="cd48a-270">Wybierz tryb bazy danych / wprowadź indeks [1]: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="cd48a-270">Select Database Mode / Enter Index [1]: -> ENTER</span></span>
    * <span data-ttu-id="cd48a-271">Użycie systemu wybierz / Wprowadź indeks [4]:</span><span class="sxs-lookup"><span data-stu-id="cd48a-271">Select System Usage / Enter Index [4]:</span></span>  
  <span data-ttu-id="cd48a-272">Wybierz system użycia</span><span class="sxs-lookup"><span data-stu-id="cd48a-272">Select the system Usage</span></span>
    * <span data-ttu-id="cd48a-273">Wprowadź lokalizację woluminów danych [/ hana/data/HDB]: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="cd48a-273">Enter Location of Data Volumes [/hana/data/HDB]: -> ENTER</span></span>
    * <span data-ttu-id="cd48a-274">Wprowadź lokalizację woluminy dziennika [/ HDB-hana/dziennika]: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="cd48a-274">Enter Location of Log Volumes [/hana/log/HDB]: -> ENTER</span></span>
    * <span data-ttu-id="cd48a-275">Ogranicz maksymalną wielkość pamięci alokacji?</span><span class="sxs-lookup"><span data-stu-id="cd48a-275">Restrict maximum memory allocation?</span></span> <span data-ttu-id="cd48a-276">[[n]: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="cd48a-276">[n]: -> ENTER</span></span>
    * <span data-ttu-id="cd48a-277">Wprowadź nazwę hosta certyfikat dla hosta "..."</span><span class="sxs-lookup"><span data-stu-id="cd48a-277">Enter Certificate Host Name For Host '...'</span></span> <span data-ttu-id="cd48a-278">[...]: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="cd48a-278">[...]: -> ENTER</span></span>
    * <span data-ttu-id="cd48a-279">Wprowadź nazwę użytkownika agenta hosta SAP (sapadm) hasło:</span><span class="sxs-lookup"><span data-stu-id="cd48a-279">Enter SAP Host Agent User (sapadm) Password:</span></span>
    * <span data-ttu-id="cd48a-280">Upewnij się, SAP hosta Agent użytkownika (sapadm) hasło:</span><span class="sxs-lookup"><span data-stu-id="cd48a-280">Confirm SAP Host Agent User (sapadm) Password:</span></span>
    * <span data-ttu-id="cd48a-281">Wprowadź administratora systemu (hdbadm) hasło:</span><span class="sxs-lookup"><span data-stu-id="cd48a-281">Enter System Administrator (hdbadm) Password:</span></span>
    * <span data-ttu-id="cd48a-282">Upewnij się, Administrator systemu (hdbadm) hasło:</span><span class="sxs-lookup"><span data-stu-id="cd48a-282">Confirm System Administrator (hdbadm) Password:</span></span>
    * <span data-ttu-id="cd48a-283">Wprowadź katalog macierzysty administratora systemu [/ usr/sap/HDB/głównej]: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="cd48a-283">Enter System Administrator Home Directory [/usr/sap/HDB/home]: -> ENTER</span></span>
    * <span data-ttu-id="cd48a-284">Wprowadź powłoka logowania administratora systemu [/ bin/sh]: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="cd48a-284">Enter System Administrator Login Shell [/bin/sh]: -> ENTER</span></span>
    * <span data-ttu-id="cd48a-285">Wprowadź identyfikator użytkownika administratora [1001]: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="cd48a-285">Enter System Administrator User ID [1001]: -> ENTER</span></span>
    * <span data-ttu-id="cd48a-286">Wprowadź identyfikator użytkownika grupy (sapsys) [79]: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="cd48a-286">Enter ID of User Group (sapsys) [79]: -> ENTER</span></span>
    * <span data-ttu-id="cd48a-287">Wprowadź hasło użytkownika (SYSTEM) bazy danych:</span><span class="sxs-lookup"><span data-stu-id="cd48a-287">Enter Database User (SYSTEM) Password:</span></span>
    * <span data-ttu-id="cd48a-288">Potwierdź hasło użytkownika (SYSTEM) bazy danych:</span><span class="sxs-lookup"><span data-stu-id="cd48a-288">Confirm Database User (SYSTEM) Password:</span></span>
    * <span data-ttu-id="cd48a-289">Uruchom ponownie system po ponownym uruchomieniu komputera?</span><span class="sxs-lookup"><span data-stu-id="cd48a-289">Restart system after machine reboot?</span></span> <span data-ttu-id="cd48a-290">[[n]: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="cd48a-290">[n]: -> ENTER</span></span>
    * <span data-ttu-id="cd48a-291">Czy chcesz kontynuować?</span><span class="sxs-lookup"><span data-stu-id="cd48a-291">Do you want to continue?</span></span> <span data-ttu-id="cd48a-292">(t/n):</span><span class="sxs-lookup"><span data-stu-id="cd48a-292">(y/n):</span></span>  
  <span data-ttu-id="cd48a-293">Sprawdź poprawność podsumowania, a następnie wprowadź t, aby kontynuować</span><span class="sxs-lookup"><span data-stu-id="cd48a-293">Validate the summary and enter y to continue</span></span>
1. <span data-ttu-id="cd48a-294">[A] Agent hosta uaktualnienia SAP</span><span class="sxs-lookup"><span data-stu-id="cd48a-294">[A] Upgrade SAP Host Agent</span></span>  
  <span data-ttu-id="cd48a-295">Pobierz najnowsze archiwum SAP Agent hosta z [SAP Softwarecenter] [ sap-swcenter] i uruchom następujące polecenie, aby uaktualnić agenta.</span><span class="sxs-lookup"><span data-stu-id="cd48a-295">Download the latest SAP Host Agent archive from the [SAP Softwarecenter][sap-swcenter] and run the following command to upgrade the agent.</span></span> <span data-ttu-id="cd48a-296">Zastąp ścieżki do archiwum, aby wskazywał pobranego pliku.</span><span class="sxs-lookup"><span data-stu-id="cd48a-296">Replace the path to the archive to point to the file you downloaded.</span></span>
    ```bash
    sudo /usr/sap/hostctrl/exe/saphostexec -upgrade -archive <path to SAP Host Agent SAR>
    ```

1. <span data-ttu-id="cd48a-297">[1] utworzyć HANA replikacji (jako główny)</span><span class="sxs-lookup"><span data-stu-id="cd48a-297">[1] Create HANA replication (as root)</span></span>  
    <span data-ttu-id="cd48a-298">Uruchom następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="cd48a-298">Run the following command.</span></span> <span data-ttu-id="cd48a-299">Upewnij się, że Zastąp bold ciągów (HANA systemu identyfikator HDB i numer wystąpienia 03) z wartościami instalację programu SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="cd48a-299">Make sure to replace bold strings (HANA System ID HDB and instance number 03) with the values of your SAP HANA installation.</span></span>
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbsql -u system -i <b>03</b> 'CREATE USER <b>hdb</b>hasync PASSWORD "<b>passwd</b>"' 
    hdbsql -u system -i <b>03</b> 'GRANT DATA ADMIN TO <b>hdb</b>hasync' 
    hdbsql -u system -i <b>03</b> 'ALTER USER <b>hdb</b>hasync DISABLE PASSWORD LIFETIME' 
    </code></pre>

1. <span data-ttu-id="cd48a-300">[A] utworzenia wpisu magazynu kluczy (jako główny)</span><span class="sxs-lookup"><span data-stu-id="cd48a-300">[A] Create keystore entry (as root)</span></span>
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbuserstore SET <b>hdb</b>haloc localhost:3<b>03</b>15 <b>hdb</b>hasync <b>passwd</b>
    </code></pre>
1. <span data-ttu-id="cd48a-301">[1] kopii zapasowej bazy danych (jako główny)</span><span class="sxs-lookup"><span data-stu-id="cd48a-301">[1] Backup database (as root)</span></span>
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbsql -u system -i <b>03</b> "BACKUP DATA USING FILE ('<b>initialbackup</b>')" 
    </code></pre>
1. <span data-ttu-id="cd48a-302">[1] Przełącz użytkownika sapsid (na przykład hdbadm) i utworzyć lokacji głównej.</span><span class="sxs-lookup"><span data-stu-id="cd48a-302">[1] Switch to the sapsid user (for example hdbadm) and create the primary site.</span></span>
    <pre><code>
    su - <b>hdb</b>adm
    hdbnsutil -sr_enable –-name=<b>SITE1</b>
    </code></pre>
1. <span data-ttu-id="cd48a-303">[2] Przełącz użytkownika sapsid (na przykład hdbadm) i utworzyć lokację dodatkową.</span><span class="sxs-lookup"><span data-stu-id="cd48a-303">[2] Switch to the sapsid user (for example hdbadm) and create the secondary site.</span></span>
    <pre><code>
    su - <b>hdb</b>adm
    sapcontrol -nr <b>03</b> -function StopWait 600 10
    hdbnsutil -sr_register --remoteHost=<b>saphanavm1</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE2</b> 
    </code></pre>

## <a name="configure-cluster-framework"></a><span data-ttu-id="cd48a-304">Konfigurowanie klastra Framework</span><span class="sxs-lookup"><span data-stu-id="cd48a-304">Configure Cluster Framework</span></span>

<span data-ttu-id="cd48a-305">Zmiany ustawień domyślnych</span><span class="sxs-lookup"><span data-stu-id="cd48a-305">Change the default settings</span></span>

<pre>
sudo vi crm-defaults.txt
# enter the following to crm-defaults.txt
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

# <a name="now-we-load-the-file-to-the-cluster"></a><span data-ttu-id="cd48a-306">Teraz możemy załadować pliku do klastra</span><span class="sxs-lookup"><span data-stu-id="cd48a-306">now we load the file to the cluster</span></span>
<span data-ttu-id="cd48a-307">sudo crm Konfigurowanie aktualizacji obciążenia crm-defaults.txt</span><span class="sxs-lookup"><span data-stu-id="cd48a-307">sudo crm configure load update crm-defaults.txt</span></span>
</pre>

### <a name="create-stonith-device"></a><span data-ttu-id="cd48a-308">Utwórz urządzenie STONITH</span><span class="sxs-lookup"><span data-stu-id="cd48a-308">Create STONITH device</span></span>

<span data-ttu-id="cd48a-309">Urządzenie STONITH używa nazwy głównej usługi do autoryzacji przed Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="cd48a-309">The STONITH device uses a Service Principal to authorize against Microsoft Azure.</span></span> <span data-ttu-id="cd48a-310">Wykonaj następujące kroki, aby utworzyć nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="cd48a-310">Please follow these steps to create a Service Principal.</span></span>

1. <span data-ttu-id="cd48a-311">Przejdź do <https://portal.azure.com></span><span class="sxs-lookup"><span data-stu-id="cd48a-311">Go to <https://portal.azure.com></span></span>
1. <span data-ttu-id="cd48a-312">Otwarcie bloku usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cd48a-312">Open the Azure Active Directory blade</span></span>  
   <span data-ttu-id="cd48a-313">Przejdź do właściwości i Zanotuj identyfikator katalogu.</span><span class="sxs-lookup"><span data-stu-id="cd48a-313">Go to Properties and write down the Directory Id.</span></span> <span data-ttu-id="cd48a-314">Jest to **identyfikator dzierżawcy**.</span><span class="sxs-lookup"><span data-stu-id="cd48a-314">This is the **tenant id**.</span></span>
1. <span data-ttu-id="cd48a-315">Kliknij przycisk rejestracji aplikacji</span><span class="sxs-lookup"><span data-stu-id="cd48a-315">Click App registrations</span></span>
1. <span data-ttu-id="cd48a-316">Kliknij pozycję Dodaj.</span><span class="sxs-lookup"><span data-stu-id="cd48a-316">Click Add</span></span>
1. <span data-ttu-id="cd48a-317">Wprowadź nazwę, wybierz typ aplikacji "Aplikacja/interfejs API sieci Web", wprowadź adres URL logowania (np. http://localhost) i kliknij przycisk Utwórz</span><span class="sxs-lookup"><span data-stu-id="cd48a-317">Enter a Name, select Application Type "Web app/API", enter a sign-on URL (for example http://localhost) and click Create</span></span>
1. <span data-ttu-id="cd48a-318">Adres URL logowania nie jest używany i może być dowolny prawidłowy adres URL</span><span class="sxs-lookup"><span data-stu-id="cd48a-318">The sign-on URL is not used and can be any valid URL</span></span>
1. <span data-ttu-id="cd48a-319">Wybierz nową aplikację i kliknij na karcie Ustawienia</span><span class="sxs-lookup"><span data-stu-id="cd48a-319">Select the new App and click Keys in the Settings tab</span></span>
1. <span data-ttu-id="cd48a-320">Wprowadź opis nowego klucza, wybierz pozycję "Nigdy nie wygasa" i kliknij przycisk Zapisz</span><span class="sxs-lookup"><span data-stu-id="cd48a-320">Enter a description for a new key, select "Never expires" and click Save</span></span>
1. <span data-ttu-id="cd48a-321">Zanotuj wartość.</span><span class="sxs-lookup"><span data-stu-id="cd48a-321">Write down the Value.</span></span> <span data-ttu-id="cd48a-322">Jest on używany jako **hasło** główną usługi</span><span class="sxs-lookup"><span data-stu-id="cd48a-322">It is used as the **password** for the Service Principal</span></span>
1. <span data-ttu-id="cd48a-323">Zanotuj identyfikator aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cd48a-323">Write down the Application Id.</span></span> <span data-ttu-id="cd48a-324">Jest on używany jako nazwa użytkownika (**identyfikatora** w poniższych krokach) główną usługi</span><span class="sxs-lookup"><span data-stu-id="cd48a-324">It is used as the username (**login id** in the steps below) of the Service Principal</span></span>

<span data-ttu-id="cd48a-325">Nazwy głównej usługi nie ma uprawnień do domyślnie dostęp do zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="cd48a-325">The Service Principal does not have permissions to access your Azure resources by default.</span></span> <span data-ttu-id="cd48a-326">Należy podać nazwę główną usługi uprawnień do uruchamiania i zatrzymywania (deallocate) wszystkich maszyn wirtualnych klastra.</span><span class="sxs-lookup"><span data-stu-id="cd48a-326">You need to give the Service Principal permissions to start and stop (deallocate) all virtual machines of the cluster.</span></span>

1. <span data-ttu-id="cd48a-327">Przejdź do https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="cd48a-327">Go to https://portal.azure.com</span></span>
1. <span data-ttu-id="cd48a-328">Otwórz wszystkie bloku zasobów</span><span class="sxs-lookup"><span data-stu-id="cd48a-328">Open the All resources blade</span></span>
1. <span data-ttu-id="cd48a-329">Wybierz maszynę wirtualną</span><span class="sxs-lookup"><span data-stu-id="cd48a-329">Select the virtual machine</span></span>
1. <span data-ttu-id="cd48a-330">Kliknij przycisk kontroli dostępu (IAM)</span><span class="sxs-lookup"><span data-stu-id="cd48a-330">Click Access control (IAM)</span></span>
1. <span data-ttu-id="cd48a-331">Kliknij pozycję Dodaj.</span><span class="sxs-lookup"><span data-stu-id="cd48a-331">Click Add</span></span>
1. <span data-ttu-id="cd48a-332">Wybierz rolę właściciela</span><span class="sxs-lookup"><span data-stu-id="cd48a-332">Select the role Owner</span></span>
1. <span data-ttu-id="cd48a-333">Wprowadź nazwę aplikacji, utworzoną wcześniej</span><span class="sxs-lookup"><span data-stu-id="cd48a-333">Enter the name of the application you created above</span></span>
1. <span data-ttu-id="cd48a-334">Kliknij przycisk OK</span><span class="sxs-lookup"><span data-stu-id="cd48a-334">Click OK</span></span>

<span data-ttu-id="cd48a-335">Po można edytowane uprawnienia dla maszyn wirtualnych, możesz skonfigurować urządzenia STONITH w klastrze.</span><span class="sxs-lookup"><span data-stu-id="cd48a-335">After you edited the permissions for the virtual machines, you can configure the STONITH devices in the cluster.</span></span>

<pre>
sudo vi crm-fencing.txt
# enter the following to crm-fencing.txt
# replace the bold string with your subscription id, resource group, tenant id, service principal id and password
<code>
primitive rsc_st_azure_1 stonith:fence_azure_arm \
    params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

primitive rsc_st_azure_2 stonith:fence_azure_arm \
    params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started
</code>

# <a name="now-we-load-the-file-to-the-cluster"></a><span data-ttu-id="cd48a-336">Teraz możemy załadować pliku do klastra</span><span class="sxs-lookup"><span data-stu-id="cd48a-336">now we load the file to the cluster</span></span>
<span data-ttu-id="cd48a-337">sudo crm Konfigurowanie aktualizacji obciążenia crm-fencing.txt</span><span class="sxs-lookup"><span data-stu-id="cd48a-337">sudo crm configure load update crm-fencing.txt</span></span>
</pre>

### <a name="create-sap-hana-resources"></a><span data-ttu-id="cd48a-338">Utwórz zasoby SAP HANA</span><span class="sxs-lookup"><span data-stu-id="cd48a-338">Create SAP HANA resources</span></span>

<pre>
sudo vi crm-saphanatop.txt
# enter the following to crm-saphana.txt
# replace the bold string with your instance number and HANA system id
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

# <a name="now-we-load-the-file-to-the-cluster"></a><span data-ttu-id="cd48a-339">Teraz możemy załadować pliku do klastra</span><span class="sxs-lookup"><span data-stu-id="cd48a-339">now we load the file to the cluster</span></span>
<span data-ttu-id="cd48a-340">sudo crm Konfigurowanie aktualizacji obciążenia crm-saphanatop.txt</span><span class="sxs-lookup"><span data-stu-id="cd48a-340">sudo crm configure load update crm-saphanatop.txt</span></span>
</pre>

<pre>
sudo vi crm-saphana.txt
# enter the following to crm-saphana.txt
# replace the bold string with your instance number, HANA system id and the frontend IP address of the Azure load balancer. 
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

# <a name="now-we-load-the-file-to-the-cluster"></a><span data-ttu-id="cd48a-341">Teraz możemy załadować pliku do klastra</span><span class="sxs-lookup"><span data-stu-id="cd48a-341">now we load the file to the cluster</span></span>
<span data-ttu-id="cd48a-342">sudo crm Konfigurowanie aktualizacji obciążenia crm-saphana.txt</span><span class="sxs-lookup"><span data-stu-id="cd48a-342">sudo crm configure load update crm-saphana.txt</span></span>
</pre>

### <a name="test-cluster-setup"></a><span data-ttu-id="cd48a-343">Konfiguracja klastra testu</span><span class="sxs-lookup"><span data-stu-id="cd48a-343">Test cluster setup</span></span>
<span data-ttu-id="cd48a-344">Rozdział opisano, jak można przetestować konfigurację.</span><span class="sxs-lookup"><span data-stu-id="cd48a-344">The following chapter describe how you can test your setup.</span></span> <span data-ttu-id="cd48a-345">Każdy test założono, że są głównymi i wzorzec SAP HANA działa na saphanavm1 maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="cd48a-345">Every test assumes that you are root and the SAP HANA master is running on the virtual machine saphanavm1.</span></span>

#### <a name="fencing-test"></a><span data-ttu-id="cd48a-346">Test ogrodzenia</span><span class="sxs-lookup"><span data-stu-id="cd48a-346">Fencing Test</span></span>

<span data-ttu-id="cd48a-347">Można przetestować instalacji agenta ogrodzenia wyłączając interfejs sieciowy na saphanavm1 węzła.</span><span class="sxs-lookup"><span data-stu-id="cd48a-347">You can test the setup of the fencing agent by disabling the network interface on node saphanavm1.</span></span>

<pre><code>
sudo ifdown eth0
</code></pre>

<span data-ttu-id="cd48a-348">Teraz Pobierz ponownie uruchomiona lub zatrzymana w zależności od konfiguracji klastra maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="cd48a-348">The virtual machine should now get restarted or stopped depending on your cluster configuration.</span></span>
<span data-ttu-id="cd48a-349">Jeśli ustawisz akcji stonith wyłączone, maszyna wirtualna zostanie zatrzymana i zasoby są migrowane do uruchomionej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="cd48a-349">If you set the stonith-action to off, the virtual machine will be stopped and the resources are migrated to the running virtual machine.</span></span>

<span data-ttu-id="cd48a-350">Po ponownym uruchomieniu maszyny wirtualnej zasobów SAP HANA nie zostanie uruchomiony jako dodatkowej po ustawieniu AUTOMATED_REGISTER = "false".</span><span class="sxs-lookup"><span data-stu-id="cd48a-350">Once you start the virtual machine again, the SAP HANA resource will fail to start as secondary if you set AUTOMATED_REGISTER="false".</span></span> <span data-ttu-id="cd48a-351">W takim przypadku należy skonfigurować wystąpienie HANA jako dodatkowej, wykonując następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="cd48a-351">In this case, you need to configure the HANA instance as secondary by executing the following command:</span></span>

<pre><code>
su - <b>hdb</b>adm

# Stop the HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b>

# switch back to root and cleanup the failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

#### <a name="testing-a-manual-failover"></a><span data-ttu-id="cd48a-352">Testowania ręcznego przełączania trybu failover</span><span class="sxs-lookup"><span data-stu-id="cd48a-352">Testing a manual failover</span></span>

<span data-ttu-id="cd48a-353">Ręcznego przełączania trybu failover można przetestować, zatrzymując usługę rozrusznik na saphanavm1 węzła.</span><span class="sxs-lookup"><span data-stu-id="cd48a-353">You can test a manual failover by stopping the pacemaker service on node saphanavm1.</span></span>
<pre><code>
service pacemaker stop
</code></pre>

<span data-ttu-id="cd48a-354">Po przejściu w tryb failover należy ponownie uruchomić usługę.</span><span class="sxs-lookup"><span data-stu-id="cd48a-354">After the failover, you can start the service again.</span></span> <span data-ttu-id="cd48a-355">Zasób SAP HANA saphanavm1 nie zostanie uruchomiony jako dodatkowej po ustawieniu AUTOMATED_REGISTER = "false".</span><span class="sxs-lookup"><span data-stu-id="cd48a-355">The SAP HANA resource on saphanavm1 will fail to start as secondary if you set AUTOMATED_REGISTER="false".</span></span> <span data-ttu-id="cd48a-356">W takim przypadku należy skonfigurować wystąpienie HANA jako dodatkowej, wykonując następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="cd48a-356">In this case, you need to configure the HANA instance as secondary by executing the following command:</span></span>

<pre><code>
service pacemaker start
su - <b>hdb</b>adm

# Stop the HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b> 


# switch back to root and cleanup the failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

#### <a name="testing-a-migration"></a><span data-ttu-id="cd48a-357">Testowanie migracji</span><span class="sxs-lookup"><span data-stu-id="cd48a-357">Testing a migration</span></span>

<span data-ttu-id="cd48a-358">Węzeł główny SAP HANA można migrować, wykonując następujące polecenie</span><span class="sxs-lookup"><span data-stu-id="cd48a-358">You can migrate the SAP HANA master node by executing the following command</span></span>
<pre><code>
crm resource migrate msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm2</b>
crm resource migrate g_ip_<b>HDB</b>_HDB<b>03</b> <b>saphanavm2</b>
</code></pre>

<span data-ttu-id="cd48a-359">To należy zmigrować węzła głównego SAP HANA i grupy, która zawiera wirtualny adres IP saphanavm2.</span><span class="sxs-lookup"><span data-stu-id="cd48a-359">This should migrate the SAP HANA master node and the group that contains the virtual IP address to saphanavm2.</span></span>
<span data-ttu-id="cd48a-360">Zasób SAP HANA saphanavm1 nie zostanie uruchomiony jako dodatkowej po ustawieniu AUTOMATED_REGISTER = "false".</span><span class="sxs-lookup"><span data-stu-id="cd48a-360">The SAP HANA resource on saphanavm1 will fail to start as secondary if you set AUTOMATED_REGISTER="false".</span></span> <span data-ttu-id="cd48a-361">W takim przypadku należy skonfigurować wystąpienie HANA jako dodatkowej, wykonując następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="cd48a-361">In this case, you need to configure the HANA instance as secondary by executing the following command:</span></span>

<pre><code>
su - <b>hdb</b>adm

# Stop the HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b> 
</code></pre>

<span data-ttu-id="cd48a-362">Migracja tworzy ograniczenia lokalizacji, które muszą zostać usunięte ponownie.</span><span class="sxs-lookup"><span data-stu-id="cd48a-362">The migration creates location contraints that need to be deleted again.</span></span>

<pre><code>
crm configure edited

# delete location contraints that are named like the following contraint. You should have two contraints, one for the SAP HANA resource and one for the IP address group.
location cli-prefer-g_ip_<b>HDB</b>_HDB<b>03</b> g_ip_<b>HDB</b>_HDB<b>03</b> role=Started inf: <b>saphanavm2</b>
</code></pre>

<span data-ttu-id="cd48a-363">Należy również oczyszczania stanu zasobu węzła pomocniczego</span><span class="sxs-lookup"><span data-stu-id="cd48a-363">You also need to cleanup the state of the secondary node resource</span></span>

<pre><code>
# switch back to root and cleanup the failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

## <a name="next-steps"></a><span data-ttu-id="cd48a-364">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cd48a-364">Next steps</span></span>
* <span data-ttu-id="cd48a-365">[Azure maszyn wirtualnych, planowania i wdrażania dla programu SAP][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="cd48a-365">[Azure Virtual Machines planning and implementation for SAP][planning-guide]</span></span>
* <span data-ttu-id="cd48a-366">[Maszyny wirtualne Azure wdrożenia SAP][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="cd48a-366">[Azure Virtual Machines deployment for SAP][deployment-guide]</span></span>
* <span data-ttu-id="cd48a-367">[Wdrożenia usługi Azure DBMS maszyny wirtualnej dla programu SAP][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="cd48a-367">[Azure Virtual Machines DBMS deployment for SAP][dbms-guide]</span></span>
* <span data-ttu-id="cd48a-368">Aby dowiedzieć się jak ustanowić wysokiej dostępności i planu odzyskiwania po awarii programu SAP HANA na platformie Azure (wystąpienia duże), zobacz [SAP HANA (duże wystąpień) wysokiej dostępności i odzyskiwania po awarii na platformie Azure](hana-overview-high-availability-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="cd48a-368">To learn how to establish high availability and plan for disaster recovery of SAP HANA on Azure (large instances), see [SAP HANA (large instances) high availability and disaster recovery on Azure](hana-overview-high-availability-disaster-recovery.md).</span></span> 
