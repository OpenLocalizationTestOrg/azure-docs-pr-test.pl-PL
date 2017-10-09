---
title: "aaaReplicate wdrażania Dynamics AX wielowarstwową przy użyciu usługi Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób tooreplicate i chronić Dynamics AX przy użyciu usługi Azure Site Recovery"
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
ms.openlocfilehash: b974315ec50ab2ec43846b3d3f95c7de88b72fc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-a-multi-tier-dynamics-ax-application-using-azure-site-recovery"></a><span data-ttu-id="29193-103">Replikowanie wielowarstwowej aplikacji Dynamics AX przy użyciu usługi Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="29193-103">Replicate a multi-tier Dynamics AX application using Azure Site Recovery</span></span>

## <a name="overview"></a><span data-ttu-id="29193-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="29193-104">Overview</span></span>


<span data-ttu-id="29193-105">Microsoft Dynamics AX jest jednym z hello najpopularniejszych rozwiązań ERP między procesu toostandardized przedsiębiorstwa w lokalizacjach, zarządzanie zasobami i uproszczenia zgodności.</span><span class="sxs-lookup"><span data-stu-id="29193-105">Microsoft Dynamics AX is one of hello most popular ERP solution among enterprises toostandardized process across locations, manage resources and simplifying compliance.</span></span> <span data-ttu-id="29193-106">Considering aplikacja hello jest biznesowe krytyczne tooan organizacji jest bardzo ważne toobe się, że jeśli wszelkie po awarii, aplikacja powinna być uruchomiona w minimalny czas.</span><span class="sxs-lookup"><span data-stu-id="29193-106">Considering hello application is business critical tooan organization it is very important toobe sure that if any disaster, application should be up and running in minimum time.</span></span>

<span data-ttu-id="29193-107">Już dziś Microsoft Dynamics AX nie zapewnia żadnych funkcji odzyskiwania po awarii poza pole.</span><span class="sxs-lookup"><span data-stu-id="29193-107">Today, Microsoft Dynamics AX  does not provide any out-of-the-box disaster recovery capabilities.</span></span> <span data-ttu-id="29193-108">Microsoft Dynamics AX składa się z wielu składników serwera, takich jak serwer bazy danych SQL serwera aplikacji, Active Directory (AD), serwer programu SharePoint, odzyskiwania po awarii itp serwera raportowania toomanage hello każdego z tych składników ręcznie jest nie tylko kosztowna, ale również podatne na błędy.</span><span class="sxs-lookup"><span data-stu-id="29193-108">Microsoft Dynamics AX consists of many server components like Application Object Server, Active Directory (AD), SQL Database Server, SharePoint Server, Reporting Server etc. toomanage hello disaster recovery of each of these components manually is not only expensive but also error-prone.</span></span>

<span data-ttu-id="29193-109">W tym artykule opisano szczegółowo dotyczące tworzenia rozwiązanie odzyskiwania po awarii dla programu Dynamics AX aplikacji przy użyciu [usługi Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="29193-109">This article explains in detail about how you can create a disaster recovery solution for your Dynamics AX application using [Azure Site Recovery](site-recovery-overview.md).</span></span> <span data-ttu-id="29193-110">Obejmuje ona również planowane/nieplanowane/testowanie oprogramowania przełączenia do trybu failover przy użyciu planu odzyskiwania jednym kliknięciem, obsługiwane konfiguracje i wymagania wstępne.</span><span class="sxs-lookup"><span data-stu-id="29193-110">It also covers planned/unplanned/test failovers using one-click recovery plan, supported configurations, and prerequisites.</span></span>
<span data-ttu-id="29193-111">Rozwiązanie odzyskiwania po awarii w usłudze Azure Site Recovery na podstawie jest w pełni przetestowane, certyfikowane i zalecanymi przez program Microsoft Dynamics AX.</span><span class="sxs-lookup"><span data-stu-id="29193-111">Azure Site Recovery based disaster recovery solution is fully tested, certified, and recommended by Microsoft Dynamics AX.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="29193-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="29193-112">Prerequisites</span></span>

<span data-ttu-id="29193-113">Wdrażanie odzyskiwania po awarii dla aplikacji Dynamics AX przy użyciu usługi Azure Site Recovery wymaga hello następujące wymagania wstępne ukończone.</span><span class="sxs-lookup"><span data-stu-id="29193-113">Implementing disaster recovery for Dynamics AX application using Azure Site Recovery requires hello following pre-requisites completed.</span></span>

<span data-ttu-id="29193-114">• Lokalnego wdrożenia programu Dynamics AX został skonfigurowany</span><span class="sxs-lookup"><span data-stu-id="29193-114">•   An on-premises Dynamics AX deployment has been set up</span></span>

<span data-ttu-id="29193-115">• Magazyn usług odzyskiwania azure lokacji został utworzony w subskrypcji Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="29193-115">•   Azure Site Recovery Services vault has been created in Microsoft Azure subscription</span></span>

<span data-ttu-id="29193-116">• Jeśli Azure to witryny odzyskiwania, uruchom narzędzie oceny gotowości maszyny wirtualnej Azure hello na tooensure maszyn wirtualnych zgodnych z maszynami wirtualnymi Azure i usług Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="29193-116">•   If Azure is your recovery site, run hello Azure Virtual Machine Readiness Assessment tool  on VMs tooensure that they are compatible with Azure VMs and Azure Site Recovery Services</span></span>


## <a name="site-recovery-support"></a><span data-ttu-id="29193-117">Obsługa odzyskiwania lokacji</span><span class="sxs-lookup"><span data-stu-id="29193-117">Site Recovery support</span></span>

<span data-ttu-id="29193-118">Witaj w celu tworzenia w tym artykule użyto maszyn wirtualnych VMware z 2012R3 Dynamics AX w systemie Windows Server 2012 R2 Enterprise.</span><span class="sxs-lookup"><span data-stu-id="29193-118">For hello purpose of creating this article, VMware virtual machines with Dynamics AX  2012R3 on Windows Server 2012 R2 Enterprise were used.</span></span> <span data-ttu-id="29193-119">Ponieważ replikacja z lokacji odzyskiwania jest niezależny od aplikacji, zalecenia hello podano tutaj toohold oczekiwanego w następujących scenariuszach również.</span><span class="sxs-lookup"><span data-stu-id="29193-119">As site recovery replication is application agnostic, hello recommendations provided here are expected toohold on following scenarios as well.</span></span>

### <a name="source-and-target"></a><span data-ttu-id="29193-120">Źródłowa i docelowa</span><span class="sxs-lookup"><span data-stu-id="29193-120">Source and target</span></span>

<span data-ttu-id="29193-121">**Scenariusz**</span><span class="sxs-lookup"><span data-stu-id="29193-121">**Scenario**</span></span> | <span data-ttu-id="29193-122">**tooa lokacji dodatkowej**</span><span class="sxs-lookup"><span data-stu-id="29193-122">**tooa secondary site**</span></span> | <span data-ttu-id="29193-123">**tooAzure**</span><span class="sxs-lookup"><span data-stu-id="29193-123">**tooAzure**</span></span>
--- | --- | ---
<span data-ttu-id="29193-124">**Funkcja Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="29193-124">**Hyper-V**</span></span> | <span data-ttu-id="29193-125">Tak</span><span class="sxs-lookup"><span data-stu-id="29193-125">Yes</span></span> | <span data-ttu-id="29193-126">Tak</span><span class="sxs-lookup"><span data-stu-id="29193-126">Yes</span></span>
<span data-ttu-id="29193-127">**VMware**</span><span class="sxs-lookup"><span data-stu-id="29193-127">**VMware**</span></span> | <span data-ttu-id="29193-128">Tak</span><span class="sxs-lookup"><span data-stu-id="29193-128">Yes</span></span> | <span data-ttu-id="29193-129">Tak</span><span class="sxs-lookup"><span data-stu-id="29193-129">Yes</span></span>
<span data-ttu-id="29193-130">**Serwer fizyczny**</span><span class="sxs-lookup"><span data-stu-id="29193-130">**Physical server**</span></span> | <span data-ttu-id="29193-131">Tak</span><span class="sxs-lookup"><span data-stu-id="29193-131">Yes</span></span> | <span data-ttu-id="29193-132">Tak</span><span class="sxs-lookup"><span data-stu-id="29193-132">Yes</span></span>

## <a name="enable-dr-of-dynamics-ax-application-using-azure-site-recovery"></a><span data-ttu-id="29193-133">Włączenie odzyskiwania po awarii programu Dynamics AX aplikacji przy użyciu usługi Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="29193-133">Enable DR of Dynamics AX application using Azure Site Recovery</span></span>
### <a name="protect-your-dynamics-ax-application"></a><span data-ttu-id="29193-134">Ochrona aplikacji Dynamics AX</span><span class="sxs-lookup"><span data-stu-id="29193-134">Protect your Dynamics AX application</span></span>
<span data-ttu-id="29193-135">Każdy składnik hello Dynamics AX potrzeb toobe chronione replikacji kompletna aplikacja hello tooenable i odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="29193-135">Each component of hello Dynamics AX needs toobe protected tooenable hello complete application replication and recovery.</span></span> <span data-ttu-id="29193-136">W tej sekcji omówiono:</span><span class="sxs-lookup"><span data-stu-id="29193-136">This section covers:</span></span>

<span data-ttu-id="29193-137">**1. Ochrona usługi Active Directory**</span><span class="sxs-lookup"><span data-stu-id="29193-137">**1. Protection of Active Directory**</span></span>

<span data-ttu-id="29193-138">**2. Ochrona warstwy SQL**</span><span class="sxs-lookup"><span data-stu-id="29193-138">**2. Protection of SQL Tier**</span></span>

<span data-ttu-id="29193-139">**3. Ochrona aplikacji i warstwy sieci Web**</span><span class="sxs-lookup"><span data-stu-id="29193-139">**3. Protection of App and Web Tiers**</span></span>

<span data-ttu-id="29193-140">**4. Konfiguracja sieci**</span><span class="sxs-lookup"><span data-stu-id="29193-140">**4. Networking configuration**</span></span>

<span data-ttu-id="29193-141">**5. Plan odzyskiwania**</span><span class="sxs-lookup"><span data-stu-id="29193-141">**5. Recovery Plan**</span></span>

### <a name="1-setup-ad-and-dns-replication"></a><span data-ttu-id="29193-142">1. Instalator usługi AD i replikacja DNS</span><span class="sxs-lookup"><span data-stu-id="29193-142">1. Setup AD and DNS replication</span></span>

<span data-ttu-id="29193-143">Usługi Active Directory jest wymagany w lokacji odzyskiwania po awarii hello toofunction aplikacji Dynamics AX.</span><span class="sxs-lookup"><span data-stu-id="29193-143">Active Directory is required on hello DR site for Dynamics AX application toofunction.</span></span> <span data-ttu-id="29193-144">Istnieją dwie opcje zalecane w zależności od złożoności hello powitania klienta w środowisku lokalnym.</span><span class="sxs-lookup"><span data-stu-id="29193-144">There are two recommended choices based on hello complexity of hello customer’s on-premises environment.</span></span>

<span data-ttu-id="29193-145">**Opcja 1**</span><span class="sxs-lookup"><span data-stu-id="29193-145">**Option 1**</span></span>

<span data-ttu-id="29193-146">Jeśli powitania klienta ma małej liczby aplikacji i jednego kontrolera domeny dla całej jego lokalnej lokacji i będzie można przechodzenie w tryb failover hello całej witryny razem, a następnie firma Microsoft zaleca używanie replikacji ASR tooreplicate hello DC maszyny toosecondary lokacji ( dotyczy zarówno tooSite lokacji i lokacji tooAzure).</span><span class="sxs-lookup"><span data-stu-id="29193-146">If hello customer has a small number of applications and a single domain controller for his entire on-premises site and will be failing over hello entire site together, then we recommend using ASR-Replication tooreplicate hello DC machine toosecondary site (applicable for both Site tooSite and Site tooAzure).</span></span>

<span data-ttu-id="29193-147">**Opcja 2**</span><span class="sxs-lookup"><span data-stu-id="29193-147">**Option 2**</span></span>

<span data-ttu-id="29193-148">Jeśli powitania klienta ma dużą liczbę aplikacji i działa w lesie usługi Active Directory i będzie miała kilka aplikacji w czasie, a następnie zalecamy skonfigurowanie dodatkowego kontrolera domeny w lokacji hello DR (lokacji dodatkowej lub na platformie Azure).</span><span class="sxs-lookup"><span data-stu-id="29193-148">If hello customer has a large number of applications and is running an Active Directory forest and will fail-over few applications at a time, then we recommend setting up an additional domain controller on hello DR site (secondary site or in Azure).</span></span>

<span data-ttu-id="29193-149">Zobacz zbyt[Przewodnik uzupełniający po na udostępnianie kontrolera domeny w lokacji odzyskiwania po awarii](site-recovery-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="29193-149">Please refer too[companion guide on making a domain controller available on DR site](site-recovery-active-directory.md).</span></span> <span data-ttu-id="29193-150">Dla pozostałej części tego dokumentu zostanie przyjęto założenie, że kontroler domeny jest dostępny w witrynie odzyskiwania po awarii.</span><span class="sxs-lookup"><span data-stu-id="29193-150">For remainder of this document we will assume a DC is available on DR site.</span></span>

### <a name="2-setup-sql-server-replication"></a><span data-ttu-id="29193-151">2. Ustawienia replikacji programu SQL Server</span><span class="sxs-lookup"><span data-stu-id="29193-151">2. Setup SQL Server replication</span></span>
<span data-ttu-id="29193-152">Można znaleźć w przewodniku toocompanion techniczne wskazówki dotyczące hello zalecana opcja ochrony [warstwy SQL](site-recovery-sql.md).</span><span class="sxs-lookup"><span data-stu-id="29193-152">Please refer toocompanion guide  for detailed technical guidance on hello recommended option for protecting [SQL tier](site-recovery-sql.md).</span></span>

### <a name="3-enable-protection-for-dynamics-ax-client-and-aos-vms"></a><span data-ttu-id="29193-153">3. Włącz ochronę Dynamics AX klienta i serwera AOS maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="29193-153">3. Enable protection for Dynamics AX client and AOS VMs</span></span>
<span data-ttu-id="29193-154">Wykonaj odpowiednie konfigurację usługi Azure Site Recovery na czy hello maszyny wirtualne są wdrażane na podstawie [funkcji Hyper-V](site-recovery-hyper-v-site-to-azure.md) lub na [VMware](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="29193-154">Perform relevant Azure Site Recovery configuration based on whether hello VMs are deployed on [Hyper-V](site-recovery-hyper-v-site-to-azure.md) or on [VMware](site-recovery-vmware-to-azure.md).</span></span>

> [!TIP]
> <span data-ttu-id="29193-155">Zalecane tooconfigure spójne częstotliwość awarii wynosi 15 minut.</span><span class="sxs-lookup"><span data-stu-id="29193-155">Recommended Crash consistent frequency tooconfigure is 15 minutes.</span></span>
>

<span data-ttu-id="29193-156">Hello poniżej migawki Wyświetla stan ochrony hello maszyn wirtualnych składnika Dynamics w scenariuszu ochrony "VMware lokacji tooAzure".</span><span class="sxs-lookup"><span data-stu-id="29193-156">hello below snapshot shows hello protection status of Dynamics component VMs in ‘VMware site tooAzure’ protection scenario.</span></span>
<span data-ttu-id="29193-157">![Elementy chronione](./media/site-recovery-dynamics-ax/protecteditems.png)</span><span class="sxs-lookup"><span data-stu-id="29193-157">![Protected items ](./media/site-recovery-dynamics-ax/protecteditems.png)</span></span>

### <a name="4-configure-networking"></a><span data-ttu-id="29193-158">4. Konfigurowanie sieci</span><span class="sxs-lookup"><span data-stu-id="29193-158">4. Configure Networking</span></span>
<span data-ttu-id="29193-159">Konfigurowanie maszyny Wirtualnej obliczeniowe i ustawień sieciowych</span><span class="sxs-lookup"><span data-stu-id="29193-159">Configure VM Compute and Network Settings</span></span>

<span data-ttu-id="29193-160">Hello AX klienta i serwera AOS maszyn wirtualnych konfigurowania ustawień sieciowych w usłudze Azure Site Recovery, tak aby hello sieci maszyn wirtualnych pobierać dołączonych toohello prawo odzyskiwania po awarii sieci po pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="29193-160">For hello AX client and AOS VMs configure network settings in Azure Site Recovery so that hello VM networks get attached toohello right DR network after failover.</span></span> <span data-ttu-id="29193-161">Upewnij się, że sieć DR hello warstw jest warstwy SQL toohello routingu.</span><span class="sxs-lookup"><span data-stu-id="29193-161">Ensure hello DR network for these tiers is routable toohello SQL tier.</span></span>

<span data-ttu-id="29193-162">Możesz wybrać hello maszyny Wirtualnej w hello replikowane ustawienia sieciowe hello tooconfigure elementów, jak pokazano w migawce hello poniżej.</span><span class="sxs-lookup"><span data-stu-id="29193-162">You can select hello VM in hello replicated items tooconfigure hello network settings as shown in hello snapshot below.</span></span>

* <span data-ttu-id="29193-163">Dla serwerów AOS wybierz hello zestawu dostępności jest prawidłowa.</span><span class="sxs-lookup"><span data-stu-id="29193-163">For AOS servers select hello correct availability set.</span></span>

* <span data-ttu-id="29193-164">Jeśli jest używany statyczny adres IP, określ IP hello, interesujące hello tootake maszyny wirtualnej w hello **docelowy adres IP** pola ![ustawień sieci](./media/site-recovery-dynamics-ax/vmpropertiesaos1.png)</span><span class="sxs-lookup"><span data-stu-id="29193-164">If you are using a static IP then specify hello IP that you want hello virtual machine tootake in hello **Target IP** field ![Network Settings ](./media/site-recovery-dynamics-ax/vmpropertiesaos1.png)</span></span>



### <a name="5-creating-a-recovery-plan"></a><span data-ttu-id="29193-165">5. Tworzenie planu odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="29193-165">5. Creating a recovery plan</span></span>

<span data-ttu-id="29193-166">Plan odzyskiwania można utworzyć procesu pracy awaryjnej hello tooautomate usługi Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="29193-166">You can create a recovery plan in Azure Site Recovery tooautomate hello failover process.</span></span> <span data-ttu-id="29193-167">Dodawanie warstwy aplikacji i warstwa sieci web w programie hello planu odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="29193-167">Add app tier and web tier in hello Recovery Plan.</span></span> <span data-ttu-id="29193-168">Kolejność ich w różnych grupach, które hello frontonu zamknięcia przed warstwy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="29193-168">Order them in different groups so that hello front-end shutdown before app tier.</span></span>

1)  <span data-ttu-id="29193-169">Wybierz magazyn Azure Site Recovery hello w ramach subskrypcji i kliknij Kafelek "Plany odzyskiwania".</span><span class="sxs-lookup"><span data-stu-id="29193-169">Select hello Azure Site Recovery vault in your subscription and click on ‘Recovery Plans’ tile.</span></span>

2)  <span data-ttu-id="29193-170">Kliknij pozycję "+ plan i określ nazwę odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="29193-170">Click on ‘+ Recovery plan and specify a name.</span></span>

3)  <span data-ttu-id="29193-171">Wybierz hello 'Source' i 'Target'.</span><span class="sxs-lookup"><span data-stu-id="29193-171">Select hello ‘Source’ and ‘Target’.</span></span> <span data-ttu-id="29193-172">Witaj docelowym może być Azure lub dodatkowej lokacji.</span><span class="sxs-lookup"><span data-stu-id="29193-172">hello target can be Azure or secondary site.</span></span> <span data-ttu-id="29193-173">W przypadku platformy Azure, należy określić hello modelu wdrażania</span><span class="sxs-lookup"><span data-stu-id="29193-173">In case you choose Azure, you must specify hello deployment model</span></span>

![Tworzenie planu odzyskiwania](./media/site-recovery-dynamics-ax/recoveryplancreation1.png)

4)  <span data-ttu-id="29193-175">Wybierz hello AOS i planu odzyskiwania toohello maszyny wirtualne klienta, a następnie kliknij przycisk ✓.</span><span class="sxs-lookup"><span data-stu-id="29193-175">Select hello AOS and client VMs toohello recovery plan and click ✓.</span></span>
<span data-ttu-id="29193-176">![Tworzenie planu odzyskiwania](./media/site-recovery-dynamics-ax/selectvms.png)</span><span class="sxs-lookup"><span data-stu-id="29193-176">![Create Recovery Plan](./media/site-recovery-dynamics-ax/selectvms.png)</span></span>


![Plan odzyskiwania](./media/site-recovery-dynamics-ax/recoveryplan.png)

<span data-ttu-id="29193-178">Plan odzyskiwania hello aplikacji Dynamics AX można dostosować, dodając różnych kroków zgodnie z opisem poniżej.</span><span class="sxs-lookup"><span data-stu-id="29193-178">You can customize hello recovery plan for Dynamics AX application by adding various steps as detailed below.</span></span> <span data-ttu-id="29193-179">Witaj powyżej migawki pokazuje hello planu odzyskiwania ukończone po dodaniu wszystkich kroków hello.</span><span class="sxs-lookup"><span data-stu-id="29193-179">hello above snapshot shows hello complete recovery plan after adding all hello steps.</span></span>

<span data-ttu-id="29193-180">*Kroki:*</span><span class="sxs-lookup"><span data-stu-id="29193-180">*Steps:*</span></span>

<span data-ttu-id="29193-181">*1. Program SQL Server w tryb failover kroki*</span><span class="sxs-lookup"><span data-stu-id="29193-181">*1. SQL Server fail over steps*</span></span>

<span data-ttu-id="29193-182">Odwołuje się zbyt["Rozwiązanie odzyskiwania po awarii programu SQL Server"](site-recovery-sql.md) Przewodnik uzupełniający po szczegółowe informacje o serwerze tooSQL określone kroki odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="29193-182">Refer too[‘SQL Server DR Solution’](site-recovery-sql.md) companion guide  for details about recovery steps specific tooSQL server.</span></span>

<span data-ttu-id="29193-183">*2. Tryb failover Grupa 1: Tryb failover maszyn wirtualnych serwera AOS hello*</span><span class="sxs-lookup"><span data-stu-id="29193-183">*2. Failover Group 1: Fail over hello AOS VMs*</span></span>

<span data-ttu-id="29193-184">Upewnij się, że wybrany punkt odzyskiwania hello jest blisko bazy danych można toohello PIT, ale nie wyprzedzeniem.</span><span class="sxs-lookup"><span data-stu-id="29193-184">Make sure that hello recovery point selected is as close as possible toohello database PIT but not ahead.</span></span>

<span data-ttu-id="29193-185">*3. Skrypt: Moduł równoważenia obciążenia Dodaj (tylko A E)* dodać skrypt (za pośrednictwem usługi Automatyzacja Azure) po grupie AOS wirtualna funkcjonuje tooadd tooit usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="29193-185">*3. Script: Add load balancer (Only E-A)* Add a script (via Azure automation) after AOS VM group comes up tooadd a load balancer tooit.</span></span> <span data-ttu-id="29193-186">Tego zadania można używać toodo skryptu.</span><span class="sxs-lookup"><span data-stu-id="29193-186">You can use a script toodo this task.</span></span> <span data-ttu-id="29193-187">Zobacz artykuł [jak tooadd Usługa równoważenia obciążenia dla aplikacji wielowarstwowych DR](https://azure.microsoft.com/blog/cloud-migration-and-disaster-recovery-of-load-balanced-multi-tier-applications-using-azure-site-recovery/)</span><span class="sxs-lookup"><span data-stu-id="29193-187">Refer article [how tooadd load balancer for multi-tier application DR](https://azure.microsoft.com/blog/cloud-migration-and-disaster-recovery-of-load-balanced-multi-tier-applications-using-azure-site-recovery/)</span></span>

<span data-ttu-id="29193-188">*4. Tryb failover, grupa 2: Awaryjnie powitania klienta AX maszyn wirtualnych.*</span><span class="sxs-lookup"><span data-stu-id="29193-188">*4. Failover Group 2: Fail over hello AX client VMs.*</span></span>
<span data-ttu-id="29193-189">Warstwa sieci web hello maszyn wirtualnych w ramach planu odzyskiwania hello pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="29193-189">Fail over hello web tier VMs as part of hello recovery plan.</span></span>


### <a name="doing-a-test-failover"></a><span data-ttu-id="29193-190">Ten test trybu failover</span><span class="sxs-lookup"><span data-stu-id="29193-190">Doing a test failover</span></span>

<span data-ttu-id="29193-191">Zobacz too'AD rozwiązanie odzyskiwania po awarii "i"Rozwiązanie odzyskiwania po awarii programu SQL Server"przewodników uzupełniających dotyczących tooAD szczególne zagadnienia i SQL server odpowiednio podczas testowania trybu Failover.</span><span class="sxs-lookup"><span data-stu-id="29193-191">Refer too‘AD DR Solution ’ and ‘SQL Server DR solution ’ companion guides for considerations specific tooAD and SQL server respectively during Test Failover.</span></span>

1.  <span data-ttu-id="29193-192">Przejdź tooAzure portalu i wybierz z magazynu usługi Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="29193-192">Go tooAzure  portal and select your Site Recovery vault.</span></span>
2.  <span data-ttu-id="29193-193">Polecenie hello planu odzyskiwania utworzone dla Dynamics AX.</span><span class="sxs-lookup"><span data-stu-id="29193-193">Click on hello recovery plan created for Dynamics AX.</span></span>
3.  <span data-ttu-id="29193-194">Kliknij na "Test trybu Failover".</span><span class="sxs-lookup"><span data-stu-id="29193-194">Click on ‘Test Failover’.</span></span>
4.  <span data-ttu-id="29193-195">Wybierz proces awaryjnej testowego hello toostart hello sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="29193-195">Select hello virtual network toostart hello test fail-over process.</span></span>
5.  <span data-ttu-id="29193-196">Po skonfigurowaniu dodatkowej środowiska hello można wykonywać z operacji sprawdzania poprawności.</span><span class="sxs-lookup"><span data-stu-id="29193-196">Once hello secondary environment is up, you can perform your validations.</span></span>
6.  <span data-ttu-id="29193-197">Po zakończeniu operacji sprawdzania poprawności hello, wybierz opcję "Ukończenie operacji sprawdzania poprawności" i hello testowe środowisko trybu failover zostaną wyczyszczone.</span><span class="sxs-lookup"><span data-stu-id="29193-197">Once hello validations are complete, you can select ‘Validations complete’ and hello test failover environment will be cleaned.</span></span>

<span data-ttu-id="29193-198">Postępuj zgodnie z [w tych wskazówkach](site-recovery-test-failover-to-azure.md) toodo test trybu failover.</span><span class="sxs-lookup"><span data-stu-id="29193-198">Follow [this guidance](site-recovery-test-failover-to-azure.md) toodo a test failover.</span></span>

### <a name="doing-a-failover"></a><span data-ttu-id="29193-199">Podczas pracy w trybie failover</span><span class="sxs-lookup"><span data-stu-id="29193-199">Doing a failover</span></span>

1.  <span data-ttu-id="29193-200">Przejdź tooAzure portalu i wybierz z magazynu usługi Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="29193-200">Go tooAzure  portal and select your Site Recovery vault.</span></span>
2.  <span data-ttu-id="29193-201">Polecenie hello planu odzyskiwania utworzone dla Dynamics AX.</span><span class="sxs-lookup"><span data-stu-id="29193-201">Click on hello recovery plan created for Dynamics AX.</span></span>
3.  <span data-ttu-id="29193-202">Kliknij "Failover" i wybierz polecenie "Failover".</span><span class="sxs-lookup"><span data-stu-id="29193-202">Click on ‘Failover’ and select ‘ Failover’.</span></span>
4.  <span data-ttu-id="29193-203">Wybierz sieć docelowa hello, a następnie kliknij przycisk ✓ toostart hello trybu failover procesu.</span><span class="sxs-lookup"><span data-stu-id="29193-203">Select hello target network and click ✓ toostart hello failover process.</span></span>

<span data-ttu-id="29193-204">Postępuj zgodnie z [w tych wskazówkach](site-recovery-failover.md) podczas wprowadzania trybu failover.</span><span class="sxs-lookup"><span data-stu-id="29193-204">Follow [this guidance](site-recovery-failover.md) when you are doing a failover.</span></span>

### <a name="perform-a-failback"></a><span data-ttu-id="29193-205">Wykonaj powrót po awarii</span><span class="sxs-lookup"><span data-stu-id="29193-205">Perform a Failback</span></span>

<span data-ttu-id="29193-206">Zobacz too'SQL rozwiązanie odzyskiwania po awarii serwera "Przewodnik uzupełniający po zagadnienia dotyczące określonych tooSQL serwera podczas powrotu po awarii.</span><span class="sxs-lookup"><span data-stu-id="29193-206">Refer too‘SQL Server DR Solution ’ companion guide for considerations specific tooSQL server during Failback.</span></span>

1.  <span data-ttu-id="29193-207">Przejdź tooAzure portalu i wybierz z magazynu usługi Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="29193-207">Go tooAzure  portal and select your Site Recovery vault.</span></span>
2.  <span data-ttu-id="29193-208">Polecenie hello planu odzyskiwania utworzone dla Dynamics AX.</span><span class="sxs-lookup"><span data-stu-id="29193-208">Click on hello recovery plan created for Dynamics AX.</span></span>
3.  <span data-ttu-id="29193-209">Kliknij "Failover" i wybierz polecenie pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="29193-209">Click on ‘Failover’ and select failover.</span></span>
4.  <span data-ttu-id="29193-210">Kliknij "Zmień kierunek".</span><span class="sxs-lookup"><span data-stu-id="29193-210">Click on ‘Change Direction’.</span></span>
5.  <span data-ttu-id="29193-211">Wybierz odpowiednie opcje hello - synchronizacji danych i opcje tworzenia maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="29193-211">Select hello appropriate options - data synchronization and VM creation options</span></span>
6.  <span data-ttu-id="29193-212">Kliknij przycisk ✓ toostart hello "Powrotu po awarii" proces.</span><span class="sxs-lookup"><span data-stu-id="29193-212">Click ✓ toostart hello ‘Failback’ process.</span></span>


<span data-ttu-id="29193-213">Postępuj zgodnie z [w tych wskazówkach](site-recovery-failback-azure-to-vmware.md) podczas wprowadzania powrotu po awarii.</span><span class="sxs-lookup"><span data-stu-id="29193-213">Follow [this guidance](site-recovery-failback-azure-to-vmware.md) when you are doing a failback.</span></span>

##<a name="summary"></a><span data-ttu-id="29193-214">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="29193-214">Summary</span></span>
<span data-ttu-id="29193-215">Za pomocą usługi Azure Site Recovery, można utworzyć plan odzyskiwania ukończenia automatycznego po awarii aplikacji Dynamics AX.</span><span class="sxs-lookup"><span data-stu-id="29193-215">Using Azure Site Recovery, you can create a complete automated disaster recovery plan for your Dynamics AX application.</span></span> <span data-ttu-id="29193-216">Możesz zainicjować hello trybu failover w ciągu kilku sekund z dowolnego miejsca w hello zdarzeń zakłócenia i pobrać aplikacji hello do pracy w minutach.</span><span class="sxs-lookup"><span data-stu-id="29193-216">You can initiate hello failover within seconds from anywhere in hello event of a disruption and get hello application up and running in minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="29193-217">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="29193-217">Next steps</span></span>
<span data-ttu-id="29193-218">Odczyt [jakie obciążenia mogę chronić?](site-recovery-workload.md) toolearn więcej o ochronie obciążeń przedsiębiorstwa z usługą Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="29193-218">Read [What workloads can I protect?](site-recovery-workload.md) toolearn more about protecting enterprise workloads with Azure Site Recovery.</span></span>
