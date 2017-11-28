---
title: "Automatyczna usługa Backup SQL Server 2014 maszyn wirtualnych platformy Azure | Dokumentacja firmy Microsoft"
description: "Zawiera opis funkcji automatycznego tworzenia kopii zapasowej dla programu SQL Server 2014 maszyn wirtualnych działających na platformie Azure. Ten artykuł dotyczy maszyn wirtualnych za pomocą Menedżera zasobów."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: bdc63fd1-db49-4e76-87d5-b5c6a890e53c
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: 91aab896dd5f06c950ee0ed8f36cc6a953d91611
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="automated-backup-for-sql-server-2014-virtual-machines-resource-manager"></a><span data-ttu-id="b1344-104">Automatyczne kopie zapasowe maszyn wirtualnych programu SQL Server 2014 (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="b1344-104">Automated Backup for SQL Server 2014 Virtual Machines (Resource Manager)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b1344-105">Program SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="b1344-105">SQL Server 2014</span></span>](virtual-machines-windows-sql-automated-backup.md)
> * [<span data-ttu-id="b1344-106">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="b1344-106">SQL Server 2016</span></span>](virtual-machines-windows-sql-automated-backup-v2.md)

<span data-ttu-id="b1344-107">Automatyczne kopie zapasowe automatycznie konfiguruje [zarządzanej kopii zapasowej Microsoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) dla wszystkich istniejących i nowych baz danych na maszynie Wirtualnej platformy Azure, programem SQL Server 2014 Standard lub Enterprise.</span><span class="sxs-lookup"><span data-stu-id="b1344-107">Automated Backup automatically configures [Managed Backup to Microsoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) for all existing and new databases on an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> <span data-ttu-id="b1344-108">Dzięki temu można skonfigurować kopie zapasowe zwykłej bazy danych, które korzystać z magazynu trwałego obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b1344-108">This enables you to configure regular database backups that utilize durable Azure blob storage.</span></span> <span data-ttu-id="b1344-109">Automatyczne kopie zapasowe jest zależna od [rozszerzenia agenta programu SQL Server IaaS](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="b1344-109">Automated Backup depends on the [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="b1344-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b1344-110">Prerequisites</span></span>
<span data-ttu-id="b1344-111">Aby korzystać z automatycznego tworzenia kopii zapasowej, należy wziąć pod uwagę następujące wymagania wstępne:</span><span class="sxs-lookup"><span data-stu-id="b1344-111">To use Automated Backup, consider the following prerequisites:</span></span>

<span data-ttu-id="b1344-112">**System operacyjny**:</span><span class="sxs-lookup"><span data-stu-id="b1344-112">**Operating System**:</span></span>

- <span data-ttu-id="b1344-113">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="b1344-113">Windows Server 2012</span></span>
- <span data-ttu-id="b1344-114">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="b1344-114">Windows Server 2012 R2</span></span>
- <span data-ttu-id="b1344-115">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="b1344-115">Windows Server 2016</span></span>

<span data-ttu-id="b1344-116">**Wydanie wersji programu SQL Server**:</span><span class="sxs-lookup"><span data-stu-id="b1344-116">**SQL Server version/edition**:</span></span>

- <span data-ttu-id="b1344-117">SQL Server 2014 Standard</span><span class="sxs-lookup"><span data-stu-id="b1344-117">SQL Server 2014 Standard</span></span>
- <span data-ttu-id="b1344-118">SQL Server 2014 Enterprise</span><span class="sxs-lookup"><span data-stu-id="b1344-118">SQL Server 2014 Enterprise</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b1344-119">Automatyczne działa kopii zapasowej z programu SQL Server 2014.</span><span class="sxs-lookup"><span data-stu-id="b1344-119">Automated Backup works with SQL Server 2014.</span></span> <span data-ttu-id="b1344-120">Jeśli używasz programu SQL Server 2016 służy v2 automatycznego tworzenia kopii zapasowej do tworzenia kopii zapasowych baz danych.</span><span class="sxs-lookup"><span data-stu-id="b1344-120">If you are using SQL Server 2016, you can use Automated Backup v2 to back up your databases.</span></span> <span data-ttu-id="b1344-121">Aby uzyskać więcej informacji, zobacz [v2 automatyczna usługa Backup SQL Server 2016 maszyn wirtualnych platformy Azure](virtual-machines-windows-sql-automated-backup-v2.md).</span><span class="sxs-lookup"><span data-stu-id="b1344-121">For more information, see [Automated Backup v2 for SQL Server 2016 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup-v2.md).</span></span>

<span data-ttu-id="b1344-122">**Baza danych konfiguracji**:</span><span class="sxs-lookup"><span data-stu-id="b1344-122">**Database configuration**:</span></span>

- <span data-ttu-id="b1344-123">Docelowej bazy danych muszą używać modelu odzyskiwania pełnego.</span><span class="sxs-lookup"><span data-stu-id="b1344-123">Target databases must use the full recovery model.</span></span> <span data-ttu-id="b1344-124">Aby uzyskać więcej informacji dotyczących wpływu modelu odzyskiwania pełnego na wykonywanie kopii zapasowych, zobacz [kopii zapasowej w obszarze pełny Model odzyskiwania](https://technet.microsoft.com/library/ms190217.aspx).</span><span class="sxs-lookup"><span data-stu-id="b1344-124">For more information about the impact of the full recovery model on backups, see [Backup Under the Full Recovery Model](https://technet.microsoft.com/library/ms190217.aspx).</span></span>
- <span data-ttu-id="b1344-125">Docelowymi bazami danych musi być w domyślnym wystąpieniu programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b1344-125">Target databases must be on the default SQL Server instance.</span></span> <span data-ttu-id="b1344-126">Rozszerzenie IaaS serwera SQL obsługuje tylko nazwane wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="b1344-126">The SQL Server IaaS Extension does not support named instances.</span></span>

<span data-ttu-id="b1344-127">**Model wdrożenia usługi Azure**:</span><span class="sxs-lookup"><span data-stu-id="b1344-127">**Azure deployment model**:</span></span>

- <span data-ttu-id="b1344-128">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b1344-128">Resource Manager</span></span>

<span data-ttu-id="b1344-129">**Program Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="b1344-129">**Azure PowerShell**:</span></span>

- <span data-ttu-id="b1344-130">[Zainstaluj najnowsze poleceń programu PowerShell Azure](/powershell/azure/overview) Jeśli planujesz Konfigurowanie automatycznego tworzenia kopii zapasowej przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b1344-130">[Install the latest Azure PowerShell commands](/powershell/azure/overview) if you plan to configure Automated Backup with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="b1344-131">Automatyczne kopie zapasowe wykorzystuje rozszerzenie agenta programu SQL Server IaaS.</span><span class="sxs-lookup"><span data-stu-id="b1344-131">Automated Backup relies on the SQL Server IaaS Agent Extension.</span></span> <span data-ttu-id="b1344-132">Bieżący obrazów Galeria maszyny wirtualnej SQL dodać to rozszerzenie domyślnie.</span><span class="sxs-lookup"><span data-stu-id="b1344-132">Current SQL virtual machine gallery images add this extension by default.</span></span> <span data-ttu-id="b1344-133">Aby uzyskać więcej informacji, zobacz [rozszerzenia agenta programu SQL Server IaaS](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="b1344-133">For more information, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="b1344-134">Ustawienia</span><span class="sxs-lookup"><span data-stu-id="b1344-134">Settings</span></span>

<span data-ttu-id="b1344-135">W poniższej tabeli opisano opcje, które można skonfigurować do automatycznego tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="b1344-135">The following table describes the options that can be configured for Automated Backup.</span></span> <span data-ttu-id="b1344-136">Kroki konfiguracji rzeczywisty zależy od przy użyciu portalu Azure lub poleceń programu PowerShell systemu Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="b1344-136">The actual configuration steps vary depending on whether you use the Azure portal or Azure Windows PowerShell commands.</span></span>

| <span data-ttu-id="b1344-137">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="b1344-137">Setting</span></span> | <span data-ttu-id="b1344-138">Zakres (ustawienie domyślne)</span><span class="sxs-lookup"><span data-stu-id="b1344-138">Range (Default)</span></span> | <span data-ttu-id="b1344-139">Opis</span><span class="sxs-lookup"><span data-stu-id="b1344-139">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b1344-140">**Automatyczne kopie zapasowe**</span><span class="sxs-lookup"><span data-stu-id="b1344-140">**Automated Backup**</span></span> | <span data-ttu-id="b1344-141">Włącza/wyłącza (wyłączone)</span><span class="sxs-lookup"><span data-stu-id="b1344-141">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="b1344-142">Włącza lub wyłącza funkcję automatycznego tworzenia kopii zapasowej dla maszyny Wirtualnej platformy Azure, programem SQL Server 2014 Standard lub Enterprise.</span><span class="sxs-lookup"><span data-stu-id="b1344-142">Enables or disables Automated Backup for an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> |
| <span data-ttu-id="b1344-143">**Okres przechowywania**</span><span class="sxs-lookup"><span data-stu-id="b1344-143">**Retention Period**</span></span> | <span data-ttu-id="b1344-144">1 do 30 dni (30 dni)</span><span class="sxs-lookup"><span data-stu-id="b1344-144">1-30 days (30 days)</span></span> | <span data-ttu-id="b1344-145">Liczba dni przechowywania kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="b1344-145">The number of days to retain a backup.</span></span> |
| <span data-ttu-id="b1344-146">**Konto magazynu**</span><span class="sxs-lookup"><span data-stu-id="b1344-146">**Storage Account**</span></span> | <span data-ttu-id="b1344-147">Konto magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="b1344-147">Azure storage account</span></span> | <span data-ttu-id="b1344-148">Konto magazynu Azure do przechowywania plików automatycznego tworzenia kopii zapasowej w magazynie obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="b1344-148">An Azure storage account to use for storing Automated Backup files in blob storage.</span></span> <span data-ttu-id="b1344-149">Kontener jest tworzony w tej lokalizacji, aby zapisać wszystkie pliki kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="b1344-149">A container is created at this location to store all backup files.</span></span> <span data-ttu-id="b1344-150">Konwencja nazewnictwa pliku kopii zapasowej obejmuje daty, godziny i nazwy komputera.</span><span class="sxs-lookup"><span data-stu-id="b1344-150">The backup file naming convention includes the date, time, and machine name.</span></span> |
| <span data-ttu-id="b1344-151">**Szyfrowanie**</span><span class="sxs-lookup"><span data-stu-id="b1344-151">**Encryption**</span></span> | <span data-ttu-id="b1344-152">Włącza/wyłącza (wyłączone)</span><span class="sxs-lookup"><span data-stu-id="b1344-152">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="b1344-153">Włącza lub wyłącza funkcję szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="b1344-153">Enables or disables encryption.</span></span> <span data-ttu-id="b1344-154">Po włączeniu szyfrowania certyfikatów służących do przywrócenia kopii zapasowej znajdują się na koncie magazynu określonym w tym samym `automaticbackup` kontenera przy użyciu tej samej konwencji nazewnictwa.</span><span class="sxs-lookup"><span data-stu-id="b1344-154">When encryption is enabled, the certificates used to restore the backup are located in the specified storage account in the same `automaticbackup` container using the same naming convention.</span></span> <span data-ttu-id="b1344-155">Zmiana hasła nowego certyfikatu jest generowana za pomocą tego hasła, ale pozostaje stary certyfikat do przywrócenia poprzedniego kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="b1344-155">If the password changes, a new certificate is generated with that password, but the old certificate remains to restore prior backups.</span></span> |
| <span data-ttu-id="b1344-156">**Hasło**</span><span class="sxs-lookup"><span data-stu-id="b1344-156">**Password**</span></span> | <span data-ttu-id="b1344-157">Tekst hasła</span><span class="sxs-lookup"><span data-stu-id="b1344-157">Password text</span></span> | <span data-ttu-id="b1344-158">Hasło dla kluczy szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="b1344-158">A password for encryption keys.</span></span> <span data-ttu-id="b1344-159">Jest to tylko wymagane, jeśli jest włączone szyfrowanie.</span><span class="sxs-lookup"><span data-stu-id="b1344-159">This is only required if encryption is enabled.</span></span> <span data-ttu-id="b1344-160">Aby przywrócić zaszyfrowanej kopii zapasowej, musi mieć prawidłowe hasło, a powiązany certyfikat, który został użyty w momencie utworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="b1344-160">In order to restore an encrypted backup, you must have the correct password and related certificate that was used at the time the backup was taken.</span></span> |

## <a name="configuration-in-the-portal"></a><span data-ttu-id="b1344-161">Konfiguracja w portalu</span><span class="sxs-lookup"><span data-stu-id="b1344-161">Configuration in the Portal</span></span>

<span data-ttu-id="b1344-162">Azure portal umożliwia konfigurowanie automatycznego tworzenia kopii zapasowej, podczas udostępniania lub dla maszyn wirtualnych istniejącego programu SQL Server 2014.</span><span class="sxs-lookup"><span data-stu-id="b1344-162">You can use the Azure portal to configure Automated Backup during provisioning or for existing SQL Server 2014 VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="b1344-163">Nowe maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="b1344-163">New VMs</span></span>

<span data-ttu-id="b1344-164">Skonfiguruj automatyczne kopie zapasowe, podczas tworzenia nowej maszyny wirtualnej 2014 serwera SQL w modelu wdrażania usługi Resource Manager za pomocą portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="b1344-164">Use the Azure portal to configure Automated Backup when you create a new SQL Server 2014 Virtual Machine in the Resource Manager deployment model.</span></span>

<span data-ttu-id="b1344-165">W **ustawienia programu SQL Server** bloku, wybierz opcję **automatyczne kopie zapasowe**.</span><span class="sxs-lookup"><span data-stu-id="b1344-165">In the **SQL Server settings** blade, select **Automated backup**.</span></span> <span data-ttu-id="b1344-166">Poniżej przedstawiono zrzut ekranu na portalu Azure **SQL automatyczna usługa Backup** bloku.</span><span class="sxs-lookup"><span data-stu-id="b1344-166">The following Azure portal screenshot shows the **SQL Automated Backup** blade.</span></span>

![Konfiguracja SQL automatyczna usługa Backup w portalu Azure](./media/virtual-machines-windows-sql-automated-backup/azure-sql-arm-autobackup.png)

<span data-ttu-id="b1344-168">Dla kontekstu, zobacz temat pełną na [obsługi maszyny wirtualnej programu SQL Server na platformie Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="b1344-168">For context, see the complete topic on [provisioning a SQL Server virtual machine in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="b1344-169">Istniejące maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="b1344-169">Existing VMs</span></span>

<span data-ttu-id="b1344-170">W przypadku istniejących maszyn wirtualnych programu SQL Server należy wybrać maszyny wirtualnej programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b1344-170">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="b1344-171">Następnie wybierz **konfigurację programu SQL Server** sekcji **ustawienia** bloku.</span><span class="sxs-lookup"><span data-stu-id="b1344-171">Then select the **SQL Server configuration** section of the **Settings** blade.</span></span>

![SQL automatyczna usługa Backup dla istniejących maszyn wirtualnych](./media/virtual-machines-windows-sql-automated-backup/azure-sql-rm-autobackup-existing-vms.png)

<span data-ttu-id="b1344-173">W **konfigurację programu SQL Server** bloku, kliknij przycisk **Edytuj** przycisk w sekcji automatycznego tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="b1344-173">In the **SQL Server configuration** blade, click the **Edit** button in the Automated backup section.</span></span>

![Konfigurowanie kopii zapasowej SQL automatycznego dla istniejących maszyn wirtualnych](./media/virtual-machines-windows-sql-automated-backup/azure-sql-rm-autobackup-configuration.png)

<span data-ttu-id="b1344-175">Gdy skończysz, kliknij przycisk **OK** przycisk w dolnej części **konfigurację programu SQL Server** bloku, aby zapisać zmiany.</span><span class="sxs-lookup"><span data-stu-id="b1344-175">When finished, click the **OK** button on the bottom of the **SQL Server configuration** blade to save your changes.</span></span>

<span data-ttu-id="b1344-176">Jeśli po raz pierwszy włączasz automatyczna usługa Backup, Azure konfiguruje agenta programu SQL Server IaaS w tle.</span><span class="sxs-lookup"><span data-stu-id="b1344-176">If you are enabling Automated Backup for the first time, Azure configures the SQL Server IaaS Agent in the background.</span></span> <span data-ttu-id="b1344-177">W tym czasie portalu Azure może nie informować, że skonfigurowano automatycznego tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="b1344-177">During this time, the Azure portal might not show that Automated Backup is configured.</span></span> <span data-ttu-id="b1344-178">Poczekaj kilka minut dla agenta, który ma zostać zainstalowany, skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="b1344-178">Wait several minutes for the agent to be installed, configured.</span></span> <span data-ttu-id="b1344-179">Po utworzeniu tego portalu Azure będzie odzwierciedlać nowe ustawienia.</span><span class="sxs-lookup"><span data-stu-id="b1344-179">After that the Azure portal will reflect the new settings.</span></span>

> [!NOTE]
> <span data-ttu-id="b1344-180">Istnieje również możliwość skonfigurowania automatycznego tworzenia kopii zapasowej przy użyciu szablonu.</span><span class="sxs-lookup"><span data-stu-id="b1344-180">You can also configure Automated Backup using a template.</span></span> <span data-ttu-id="b1344-181">Aby uzyskać więcej informacji, zobacz [szablonu Azure szybkiego startu dla automatyczna usługa Backup](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autobackup-update).</span><span class="sxs-lookup"><span data-stu-id="b1344-181">For more information, see [Azure quickstart template for Automated Backup](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autobackup-update).</span></span>

## <a name="configuration-with-powershell"></a><span data-ttu-id="b1344-182">Konfiguracja przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="b1344-182">Configuration with PowerShell</span></span>

<span data-ttu-id="b1344-183">Można skonfigurować automatyczne tworzenie kopii zapasowych za pomocą programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b1344-183">You can use PowerShell to configure Automated Backup.</span></span> <span data-ttu-id="b1344-184">Przed rozpoczęciem należy:</span><span class="sxs-lookup"><span data-stu-id="b1344-184">Before you begin, you must:</span></span>

- <span data-ttu-id="b1344-185">[Pobierz i zainstaluj najnowsze programu Azure PowerShell](http://aka.ms/webpi-azps).</span><span class="sxs-lookup"><span data-stu-id="b1344-185">[Download and install the latest Azure PowerShell](http://aka.ms/webpi-azps).</span></span>
- <span data-ttu-id="b1344-186">Otwórz program Windows PowerShell i skojarzyć go z Twoim kontem.</span><span class="sxs-lookup"><span data-stu-id="b1344-186">Open Windows PowerShell and associate it with your account.</span></span> <span data-ttu-id="b1344-187">Można to zrobić, wykonując kroki opisane w [skonfiguruj subskrypcję](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) tematu inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="b1344-187">You can do this by following the steps in the [Configure your subscription](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) section of the provisioning topic.</span></span>

### <a name="install-the-sql-iaas-extension"></a><span data-ttu-id="b1344-188">Zainstaluj rozszerzenie IaaS SQL</span><span class="sxs-lookup"><span data-stu-id="b1344-188">Install the SQL IaaS Extension</span></span>
<span data-ttu-id="b1344-189">Jeśli aprowizowanej maszyny wirtualnej programu SQL Server w portalu Azure, rozszerzenie IaaS serwera SQL powinno być już zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="b1344-189">If you provisioned a SQL Server virtual machine from the Azure portal, the SQL Server IaaS Extension should already be installed.</span></span> <span data-ttu-id="b1344-190">Można określić, czy jest ona instalowana dla maszyny Wirtualnej przez wywołanie metody **Get-AzureRmVM** polecenia i sprawdzeniu **rozszerzenia** właściwości.</span><span class="sxs-lookup"><span data-stu-id="b1344-190">You can determine if it is installed for your VM by calling **Get-AzureRmVM** command and examining the **Extensions** property.</span></span>

```powershell
$vmname = "vmname"
$resourcegroupname = "resourcegroupname"

(Get-AzureRmVM -Name $vmname -ResourceGroupName $resourcegroupname).Extensions
```

<span data-ttu-id="b1344-191">Jeśli zainstalowano rozszerzenia SQL Server IaaS Agent, powinien pojawić się wymienionym "SqlIaaSAgent" lub "SQLIaaSExtension".</span><span class="sxs-lookup"><span data-stu-id="b1344-191">If the SQL Server IaaS Agent extension is installed, you should see it listed as “SqlIaaSAgent” or “SQLIaaSExtension”.</span></span> <span data-ttu-id="b1344-192">**ProvisioningState** dla rozszerzenia należy również wyświetlić "Powodzenie".</span><span class="sxs-lookup"><span data-stu-id="b1344-192">**ProvisioningState** for the extension should also show “Succeeded”.</span></span>

<span data-ttu-id="b1344-193">Jeśli nie jest zainstalowane lub nie można zainicjować obsługi administracyjnej, należy zainstalować go za pomocą następującego polecenia.</span><span class="sxs-lookup"><span data-stu-id="b1344-193">If it is not installed or failed to be provisioned, you can install it with the following command.</span></span> <span data-ttu-id="b1344-194">Oprócz grupy nazwy i zasobów maszyny Wirtualnej, należy także określić region (**$region**) maszyny Wirtualnej znajdujący się w.</span><span class="sxs-lookup"><span data-stu-id="b1344-194">In addition to the VM name and resource group, you must also specify the region (**$region**) that your VM is located in.</span></span>

```powershell
$region = “EASTUS2”
Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region
```

### <span data-ttu-id="b1344-195"><a id="verifysettings"></a>Sprawdź bieżące ustawienia</span><span class="sxs-lookup"><span data-stu-id="b1344-195"><a id="verifysettings"></a> Verify current settings</span></span>

<span data-ttu-id="b1344-196">Jeśli włączono automatyczne kopie zapasowe podczas inicjowania obsługi, można sprawdzić bieżącej konfiguracji za pomocą programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b1344-196">If you enabled automated backup during provisioning, you can use PowerShell to check your current configuration.</span></span> <span data-ttu-id="b1344-197">Uruchom **Get-AzureRmVMSqlServerExtension** polecenia i sprawdź, czy **AutoBackupSettings** właściwości:</span><span class="sxs-lookup"><span data-stu-id="b1344-197">Run the **Get-AzureRmVMSqlServerExtension** command and examine the **AutoBackupSettings** property:</span></span>

```powershell
(Get-AzureRmVMSqlServerExtension -VMName $vmname -ResourceGroupName $resourcegroupname).AutoBackupSettings
```

<span data-ttu-id="b1344-198">Należy pobrać dane wyjściowe podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="b1344-198">You should get output similar to the following:</span></span>

```
Enable                      : False
EnableEncryption            : False
RetentionPeriod             : -1
StorageUrl                  : NOTSET
StorageAccessKey            : 
Password                    : 
BackupSystemDbs             : False
BackupScheduleType          : 
FullBackupFrequency         : 
FullBackupStartTime         : 
FullBackupWindowHours       : 
LogBackupFrequency          : 
```

<span data-ttu-id="b1344-199">Jeśli dane wyjściowe wskazuje, że **włączyć** ma ustawioną wartość **False**, a następnie należy włączyć automatyczne kopie zapasowe.</span><span class="sxs-lookup"><span data-stu-id="b1344-199">If your output shows that **Enable** is set to **False**, then you have to enable automated backup.</span></span> <span data-ttu-id="b1344-200">Dobre wieści jest włączone, a następnie skonfiguruj automatyczne kopie zapasowe w taki sam sposób.</span><span class="sxs-lookup"><span data-stu-id="b1344-200">The good news is that you enable and configure Automated Backup in the same way.</span></span> <span data-ttu-id="b1344-201">W następnej sekcji dla tych informacji.</span><span class="sxs-lookup"><span data-stu-id="b1344-201">See the next section for this information.</span></span>

> [!NOTE] 
> <span data-ttu-id="b1344-202">Jeśli wybierzesz ustawienia natychmiast po wprowadzeniu zmian jest możliwe, że wystąpi ponownie starych wartości konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="b1344-202">If you check the settings immediately after making a change, it is possible that you will get back the old configuration values.</span></span> <span data-ttu-id="b1344-203">Poczekaj kilka minut, a następnie sprawdź ustawienia ponownie, aby upewnić się, że zmiany zostały zastosowane.</span><span class="sxs-lookup"><span data-stu-id="b1344-203">Wait a few minutes and check the settings again to make sure that your changes were applied.</span></span>

### <a name="configure-automated-backup"></a><span data-ttu-id="b1344-204">Skonfiguruj automatyczne kopie zapasowe</span><span class="sxs-lookup"><span data-stu-id="b1344-204">Configure Automated Backup</span></span>
<span data-ttu-id="b1344-205">Można włączyć automatycznego tworzenia kopii zapasowej oraz aby zmodyfikować jego konfigurację i zachowanie w dowolnej chwili za pomocą programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b1344-205">You can use PowerShell to enable Automated Backup as well as to modify its configuration and behavior at any time.</span></span>

<span data-ttu-id="b1344-206">Najpierw wybierz lub Utwórz konto magazynu w przypadku plików kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="b1344-206">First, select or create a storage account for the backup files.</span></span> <span data-ttu-id="b1344-207">Poniższy skrypt wybiera konta magazynu lub jeśli nie istnieje, tworzy go.</span><span class="sxs-lookup"><span data-stu-id="b1344-207">The following script selects a storage account or creates it if it does not exist.</span></span>

```powershell
$storage_accountname = “yourstorageaccount”
$storage_resourcegroupname = $resourcegroupname

$storage = Get-AzureRmStorageAccount -ResourceGroupName $resourcegroupname `
    -Name $storage_accountname -ErrorAction SilentlyContinue
If (-Not $storage)
    { $storage = New-AzureRmStorageAccount -ResourceGroupName $storage_resourcegroupname `
    -Name $storage_accountname -SkuName Standard_GRS -Location $region }
```

> [!NOTE]
> <span data-ttu-id="b1344-208">Automatyczne kopie zapasowe nie obsługuje przechowywania kopii zapasowych w magazynie premium, ale może potrwać kopii zapasowych z dysków maszyny Wirtualnej, które używają magazyn w warstwie Premium.</span><span class="sxs-lookup"><span data-stu-id="b1344-208">Automated Backup does not support storing backups in premium storage, but it can take backups from VM disks which use Premium Storage.</span></span>

<span data-ttu-id="b1344-209">Następnie użyj **AzureRmVMSqlServerAutoBackupConfig nowy** polecenie, aby włączyć i skonfigurować ustawienia automatycznego tworzenia kopii zapasowej do przechowywania kopii zapasowych w ramach konta magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b1344-209">Then use the **New-AzureRmVMSqlServerAutoBackupConfig** command to enable and configure the Automated Backup settings to store backups in the Azure storage account.</span></span> <span data-ttu-id="b1344-210">W tym przykładzie ustawiono kopie zapasowe będą przechowywane w ciągu 10 dni.</span><span class="sxs-lookup"><span data-stu-id="b1344-210">In this example, the backups are set to be retained for 10 days.</span></span> <span data-ttu-id="b1344-211">Drugie polecenie **AzureRmVMSqlServerExtension zestaw**, aktualizuje określonej maszyny Wirtualnej platformy Azure przy użyciu tych ustawień.</span><span class="sxs-lookup"><span data-stu-id="b1344-211">The second command, **Set-AzureRmVMSqlServerExtension**, updates the specified Azure VM with these settings.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

<span data-ttu-id="b1344-212">Go może potrwać kilka minut, aby zainstalować i skonfigurować agenta programu SQL Server IaaS.</span><span class="sxs-lookup"><span data-stu-id="b1344-212">It could take several minutes to install and configure the SQL Server IaaS Agent.</span></span>

> [!NOTE]
> <span data-ttu-id="b1344-213">Istnieją inne ustawienia **AzureRmVMSqlServerAutoBackupConfig nowy** dotyczą tylko programu SQL Server 2016 i automatyczna usługa Backup v2.</span><span class="sxs-lookup"><span data-stu-id="b1344-213">There are other settings for **New-AzureRmVMSqlServerAutoBackupConfig** that apply only to SQL Server 2016 and Automated Backup v2.</span></span> <span data-ttu-id="b1344-214">SQL Server 2014 nie obsługuje następujące ustawienia: **BackupSystemDbs**, **BackupScheduleType**, **FullBackupFrequency**,  **FullBackupStartHour**, **FullBackupWindowInHours**, i **LogBackupFrequencyInMinutes**.</span><span class="sxs-lookup"><span data-stu-id="b1344-214">SQL Server 2014 does not support the following settings: **BackupSystemDbs**, **BackupScheduleType**, **FullBackupFrequency**, **FullBackupStartHour**, **FullBackupWindowInHours**, and **LogBackupFrequencyInMinutes**.</span></span> <span data-ttu-id="b1344-215">Jeśli do konfigurowania tych ustawień na maszynie wirtualnej programu SQL Server 2014, nie było błędu, ale nie zostać zastosowane ustawienia.</span><span class="sxs-lookup"><span data-stu-id="b1344-215">If you attempt to configure these settings on a SQL Server 2014 virtual machine, there is no error, but the settings do not get applied.</span></span> <span data-ttu-id="b1344-216">Jeśli chcesz użyć tych ustawień maszyny wirtualnej programu SQL Server 2016, zobacz [v2 automatyczna usługa Backup SQL Server 2016 maszyn wirtualnych platformy Azure](virtual-machines-windows-sql-automated-backup-v2.md).</span><span class="sxs-lookup"><span data-stu-id="b1344-216">If you want to use these settings on a SQL Server 2016 virtual machine, see [Automated Backup v2 for SQL Server 2016 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup-v2.md).</span></span>

<span data-ttu-id="b1344-217">Aby włączyć szyfrowanie, zmodyfikuj poprzedni skrypt do przekazania **EnableEncryption** parametru wraz z hasła (bezpieczny ciąg) **CertificatePassword** parametru.</span><span class="sxs-lookup"><span data-stu-id="b1344-217">To enable encryption, modify the previous script to pass the **EnableEncryption** parameter along with a password (secure string) for the **CertificatePassword** parameter.</span></span> <span data-ttu-id="b1344-218">Poniższy skrypt umożliwia ustawienia automatycznego tworzenia kopii zapasowej w poprzednim przykładzie i dodaje szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="b1344-218">The following script enables the Automated Backup settings in the previous example and adds encryption.</span></span>

```powershell
$password = "P@ssw0rd"
$encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -EnableEncryption -CertificatePassword $encryptionpassword `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

<span data-ttu-id="b1344-219">Aby potwierdzić ustawienia są stosowane, [Sprawdź konfigurację automatycznego tworzenia kopii zapasowej](#verifysettings).</span><span class="sxs-lookup"><span data-stu-id="b1344-219">To confirm your settings are applied, [verify the Automated Backup configuration](#verifysettings).</span></span>

### <a name="disable-automated-backup"></a><span data-ttu-id="b1344-220">Wyłącz automatyczne kopie zapasowe</span><span class="sxs-lookup"><span data-stu-id="b1344-220">Disable Automated Backup</span></span>

<span data-ttu-id="b1344-221">Aby wyłączyć automatyczna usługa Backup, uruchom ten sam skrypt bez **— Włącz** parametr **AzureRmVMSqlServerAutoBackupConfig nowy** polecenia.</span><span class="sxs-lookup"><span data-stu-id="b1344-221">To disable Automated Backup, run the same script without the **-Enable** parameter to the **New-AzureRmVMSqlServerAutoBackupConfig** command.</span></span> <span data-ttu-id="b1344-222">Brak **-Włącz** parametru sygnały polecenie, aby wyłączyć funkcję.</span><span class="sxs-lookup"><span data-stu-id="b1344-222">The absence of the **-Enable** parameter signals the command to disable the feature.</span></span> <span data-ttu-id="b1344-223">Podobnie jak w przypadku instalacji, może upłynąć kilka minut, aby wyłączyć automatyczne wykonywanie kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="b1344-223">As with installation, it can take several minutes to disable Automated Backup.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

### <a name="example-script"></a><span data-ttu-id="b1344-224">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="b1344-224">Example script</span></span>

<span data-ttu-id="b1344-225">Poniższy skrypt zawiera zestaw zmiennych, które można dostosować, aby włączyć i skonfigurować automatyczna usługa Backup dla maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b1344-225">The following script provides a set of variables that you can customize to enable and configure Automated Backup for your VM.</span></span> <span data-ttu-id="b1344-226">W Twoim przypadku może być konieczne dostosowanie skryptu, w zależności od wymagań.</span><span class="sxs-lookup"><span data-stu-id="b1344-226">In your case, you might need to customize the script based on your requirements.</span></span> <span data-ttu-id="b1344-227">Na przykład użytkownik musi wprowadzić zmiany, aby wyłączyć tworzenie kopii zapasowej bazy danych systemu lub włączyć szyfrowanie.</span><span class="sxs-lookup"><span data-stu-id="b1344-227">For example, you would have to make changes if you wanted to disable the backup of system databases or enable encryption.</span></span>

```powershell
$vmname = "yourvmname"
$resourcegroupname = "vmresourcegroupname"
$region = “Azure region name such as EASTUS2”
$storage_accountname = “storageaccountname”
$storage_resourcegroupname = $resourcegroupname
$retentionperiod = 10

# ResourceGroupName is the resource group which is hosting the VM where you are deploying the SQL IaaS Extension

Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region

# Creates/use a storage account to store the backups

$storage = Get-AzureRmStorageAccount -ResourceGroupName $resourcegroupname `
    -Name $storage_accountname -ErrorAction SilentlyContinue
If (-Not $storage)
    { $storage = New-AzureRmStorageAccount -ResourceGroupName $storage_resourcegroupname `
    -Name $storage_accountname -SkuName Standard_GRS -Location $region }

# Configure Automated Backup settings

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays $retentionperiod -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

# Apply the Automated Backup settings to the VM

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="b1344-228">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b1344-228">Next steps</span></span>

<span data-ttu-id="b1344-229">Automatyczne kopie zapasowe konfiguruje zarządzanej kopii zapasowej na maszynach wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b1344-229">Automated Backup configures Managed Backup on Azure VMs.</span></span> <span data-ttu-id="b1344-230">Dlatego ważne jest, aby [zapoznaj się z dokumentacją dla zarządzanej kopii zapasowej](https://msdn.microsoft.com/library/dn449496.aspx) zrozumienie zachowania i skutki.</span><span class="sxs-lookup"><span data-stu-id="b1344-230">So it is important to [review the documentation for Managed Backup](https://msdn.microsoft.com/library/dn449496.aspx) to understand the behavior and implications.</span></span>

<span data-ttu-id="b1344-231">Można znaleźć dodatkowe kopii zapasowej i przywracanie wskazówki dotyczące programu SQL Server na maszynach wirtualnych Azure w następującym temacie: [kopii zapasowej i przywracania dla programu SQL Server w usłudze Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="b1344-231">You can find additional backup and restore guidance for SQL Server on Azure VMs in the following topic: [Backup and Restore for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md).</span></span>

<span data-ttu-id="b1344-232">Informacje o innych zadaniach automatyzacji dostępny, zobacz [rozszerzenia agenta programu SQL Server IaaS](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="b1344-232">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

<span data-ttu-id="b1344-233">Aby uzyskać więcej informacji na temat uruchamiania programu SQL Server na maszynach wirtualnych Azure, zobacz [programu SQL Server na maszynach wirtualnych platformy Azure — omówienie](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b1344-233">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

