---
title: aaaAutomated poprawki dla programu SQL Server VMs (klasyczne) | Dokumentacja firmy Microsoft
description: "Zawiera opis funkcji Automatyczne stosowanie poprawek powitania dla SQL Server maszyn wirtualnych działających w trybie klasycznym wdrożenia hello Azure."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 737b2f65-08b9-4f54-b867-e987730265a8
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: 2ef06b95705fc457605d6eb2fbc0afd490321843
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="automated-patching-for-sql-server-in-azure-virtual-machines-classic"></a><span data-ttu-id="572dd-103">Automatyczne stosowanie poprawek dla programu SQL Server na maszynach wirtualnych platformy Azure (klasyczne)</span><span class="sxs-lookup"><span data-stu-id="572dd-103">Automated Patching for SQL Server in Azure Virtual Machines (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="572dd-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="572dd-104">Resource Manager</span></span>](../sql/virtual-machines-windows-sql-automated-patching.md)
> * [<span data-ttu-id="572dd-105">Wdrożenie klasyczne</span><span class="sxs-lookup"><span data-stu-id="572dd-105">Classic</span></span>](../classic/sql-automated-patching.md)
> 
> 

<span data-ttu-id="572dd-106">Automatyczne Patching ustanawia okna obsługi dla maszyny wirtualnej platformy Azure działa program SQL Server.</span><span class="sxs-lookup"><span data-stu-id="572dd-106">Automated Patching establishes a maintenance window for an Azure Virtual Machine running SQL Server.</span></span> <span data-ttu-id="572dd-107">Automatyczne aktualizacje można zainstalować tylko w tym oknie obsługi.</span><span class="sxs-lookup"><span data-stu-id="572dd-107">Automated Updates can only be installed during this maintenance window.</span></span> <span data-ttu-id="572dd-108">Dla programu SQL Server zapewnia, że aktualizacje systemu i ponowne uruchomienia, skojarzone są wykonywane hello najlepsze możliwe hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="572dd-108">For SQL Server, this ensures that system updates and any associated restarts occur at hello best possible time for hello database.</span></span> <span data-ttu-id="572dd-109">Automatyczne Patching zależy od hello [rozszerzenia agenta programu SQL Server IaaS](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="572dd-109">Automated Patching depends on hello [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="572dd-110">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="572dd-110">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="572dd-111">W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello.</span><span class="sxs-lookup"><span data-stu-id="572dd-111">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="572dd-112">Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="572dd-112">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="572dd-113">wersja Menedżera zasobów hello tooview tego artykułu, zobacz [automatyczne stosowanie poprawek dla programu SQL Server w Menedżerze zasobów maszyn wirtualnych Azure](../sql/virtual-machines-windows-sql-automated-patching.md).</span><span class="sxs-lookup"><span data-stu-id="572dd-113">tooview hello Resource Manager version of this article, see [Automated Patching for SQL Server in Azure Virtual Machines Resource Manager](../sql/virtual-machines-windows-sql-automated-patching.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="572dd-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="572dd-114">Prerequisites</span></span>
<span data-ttu-id="572dd-115">toouse automatyczne stosowanie poprawek, należy wziąć pod uwagę następujące wymagania wstępne hello:</span><span class="sxs-lookup"><span data-stu-id="572dd-115">toouse Automated Patching, consider hello following prerequisites:</span></span>

<span data-ttu-id="572dd-116">**System operacyjny**:</span><span class="sxs-lookup"><span data-stu-id="572dd-116">**Operating System**:</span></span>

* <span data-ttu-id="572dd-117">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="572dd-117">Windows Server 2012</span></span>
* <span data-ttu-id="572dd-118">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="572dd-118">Windows Server 2012 R2</span></span>
* <span data-ttu-id="572dd-119">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="572dd-119">Windows Server 2016</span></span>

<span data-ttu-id="572dd-120">**Wersja programu SQL Server**:</span><span class="sxs-lookup"><span data-stu-id="572dd-120">**SQL Server version**:</span></span>

* <span data-ttu-id="572dd-121">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="572dd-121">SQL Server 2012</span></span>
* <span data-ttu-id="572dd-122">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="572dd-122">SQL Server 2014</span></span>
* <span data-ttu-id="572dd-123">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="572dd-123">SQL Server 2016</span></span>

<span data-ttu-id="572dd-124">**Program Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="572dd-124">**Azure PowerShell**:</span></span>

* <span data-ttu-id="572dd-125">[Zainstaluj najnowsze poleceń programu Azure PowerShell hello](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="572dd-125">[Install hello latest Azure PowerShell commands](/powershell/azure/overview).</span></span>

<span data-ttu-id="572dd-126">**Rozszerzenia programu SQL Server IaaS**:</span><span class="sxs-lookup"><span data-stu-id="572dd-126">**SQL Server IaaS Extension**:</span></span>

* <span data-ttu-id="572dd-127">[Zainstaluj hello IaaS rozszerzenie dotyczące programu SQL Server](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="572dd-127">[Install hello SQL Server IaaS Extension](../classic/sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="572dd-128">Ustawienia</span><span class="sxs-lookup"><span data-stu-id="572dd-128">Settings</span></span>
<span data-ttu-id="572dd-129">Witaj poniższej tabeli opisano opcje hello, które można skonfigurować dla automatyczne stosowanie poprawek.</span><span class="sxs-lookup"><span data-stu-id="572dd-129">hello following table describes hello options that can be configured for Automated Patching.</span></span> <span data-ttu-id="572dd-130">Klasycznych maszyn wirtualnych należy użyć programu PowerShell tooconfigure te ustawienia.</span><span class="sxs-lookup"><span data-stu-id="572dd-130">For classic VMs, you must use PowerShell tooconfigure these settings.</span></span>

| <span data-ttu-id="572dd-131">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="572dd-131">Setting</span></span> | <span data-ttu-id="572dd-132">Możliwe wartości</span><span class="sxs-lookup"><span data-stu-id="572dd-132">Possible values</span></span> | <span data-ttu-id="572dd-133">Opis</span><span class="sxs-lookup"><span data-stu-id="572dd-133">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="572dd-134">**Automatyczne stosowanie poprawek**</span><span class="sxs-lookup"><span data-stu-id="572dd-134">**Automated Patching**</span></span> |<span data-ttu-id="572dd-135">Włącza/wyłącza (wyłączone)</span><span class="sxs-lookup"><span data-stu-id="572dd-135">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="572dd-136">Włącza lub wyłącza automatyczne stosowanie poprawek dla maszyny wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="572dd-136">Enables or disables Automated Patching for an Azure virtual machine.</span></span> |
| <span data-ttu-id="572dd-137">**Harmonogram konserwacji**</span><span class="sxs-lookup"><span data-stu-id="572dd-137">**Maintenance schedule**</span></span> |<span data-ttu-id="572dd-138">Codziennie, poniedziałek, Wtorek, środę, czwartek, piątek, sobota, niedziela</span><span class="sxs-lookup"><span data-stu-id="572dd-138">Everyday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday</span></span> |<span data-ttu-id="572dd-139">Harmonogram Hello pobieranie i instalowanie aktualizacji systemu Windows, programu SQL Server i Microsoft dla maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="572dd-139">hello schedule for downloading and installing Windows, SQL Server, and Microsoft updates for your virtual machine.</span></span> |
| <span data-ttu-id="572dd-140">**Godzina rozpoczęcia konserwacji**</span><span class="sxs-lookup"><span data-stu-id="572dd-140">**Maintenance start hour**</span></span> |<span data-ttu-id="572dd-141">0-24</span><span class="sxs-lookup"><span data-stu-id="572dd-141">0-24</span></span> |<span data-ttu-id="572dd-142">Witaj uruchamiania lokalnego czasu tooupdate hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="572dd-142">hello local start time tooupdate hello virtual machine.</span></span> |
| <span data-ttu-id="572dd-143">**Czas trwania okna obsługi**</span><span class="sxs-lookup"><span data-stu-id="572dd-143">**Maintenance window duration**</span></span> |<span data-ttu-id="572dd-144">30-180</span><span class="sxs-lookup"><span data-stu-id="572dd-144">30-180</span></span> |<span data-ttu-id="572dd-145">Witaj liczbę minut dozwolone toocomplete hello pobierania i instalacji aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="572dd-145">hello number of minutes permitted toocomplete hello download and installation of updates.</span></span> |
| <span data-ttu-id="572dd-146">**Poprawka kategorii**</span><span class="sxs-lookup"><span data-stu-id="572dd-146">**Patch Category**</span></span> |<span data-ttu-id="572dd-147">Ważne</span><span class="sxs-lookup"><span data-stu-id="572dd-147">Important</span></span> |<span data-ttu-id="572dd-148">Kategoria Hello toodownload aktualizacji i instalacji.</span><span class="sxs-lookup"><span data-stu-id="572dd-148">hello category of updates toodownload and install.</span></span> |

## <a name="configuration-with-powershell"></a><span data-ttu-id="572dd-149">Konfiguracja przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="572dd-149">Configuration with PowerShell</span></span>
<span data-ttu-id="572dd-150">Poniższy przykład hello, programu PowerShell jest używane tooconfigure automatyczne stosowanie poprawek na istniejącej maszyny Wirtualnej programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="572dd-150">In hello following example, PowerShell is used tooconfigure Automated Patching on an existing SQL Server VM.</span></span> <span data-ttu-id="572dd-151">Witaj **AzureVMSqlServerAutoPatchingConfig nowy** polecenie konfiguruje nowe okno obsługi, aktualizacje automatyczne.</span><span class="sxs-lookup"><span data-stu-id="572dd-151">hello **New-AzureVMSqlServerAutoPatchingConfig** command configures a new maintenance window for automatic updates.</span></span>

    $aps = New-AzureVMSqlServerAutoPatchingConfig -Enable -DayOfWeek "Thursday" -MaintenanceWindowStartingHour 11 -MaintenanceWindowDuration 120  -PatchCategory "Important"

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoPatchingSettings $aps | Update-AzureVM

<span data-ttu-id="572dd-152">Na podstawie tego przykładu, hello poniższej tabeli opisano praktyce hello w celu hello maszyny Wirtualnej platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="572dd-152">Based on this example, hello following table describes hello practical effect on hello target Azure VM:</span></span>

| <span data-ttu-id="572dd-153">Parametr</span><span class="sxs-lookup"><span data-stu-id="572dd-153">Parameter</span></span> | <span data-ttu-id="572dd-154">Efekt</span><span class="sxs-lookup"><span data-stu-id="572dd-154">Effect</span></span> |
| --- | --- |
| <span data-ttu-id="572dd-155">**DayOfWeek**</span><span class="sxs-lookup"><span data-stu-id="572dd-155">**DayOfWeek**</span></span> |<span data-ttu-id="572dd-156">Każdy czwartek zainstalowanych poprawek.</span><span class="sxs-lookup"><span data-stu-id="572dd-156">Patches installed every Thursday.</span></span> |
| <span data-ttu-id="572dd-157">**MaintenanceWindowStartingHour**</span><span class="sxs-lookup"><span data-stu-id="572dd-157">**MaintenanceWindowStartingHour**</span></span> |<span data-ttu-id="572dd-158">Aktualizacje BEGIN o 11:00.</span><span class="sxs-lookup"><span data-stu-id="572dd-158">Begin updates at 11:00am.</span></span> |
| <span data-ttu-id="572dd-159">**MaintenanceWindowsDuration**</span><span class="sxs-lookup"><span data-stu-id="572dd-159">**MaintenanceWindowsDuration**</span></span> |<span data-ttu-id="572dd-160">Poprawki muszą być zainstalowane w ciągu 120 minut.</span><span class="sxs-lookup"><span data-stu-id="572dd-160">Patches must be installed within 120 minutes.</span></span> <span data-ttu-id="572dd-161">Na podstawie hello czasu rozpoczęcia, użytkownicy muszą wykonać przez 1:00 pm.</span><span class="sxs-lookup"><span data-stu-id="572dd-161">Based on hello start time, they must complete by 1:00pm.</span></span> |
| <span data-ttu-id="572dd-162">**PatchCategory**</span><span class="sxs-lookup"><span data-stu-id="572dd-162">**PatchCategory**</span></span> |<span data-ttu-id="572dd-163">Witaj tylko ustawień dla tego parametru jest "Ważne".</span><span class="sxs-lookup"><span data-stu-id="572dd-163">hello only possible setting for this parameter is “Important”.</span></span> |

<span data-ttu-id="572dd-164">Go może potrwać kilka minut tooinstall i skonfiguruj hello Agent środowiska IaaS programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="572dd-164">It could take several minutes tooinstall and configure hello SQL Server IaaS Agent.</span></span>

<span data-ttu-id="572dd-165">toodisable automatyczne stosowanie poprawek, uruchom hello sam skrypt bez hello - Włącz parametr toohello AzureVMSqlServerAutoPatchingConfig nowy.</span><span class="sxs-lookup"><span data-stu-id="572dd-165">toodisable Automated Patching, run hello same script without hello -Enable parameter toohello New-AzureVMSqlServerAutoPatchingConfig.</span></span> <span data-ttu-id="572dd-166">Zgodnie z instalacją, może upłynąć kilka minut toodisable automatyczne stosowanie poprawek.</span><span class="sxs-lookup"><span data-stu-id="572dd-166">As with installation, it can take several minutes toodisable Automated Patching.</span></span>

## <a name="next-steps"></a><span data-ttu-id="572dd-167">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="572dd-167">Next steps</span></span>
<span data-ttu-id="572dd-168">Informacje o innych zadaniach automatyzacji dostępny, zobacz [rozszerzenia agenta programu SQL Server IaaS](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="572dd-168">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md).</span></span>

<span data-ttu-id="572dd-169">Aby uzyskać więcej informacji na temat uruchamiania programu SQL Server na maszynach wirtualnych Azure, zobacz [programu SQL Server na maszynach wirtualnych platformy Azure — omówienie](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="572dd-169">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

