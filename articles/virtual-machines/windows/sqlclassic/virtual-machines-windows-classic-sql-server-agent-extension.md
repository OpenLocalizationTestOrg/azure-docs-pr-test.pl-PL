---
title: "Automatyzacji zadań zarządzania na maszynach wirtualnych SQL (klasyczne) | Dokumentacja firmy Microsoft"
description: "W tym temacie opisano sposób zarządzania rozszerzenie agenta programu SQL Server, który automatyzuje określonych zadań administracyjnych programu SQL Server. Obejmują one automatyczna usługa Backup, automatyczne stosowanie poprawek i integracji magazynu kluczy Azure. W tym temacie używa trybu klasycznego wdrożenia."
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a9bda2e7-cdba-427c-bc30-77cde4376f3a
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 30fa9128cd51a7498449c991b58500ad9acdd3d4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="automate-management-tasks-on-azure-virtual-machines-with-the-sql-server-agent-extension-classic"></a><span data-ttu-id="e9ee4-105">Automatyzacji zadań zarządzania na maszynach wirtualnych Azure z rozszerzeniem agenta serwera SQL (klasyczne)</span><span class="sxs-lookup"><span data-stu-id="e9ee4-105">Automate management tasks on Azure Virtual Machines with the SQL Server Agent Extension (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e9ee4-106">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e9ee4-106">Resource Manager</span></span>](../sql/virtual-machines-windows-sql-server-agent-extension.md)
> * [<span data-ttu-id="e9ee4-107">Wdrożenie klasyczne</span><span class="sxs-lookup"><span data-stu-id="e9ee4-107">Classic</span></span>](../classic/sql-server-agent-extension.md)
> 
>
 
<span data-ttu-id="e9ee4-108">Rozszerzenie agenta SQL Server IaaS (SQLIaaSAgent) działa na maszynach wirtualnych Azure w celu zautomatyzowania zadań administracyjnych.</span><span class="sxs-lookup"><span data-stu-id="e9ee4-108">The SQL Server IaaS Agent Extension (SQLIaaSAgent) runs on Azure virtual machines to automate administration tasks.</span></span> <span data-ttu-id="e9ee4-109">Ten temat zawiera omówienie usług obsługiwanych przez rozszerzenie, jak również instrukcje dotyczące instalacji, stanu i usuwania.</span><span class="sxs-lookup"><span data-stu-id="e9ee4-109">This topic provides an overview of the services supported by the extension as well as instructions for installation, status, and removal.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="e9ee4-110">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="e9ee4-110">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="e9ee4-111">W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="e9ee4-111">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="e9ee4-112">Firma Microsoft zaleca, aby w przypadku większości nowych wdrożeń korzystać z modelu opartego na programie Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e9ee4-112">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="e9ee4-113">Aby wyświetlić wersję usługi Resource Manager w tym artykule, zobacz [rozszerzenie agenta serwera SQL dla programu SQL Server maszyn wirtualnych Menedżera zasobów](../sql/virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="e9ee4-113">To view the Resource Manager version of this article, see [SQL Server Agent Extension for SQL Server VMs Resource Manager](../sql/virtual-machines-windows-sql-server-agent-extension.md).</span></span>

## <a name="supported-services"></a><span data-ttu-id="e9ee4-114">Obsługiwane usługi</span><span class="sxs-lookup"><span data-stu-id="e9ee4-114">Supported services</span></span>
<span data-ttu-id="e9ee4-115">Rozszerzenie agenta programu SQL Server IaaS obsługuje następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="e9ee4-115">The SQL Server IaaS Agent Extension supports the following administration tasks:</span></span>

| <span data-ttu-id="e9ee4-116">Funkcja administracji</span><span class="sxs-lookup"><span data-stu-id="e9ee4-116">Administration feature</span></span> | <span data-ttu-id="e9ee4-117">Opis</span><span class="sxs-lookup"><span data-stu-id="e9ee4-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e9ee4-118">**Automatyczna usługa Backup SQL**</span><span class="sxs-lookup"><span data-stu-id="e9ee4-118">**SQL Automated Backup**</span></span> |<span data-ttu-id="e9ee4-119">Automatyzuje Planowanie kopii zapasowych dla wszystkich baz danych dla domyślnego wystąpienia programu SQL Server w maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e9ee4-119">Automates the scheduling of backups for all databases for the default instance of SQL Server in the VM.</span></span> <span data-ttu-id="e9ee4-120">Aby uzyskać więcej informacji, zobacz [automatycznego tworzenia kopii zapasowej dla programu SQL Server w maszynach wirtualnych platformy Azure (klasyczne)](../classic/sql-automated-backup.md).</span><span class="sxs-lookup"><span data-stu-id="e9ee4-120">For more information, see [Automated backup for SQL Server in Azure Virtual Machines (Classic)](../classic/sql-automated-backup.md).</span></span> |
| <span data-ttu-id="e9ee4-121">**Automatyczne stosowanie poprawek SQL**</span><span class="sxs-lookup"><span data-stu-id="e9ee4-121">**SQL Automated Patching**</span></span> |<span data-ttu-id="e9ee4-122">Konfiguruje okno obsługi, w którym do maszyny Wirtualnej można przeprowadzać aktualizacje, aby uniknąć aktualizacje w godzinach szczytu dla obciążenia.</span><span class="sxs-lookup"><span data-stu-id="e9ee4-122">Configures a maintenance window during which updates to your VM can take place, so  you can avoid updates during peak times for your workload.</span></span> <span data-ttu-id="e9ee4-123">Aby uzyskać więcej informacji, zobacz [automatyczne stosowanie poprawek dla programu SQL Server w maszynach wirtualnych platformy Azure (klasyczne)](../classic/sql-automated-patching.md).</span><span class="sxs-lookup"><span data-stu-id="e9ee4-123">For more information, see [Automated patching for SQL Server in Azure Virtual Machines (Classic)](../classic/sql-automated-patching.md).</span></span> |
| <span data-ttu-id="e9ee4-124">**Integracja z usługą Azure Key Vault**</span><span class="sxs-lookup"><span data-stu-id="e9ee4-124">**Azure Key Vault Integration**</span></span> |<span data-ttu-id="e9ee4-125">Umożliwia automatyczne instalowanie i konfigurowanie usługi Azure Key Vault na maszyną Wirtualną programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e9ee4-125">Enables you to automatically install and configure Azure Key Vault on your SQL Server VM.</span></span> <span data-ttu-id="e9ee4-126">Aby uzyskać więcej informacji, zobacz [Konfigurowanie integracji magazynu kluczy Azure dla programu SQL Server na maszynach wirtualnych Azure (klasyczne)](../classic/ps-sql-keyvault.md).</span><span class="sxs-lookup"><span data-stu-id="e9ee4-126">For more information, see [Configure Azure Key Vault Integration for SQL Server on Azure VMs (Classic)](../classic/ps-sql-keyvault.md).</span></span> |

## <a name="prerequisites"></a><span data-ttu-id="e9ee4-127">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e9ee4-127">Prerequisites</span></span>
<span data-ttu-id="e9ee4-128">Wymagania dotyczące używania rozszerzenie agenta IaaS serwera SQL na maszynie Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="e9ee4-128">Requirements to use the SQL Server IaaS Agent Extension on your VM:</span></span>

### <a name="operating-system"></a><span data-ttu-id="e9ee4-129">System operacyjny:</span><span class="sxs-lookup"><span data-stu-id="e9ee4-129">Operating System:</span></span>
* <span data-ttu-id="e9ee4-130">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="e9ee4-130">Windows Server 2012</span></span>
* <span data-ttu-id="e9ee4-131">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="e9ee4-131">Windows Server 2012 R2</span></span>
* <span data-ttu-id="e9ee4-132">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="e9ee4-132">Windows Server 2016</span></span>

### <a name="sql-server-versions"></a><span data-ttu-id="e9ee4-133">Wersje programu SQL Server:</span><span class="sxs-lookup"><span data-stu-id="e9ee4-133">SQL Server versions:</span></span>
* <span data-ttu-id="e9ee4-134">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="e9ee4-134">SQL Server 2012</span></span>
* <span data-ttu-id="e9ee4-135">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="e9ee4-135">SQL Server 2014</span></span>
* <span data-ttu-id="e9ee4-136">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="e9ee4-136">SQL Server 2016</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="e9ee4-137">Program Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="e9ee4-137">Azure PowerShell:</span></span>
<span data-ttu-id="e9ee4-138">[Pobierz i skonfiguruj najnowszych poleceń programu PowerShell Azure](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e9ee4-138">[Download and configure the latest Azure PowerShell commands](/powershell/azure/overview).</span></span>

<span data-ttu-id="e9ee4-139">Uruchom program Windows PowerShell i połącz go z subskrypcją platformy Azure z **Add-AzureAccount** polecenia.</span><span class="sxs-lookup"><span data-stu-id="e9ee4-139">Start Windows PowerShell, and connect it to your Azure subscription with the **Add-AzureAccount** command.</span></span>

    Add-AzureAccount

<span data-ttu-id="e9ee4-140">Jeśli masz wiele subskrypcji, użyj **AzureSubscription wybierz** Wybierz subskrypcję, która zawiera urządzenie docelowe klasyczne maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e9ee4-140">If you have multiple subscriptions, use **Select-AzureSubscription** to select the subscription that contains your target classic VM.</span></span>

    Select-AzureSubscription -SubscriptionName <subscriptionname>

<span data-ttu-id="e9ee4-141">W tym momencie można uzyskać listy klasycznych maszyn wirtualnych i ich nazwy usługi skojarzone z **Get-AzureVM** polecenia.</span><span class="sxs-lookup"><span data-stu-id="e9ee4-141">At this point, you can get a list of the classic virtual machines and their associated service names with the **Get-AzureVM** command.</span></span>

    Get-AzureVM

## <a name="installation"></a><span data-ttu-id="e9ee4-142">Instalacja</span><span class="sxs-lookup"><span data-stu-id="e9ee4-142">Installation</span></span>
<span data-ttu-id="e9ee4-143">Dla klasycznych maszyn wirtualnych należy użyć programu PowerShell, aby zainstalować rozszerzenie agenta programu SQL Server IaaS i skonfigurować skojarzonych z nimi usług.</span><span class="sxs-lookup"><span data-stu-id="e9ee4-143">For classic VMs, you must use PowerShell to install the SQL Server IaaS Agent Extension and configure its associated services.</span></span> <span data-ttu-id="e9ee4-144">Użyj **AzureVMSqlServerExtension zestaw** polecenia cmdlet programu PowerShell, aby zainstalować to rozszerzenie.</span><span class="sxs-lookup"><span data-stu-id="e9ee4-144">Use the **Set-AzureVMSqlServerExtension** PowerShell cmdlet to install the extension.</span></span> <span data-ttu-id="e9ee4-145">Na przykład następujące polecenie instaluje rozszerzenie na maszynie Wirtualnej serwera systemu Windows (klasyczne) i nazwy jej "SQLIaaSExtension".</span><span class="sxs-lookup"><span data-stu-id="e9ee4-145">For example, the following command installs the extension on a Windows Server VM (classic) and names it "SQLIaaSExtension".</span></span>

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -ReferenceName "SQLIaasExtension" -Version "1.2" | Update-AzureVM

<span data-ttu-id="e9ee4-146">Po aktualizacji do najnowszej wersji rozszerzenia agenta IaaS SQL, należy ponownie uruchomić maszynę wirtualną po zaktualizowaniu rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="e9ee4-146">If you update to the latest version of the SQL IaaS Agent Extension, you must restart your virtual machine after updating the extension.</span></span>

> [!NOTE]
> <span data-ttu-id="e9ee4-147">Klasycznych maszyn wirtualnych nie ma możliwości, aby zainstalować i skonfigurować rozszerzenia SQL IaaS agenta za pośrednictwem portalu.</span><span class="sxs-lookup"><span data-stu-id="e9ee4-147">Classic virtual machines do not have an option to install and configure the SQL IaaS Agent Extension through the portal.</span></span>
> 
> 

## <a name="status"></a><span data-ttu-id="e9ee4-148">Stan</span><span class="sxs-lookup"><span data-stu-id="e9ee4-148">Status</span></span>
<span data-ttu-id="e9ee4-149">Jest jednym ze sposobów Sprawdź, czy rozszerzenie jest zainstalowane, aby wyświetlić stan agenta w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e9ee4-149">One way to verify that the extension is installed is to view the agent status in the Azure Portal.</span></span> <span data-ttu-id="e9ee4-150">Wybierz maszynę wirtualną na liście w bloku maszyny wirtualnej, a następnie kliknij polecenie **rozszerzenia**.</span><span class="sxs-lookup"><span data-stu-id="e9ee4-150">Select a virtual machine listed in the virtual machine blade, and then click on **Extensions**.</span></span> <span data-ttu-id="e9ee4-151">Powinny pojawić się **SQLIaaSAgent** rozszerzenie na liście.</span><span class="sxs-lookup"><span data-stu-id="e9ee4-151">You should see the **SQLIaaSAgent** extension listed.</span></span>

![Rozszerzenie IaaS agenta serwera SQL w portalu Azure](./media/virtual-machines-windows-classic-sql-server-agent-extension/azure-sql-server-iaas-agent-portal.png)

<span data-ttu-id="e9ee4-153">Można również użyć **Get-AzureVMSqlServerExtension** polecenia cmdlet programu Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="e9ee4-153">You can also use the **Get-AzureVMSqlServerExtension** Azure Powershell cmdlet.</span></span>

    Get-AzureVM –ServiceName "service" –Name "vmname" | Get-AzureVMSqlServerExtension

## <a name="removal"></a><span data-ttu-id="e9ee4-154">Usuwanie</span><span class="sxs-lookup"><span data-stu-id="e9ee4-154">Removal</span></span>
<span data-ttu-id="e9ee4-155">W portalu Azure, można odinstalować rozszerzenia, klikając wielokropek **rozszerzenia** bloku właściwości maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e9ee4-155">In the Azure Portal, you can uninstall the extension by clicking the ellipsis on the **Extensions** blade of your virtual machine properties.</span></span> <span data-ttu-id="e9ee4-156">Następnie kliknij przycisk **Odinstaluj**.</span><span class="sxs-lookup"><span data-stu-id="e9ee4-156">Then click **Uninstall**.</span></span>

![Odinstaluj rozszerzenie programu SQL Server Agent środowiska IaaS w portalu Azure](./media/virtual-machines-windows-classic-sql-server-agent-extension/azure-sql-server-iaas-agent-uninstall.png)

<span data-ttu-id="e9ee4-158">Można również użyć **AzureVMSqlServerExtension Usuń** polecenia cmdlet programu Powershell.</span><span class="sxs-lookup"><span data-stu-id="e9ee4-158">You can also use the **Remove-AzureVMSqlServerExtension** Powershell cmdlet.</span></span>

    Get-AzureVM –ServiceName "service" –Name "vmname" | Remove-AzureVMSqlServerExtension | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="e9ee4-159">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e9ee4-159">Next Steps</span></span>
<span data-ttu-id="e9ee4-160">Rozpocznij przy użyciu jednej z usług obsługiwanych przez rozszerzenie.</span><span class="sxs-lookup"><span data-stu-id="e9ee4-160">Begin using one of the services supported by the extension.</span></span> <span data-ttu-id="e9ee4-161">Aby uzyskać więcej informacji, zobacz tematy, do którego odwołuje się [obsługiwane usługi](#supported-services) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="e9ee4-161">For more details, see the topics referenced in the [Supported services](#supported-services) section of this article.</span></span>

<span data-ttu-id="e9ee4-162">Aby uzyskać więcej informacji na temat uruchamiania programu SQL Server na maszynach wirtualnych platformy Azure, zobacz [programu SQL Server na maszynach wirtualnych platformy Azure — omówienie](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e9ee4-162">For more information about running SQL Server on Azure Virtual Machines, see [SQL Server on Azure Virtual Machines overview](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

