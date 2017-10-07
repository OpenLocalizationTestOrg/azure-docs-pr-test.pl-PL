---
title: "zadania zarządzania aaaAutomate na maszynach wirtualnych SQL (Resource Manager) | Dokumentacja firmy Microsoft"
description: "W tym temacie opisano, jak toomanage hello rozszerzenia agenta programu SQL Server, który automatyzuje określonych zadań administracyjnych programu SQL Server. Obejmują one automatyczna usługa Backup, automatyczne stosowanie poprawek i integracji magazynu kluczy Azure. W tym temacie tryb hello Menedżera zasobów wdrożenia."
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: effe4e2f-35b5-490a-b5ef-b06746083da4
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/07/2017
ms.author: jroth
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ae917612c4af59f12c0b083440673bdc555e9d56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="automate-management-tasks-on-azure-virtual-machines-with-hello-sql-server-agent-extension-resource-manager"></a><span data-ttu-id="984a1-105">Automatyzacji zadań zarządzania na maszynach wirtualnych platformy Azure z hello rozszerzenie agenta serwera SQL (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="984a1-105">Automate management tasks on Azure Virtual Machines with hello SQL Server Agent Extension (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="984a1-106">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="984a1-106">Resource Manager</span></span>](virtual-machines-windows-sql-server-agent-extension.md)
> * [<span data-ttu-id="984a1-107">Wdrożenie klasyczne</span><span class="sxs-lookup"><span data-stu-id="984a1-107">Classic</span></span>](../classic/sql-server-agent-extension.md)
> 
> 

<span data-ttu-id="984a1-108">Witaj rozszerzenia agenta IaaS programu SQL Server (SQLIaaSExtension) działa na zadań administracyjnych tooautomate maszyn wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="984a1-108">hello SQL Server IaaS Agent Extension (SQLIaaSExtension) runs on Azure virtual machines tooautomate administration tasks.</span></span> <span data-ttu-id="984a1-109">Ten temat zawiera omówienie usług hello obsługiwany przez rozszerzenie hello, jak również instrukcje dotyczące instalacji, stanu i usuwania.</span><span class="sxs-lookup"><span data-stu-id="984a1-109">This topic provides an overview of hello services supported by hello extension as well as instructions for installation, status, and removal.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="984a1-110">Zobacz tooview hello klasycznej wersji w tym artykule [rozszerzenie agenta serwera SQL dla programu SQL Server VMs klasycznego](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="984a1-110">tooview hello classic version of this article, see [SQL Server Agent Extension for SQL Server VMs Classic](../classic/sql-server-agent-extension.md).</span></span>

## <a name="supported-services"></a><span data-ttu-id="984a1-111">Obsługiwane usługi</span><span class="sxs-lookup"><span data-stu-id="984a1-111">Supported services</span></span>
<span data-ttu-id="984a1-112">Witaj rozszerzenia agenta programu SQL Server IaaS obsługuje hello następujące zadania administracyjne:</span><span class="sxs-lookup"><span data-stu-id="984a1-112">hello SQL Server IaaS Agent Extension supports hello following administration tasks:</span></span>

| <span data-ttu-id="984a1-113">Funkcja administracji</span><span class="sxs-lookup"><span data-stu-id="984a1-113">Administration feature</span></span> | <span data-ttu-id="984a1-114">Opis</span><span class="sxs-lookup"><span data-stu-id="984a1-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="984a1-115">**Automatyczna usługa Backup SQL**</span><span class="sxs-lookup"><span data-stu-id="984a1-115">**SQL Automated Backup**</span></span> |<span data-ttu-id="984a1-116">Automatyzuje hello Planowanie tworzenia kopii zapasowych dla wszystkich baz danych dla hello domyślnego wystąpienia programu SQL Server w hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="984a1-116">Automates hello scheduling of backups for all databases for hello default instance of SQL Server in hello VM.</span></span> <span data-ttu-id="984a1-117">Aby uzyskać więcej informacji, zobacz [automatycznego tworzenia kopii zapasowej dla programu SQL Server w maszynach wirtualnych platformy Azure (Resource Manager)](virtual-machines-windows-sql-automated-backup.md).</span><span class="sxs-lookup"><span data-stu-id="984a1-117">For more information, see [Automated backup for SQL Server in Azure Virtual Machines (Resource Manager)](virtual-machines-windows-sql-automated-backup.md).</span></span> |
| <span data-ttu-id="984a1-118">**Automatyczne stosowanie poprawek SQL**</span><span class="sxs-lookup"><span data-stu-id="984a1-118">**SQL Automated Patching**</span></span> |<span data-ttu-id="984a1-119">Konfiguruje podczas aktualizacji, które tooyour, maszyna wirtualna może potrwać umieszczone, okna obsługi, aby uniknąć aktualizacje w godzinach szczytu dla obciążenia.</span><span class="sxs-lookup"><span data-stu-id="984a1-119">Configures a maintenance window during which updates tooyour VM can take place, so  you can avoid updates during peak times for your workload.</span></span> <span data-ttu-id="984a1-120">Aby uzyskać więcej informacji, zobacz [automatyczne stosowanie poprawek dla programu SQL Server w maszynach wirtualnych platformy Azure (Resource Manager)](virtual-machines-windows-sql-automated-patching.md).</span><span class="sxs-lookup"><span data-stu-id="984a1-120">For more information, see [Automated patching for SQL Server in Azure Virtual Machines (Resource Manager)](virtual-machines-windows-sql-automated-patching.md).</span></span> |
| <span data-ttu-id="984a1-121">**Integracja z usługą Azure Key Vault**</span><span class="sxs-lookup"><span data-stu-id="984a1-121">**Azure Key Vault Integration**</span></span> |<span data-ttu-id="984a1-122">Umożliwia tooautomatically należy zainstalować i skonfigurować usługi Azure Key Vault na maszyną Wirtualną programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="984a1-122">Enables you tooautomatically install and configure Azure Key Vault on your SQL Server VM.</span></span> <span data-ttu-id="984a1-123">Aby uzyskać więcej informacji, zobacz [Konfigurowanie integracji magazynu kluczy Azure dla programu SQL Server na maszynach wirtualnych Azure (Resource Manager)](virtual-machines-windows-ps-sql-keyvault.md).</span><span class="sxs-lookup"><span data-stu-id="984a1-123">For more information, see [Configure Azure Key Vault Integration for SQL Server on Azure VMs (Resource Manager)](virtual-machines-windows-ps-sql-keyvault.md).</span></span> |

<span data-ttu-id="984a1-124">Po zainstalowaniu i uruchomione, hello rozszerzenia agenta programu SQL Server IaaS udostępnia te funkcje administracyjne w panelu programu SQL Server hello hello maszyny wirtualnej w portalu Azure hello i za pomocą programu Azure PowerShell dla obrazów w witrynie marketplace programu SQL Server i za pośrednictwem W przypadku ręcznej instalacji rozszerzenia hello programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="984a1-124">Once installed and running, hello SQL Server IaaS Agent Extension makes these administration features available on hello SQL Server panel of hello virtual machine in hello Azure Portal and through Azure PowerShell for SQL Server marketplace images, and through Azure PowerShell for manual installations of hello extension.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="984a1-125">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="984a1-125">Prerequisites</span></span>
<span data-ttu-id="984a1-126">Wymagania dotyczące toouse hello rozszerzenie agenta IaaS serwera SQL na maszynie Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="984a1-126">Requirements toouse hello SQL Server IaaS Agent Extension on your VM:</span></span>

<span data-ttu-id="984a1-127">**System operacyjny**:</span><span class="sxs-lookup"><span data-stu-id="984a1-127">**Operating System**:</span></span>

* <span data-ttu-id="984a1-128">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="984a1-128">Windows Server 2012</span></span>
* <span data-ttu-id="984a1-129">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="984a1-129">Windows Server 2012 R2</span></span>
* <span data-ttu-id="984a1-130">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="984a1-130">Windows Server 2016</span></span>

<span data-ttu-id="984a1-131">**Wersje programu SQL Server**:</span><span class="sxs-lookup"><span data-stu-id="984a1-131">**SQL Server versions**:</span></span>

* <span data-ttu-id="984a1-132">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="984a1-132">SQL Server 2012</span></span>
* <span data-ttu-id="984a1-133">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="984a1-133">SQL Server 2014</span></span>
* <span data-ttu-id="984a1-134">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="984a1-134">SQL Server 2016</span></span>

<span data-ttu-id="984a1-135">**Program Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="984a1-135">**Azure PowerShell**:</span></span>

* [<span data-ttu-id="984a1-136">Pobierz i skonfiguruj hello najnowszych poleceń programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="984a1-136">Download and configure hello latest Azure PowerShell commands</span></span>](/powershell/azure/overview)

## <a name="installation"></a><span data-ttu-id="984a1-137">Instalacja</span><span class="sxs-lookup"><span data-stu-id="984a1-137">Installation</span></span>
<span data-ttu-id="984a1-138">Rozszerzenie agenta programu SQL Server IaaS Hello jest automatycznie instalowany podczas udostępniania jednego z obrazów Galeria maszyny wirtualnej programu SQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="984a1-138">hello SQL Server IaaS Agent Extension is automatically installed when you provision one of hello SQL Server virtual machine gallery images.</span></span> <span data-ttu-id="984a1-139">Rozszerzenie hello tooreinstall ręcznie na jednym z tych maszyn wirtualnych serwera SQL, należy użyć hello następującego polecenia programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="984a1-139">If you need tooreinstall hello extension manually on one of these SQL Server VMs, use hello following PowerShell command:</span></span>

```powershell
Set-AzureRmVMSqlServerExtension -ResourceGroupName "resourcegroupname" -VMName "vmname" -Name "SQLIaasExtension" -Version "1.2" -Location "East US 2"
```

<span data-ttu-id="984a1-140">Możliwe jest również możliwe tooinstall hello rozszerzenie agenta IaaS serwera SQL na maszynie wirtualnej tylko do systemu operacyjnego Windows Server.</span><span class="sxs-lookup"><span data-stu-id="984a1-140">It is also possible tooinstall hello SQL Server IaaS Agent Extension on an OS-only Windows Server virtual machine.</span></span> <span data-ttu-id="984a1-141">To ustawienie jest obsługiwane tylko, jeśli ręcznie zainstalowano program SQL Server na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="984a1-141">This is only supported if you have also manually installed SQL Server on that machine.</span></span> <span data-ttu-id="984a1-142">Następnie zainstaluj rozszerzenie hello ręcznie przy użyciu hello sam **AzureVMSqlServerExtension zestaw** polecenia cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="984a1-142">Then install hello extension manually by using hello same **Set-AzureVMSqlServerExtension** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="984a1-143">Jeśli hello rozszerzenia agenta programu SQL Server IaaS można ręcznie zainstalować na maszynie Wirtualnej tylko do systemu operacyjnego Windows Server, nie można zarządzać hello ustawień konfiguracji programu SQL Server za pośrednictwem hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="984a1-143">If you manually install hello SQL Server IaaS Agent Extension on an OS-only Windows Server VM, you can not manage hello SQL Server configuration settings through hello Azure portal.</span></span> <span data-ttu-id="984a1-144">W tym scenariuszu należy wszystkie zmiany przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="984a1-144">In this scenario, you must make all changes with PowerShell.</span></span>

## <a name="status"></a><span data-ttu-id="984a1-145">Stan</span><span class="sxs-lookup"><span data-stu-id="984a1-145">Status</span></span>
<span data-ttu-id="984a1-146">Jednokierunkowej tooverify, że zainstalowano rozszerzenia hello jest stan agenta hello tooview w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="984a1-146">One way tooverify that hello extension is installed is tooview hello agent status in hello Azure Portal.</span></span> <span data-ttu-id="984a1-147">Wybierz **wszystkie ustawienia** w hello bloku maszyny wirtualnej, a następnie kliknij polecenie **rozszerzenia**.</span><span class="sxs-lookup"><span data-stu-id="984a1-147">Select **All settings** in hello virtual machine blade, and then click on **Extensions**.</span></span> <span data-ttu-id="984a1-148">Powinny pojawić się hello **SQLIaaSExtension** rozszerzenie na liście.</span><span class="sxs-lookup"><span data-stu-id="984a1-148">You should see hello **SQLIaaSExtension** extension listed.</span></span>

![Rozszerzenie IaaS agenta serwera SQL w portalu Azure](./media/virtual-machines-windows-sql-server-agent-extension/azure-rm-sql-server-iaas-agent-portal.png)

<span data-ttu-id="984a1-150">Można również użyć hello **Get-AzureVMSqlServerExtension** polecenia cmdlet programu Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="984a1-150">You can also use hello **Get-AzureVMSqlServerExtension** Azure Powershell cmdlet.</span></span>

    Get-AzureRmVMSqlServerExtension -VMName "vmname" -ResourceGroupName "resourcegroupname"

<span data-ttu-id="984a1-151">poprzednie polecenie Hello potwierdza hello agent jest zainstalowany i zawiera ogólne informacje.</span><span class="sxs-lookup"><span data-stu-id="984a1-151">hello previous command confirms hello agent is installed and provides general status information.</span></span> <span data-ttu-id="984a1-152">Można także uzyskać informacje dotyczące automatycznego tworzenia kopii zapasowej i Patching określonego stanu z hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="984a1-152">You can also get specific status information about Automated Backup and Patching with hello following commands.</span></span>

    $sqlext = Get-AzureRmVMSqlServerExtension -VMName "vmname" -ResourceGroupName "resourcegroupname"
    $sqlext.AutoPatchingSettings
    $sqlext.AutoBackupSettings

## <a name="removal"></a><span data-ttu-id="984a1-153">Usuwanie</span><span class="sxs-lookup"><span data-stu-id="984a1-153">Removal</span></span>
<span data-ttu-id="984a1-154">W portalu Azure hello, można odinstalować rozszerzenia hello przez kliknięcie przycisku wielokropka hello na powitania **rozszerzenia** bloku właściwości maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="984a1-154">In hello Azure Portal, you can uninstall hello extension by clicking hello ellipsis on hello **Extensions** blade of your virtual machine properties.</span></span> <span data-ttu-id="984a1-155">Następnie kliknij przycisk **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="984a1-155">Then click **Delete**.</span></span>

![Odinstaluj hello rozszerzenia agenta programu SQL Server IaaS w portalu Azure](./media/virtual-machines-windows-sql-server-agent-extension/azure-rm-sql-server-iaas-agent-uninstall.png)

<span data-ttu-id="984a1-157">Można również użyć hello **AzureRmVMSqlServerExtension Usuń** polecenia cmdlet programu Powershell.</span><span class="sxs-lookup"><span data-stu-id="984a1-157">You can also use hello **Remove-AzureRmVMSqlServerExtension** Powershell cmdlet.</span></span>

    Remove-AzureRmVMSqlServerExtension -ResourceGroupName "resourcegroupname" -VMName "vmname" -Name "SQLIaasExtension"

## <a name="next-steps"></a><span data-ttu-id="984a1-158">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="984a1-158">Next Steps</span></span>
<span data-ttu-id="984a1-159">Przy użyciu jednej z usług hello obsługiwany przez rozszerzenie hello BEGIN.</span><span class="sxs-lookup"><span data-stu-id="984a1-159">Begin using one of hello services supported by hello extension.</span></span> <span data-ttu-id="984a1-160">Aby uzyskać więcej informacji, zobacz Tematy hello, występujący w odwołaniu w hello [obsługiwane usługi](#supported-services) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="984a1-160">For more details, see hello topics referenced in hello [Supported services](#supported-services) section of this article.</span></span>

<span data-ttu-id="984a1-161">Aby uzyskać więcej informacji na temat uruchamiania programu SQL Server na maszynach wirtualnych platformy Azure, zobacz [programu SQL Server na maszynach wirtualnych platformy Azure — omówienie](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="984a1-161">For more information about running SQL Server on Azure Virtual Machines, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

