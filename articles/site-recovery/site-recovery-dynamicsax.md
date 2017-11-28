---
title: "Replikowanie wdrażania Dynamics AX wielowarstwową przy użyciu usługi Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób replikowania i chronić Dynamics AX przy użyciu usługi Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: asgang
manager: rochakm
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/24/2017
ms.author: asgang
ms.openlocfilehash: 03127c8f4841b67436c4819628319705af0b2cd5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="replicate-a-multi-tier-dynamics-ax-application-using-azure-site-recovery"></a><span data-ttu-id="67110-103">Replikowanie wielowarstwowej aplikacji Dynamics AX przy użyciu usługi Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="67110-103">Replicate a multi-tier Dynamics AX application using Azure Site Recovery</span></span>

## <a name="overview"></a><span data-ttu-id="67110-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="67110-104">Overview</span></span>


<span data-ttu-id="67110-105">Microsoft Dynamics AX jest jednym z najbardziej popularnych rozwiązań ERP między przedsiębiorstwom standardowy proces w lokalizacjach, zarządzanie zasobami i uproszczenia zgodności.</span><span class="sxs-lookup"><span data-stu-id="67110-105">Microsoft Dynamics AX is one of the most popular ERP solution among enterprises to standardized process across locations, manage resources and simplifying compliance.</span></span> <span data-ttu-id="67110-106">Considering aplikacji jest firma krytyczne znaczenie dla organizacji jest bardzo ważne, upewnij się, że jeśli wszelkie po awarii, aplikacja powinna być uruchomiona w minimalny czas.</span><span class="sxs-lookup"><span data-stu-id="67110-106">Considering the application is business critical to an organization it is very important to be sure that if any disaster, application should be up and running in minimum time.</span></span>

<span data-ttu-id="67110-107">Już dziś Microsoft Dynamics AX nie zapewnia żadnych funkcji odzyskiwania po awarii poza pole.</span><span class="sxs-lookup"><span data-stu-id="67110-107">Today, Microsoft Dynamics AX  does not provide any out-of-the-box disaster recovery capabilities.</span></span> <span data-ttu-id="67110-108">Microsoft Dynamics AX składa się z wielu składników serwera, takich jak serwera aplikacji, Active Directory (AD), serwer bazy danych SQL, program SharePoint Server Reporting Server itd. Aby zarządzać awarią odzyskiwania każdego z tych składników ręcznie jest nie tylko kosztowna, ale również podatne na błędy.</span><span class="sxs-lookup"><span data-stu-id="67110-108">Microsoft Dynamics AX consists of many server components like Application Object Server, Active Directory (AD), SQL Database Server, SharePoint Server, Reporting Server etc. To manage the disaster recovery of each of these components manually is not only expensive but also error-prone.</span></span>

<span data-ttu-id="67110-109">W tym artykule opisano szczegółowo dotyczące tworzenia rozwiązanie odzyskiwania po awarii dla programu Dynamics AX aplikacji przy użyciu [usługi Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="67110-109">This article explains in detail about how you can create a disaster recovery solution for your Dynamics AX application using [Azure Site Recovery](site-recovery-overview.md).</span></span> <span data-ttu-id="67110-110">Obejmuje ona również planowane/nieplanowane/testowanie oprogramowania przełączenia do trybu failover przy użyciu planu odzyskiwania jednym kliknięciem, obsługiwane konfiguracje i wymagania wstępne.</span><span class="sxs-lookup"><span data-stu-id="67110-110">It also covers planned/unplanned/test failovers using one-click recovery plan, supported configurations, and prerequisites.</span></span>
<span data-ttu-id="67110-111">Rozwiązanie odzyskiwania po awarii w usłudze Azure Site Recovery na podstawie jest w pełni przetestowane, certyfikowane i zalecanymi przez program Microsoft Dynamics AX.</span><span class="sxs-lookup"><span data-stu-id="67110-111">Azure Site Recovery based disaster recovery solution is fully tested, certified, and recommended by Microsoft Dynamics AX.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="67110-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="67110-112">Prerequisites</span></span>

<span data-ttu-id="67110-113">Wdrażanie odzyskiwania po awarii dla aplikacji Dynamics AX przy użyciu usługi Azure Site Recovery wymaga następujące wymagania wstępne ukończone.</span><span class="sxs-lookup"><span data-stu-id="67110-113">Implementing disaster recovery for Dynamics AX application using Azure Site Recovery requires the following pre-requisites completed.</span></span>

<span data-ttu-id="67110-114">• Lokalnego wdrożenia programu Dynamics AX został skonfigurowany</span><span class="sxs-lookup"><span data-stu-id="67110-114">•   An on-premises Dynamics AX deployment has been set up</span></span>

<span data-ttu-id="67110-115">• Magazyn usług odzyskiwania azure lokacji został utworzony w subskrypcji Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="67110-115">•   Azure Site Recovery Services vault has been created in Microsoft Azure subscription</span></span>

<span data-ttu-id="67110-116">• Jeśli Azure to witryny odzyskiwania, uruchom narzędzie oceny gotowości maszyny wirtualnej platformy Azure na maszynach wirtualnych, aby upewnić się, że są one zgodne z maszynami wirtualnymi Azure i usług Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="67110-116">•   If Azure is your recovery site, run the Azure Virtual Machine Readiness Assessment tool  on VMs to ensure that they are compatible with Azure VMs and Azure Site Recovery Services</span></span>


## <a name="site-recovery-support"></a><span data-ttu-id="67110-117">Obsługa odzyskiwania lokacji</span><span class="sxs-lookup"><span data-stu-id="67110-117">Site Recovery support</span></span>

<span data-ttu-id="67110-118">Na potrzeby tworzenia w tym artykule, użyto maszyn wirtualnych VMware z 2012R3 Dynamics AX w systemie Windows Server 2012 R2 Enterprise.</span><span class="sxs-lookup"><span data-stu-id="67110-118">For the purpose of creating this article, VMware virtual machines with Dynamics AX  2012R3 on Windows Server 2012 R2 Enterprise were used.</span></span> <span data-ttu-id="67110-119">Ponieważ replikacja z lokacji odzyskiwania jest niezależny od aplikacji, do przechowywania w następujących scenariuszach również powinny zalecenia zawarte w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="67110-119">As site recovery replication is application agnostic, the recommendations provided here are expected to hold on following scenarios as well.</span></span>

### <a name="source-and-target"></a><span data-ttu-id="67110-120">Źródłowa i docelowa</span><span class="sxs-lookup"><span data-stu-id="67110-120">Source and target</span></span>

<span data-ttu-id="67110-121">**Scenariusz**</span><span class="sxs-lookup"><span data-stu-id="67110-121">**Scenario**</span></span> | <span data-ttu-id="67110-122">**Do lokacji dodatkowej**</span><span class="sxs-lookup"><span data-stu-id="67110-122">**To a secondary site**</span></span> | <span data-ttu-id="67110-123">**Na platformie Azure**</span><span class="sxs-lookup"><span data-stu-id="67110-123">**To Azure**</span></span>
--- | --- | ---
<span data-ttu-id="67110-124">**Funkcja Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="67110-124">**Hyper-V**</span></span> | <span data-ttu-id="67110-125">Tak</span><span class="sxs-lookup"><span data-stu-id="67110-125">Yes</span></span> | <span data-ttu-id="67110-126">Tak</span><span class="sxs-lookup"><span data-stu-id="67110-126">Yes</span></span>
<span data-ttu-id="67110-127">**VMware**</span><span class="sxs-lookup"><span data-stu-id="67110-127">**VMware**</span></span> | <span data-ttu-id="67110-128">Tak</span><span class="sxs-lookup"><span data-stu-id="67110-128">Yes</span></span> | <span data-ttu-id="67110-129">Tak</span><span class="sxs-lookup"><span data-stu-id="67110-129">Yes</span></span>
<span data-ttu-id="67110-130">**Serwer fizyczny**</span><span class="sxs-lookup"><span data-stu-id="67110-130">**Physical server**</span></span> | <span data-ttu-id="67110-131">Tak</span><span class="sxs-lookup"><span data-stu-id="67110-131">Yes</span></span> | <span data-ttu-id="67110-132">Tak</span><span class="sxs-lookup"><span data-stu-id="67110-132">Yes</span></span>

## <a name="enable-dr-of-dynamics-ax-application-using-azure-site-recovery"></a><span data-ttu-id="67110-133">Włączenie odzyskiwania po awarii programu Dynamics AX aplikacji przy użyciu usługi Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="67110-133">Enable DR of Dynamics AX application using Azure Site Recovery</span></span>
### <a name="protect-your-dynamics-ax-application"></a><span data-ttu-id="67110-134">Ochrona aplikacji Dynamics AX</span><span class="sxs-lookup"><span data-stu-id="67110-134">Protect your Dynamics AX application</span></span>
<span data-ttu-id="67110-135">Każdego składnika programu Dynamics AX musi być chronione, aby włączyć replikację kompletna aplikacja i odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="67110-135">Each component of the Dynamics AX needs to be protected to enable the complete application replication and recovery.</span></span> <span data-ttu-id="67110-136">W tej sekcji omówiono:</span><span class="sxs-lookup"><span data-stu-id="67110-136">This section covers:</span></span>

<span data-ttu-id="67110-137">**1. Ochrona usługi Active Directory**</span><span class="sxs-lookup"><span data-stu-id="67110-137">**1. Protection of Active Directory**</span></span>

<span data-ttu-id="67110-138">**2. Ochrona warstwy SQL**</span><span class="sxs-lookup"><span data-stu-id="67110-138">**2. Protection of SQL Tier**</span></span>

<span data-ttu-id="67110-139">**3. Ochrona aplikacji i warstwy sieci Web**</span><span class="sxs-lookup"><span data-stu-id="67110-139">**3. Protection of App and Web Tiers**</span></span>

<span data-ttu-id="67110-140">**4. Konfiguracja sieci**</span><span class="sxs-lookup"><span data-stu-id="67110-140">**4. Networking configuration**</span></span>

<span data-ttu-id="67110-141">**5. Plan odzyskiwania**</span><span class="sxs-lookup"><span data-stu-id="67110-141">**5. Recovery Plan**</span></span>

### <a name="1-setup-ad-and-dns-replication"></a><span data-ttu-id="67110-142">1. Instalator usługi AD i replikacja DNS</span><span class="sxs-lookup"><span data-stu-id="67110-142">1. Setup AD and DNS replication</span></span>

<span data-ttu-id="67110-143">Usługi Active Directory jest wymagany w lokacji odzyskiwania po awarii dla aplikacji Dynamics AX do funkcji.</span><span class="sxs-lookup"><span data-stu-id="67110-143">Active Directory is required on the DR site for Dynamics AX application to function.</span></span> <span data-ttu-id="67110-144">Istnieją dwie opcje zalecane w zależności od złożoności klienta w środowisku lokalnym.</span><span class="sxs-lookup"><span data-stu-id="67110-144">There are two recommended choices based on the complexity of the customer’s on-premises environment.</span></span>

<span data-ttu-id="67110-145">**Opcja 1**</span><span class="sxs-lookup"><span data-stu-id="67110-145">**Option 1**</span></span>

<span data-ttu-id="67110-146">Jeśli klient ma niewielkiej liczby aplikacji i jednego kontrolera domeny dla jego całą lokalnej lokacji i będzie można przechodzenie w tryb failover całej witryny razem, a następnie zaleca się używanie ASR replikacji do replikowania maszyny kontrolera domeny do lokacji dodatkowej (dotyczy zarówno lokacji do lokacji i lokacji na platformę Azure).</span><span class="sxs-lookup"><span data-stu-id="67110-146">If the customer has a small number of applications and a single domain controller for his entire on-premises site and will be failing over the entire site together, then we recommend using ASR-Replication to replicate the DC machine to secondary site (applicable for both Site to Site and Site to Azure).</span></span>

<span data-ttu-id="67110-147">**Opcja 2**</span><span class="sxs-lookup"><span data-stu-id="67110-147">**Option 2**</span></span>

<span data-ttu-id="67110-148">Jeśli klient ma dużą liczbę aplikacji i działa w lesie usługi Active Directory i będzie miała kilka aplikacji w czasie, a następnie zalecamy skonfigurowanie dodatkowego kontrolera domeny w lokacji odzyskiwania po awarii (lokacji dodatkowej lub na platformie Azure).</span><span class="sxs-lookup"><span data-stu-id="67110-148">If the customer has a large number of applications and is running an Active Directory forest and will fail-over few applications at a time, then we recommend setting up an additional domain controller on the DR site (secondary site or in Azure).</span></span>

<span data-ttu-id="67110-149">Zapoznaj się z [Przewodnik uzupełniający po na udostępnianie kontrolera domeny w lokacji odzyskiwania po awarii](site-recovery-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="67110-149">Please refer to [companion guide on making a domain controller available on DR site](site-recovery-active-directory.md).</span></span> <span data-ttu-id="67110-150">Dla pozostałej części tego dokumentu zostanie przyjęto założenie, że kontroler domeny jest dostępny w witrynie odzyskiwania po awarii.</span><span class="sxs-lookup"><span data-stu-id="67110-150">For remainder of this document we will assume a DC is available on DR site.</span></span>

### <a name="2-setup-sql-server-replication"></a><span data-ttu-id="67110-151">2. Ustawienia replikacji programu SQL Server</span><span class="sxs-lookup"><span data-stu-id="67110-151">2. Setup SQL Server replication</span></span>
<span data-ttu-id="67110-152">Zapoznaj się z Przewodnik uzupełniający po szczegółowe wskazówki techniczne na to zalecana opcja ochrony [warstwy SQL](site-recovery-sql.md).</span><span class="sxs-lookup"><span data-stu-id="67110-152">Please refer to companion guide  for detailed technical guidance on the recommended option for protecting [SQL tier](site-recovery-sql.md).</span></span>

### <a name="3-enable-protection-for-dynamics-ax-client-and-aos-vms"></a><span data-ttu-id="67110-153">3. Włącz ochronę Dynamics AX klienta i serwera AOS maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="67110-153">3. Enable protection for Dynamics AX client and AOS VMs</span></span>
<span data-ttu-id="67110-154">Wykonaj odpowiednie konfigurację usługi Azure Site Recovery na czy maszyny wirtualne są wdrażane na podstawie [funkcji Hyper-V](site-recovery-hyper-v-site-to-azure.md) lub na [VMware](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="67110-154">Perform relevant Azure Site Recovery configuration based on whether the VMs are deployed on [Hyper-V](site-recovery-hyper-v-site-to-azure.md) or on [VMware](site-recovery-vmware-to-azure.md).</span></span>

> [!TIP]
> <span data-ttu-id="67110-155">Zalecana częstotliwość spójne awarii do skonfigurowania to 15 minut.</span><span class="sxs-lookup"><span data-stu-id="67110-155">Recommended Crash consistent frequency to configure is 15 minutes.</span></span>
>

<span data-ttu-id="67110-156">Poniżej migawki pokazuje stan ochrony maszyn wirtualnych składnika Dynamics w scenariuszu ochrony "Lokacji oprogramowania VMware do platformy Azure".</span><span class="sxs-lookup"><span data-stu-id="67110-156">The below snapshot shows the protection status of Dynamics component VMs in ‘VMware site to Azure’ protection scenario.</span></span>
<span data-ttu-id="67110-157">![Elementy chronione](./media/site-recovery-dynamics-ax/protecteditems.png)</span><span class="sxs-lookup"><span data-stu-id="67110-157">![Protected items ](./media/site-recovery-dynamics-ax/protecteditems.png)</span></span>

### <a name="4-configure-networking"></a><span data-ttu-id="67110-158">4. Konfigurowanie sieci</span><span class="sxs-lookup"><span data-stu-id="67110-158">4. Configure Networking</span></span>
<span data-ttu-id="67110-159">Konfigurowanie maszyny Wirtualnej obliczeniowe i ustawień sieciowych</span><span class="sxs-lookup"><span data-stu-id="67110-159">Configure VM Compute and Network Settings</span></span>

<span data-ttu-id="67110-160">AX klienta i serwera AOS maszyny wirtualne należy skonfigurować ustawienia sieciowe w usłudze Azure Site Recovery, aby sieci maszyn wirtualnych uzyskać dołączona do prawej sieci DR po pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="67110-160">For the AX client and AOS VMs configure network settings in Azure Site Recovery so that the VM networks get attached to the right DR network after failover.</span></span> <span data-ttu-id="67110-161">Upewnij się, że sieć DR warstw jest routingu do warstwy SQL.</span><span class="sxs-lookup"><span data-stu-id="67110-161">Ensure the DR network for these tiers is routable to the SQL tier.</span></span>

<span data-ttu-id="67110-162">Możesz wybrać maszynę Wirtualną w zreplikowanych elementów, aby skonfigurować ustawienia sieciowe, jak pokazano poniżej migawki.</span><span class="sxs-lookup"><span data-stu-id="67110-162">You can select the VM in the replicated items to configure the network settings as shown in the snapshot below.</span></span>

* <span data-ttu-id="67110-163">Dla serwerów AOS wybrać zestaw dostępności jest prawidłowa.</span><span class="sxs-lookup"><span data-stu-id="67110-163">For AOS servers select the correct availability set.</span></span>

* <span data-ttu-id="67110-164">Jeśli jest używany statyczny adres IP, należy określić adres IP, który ma maszyny wirtualnej w **docelowy adres IP** pola ![ustawień sieci](./media/site-recovery-dynamics-ax/vmpropertiesaos1.png)</span><span class="sxs-lookup"><span data-stu-id="67110-164">If you are using a static IP then specify the IP that you want the virtual machine to take in the **Target IP** field ![Network Settings ](./media/site-recovery-dynamics-ax/vmpropertiesaos1.png)</span></span>



### <a name="5-creating-a-recovery-plan"></a><span data-ttu-id="67110-165">5. Tworzenie planu odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="67110-165">5. Creating a recovery plan</span></span>

<span data-ttu-id="67110-166">W usłudze Azure Site Recovery można zautomatyzować proces trybu failover można utworzyć planu odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="67110-166">You can create a recovery plan in Azure Site Recovery to automate the failover process.</span></span> <span data-ttu-id="67110-167">Dodawanie warstwy aplikacji i warstwy sieci web w planie odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="67110-167">Add app tier and web tier in the Recovery Plan.</span></span> <span data-ttu-id="67110-168">Kolejność ich w różnych grupach tak, aby warstwy frontonu zamknięcia przed aplikacji.</span><span class="sxs-lookup"><span data-stu-id="67110-168">Order them in different groups so that the front-end shutdown before app tier.</span></span>

1)  <span data-ttu-id="67110-169">Wybierz magazyn Azure Site Recovery w ramach subskrypcji i kliknij Kafelek "Plany odzyskiwania".</span><span class="sxs-lookup"><span data-stu-id="67110-169">Select the Azure Site Recovery vault in your subscription and click on ‘Recovery Plans’ tile.</span></span>

2)  <span data-ttu-id="67110-170">Kliknij pozycję "+ plan i określ nazwę odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="67110-170">Click on ‘+ Recovery plan and specify a name.</span></span>

3)  <span data-ttu-id="67110-171">Wybierz 'Source' i 'Target'.</span><span class="sxs-lookup"><span data-stu-id="67110-171">Select the ‘Source’ and ‘Target’.</span></span> <span data-ttu-id="67110-172">Element docelowy może być Azure lub dodatkowej lokacji.</span><span class="sxs-lookup"><span data-stu-id="67110-172">The target can be Azure or secondary site.</span></span> <span data-ttu-id="67110-173">W przypadku platformy Azure, należy określić model wdrażania</span><span class="sxs-lookup"><span data-stu-id="67110-173">In case you choose Azure, you must specify the deployment model</span></span>

![Tworzenie planu odzyskiwania](./media/site-recovery-dynamics-ax/recoveryplancreation1.png)

4)  <span data-ttu-id="67110-175">Wybierz AOS i klienta maszyn wirtualnych do planu odzyskiwania, a następnie kliknij przycisk ✓.</span><span class="sxs-lookup"><span data-stu-id="67110-175">Select the AOS and client VMs to the recovery plan and click ✓.</span></span>
<span data-ttu-id="67110-176">![Tworzenie planu odzyskiwania](./media/site-recovery-dynamics-ax/selectvms.png)</span><span class="sxs-lookup"><span data-stu-id="67110-176">![Create Recovery Plan](./media/site-recovery-dynamics-ax/selectvms.png)</span></span>


![Plan odzyskiwania](./media/site-recovery-dynamics-ax/recoveryplan.png)

<span data-ttu-id="67110-178">Plan odzyskiwania aplikacji Dynamics AX można dostosować, dodając różnych kroków zgodnie z opisem poniżej.</span><span class="sxs-lookup"><span data-stu-id="67110-178">You can customize the recovery plan for Dynamics AX application by adding various steps as detailed below.</span></span> <span data-ttu-id="67110-179">Migawki powyżej przedstawiono planu odzyskiwania ukończone po dodaniu wszystkich kroków.</span><span class="sxs-lookup"><span data-stu-id="67110-179">The above snapshot shows the complete recovery plan after adding all the steps.</span></span>

<span data-ttu-id="67110-180">*Kroki:*</span><span class="sxs-lookup"><span data-stu-id="67110-180">*Steps:*</span></span>

<span data-ttu-id="67110-181">*1. Program SQL Server w tryb failover kroki*</span><span class="sxs-lookup"><span data-stu-id="67110-181">*1. SQL Server fail over steps*</span></span>

<span data-ttu-id="67110-182">Zapoznaj się ["Rozwiązanie odzyskiwania po awarii programu SQL Server"](site-recovery-sql.md) Przewodnik uzupełniający po szczegółowe informacje na temat określonych czynności odzyskiwania do programu SQL server.</span><span class="sxs-lookup"><span data-stu-id="67110-182">Refer to [‘SQL Server DR Solution’](site-recovery-sql.md) companion guide  for details about recovery steps specific to SQL server.</span></span>

<span data-ttu-id="67110-183">*2. Tryb failover Grupa 1: Tryb failover maszyn wirtualnych serwera AOS*</span><span class="sxs-lookup"><span data-stu-id="67110-183">*2. Failover Group 1: Fail over the AOS VMs*</span></span>

<span data-ttu-id="67110-184">Upewnij się, że wybrany punkt odzyskiwania jest możliwie najbliżej PIT bazy danych, lecz nie wyprzedzeniem.</span><span class="sxs-lookup"><span data-stu-id="67110-184">Make sure that the recovery point selected is as close as possible to the database PIT but not ahead.</span></span>

<span data-ttu-id="67110-185">*3. Skrypt: Moduł równoważenia obciążenia Dodaj (tylko A E)* Dodaj skryptów (za pośrednictwem usługi Automatyzacja Azure) po grupie maszyny Wirtualnej serwera AOS pojawia się, aby dodać usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="67110-185">*3. Script: Add load balancer (Only E-A)* Add a script (via Azure automation) after AOS VM group comes up to add a load balancer to it.</span></span> <span data-ttu-id="67110-186">Skrypt służy do wykonania tego zadania.</span><span class="sxs-lookup"><span data-stu-id="67110-186">You can use a script to do this task.</span></span> <span data-ttu-id="67110-187">Zobacz artykuł [sposób dodawania usługi równoważenia obciążenia dla aplikacji wielowarstwowych DR](https://azure.microsoft.com/blog/cloud-migration-and-disaster-recovery-of-load-balanced-multi-tier-applications-using-azure-site-recovery/)</span><span class="sxs-lookup"><span data-stu-id="67110-187">Refer article [how to add load balancer for multi-tier application DR](https://azure.microsoft.com/blog/cloud-migration-and-disaster-recovery-of-load-balanced-multi-tier-applications-using-azure-site-recovery/)</span></span>

<span data-ttu-id="67110-188">*4. Tryb failover, grupa 2: Awaryjnie klienta AX maszyn wirtualnych.*</span><span class="sxs-lookup"><span data-stu-id="67110-188">*4. Failover Group 2: Fail over the AX client VMs.*</span></span>
<span data-ttu-id="67110-189">Tryb failover warstwa sieci web maszyn wirtualnych w ramach planu odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="67110-189">Fail over the web tier VMs as part of the recovery plan.</span></span>


### <a name="doing-a-test-failover"></a><span data-ttu-id="67110-190">Ten test trybu failover</span><span class="sxs-lookup"><span data-stu-id="67110-190">Doing a test failover</span></span>

<span data-ttu-id="67110-191">Zobacz "Rozwiązanie odzyskiwania po awarii AD" i "Rozwiązanie odzyskiwania po awarii programu SQL Server" przewodników uzupełniających dotyczących kwestii związanych z określonego celu AD i programu SQL server odpowiednio podczas testowania trybu Failover.</span><span class="sxs-lookup"><span data-stu-id="67110-191">Refer to ‘AD DR Solution ’ and ‘SQL Server DR solution ’ companion guides for considerations specific to AD and SQL server respectively during Test Failover.</span></span>

1.  <span data-ttu-id="67110-192">Przejdź do portalu Azure i wybierz z magazynu usługi Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="67110-192">Go to Azure  portal and select your Site Recovery vault.</span></span>
2.  <span data-ttu-id="67110-193">Kliknij utworzony dla Dynamics AX planu odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="67110-193">Click on the recovery plan created for Dynamics AX.</span></span>
3.  <span data-ttu-id="67110-194">Kliknij na "Test trybu Failover".</span><span class="sxs-lookup"><span data-stu-id="67110-194">Click on ‘Test Failover’.</span></span>
4.  <span data-ttu-id="67110-195">Wybierz sieć wirtualną, aby rozpocząć proces awaryjnej testu.</span><span class="sxs-lookup"><span data-stu-id="67110-195">Select the virtual network to start the test fail-over process.</span></span>
5.  <span data-ttu-id="67110-196">Po skonfigurowaniu dodatkowej środowiska można wykonywać z operacji sprawdzania poprawności.</span><span class="sxs-lookup"><span data-stu-id="67110-196">Once the secondary environment is up, you can perform your validations.</span></span>
6.  <span data-ttu-id="67110-197">Po zakończeniu operacji sprawdzania poprawności, wybierz opcję "Ukończenie operacji sprawdzania poprawności" i testowe środowisko trybu failover zostaną wyczyszczone.</span><span class="sxs-lookup"><span data-stu-id="67110-197">Once the validations are complete, you can select ‘Validations complete’ and the test failover environment will be cleaned.</span></span>

<span data-ttu-id="67110-198">Postępuj zgodnie z [w tych wskazówkach](site-recovery-test-failover-to-azure.md) przeprowadzić test trybu failover.</span><span class="sxs-lookup"><span data-stu-id="67110-198">Follow [this guidance](site-recovery-test-failover-to-azure.md) to do a test failover.</span></span>

### <a name="doing-a-failover"></a><span data-ttu-id="67110-199">Podczas pracy w trybie failover</span><span class="sxs-lookup"><span data-stu-id="67110-199">Doing a failover</span></span>

1.  <span data-ttu-id="67110-200">Przejdź do portalu Azure i wybierz z magazynu usługi Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="67110-200">Go to Azure  portal and select your Site Recovery vault.</span></span>
2.  <span data-ttu-id="67110-201">Kliknij utworzony dla Dynamics AX planu odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="67110-201">Click on the recovery plan created for Dynamics AX.</span></span>
3.  <span data-ttu-id="67110-202">Kliknij "Failover" i wybierz polecenie "Failover".</span><span class="sxs-lookup"><span data-stu-id="67110-202">Click on ‘Failover’ and select ‘ Failover’.</span></span>
4.  <span data-ttu-id="67110-203">Wybierz sieć docelowa, a następnie kliknij przycisk ✓, aby rozpocząć proces trybu failover.</span><span class="sxs-lookup"><span data-stu-id="67110-203">Select the target network and click ✓ to start the failover process.</span></span>

<span data-ttu-id="67110-204">Postępuj zgodnie z [w tych wskazówkach](site-recovery-failover.md) podczas wprowadzania trybu failover.</span><span class="sxs-lookup"><span data-stu-id="67110-204">Follow [this guidance](site-recovery-failover.md) when you are doing a failover.</span></span>

### <a name="perform-a-failback"></a><span data-ttu-id="67110-205">Wykonaj powrót po awarii</span><span class="sxs-lookup"><span data-stu-id="67110-205">Perform a Failback</span></span>

<span data-ttu-id="67110-206">Zapoznaj się Przewodnik uzupełniający po "Rozwiązanie odzyskiwania po awarii programu SQL Server" Aby uzyskać informacje o określonym do programu SQL server podczas powrotu po awarii.</span><span class="sxs-lookup"><span data-stu-id="67110-206">Refer to ‘SQL Server DR Solution ’ companion guide for considerations specific to SQL server during Failback.</span></span>

1.  <span data-ttu-id="67110-207">Przejdź do portalu Azure i wybierz z magazynu usługi Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="67110-207">Go to Azure  portal and select your Site Recovery vault.</span></span>
2.  <span data-ttu-id="67110-208">Kliknij utworzony dla Dynamics AX planu odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="67110-208">Click on the recovery plan created for Dynamics AX.</span></span>
3.  <span data-ttu-id="67110-209">Kliknij "Failover" i wybierz polecenie pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="67110-209">Click on ‘Failover’ and select failover.</span></span>
4.  <span data-ttu-id="67110-210">Kliknij "Zmień kierunek".</span><span class="sxs-lookup"><span data-stu-id="67110-210">Click on ‘Change Direction’.</span></span>
5.  <span data-ttu-id="67110-211">Wybierz odpowiednie opcje - synchronizacji danych i opcje tworzenia maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="67110-211">Select the appropriate options - data synchronization and VM creation options</span></span>
6.  <span data-ttu-id="67110-212">Kliknij przycisk ✓, aby rozpocząć proces "Powrotu po awarii".</span><span class="sxs-lookup"><span data-stu-id="67110-212">Click ✓ to start the ‘Failback’ process.</span></span>


<span data-ttu-id="67110-213">Postępuj zgodnie z [w tych wskazówkach](site-recovery-failback-azure-to-vmware.md) podczas wprowadzania powrotu po awarii.</span><span class="sxs-lookup"><span data-stu-id="67110-213">Follow [this guidance](site-recovery-failback-azure-to-vmware.md) when you are doing a failback.</span></span>

##<a name="summary"></a><span data-ttu-id="67110-214">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="67110-214">Summary</span></span>
<span data-ttu-id="67110-215">Za pomocą usługi Azure Site Recovery, można utworzyć plan odzyskiwania ukończenia automatycznego po awarii aplikacji Dynamics AX.</span><span class="sxs-lookup"><span data-stu-id="67110-215">Using Azure Site Recovery, you can create a complete automated disaster recovery plan for your Dynamics AX application.</span></span> <span data-ttu-id="67110-216">Możesz zainicjować trybu failover w ciągu kilku sekund z dowolnego miejsca w przypadku przerwy w pracy i get aplikacji do pracy w minutach.</span><span class="sxs-lookup"><span data-stu-id="67110-216">You can initiate the failover within seconds from anywhere in the event of a disruption and get the application up and running in minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="67110-217">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="67110-217">Next steps</span></span>
<span data-ttu-id="67110-218">Odczyt [jakie obciążenia mogę chronić?](site-recovery-workload.md) Aby dowiedzieć się więcej o ochronie obciążeń przedsiębiorstwa z usługą Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="67110-218">Read [What workloads can I protect?](site-recovery-workload.md) to learn more about protecting enterprise workloads with Azure Site Recovery.</span></span>
