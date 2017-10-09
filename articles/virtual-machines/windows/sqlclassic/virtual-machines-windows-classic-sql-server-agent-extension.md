---
title: "zadania zarządzania aaaAutomate na maszynach wirtualnych SQL (klasyczne) | Dokumentacja firmy Microsoft"
description: "W tym temacie opisano, jak toomanage hello rozszerzenia agenta programu SQL Server, który automatyzuje określonych zadań administracyjnych programu SQL Server. Obejmują one automatyczna usługa Backup, automatyczne stosowanie poprawek i integracji magazynu kluczy Azure. W tym temacie używa trybu klasycznego wdrożenia hello."
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
ms.openlocfilehash: a1dc011e0526845701eaf0c365007938f9ee32ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="automate-management-tasks-on-azure-virtual-machines-with-hello-sql-server-agent-extension-classic"></a><span data-ttu-id="1536b-105">Automatyzacji zadań zarządzania na maszynach wirtualnych platformy Azure z hello rozszerzenie agenta serwera SQL (klasyczne)</span><span class="sxs-lookup"><span data-stu-id="1536b-105">Automate management tasks on Azure Virtual Machines with hello SQL Server Agent Extension (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1536b-106">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1536b-106">Resource Manager</span></span>](../sql/virtual-machines-windows-sql-server-agent-extension.md)
> * [<span data-ttu-id="1536b-107">Wdrożenie klasyczne</span><span class="sxs-lookup"><span data-stu-id="1536b-107">Classic</span></span>](../classic/sql-server-agent-extension.md)
> 
>
 
<span data-ttu-id="1536b-108">Witaj rozszerzenia agenta IaaS programu SQL Server (SQLIaaSAgent) działa na zadań administracyjnych tooautomate maszyn wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1536b-108">hello SQL Server IaaS Agent Extension (SQLIaaSAgent) runs on Azure virtual machines tooautomate administration tasks.</span></span> <span data-ttu-id="1536b-109">Ten temat zawiera omówienie usług hello obsługiwany przez rozszerzenie hello, jak również instrukcje dotyczące instalacji, stanu i usuwania.</span><span class="sxs-lookup"><span data-stu-id="1536b-109">This topic provides an overview of hello services supported by hello extension as well as instructions for installation, status, and removal.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="1536b-110">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="1536b-110">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="1536b-111">W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello.</span><span class="sxs-lookup"><span data-stu-id="1536b-111">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="1536b-112">Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1536b-112">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="1536b-113">wersja Menedżera zasobów hello tooview tego artykułu, zobacz [rozszerzenie agenta serwera SQL dla programu SQL Server maszyn wirtualnych Menedżera zasobów](../sql/virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="1536b-113">tooview hello Resource Manager version of this article, see [SQL Server Agent Extension for SQL Server VMs Resource Manager](../sql/virtual-machines-windows-sql-server-agent-extension.md).</span></span>

## <a name="supported-services"></a><span data-ttu-id="1536b-114">Obsługiwane usługi</span><span class="sxs-lookup"><span data-stu-id="1536b-114">Supported services</span></span>
<span data-ttu-id="1536b-115">Witaj rozszerzenia agenta programu SQL Server IaaS obsługuje hello następujące zadania administracyjne:</span><span class="sxs-lookup"><span data-stu-id="1536b-115">hello SQL Server IaaS Agent Extension supports hello following administration tasks:</span></span>

| <span data-ttu-id="1536b-116">Funkcja administracji</span><span class="sxs-lookup"><span data-stu-id="1536b-116">Administration feature</span></span> | <span data-ttu-id="1536b-117">Opis</span><span class="sxs-lookup"><span data-stu-id="1536b-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1536b-118">**Automatyczna usługa Backup SQL**</span><span class="sxs-lookup"><span data-stu-id="1536b-118">**SQL Automated Backup**</span></span> |<span data-ttu-id="1536b-119">Automatyzuje hello Planowanie tworzenia kopii zapasowych dla wszystkich baz danych dla hello domyślnego wystąpienia programu SQL Server w hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1536b-119">Automates hello scheduling of backups for all databases for hello default instance of SQL Server in hello VM.</span></span> <span data-ttu-id="1536b-120">Aby uzyskać więcej informacji, zobacz [automatycznego tworzenia kopii zapasowej dla programu SQL Server w maszynach wirtualnych platformy Azure (klasyczne)](../classic/sql-automated-backup.md).</span><span class="sxs-lookup"><span data-stu-id="1536b-120">For more information, see [Automated backup for SQL Server in Azure Virtual Machines (Classic)](../classic/sql-automated-backup.md).</span></span> |
| <span data-ttu-id="1536b-121">**Automatyczne stosowanie poprawek SQL**</span><span class="sxs-lookup"><span data-stu-id="1536b-121">**SQL Automated Patching**</span></span> |<span data-ttu-id="1536b-122">Konfiguruje podczas aktualizacji, które tooyour, maszyna wirtualna może potrwać umieszczone, okna obsługi, aby uniknąć aktualizacje w godzinach szczytu dla obciążenia.</span><span class="sxs-lookup"><span data-stu-id="1536b-122">Configures a maintenance window during which updates tooyour VM can take place, so  you can avoid updates during peak times for your workload.</span></span> <span data-ttu-id="1536b-123">Aby uzyskać więcej informacji, zobacz [automatyczne stosowanie poprawek dla programu SQL Server w maszynach wirtualnych platformy Azure (klasyczne)](../classic/sql-automated-patching.md).</span><span class="sxs-lookup"><span data-stu-id="1536b-123">For more information, see [Automated patching for SQL Server in Azure Virtual Machines (Classic)](../classic/sql-automated-patching.md).</span></span> |
| <span data-ttu-id="1536b-124">**Integracja z usługą Azure Key Vault**</span><span class="sxs-lookup"><span data-stu-id="1536b-124">**Azure Key Vault Integration**</span></span> |<span data-ttu-id="1536b-125">Umożliwia tooautomatically należy zainstalować i skonfigurować usługi Azure Key Vault na maszyną Wirtualną programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="1536b-125">Enables you tooautomatically install and configure Azure Key Vault on your SQL Server VM.</span></span> <span data-ttu-id="1536b-126">Aby uzyskać więcej informacji, zobacz [Konfigurowanie integracji magazynu kluczy Azure dla programu SQL Server na maszynach wirtualnych Azure (klasyczne)](../classic/ps-sql-keyvault.md).</span><span class="sxs-lookup"><span data-stu-id="1536b-126">For more information, see [Configure Azure Key Vault Integration for SQL Server on Azure VMs (Classic)](../classic/ps-sql-keyvault.md).</span></span> |

## <a name="prerequisites"></a><span data-ttu-id="1536b-127">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1536b-127">Prerequisites</span></span>
<span data-ttu-id="1536b-128">Wymagania dotyczące toouse hello rozszerzenie agenta IaaS serwera SQL na maszynie Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="1536b-128">Requirements toouse hello SQL Server IaaS Agent Extension on your VM:</span></span>

### <a name="operating-system"></a><span data-ttu-id="1536b-129">System operacyjny:</span><span class="sxs-lookup"><span data-stu-id="1536b-129">Operating System:</span></span>
* <span data-ttu-id="1536b-130">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="1536b-130">Windows Server 2012</span></span>
* <span data-ttu-id="1536b-131">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="1536b-131">Windows Server 2012 R2</span></span>
* <span data-ttu-id="1536b-132">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="1536b-132">Windows Server 2016</span></span>

### <a name="sql-server-versions"></a><span data-ttu-id="1536b-133">Wersje programu SQL Server:</span><span class="sxs-lookup"><span data-stu-id="1536b-133">SQL Server versions:</span></span>
* <span data-ttu-id="1536b-134">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="1536b-134">SQL Server 2012</span></span>
* <span data-ttu-id="1536b-135">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="1536b-135">SQL Server 2014</span></span>
* <span data-ttu-id="1536b-136">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="1536b-136">SQL Server 2016</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="1536b-137">Program Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="1536b-137">Azure PowerShell:</span></span>
<span data-ttu-id="1536b-138">[Pobierz i skonfiguruj hello najnowszych poleceń programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1536b-138">[Download and configure hello latest Azure PowerShell commands](/powershell/azure/overview).</span></span>

<span data-ttu-id="1536b-139">Uruchom program Windows PowerShell i podłącz go tooyour subskrypcji platformy Azure z hello **Add-AzureAccount** polecenia.</span><span class="sxs-lookup"><span data-stu-id="1536b-139">Start Windows PowerShell, and connect it tooyour Azure subscription with hello **Add-AzureAccount** command.</span></span>

    Add-AzureAccount

<span data-ttu-id="1536b-140">Jeśli masz wiele subskrypcji, użyj **AzureSubscription wybierz** tooselect hello subskrypcji, która zawiera urządzenie docelowe klasyczne maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1536b-140">If you have multiple subscriptions, use **Select-AzureSubscription** tooselect hello subscription that contains your target classic VM.</span></span>

    Select-AzureSubscription -SubscriptionName <subscriptionname>

<span data-ttu-id="1536b-141">W tym momencie można uzyskać listę hello klasycznych maszyn wirtualnych i ich nazwy usługi skojarzone z hello **Get-AzureVM** polecenia.</span><span class="sxs-lookup"><span data-stu-id="1536b-141">At this point, you can get a list of hello classic virtual machines and their associated service names with hello **Get-AzureVM** command.</span></span>

    Get-AzureVM

## <a name="installation"></a><span data-ttu-id="1536b-142">Instalacja</span><span class="sxs-lookup"><span data-stu-id="1536b-142">Installation</span></span>
<span data-ttu-id="1536b-143">Klasycznych maszyn wirtualnych należy użyć programu PowerShell tooinstall hello rozszerzenia agenta programu SQL Server IaaS i skonfigurować skojarzonych z nimi usług.</span><span class="sxs-lookup"><span data-stu-id="1536b-143">For classic VMs, you must use PowerShell tooinstall hello SQL Server IaaS Agent Extension and configure its associated services.</span></span> <span data-ttu-id="1536b-144">Użyj hello **AzureVMSqlServerExtension zestaw** rozszerzenia hello tooinstall polecenia cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1536b-144">Use hello **Set-AzureVMSqlServerExtension** PowerShell cmdlet tooinstall hello extension.</span></span> <span data-ttu-id="1536b-145">Na przykład hello następujące polecenie instaluje hello rozszerzenia na maszynie Wirtualnej serwera systemu Windows (klasyczne) i nadaje "SQLIaaSExtension".</span><span class="sxs-lookup"><span data-stu-id="1536b-145">For example, hello following command installs hello extension on a Windows Server VM (classic) and names it "SQLIaaSExtension".</span></span>

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -ReferenceName "SQLIaasExtension" -Version "1.2" | Update-AzureVM

<span data-ttu-id="1536b-146">Po aktualizacji najnowszej wersji toohello hello rozszerzenia agenta IaaS SQL, należy ponownie uruchomić maszynę wirtualną po zaktualizowaniu hello rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="1536b-146">If you update toohello latest version of hello SQL IaaS Agent Extension, you must restart your virtual machine after updating hello extension.</span></span>

> [!NOTE]
> <span data-ttu-id="1536b-147">Klasycznych maszyn wirtualnych nie ma tooinstall opcji i skonfigurować hello rozszerzenia agenta SQL IaaS za pośrednictwem portalu hello.</span><span class="sxs-lookup"><span data-stu-id="1536b-147">Classic virtual machines do not have an option tooinstall and configure hello SQL IaaS Agent Extension through hello portal.</span></span>
> 
> 

## <a name="status"></a><span data-ttu-id="1536b-148">Stan</span><span class="sxs-lookup"><span data-stu-id="1536b-148">Status</span></span>
<span data-ttu-id="1536b-149">Jednokierunkowej tooverify, że zainstalowano rozszerzenia hello jest stan agenta hello tooview w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="1536b-149">One way tooverify that hello extension is installed is tooview hello agent status in hello Azure Portal.</span></span> <span data-ttu-id="1536b-150">Wybierz maszynę wirtualną na liście hello bloku maszyny wirtualnej, a następnie kliknij polecenie **rozszerzenia**.</span><span class="sxs-lookup"><span data-stu-id="1536b-150">Select a virtual machine listed in hello virtual machine blade, and then click on **Extensions**.</span></span> <span data-ttu-id="1536b-151">Powinny pojawić się hello **SQLIaaSAgent** rozszerzenie na liście.</span><span class="sxs-lookup"><span data-stu-id="1536b-151">You should see hello **SQLIaaSAgent** extension listed.</span></span>

![Rozszerzenie IaaS agenta serwera SQL w portalu Azure](./media/virtual-machines-windows-classic-sql-server-agent-extension/azure-sql-server-iaas-agent-portal.png)

<span data-ttu-id="1536b-153">Można również użyć hello **Get-AzureVMSqlServerExtension** polecenia cmdlet programu Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="1536b-153">You can also use hello **Get-AzureVMSqlServerExtension** Azure Powershell cmdlet.</span></span>

    Get-AzureVM –ServiceName "service" –Name "vmname" | Get-AzureVMSqlServerExtension

## <a name="removal"></a><span data-ttu-id="1536b-154">Usuwanie</span><span class="sxs-lookup"><span data-stu-id="1536b-154">Removal</span></span>
<span data-ttu-id="1536b-155">W portalu Azure hello, można odinstalować rozszerzenia hello przez kliknięcie przycisku wielokropka hello na powitania **rozszerzenia** bloku właściwości maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1536b-155">In hello Azure Portal, you can uninstall hello extension by clicking hello ellipsis on hello **Extensions** blade of your virtual machine properties.</span></span> <span data-ttu-id="1536b-156">Następnie kliknij przycisk **Odinstaluj**.</span><span class="sxs-lookup"><span data-stu-id="1536b-156">Then click **Uninstall**.</span></span>

![Odinstaluj hello rozszerzenia agenta programu SQL Server IaaS w portalu Azure](./media/virtual-machines-windows-classic-sql-server-agent-extension/azure-sql-server-iaas-agent-uninstall.png)

<span data-ttu-id="1536b-158">Można również użyć hello **AzureVMSqlServerExtension Usuń** polecenia cmdlet programu Powershell.</span><span class="sxs-lookup"><span data-stu-id="1536b-158">You can also use hello **Remove-AzureVMSqlServerExtension** Powershell cmdlet.</span></span>

    Get-AzureVM –ServiceName "service" –Name "vmname" | Remove-AzureVMSqlServerExtension | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="1536b-159">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1536b-159">Next Steps</span></span>
<span data-ttu-id="1536b-160">Przy użyciu jednej z usług hello obsługiwany przez rozszerzenie hello BEGIN.</span><span class="sxs-lookup"><span data-stu-id="1536b-160">Begin using one of hello services supported by hello extension.</span></span> <span data-ttu-id="1536b-161">Aby uzyskać więcej informacji, zobacz Tematy hello, występujący w odwołaniu w hello [obsługiwane usługi](#supported-services) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="1536b-161">For more details, see hello topics referenced in hello [Supported services](#supported-services) section of this article.</span></span>

<span data-ttu-id="1536b-162">Aby uzyskać więcej informacji na temat uruchamiania programu SQL Server na maszynach wirtualnych platformy Azure, zobacz [programu SQL Server na maszynach wirtualnych platformy Azure — omówienie](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1536b-162">For more information about running SQL Server on Azure Virtual Machines, see [SQL Server on Azure Virtual Machines overview](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

