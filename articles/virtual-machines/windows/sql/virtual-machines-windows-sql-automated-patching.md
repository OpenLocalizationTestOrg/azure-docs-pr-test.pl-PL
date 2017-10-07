---
title: aaaAutomated poprawki dla programu SQL Server VMs (Resource Manager) | Dokumentacja firmy Microsoft
description: "Zawiera opis funkcji Automatyczne stosowanie poprawek powitania dla programu SQL Server maszyn wirtualnych działających na platformie Azure za pomocą Menedżera zasobów."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: 58232e92-318f-456b-8f0a-2201a541e08d
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: 8bb8d0fb265e69d7bbf1fa047f5ceef02e7c56fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="automated-patching-for-sql-server-in-azure-virtual-machines-resource-manager"></a><span data-ttu-id="eadc4-103">Automatyczne stosowanie poprawek dla programu SQL Server w usłudze Azure Virtual Machines (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="eadc4-103">Automated Patching for SQL Server in Azure Virtual Machines (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="eadc4-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="eadc4-104">Resource Manager</span></span>](virtual-machines-windows-sql-automated-patching.md)
> * [<span data-ttu-id="eadc4-105">Wdrożenie klasyczne</span><span class="sxs-lookup"><span data-stu-id="eadc4-105">Classic</span></span>](../classic/sql-automated-patching.md)
> 
> 

<span data-ttu-id="eadc4-106">Automatyczne Patching ustanawia okna obsługi dla maszyny wirtualnej platformy Azure działa program SQL Server.</span><span class="sxs-lookup"><span data-stu-id="eadc4-106">Automated Patching establishes a maintenance window for an Azure Virtual Machine running SQL Server.</span></span> <span data-ttu-id="eadc4-107">Automatyczne aktualizacje można zainstalować tylko w tym oknie obsługi.</span><span class="sxs-lookup"><span data-stu-id="eadc4-107">Automated Updates can only be installed during this maintenance window.</span></span> <span data-ttu-id="eadc4-108">Dla programu SQL Server to rescriction gwarantuje, że aktualizacje systemu i ponowne uruchomienia, skojarzone są wykonywane hello najlepsze możliwe hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="eadc4-108">For SQL Server, this rescriction ensures that system updates and any associated restarts occur at hello best possible time for hello database.</span></span> <span data-ttu-id="eadc4-109">Automatyczne Patching zależy od hello [rozszerzenia agenta programu SQL Server IaaS](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="eadc4-109">Automated Patching depends on hello [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="eadc4-110">Zobacz tooview hello klasycznej wersji w tym artykule [automatyczne stosowanie poprawek dla programu SQL Server w klasycznym maszyny wirtualne Azure](../classic/sql-automated-patching.md).</span><span class="sxs-lookup"><span data-stu-id="eadc4-110">tooview hello classic version of this article, see [Automated Patching for SQL Server in Azure Virtual Machines Classic](../classic/sql-automated-patching.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eadc4-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="eadc4-111">Prerequisites</span></span>
<span data-ttu-id="eadc4-112">toouse automatyczne stosowanie poprawek, należy wziąć pod uwagę następujące wymagania wstępne hello:</span><span class="sxs-lookup"><span data-stu-id="eadc4-112">toouse Automated Patching, consider hello following prerequisites:</span></span>

<span data-ttu-id="eadc4-113">**System operacyjny**:</span><span class="sxs-lookup"><span data-stu-id="eadc4-113">**Operating System**:</span></span>

* <span data-ttu-id="eadc4-114">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="eadc4-114">Windows Server 2012</span></span>
* <span data-ttu-id="eadc4-115">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="eadc4-115">Windows Server 2012 R2</span></span>
* <span data-ttu-id="eadc4-116">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="eadc4-116">Windows Server 2016</span></span>

<span data-ttu-id="eadc4-117">**Wersja programu SQL Server**:</span><span class="sxs-lookup"><span data-stu-id="eadc4-117">**SQL Server version**:</span></span>

* <span data-ttu-id="eadc4-118">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="eadc4-118">SQL Server 2012</span></span>
* <span data-ttu-id="eadc4-119">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="eadc4-119">SQL Server 2014</span></span>
* <span data-ttu-id="eadc4-120">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="eadc4-120">SQL Server 2016</span></span>

<span data-ttu-id="eadc4-121">**Program Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="eadc4-121">**Azure PowerShell**:</span></span>

* <span data-ttu-id="eadc4-122">[Zainstaluj najnowsze poleceń programu Azure PowerShell hello](/powershell/azure/overview) Jeśli planujesz tooconfigure automatyczne stosowanie poprawek przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="eadc4-122">[Install hello latest Azure PowerShell commands](/powershell/azure/overview) if you plan tooconfigure Automated Patching with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="eadc4-123">Automatyczne Patching polega na powitania rozszerzenia agenta programu SQL Server IaaS.</span><span class="sxs-lookup"><span data-stu-id="eadc4-123">Automated Patching relies on hello SQL Server IaaS Agent Extension.</span></span> <span data-ttu-id="eadc4-124">Bieżący obrazów Galeria maszyny wirtualnej SQL dodać to rozszerzenie domyślnie.</span><span class="sxs-lookup"><span data-stu-id="eadc4-124">Current SQL virtual machine gallery images add this extension by default.</span></span> <span data-ttu-id="eadc4-125">Aby uzyskać więcej informacji, zobacz [rozszerzenia agenta programu SQL Server IaaS](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="eadc4-125">For more information, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>
> 
> 

## <a name="settings"></a><span data-ttu-id="eadc4-126">Ustawienia</span><span class="sxs-lookup"><span data-stu-id="eadc4-126">Settings</span></span>
<span data-ttu-id="eadc4-127">Witaj poniższej tabeli opisano opcje hello, które można skonfigurować dla automatyczne stosowanie poprawek.</span><span class="sxs-lookup"><span data-stu-id="eadc4-127">hello following table describes hello options that can be configured for Automated Patching.</span></span> <span data-ttu-id="eadc4-128">kroki rzeczywista konfiguracja Hello się różnić w zależności od tego, czy używać hello portalu Azure lub poleceń programu Windows PowerShell dla usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="eadc4-128">hello actual configuration steps vary depending on whether you use hello Azure portal or Azure Windows PowerShell commands.</span></span>

| <span data-ttu-id="eadc4-129">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="eadc4-129">Setting</span></span> | <span data-ttu-id="eadc4-130">Możliwe wartości</span><span class="sxs-lookup"><span data-stu-id="eadc4-130">Possible values</span></span> | <span data-ttu-id="eadc4-131">Opis</span><span class="sxs-lookup"><span data-stu-id="eadc4-131">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="eadc4-132">**Automatyczne stosowanie poprawek**</span><span class="sxs-lookup"><span data-stu-id="eadc4-132">**Automated Patching**</span></span> |<span data-ttu-id="eadc4-133">Włącza/wyłącza (wyłączone)</span><span class="sxs-lookup"><span data-stu-id="eadc4-133">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="eadc4-134">Włącza lub wyłącza automatyczne stosowanie poprawek dla maszyny wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="eadc4-134">Enables or disables Automated Patching for an Azure virtual machine.</span></span> |
| <span data-ttu-id="eadc4-135">**Harmonogram konserwacji**</span><span class="sxs-lookup"><span data-stu-id="eadc4-135">**Maintenance schedule**</span></span> |<span data-ttu-id="eadc4-136">Codziennie, poniedziałek, Wtorek, środę, czwartek, piątek, sobota, niedziela</span><span class="sxs-lookup"><span data-stu-id="eadc4-136">Everyday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday</span></span> |<span data-ttu-id="eadc4-137">Harmonogram Hello pobieranie i instalowanie aktualizacji systemu Windows, programu SQL Server i Microsoft dla maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="eadc4-137">hello schedule for downloading and installing Windows, SQL Server, and Microsoft updates for your virtual machine.</span></span> |
| <span data-ttu-id="eadc4-138">**Godzina rozpoczęcia konserwacji**</span><span class="sxs-lookup"><span data-stu-id="eadc4-138">**Maintenance start hour**</span></span> |<span data-ttu-id="eadc4-139">0-24</span><span class="sxs-lookup"><span data-stu-id="eadc4-139">0-24</span></span> |<span data-ttu-id="eadc4-140">Witaj uruchamiania lokalnego czasu tooupdate hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="eadc4-140">hello local start time tooupdate hello virtual machine.</span></span> |
| <span data-ttu-id="eadc4-141">**Czas trwania okna obsługi**</span><span class="sxs-lookup"><span data-stu-id="eadc4-141">**Maintenance window duration**</span></span> |<span data-ttu-id="eadc4-142">30-180</span><span class="sxs-lookup"><span data-stu-id="eadc4-142">30-180</span></span> |<span data-ttu-id="eadc4-143">Witaj liczbę minut dozwolone toocomplete hello pobierania i instalacji aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="eadc4-143">hello number of minutes permitted toocomplete hello download and installation of updates.</span></span> |
| <span data-ttu-id="eadc4-144">**Poprawka kategorii**</span><span class="sxs-lookup"><span data-stu-id="eadc4-144">**Patch Category**</span></span> |<span data-ttu-id="eadc4-145">Ważne</span><span class="sxs-lookup"><span data-stu-id="eadc4-145">Important</span></span> |<span data-ttu-id="eadc4-146">Kategoria Hello toodownload aktualizacji i instalacji.</span><span class="sxs-lookup"><span data-stu-id="eadc4-146">hello category of updates toodownload and install.</span></span> |

## <a name="configuration-in-hello-portal"></a><span data-ttu-id="eadc4-147">Konfiguracja w hello portalu</span><span class="sxs-lookup"><span data-stu-id="eadc4-147">Configuration in hello Portal</span></span>
<span data-ttu-id="eadc4-148">Można użyć hello tooconfigure portalu Azure automatyczne stosowanie poprawek podczas inicjowania obsługi lub dla istniejących maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="eadc4-148">You can use hello Azure portal tooconfigure Automated Patching during provisioning or for existing VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="eadc4-149">Nowe maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="eadc4-149">New VMs</span></span>
<span data-ttu-id="eadc4-150">Użyj hello tooconfigure portalu Azure automatyczne stosowanie poprawek podczas tworzenia nowej maszyny wirtualnej serwera SQL w modelu wdrażania usługi Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="eadc4-150">Use hello Azure portal tooconfigure Automated Patching when you create a new SQL Server Virtual Machine in hello Resource Manager deployment model.</span></span>

<span data-ttu-id="eadc4-151">W hello **ustawienia programu SQL Server** bloku, wybierz opcję **automatyczne stosowanie poprawek**.</span><span class="sxs-lookup"><span data-stu-id="eadc4-151">In hello **SQL Server settings** blade, select **Automated patching**.</span></span> <span data-ttu-id="eadc4-152">Witaj Poniższy zrzut ekranu portalu Azure zawiera hello **automatyczne stosowanie poprawek SQL** bloku.</span><span class="sxs-lookup"><span data-stu-id="eadc4-152">hello following Azure portal screenshot shows hello **SQL Automated Patching** blade.</span></span>

![SQL automatyczne stosowanie poprawek w portalu Azure](./media/virtual-machines-windows-sql-automated-patching/azure-sql-arm-patching.png)

<span data-ttu-id="eadc4-154">Dla kontekstu, zobacz temat pełną hello na [obsługi maszyny wirtualnej programu SQL Server na platformie Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="eadc4-154">For context, see hello complete topic on [provisioning a SQL Server virtual machine in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="eadc4-155">Istniejące maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="eadc4-155">Existing VMs</span></span>
<span data-ttu-id="eadc4-156">W przypadku istniejących maszyn wirtualnych programu SQL Server należy wybrać maszyny wirtualnej programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="eadc4-156">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="eadc4-157">Następnie wybierz hello **konfigurację programu SQL Server** sekcji hello **ustawienia** bloku.</span><span class="sxs-lookup"><span data-stu-id="eadc4-157">Then select hello **SQL Server configuration** section of hello **Settings** blade.</span></span>

![SQL automatyczne stosowanie poprawek dla istniejących maszyn wirtualnych](./media/virtual-machines-windows-sql-automated-patching/azure-sql-rm-patching-existing-vms.png)

<span data-ttu-id="eadc4-159">W hello **konfigurację programu SQL Server** bloku, kliknij przycisk hello **Edytuj** przycisku na powitania automatycznego stosowania poprawek sekcji.</span><span class="sxs-lookup"><span data-stu-id="eadc4-159">In hello **SQL Server configuration** blade, click hello **Edit** button in hello Automated patching section.</span></span>

![Skonfiguruj automatyczne stosowanie poprawek SQL dla istniejących maszyn wirtualnych](./media/virtual-machines-windows-sql-automated-patching/azure-sql-rm-patching-configuration.png)

<span data-ttu-id="eadc4-161">Po zakończeniu kliknij przycisk hello **OK** przycisk u dołu hello hello **konfigurację programu SQL Server** toosave bloku zmiany.</span><span class="sxs-lookup"><span data-stu-id="eadc4-161">When finished, click hello **OK** button on hello bottom of hello **SQL Server configuration** blade toosave your changes.</span></span>

<span data-ttu-id="eadc4-162">Jeśli włączasz automatyczne stosowanie poprawek dla powitania po raz pierwszy, Azure konfiguruje hello Agent środowiska IaaS programu SQL Server w tle hello.</span><span class="sxs-lookup"><span data-stu-id="eadc4-162">If you are enabling Automated Patching for hello first time, Azure configures hello SQL Server IaaS Agent in hello background.</span></span> <span data-ttu-id="eadc4-163">W tym czasie hello portalu Azure może nie informować, że skonfigurowano automatyczne stosowanie poprawek.</span><span class="sxs-lookup"><span data-stu-id="eadc4-163">During this time, hello Azure portal might not show that Automated Patching is configured.</span></span> <span data-ttu-id="eadc4-164">Poczekaj kilka minut dla hello toobe agent zainstalowany, skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="eadc4-164">Wait several minutes for hello agent toobe installed, configured.</span></span> <span data-ttu-id="eadc4-165">Po tym hello Azure portal odzwierciedla hello nowych ustawień.</span><span class="sxs-lookup"><span data-stu-id="eadc4-165">After that hello Azure portal reflects hello new settings.</span></span>

> [!NOTE]
> <span data-ttu-id="eadc4-166">Można również skonfigurować automatyczne stosowanie poprawek za pomocą szablonu.</span><span class="sxs-lookup"><span data-stu-id="eadc4-166">You can also configure Automated Patching using a template.</span></span> <span data-ttu-id="eadc4-167">Aby uzyskać więcej informacji, zobacz [szablon Szybki Start Azure automatyczne stosowanie poprawek](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autopatching-update).</span><span class="sxs-lookup"><span data-stu-id="eadc4-167">For more information, see [Azure quickstart template for Automated Patching](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autopatching-update).</span></span>
> 
> 

## <a name="configuration-with-powershell"></a><span data-ttu-id="eadc4-168">Konfiguracja przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="eadc4-168">Configuration with PowerShell</span></span>
<span data-ttu-id="eadc4-169">Po aprowizacji maszyny Wirtualnej SQL, użyj programu PowerShell tooconfigure automatyczne stosowanie poprawek.</span><span class="sxs-lookup"><span data-stu-id="eadc4-169">After provisioning your SQL VM, use PowerShell tooconfigure Automated Patching.</span></span>

<span data-ttu-id="eadc4-170">Poniższy przykład hello, programu PowerShell jest używane tooconfigure automatyczne stosowanie poprawek na istniejącej maszyny Wirtualnej programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="eadc4-170">In hello following example, PowerShell is used tooconfigure Automated Patching on an existing SQL Server VM.</span></span> <span data-ttu-id="eadc4-171">Witaj **AzureRM.Compute\New AzureVMSqlServerAutoPatchingConfig** polecenie konfiguruje nowe okno obsługi, aktualizacje automatyczne.</span><span class="sxs-lookup"><span data-stu-id="eadc4-171">hello **AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig** command configures a new maintenance window for automatic updates.</span></span>

    $vmname = "vmname"
    $resourcegroupname = "resourcegroupname"
    $aps = AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig -Enable -DayOfWeek "Thursday" -MaintenanceWindowStartingHour 11 -MaintenanceWindowDuration 120  -PatchCategory "Important"

    Set-AzureRmVMSqlServerExtension -AutoPatchingSettings $aps -VMName $vmname -ResourceGroupName $resourcegroupname

<span data-ttu-id="eadc4-172">Na podstawie tego przykładu, hello poniższej tabeli opisano praktyce hello w celu hello maszyny Wirtualnej platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="eadc4-172">Based on this example, hello following table describes hello practical effect on hello target Azure VM:</span></span>

| <span data-ttu-id="eadc4-173">Parametr</span><span class="sxs-lookup"><span data-stu-id="eadc4-173">Parameter</span></span> | <span data-ttu-id="eadc4-174">Efekt</span><span class="sxs-lookup"><span data-stu-id="eadc4-174">Effect</span></span> |
| --- | --- |
| <span data-ttu-id="eadc4-175">**DayOfWeek**</span><span class="sxs-lookup"><span data-stu-id="eadc4-175">**DayOfWeek**</span></span> |<span data-ttu-id="eadc4-176">Każdy czwartek zainstalowanych poprawek.</span><span class="sxs-lookup"><span data-stu-id="eadc4-176">Patches installed every Thursday.</span></span> |
| <span data-ttu-id="eadc4-177">**MaintenanceWindowStartingHour**</span><span class="sxs-lookup"><span data-stu-id="eadc4-177">**MaintenanceWindowStartingHour**</span></span> |<span data-ttu-id="eadc4-178">Aktualizacje BEGIN o 11:00.</span><span class="sxs-lookup"><span data-stu-id="eadc4-178">Begin updates at 11:00am.</span></span> |
| <span data-ttu-id="eadc4-179">**MaintenanceWindowsDuration**</span><span class="sxs-lookup"><span data-stu-id="eadc4-179">**MaintenanceWindowsDuration**</span></span> |<span data-ttu-id="eadc4-180">Poprawki muszą być zainstalowane w ciągu 120 minut.</span><span class="sxs-lookup"><span data-stu-id="eadc4-180">Patches must be installed within 120 minutes.</span></span> <span data-ttu-id="eadc4-181">Na podstawie hello czasu rozpoczęcia, użytkownicy muszą wykonać przez 1:00 pm.</span><span class="sxs-lookup"><span data-stu-id="eadc4-181">Based on hello start time, they must complete by 1:00pm.</span></span> |
| <span data-ttu-id="eadc4-182">**PatchCategory**</span><span class="sxs-lookup"><span data-stu-id="eadc4-182">**PatchCategory**</span></span> |<span data-ttu-id="eadc4-183">Witaj, to tylko możliwe ustawienie tego parametru to **ważne**.</span><span class="sxs-lookup"><span data-stu-id="eadc4-183">hello only possible setting for this parameter is **Important**.</span></span> |

<span data-ttu-id="eadc4-184">Go może potrwać kilka minut tooinstall i skonfiguruj hello Agent środowiska IaaS programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="eadc4-184">It could take several minutes tooinstall and configure hello SQL Server IaaS Agent.</span></span>

<span data-ttu-id="eadc4-185">toodisable automatyczne stosowanie poprawek, uruchom hello sam skrypt bez hello **-Włącz** toohello parametru **AzureRM.Compute\New AzureVMSqlServerAutoPatchingConfig**.</span><span class="sxs-lookup"><span data-stu-id="eadc4-185">toodisable Automated Patching, run hello same script without hello **-Enable** parameter toohello **AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig**.</span></span> <span data-ttu-id="eadc4-186">Witaj braku hello **-Włącz** parametru sygnały hello polecenia toodisable hello funkcji.</span><span class="sxs-lookup"><span data-stu-id="eadc4-186">hello absence of hello **-Enable** parameter signals hello command toodisable hello feature.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eadc4-187">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="eadc4-187">Next steps</span></span>
<span data-ttu-id="eadc4-188">Informacje o innych zadaniach automatyzacji dostępny, zobacz [rozszerzenia agenta programu SQL Server IaaS](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="eadc4-188">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

<span data-ttu-id="eadc4-189">Aby uzyskać więcej informacji na temat uruchamiania programu SQL Server na maszynach wirtualnych Azure, zobacz [programu SQL Server na maszynach wirtualnych platformy Azure — omówienie](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="eadc4-189">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

