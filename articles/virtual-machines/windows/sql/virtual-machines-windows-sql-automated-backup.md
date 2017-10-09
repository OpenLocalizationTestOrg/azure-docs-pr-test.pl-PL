---
title: aaaAutomated kopii zapasowej programu SQL Server 2014 maszyn wirtualnych platformy Azure | Dokumentacja firmy Microsoft
description: "Zawiera opis funkcji automatycznego tworzenia kopii zapasowej hello programu SQL Server 2014 w maszynach wirtualnych działających na platformie Azure. W tym artykule jest tooVMs określonego za pomocą hello Menedżera zasobów."
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
ms.openlocfilehash: c6803d8ef9f80e44a2f87918d87e099f1b562483
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="automated-backup-for-sql-server-2014-virtual-machines-resource-manager"></a><span data-ttu-id="1a299-104">Automatyczne kopie zapasowe maszyn wirtualnych programu SQL Server 2014 (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="1a299-104">Automated Backup for SQL Server 2014 Virtual Machines (Resource Manager)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="1a299-105">Program SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="1a299-105">SQL Server 2014</span></span>](virtual-machines-windows-sql-automated-backup.md)
> * [<span data-ttu-id="1a299-106">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="1a299-106">SQL Server 2016</span></span>](virtual-machines-windows-sql-automated-backup-v2.md)

<span data-ttu-id="1a299-107">Automatyczne kopie zapasowe automatycznie konfiguruje [tooMicrosoft zarządzanej kopii zapasowej Azure](https://msdn.microsoft.com/library/dn449496.aspx) dla wszystkich istniejących i nowych baz danych na maszynie Wirtualnej platformy Azure, programem SQL Server 2014 Standard lub Enterprise.</span><span class="sxs-lookup"><span data-stu-id="1a299-107">Automated Backup automatically configures [Managed Backup tooMicrosoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) for all existing and new databases on an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> <span data-ttu-id="1a299-108">Dzięki temu tooconfigure kopie zapasowe zwykłej bazy danych, które korzystać z magazynu trwałego obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1a299-108">This enables you tooconfigure regular database backups that utilize durable Azure blob storage.</span></span> <span data-ttu-id="1a299-109">Automatyczne kopie zapasowe zależy od hello [rozszerzenia agenta programu SQL Server IaaS](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="1a299-109">Automated Backup depends on hello [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="1a299-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1a299-110">Prerequisites</span></span>
<span data-ttu-id="1a299-111">toouse automatyczne kopie zapasowe, należy wziąć pod uwagę następujące wymagania wstępne hello:</span><span class="sxs-lookup"><span data-stu-id="1a299-111">toouse Automated Backup, consider hello following prerequisites:</span></span>

<span data-ttu-id="1a299-112">**System operacyjny**:</span><span class="sxs-lookup"><span data-stu-id="1a299-112">**Operating System**:</span></span>

- <span data-ttu-id="1a299-113">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="1a299-113">Windows Server 2012</span></span>
- <span data-ttu-id="1a299-114">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="1a299-114">Windows Server 2012 R2</span></span>
- <span data-ttu-id="1a299-115">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="1a299-115">Windows Server 2016</span></span>

<span data-ttu-id="1a299-116">**Wydanie wersji programu SQL Server**:</span><span class="sxs-lookup"><span data-stu-id="1a299-116">**SQL Server version/edition**:</span></span>

- <span data-ttu-id="1a299-117">SQL Server 2014 Standard</span><span class="sxs-lookup"><span data-stu-id="1a299-117">SQL Server 2014 Standard</span></span>
- <span data-ttu-id="1a299-118">SQL Server 2014 Enterprise</span><span class="sxs-lookup"><span data-stu-id="1a299-118">SQL Server 2014 Enterprise</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1a299-119">Automatyczne działa kopii zapasowej z programu SQL Server 2014.</span><span class="sxs-lookup"><span data-stu-id="1a299-119">Automated Backup works with SQL Server 2014.</span></span> <span data-ttu-id="1a299-120">Jeśli używasz programu SQL Server 2016, można użyć automatycznego tworzenia kopii zapasowej v2 tooback zapasową baz danych.</span><span class="sxs-lookup"><span data-stu-id="1a299-120">If you are using SQL Server 2016, you can use Automated Backup v2 tooback up your databases.</span></span> <span data-ttu-id="1a299-121">Aby uzyskać więcej informacji, zobacz [v2 automatyczna usługa Backup SQL Server 2016 maszyn wirtualnych platformy Azure](virtual-machines-windows-sql-automated-backup-v2.md).</span><span class="sxs-lookup"><span data-stu-id="1a299-121">For more information, see [Automated Backup v2 for SQL Server 2016 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup-v2.md).</span></span>

<span data-ttu-id="1a299-122">**Baza danych konfiguracji**:</span><span class="sxs-lookup"><span data-stu-id="1a299-122">**Database configuration**:</span></span>

- <span data-ttu-id="1a299-123">Docelowymi bazami danych, należy użyć hello modelu odzyskiwania pełnego.</span><span class="sxs-lookup"><span data-stu-id="1a299-123">Target databases must use hello full recovery model.</span></span> <span data-ttu-id="1a299-124">Aby uzyskać więcej informacji dotyczących wpływu hello modelu odzyskiwania pełnego hello na wykonywanie kopii zapasowych, zobacz [hello kopii zapasowych w ramach modelu odzyskiwania pełnego](https://technet.microsoft.com/library/ms190217.aspx).</span><span class="sxs-lookup"><span data-stu-id="1a299-124">For more information about hello impact of hello full recovery model on backups, see [Backup Under hello Full Recovery Model](https://technet.microsoft.com/library/ms190217.aspx).</span></span>
- <span data-ttu-id="1a299-125">Docelowymi bazami danych musi znajdować się na powitania domyślnego wystąpienia programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="1a299-125">Target databases must be on hello default SQL Server instance.</span></span> <span data-ttu-id="1a299-126">Witaj IaaS rozszerzenie dotyczące programu SQL Server nie obsługuje nazwanych wystąpień.</span><span class="sxs-lookup"><span data-stu-id="1a299-126">hello SQL Server IaaS Extension does not support named instances.</span></span>

<span data-ttu-id="1a299-127">**Model wdrożenia usługi Azure**:</span><span class="sxs-lookup"><span data-stu-id="1a299-127">**Azure deployment model**:</span></span>

- <span data-ttu-id="1a299-128">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1a299-128">Resource Manager</span></span>

<span data-ttu-id="1a299-129">**Program Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="1a299-129">**Azure PowerShell**:</span></span>

- <span data-ttu-id="1a299-130">[Zainstaluj najnowsze poleceń programu Azure PowerShell hello](/powershell/azure/overview) Jeśli planujesz tooconfigure automatyczne kopie zapasowe przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1a299-130">[Install hello latest Azure PowerShell commands](/powershell/azure/overview) if you plan tooconfigure Automated Backup with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="1a299-131">Automatyczne kopie zapasowe polega na powitania rozszerzenia agenta programu SQL Server IaaS.</span><span class="sxs-lookup"><span data-stu-id="1a299-131">Automated Backup relies on hello SQL Server IaaS Agent Extension.</span></span> <span data-ttu-id="1a299-132">Bieżący obrazów Galeria maszyny wirtualnej SQL dodać to rozszerzenie domyślnie.</span><span class="sxs-lookup"><span data-stu-id="1a299-132">Current SQL virtual machine gallery images add this extension by default.</span></span> <span data-ttu-id="1a299-133">Aby uzyskać więcej informacji, zobacz [rozszerzenia agenta programu SQL Server IaaS](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="1a299-133">For more information, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="1a299-134">Ustawienia</span><span class="sxs-lookup"><span data-stu-id="1a299-134">Settings</span></span>

<span data-ttu-id="1a299-135">Witaj poniższej tabeli opisano opcje hello, które można skonfigurować do automatycznego tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="1a299-135">hello following table describes hello options that can be configured for Automated Backup.</span></span> <span data-ttu-id="1a299-136">kroki rzeczywista konfiguracja Hello się różnić w zależności od tego, czy używać hello portalu Azure lub poleceń programu Windows PowerShell dla usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="1a299-136">hello actual configuration steps vary depending on whether you use hello Azure portal or Azure Windows PowerShell commands.</span></span>

| <span data-ttu-id="1a299-137">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="1a299-137">Setting</span></span> | <span data-ttu-id="1a299-138">Zakres (ustawienie domyślne)</span><span class="sxs-lookup"><span data-stu-id="1a299-138">Range (Default)</span></span> | <span data-ttu-id="1a299-139">Opis</span><span class="sxs-lookup"><span data-stu-id="1a299-139">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a299-140">**Automatyczne kopie zapasowe**</span><span class="sxs-lookup"><span data-stu-id="1a299-140">**Automated Backup**</span></span> | <span data-ttu-id="1a299-141">Włącza/wyłącza (wyłączone)</span><span class="sxs-lookup"><span data-stu-id="1a299-141">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="1a299-142">Włącza lub wyłącza funkcję automatycznego tworzenia kopii zapasowej dla maszyny Wirtualnej platformy Azure, programem SQL Server 2014 Standard lub Enterprise.</span><span class="sxs-lookup"><span data-stu-id="1a299-142">Enables or disables Automated Backup for an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> |
| <span data-ttu-id="1a299-143">**Okres przechowywania**</span><span class="sxs-lookup"><span data-stu-id="1a299-143">**Retention Period**</span></span> | <span data-ttu-id="1a299-144">1 do 30 dni (30 dni)</span><span class="sxs-lookup"><span data-stu-id="1a299-144">1-30 days (30 days)</span></span> | <span data-ttu-id="1a299-145">Witaj liczbę dni tooretain kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="1a299-145">hello number of days tooretain a backup.</span></span> |
| <span data-ttu-id="1a299-146">**Konto magazynu**</span><span class="sxs-lookup"><span data-stu-id="1a299-146">**Storage Account**</span></span> | <span data-ttu-id="1a299-147">Konto magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="1a299-147">Azure storage account</span></span> | <span data-ttu-id="1a299-148">Toouse konto magazynu Azure do przechowywania plików automatycznego tworzenia kopii zapasowej w magazynie obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="1a299-148">An Azure storage account toouse for storing Automated Backup files in blob storage.</span></span> <span data-ttu-id="1a299-149">Kontener jest tworzony w tej lokalizacji toostore wszystkie pliki kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="1a299-149">A container is created at this location toostore all backup files.</span></span> <span data-ttu-id="1a299-150">Plik kopii zapasowej Hello konwencji nazewnictwa obejmuje hello daty, godziny i nazwy komputera.</span><span class="sxs-lookup"><span data-stu-id="1a299-150">hello backup file naming convention includes hello date, time, and machine name.</span></span> |
| <span data-ttu-id="1a299-151">**Szyfrowanie**</span><span class="sxs-lookup"><span data-stu-id="1a299-151">**Encryption**</span></span> | <span data-ttu-id="1a299-152">Włącza/wyłącza (wyłączone)</span><span class="sxs-lookup"><span data-stu-id="1a299-152">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="1a299-153">Włącza lub wyłącza funkcję szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="1a299-153">Enables or disables encryption.</span></span> <span data-ttu-id="1a299-154">Po włączeniu szyfrowania hello używane certyfikaty toorestore hello w kopii zapasowej znajdują się w hello określony magazynu konta w hello sam `automaticbackup` przy użyciu kontenera hello tej samej konwencji nazewnictwa.</span><span class="sxs-lookup"><span data-stu-id="1a299-154">When encryption is enabled, hello certificates used toorestore hello backup are located in hello specified storage account in hello same `automaticbackup` container using hello same naming convention.</span></span> <span data-ttu-id="1a299-155">Zmiana hasła hello nowego certyfikatu jest generowana za pomocą tego hasła, ale hello stary certyfikat pozostaje toorestore poprzednich kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="1a299-155">If hello password changes, a new certificate is generated with that password, but hello old certificate remains toorestore prior backups.</span></span> |
| <span data-ttu-id="1a299-156">**Hasło**</span><span class="sxs-lookup"><span data-stu-id="1a299-156">**Password**</span></span> | <span data-ttu-id="1a299-157">Tekst hasła</span><span class="sxs-lookup"><span data-stu-id="1a299-157">Password text</span></span> | <span data-ttu-id="1a299-158">Hasło dla kluczy szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="1a299-158">A password for encryption keys.</span></span> <span data-ttu-id="1a299-159">Jest to tylko wymagane, jeśli jest włączone szyfrowanie.</span><span class="sxs-lookup"><span data-stu-id="1a299-159">This is only required if encryption is enabled.</span></span> <span data-ttu-id="1a299-160">W kolejności toorestore zaszyfrowanej kopii zapasowej, trzeba hello prawidłowe hasło i powiązane certyfikatu, który został użyty w czasie hello hello tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="1a299-160">In order toorestore an encrypted backup, you must have hello correct password and related certificate that was used at hello time hello backup was taken.</span></span> |

## <a name="configuration-in-hello-portal"></a><span data-ttu-id="1a299-161">Konfiguracja w hello portalu</span><span class="sxs-lookup"><span data-stu-id="1a299-161">Configuration in hello Portal</span></span>

<span data-ttu-id="1a299-162">Witaj tooconfigure portalu Azure automatyczne kopie zapasowe można użyć podczas inicjowania obsługi lub dla maszyn wirtualnych istniejącego programu SQL Server 2014.</span><span class="sxs-lookup"><span data-stu-id="1a299-162">You can use hello Azure portal tooconfigure Automated Backup during provisioning or for existing SQL Server 2014 VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="1a299-163">Nowe maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="1a299-163">New VMs</span></span>

<span data-ttu-id="1a299-164">Podczas tworzenia nowej maszyny wirtualnej 2014 serwera SQL w modelu wdrażania usługi Resource Manager hello za pomocą hello Azure tooconfigure portalu automatyczne kopie zapasowe.</span><span class="sxs-lookup"><span data-stu-id="1a299-164">Use hello Azure portal tooconfigure Automated Backup when you create a new SQL Server 2014 Virtual Machine in hello Resource Manager deployment model.</span></span>

<span data-ttu-id="1a299-165">W hello **ustawienia programu SQL Server** bloku, wybierz opcję **automatyczne kopie zapasowe**.</span><span class="sxs-lookup"><span data-stu-id="1a299-165">In hello **SQL Server settings** blade, select **Automated backup**.</span></span> <span data-ttu-id="1a299-166">Witaj Poniższy zrzut ekranu portalu Azure zawiera hello **SQL automatyczna usługa Backup** bloku.</span><span class="sxs-lookup"><span data-stu-id="1a299-166">hello following Azure portal screenshot shows hello **SQL Automated Backup** blade.</span></span>

![Konfiguracja SQL automatyczna usługa Backup w portalu Azure](./media/virtual-machines-windows-sql-automated-backup/azure-sql-arm-autobackup.png)

<span data-ttu-id="1a299-168">Dla kontekstu, zobacz temat pełną hello na [obsługi maszyny wirtualnej programu SQL Server na platformie Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="1a299-168">For context, see hello complete topic on [provisioning a SQL Server virtual machine in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="1a299-169">Istniejące maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="1a299-169">Existing VMs</span></span>

<span data-ttu-id="1a299-170">W przypadku istniejących maszyn wirtualnych programu SQL Server należy wybrać maszyny wirtualnej programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="1a299-170">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="1a299-171">Następnie wybierz hello **konfigurację programu SQL Server** sekcji hello **ustawienia** bloku.</span><span class="sxs-lookup"><span data-stu-id="1a299-171">Then select hello **SQL Server configuration** section of hello **Settings** blade.</span></span>

![SQL automatyczna usługa Backup dla istniejących maszyn wirtualnych](./media/virtual-machines-windows-sql-automated-backup/azure-sql-rm-autobackup-existing-vms.png)

<span data-ttu-id="1a299-173">W hello **konfigurację programu SQL Server** bloku, kliknij hello **Edytuj** przycisku na powitania automatycznego tworzenia kopii zapasowej sekcji.</span><span class="sxs-lookup"><span data-stu-id="1a299-173">In hello **SQL Server configuration** blade, click hello **Edit** button in hello Automated backup section.</span></span>

![Konfigurowanie kopii zapasowej SQL automatycznego dla istniejących maszyn wirtualnych](./media/virtual-machines-windows-sql-automated-backup/azure-sql-rm-autobackup-configuration.png)

<span data-ttu-id="1a299-175">Po zakończeniu kliknij przycisk hello **OK** przycisk u dołu hello hello **konfigurację programu SQL Server** toosave bloku zmiany.</span><span class="sxs-lookup"><span data-stu-id="1a299-175">When finished, click hello **OK** button on hello bottom of hello **SQL Server configuration** blade toosave your changes.</span></span>

<span data-ttu-id="1a299-176">Jeśli włączasz automatyczna usługa Backup dla powitania po raz pierwszy, Azure konfiguruje hello Agent środowiska IaaS programu SQL Server w tle hello.</span><span class="sxs-lookup"><span data-stu-id="1a299-176">If you are enabling Automated Backup for hello first time, Azure configures hello SQL Server IaaS Agent in hello background.</span></span> <span data-ttu-id="1a299-177">W tym czasie hello portalu Azure może nie informować, że skonfigurowano automatycznego tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="1a299-177">During this time, hello Azure portal might not show that Automated Backup is configured.</span></span> <span data-ttu-id="1a299-178">Poczekaj kilka minut dla hello toobe agent zainstalowany, skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="1a299-178">Wait several minutes for hello agent toobe installed, configured.</span></span> <span data-ttu-id="1a299-179">Po tym hello Azure portalu będzie odzwierciedlać hello nowych ustawień.</span><span class="sxs-lookup"><span data-stu-id="1a299-179">After that hello Azure portal will reflect hello new settings.</span></span>

> [!NOTE]
> <span data-ttu-id="1a299-180">Istnieje również możliwość skonfigurowania automatycznego tworzenia kopii zapasowej przy użyciu szablonu.</span><span class="sxs-lookup"><span data-stu-id="1a299-180">You can also configure Automated Backup using a template.</span></span> <span data-ttu-id="1a299-181">Aby uzyskać więcej informacji, zobacz [szablonu Azure szybkiego startu dla automatyczna usługa Backup](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autobackup-update).</span><span class="sxs-lookup"><span data-stu-id="1a299-181">For more information, see [Azure quickstart template for Automated Backup](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autobackup-update).</span></span>

## <a name="configuration-with-powershell"></a><span data-ttu-id="1a299-182">Konfiguracja przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="1a299-182">Configuration with PowerShell</span></span>

<span data-ttu-id="1a299-183">Możesz użyć programu PowerShell tooconfigure automatyczne kopie zapasowe.</span><span class="sxs-lookup"><span data-stu-id="1a299-183">You can use PowerShell tooconfigure Automated Backup.</span></span> <span data-ttu-id="1a299-184">Przed rozpoczęciem należy:</span><span class="sxs-lookup"><span data-stu-id="1a299-184">Before you begin, you must:</span></span>

- <span data-ttu-id="1a299-185">[Pobierz i zainstaluj najnowsze programu Azure PowerShell hello](http://aka.ms/webpi-azps).</span><span class="sxs-lookup"><span data-stu-id="1a299-185">[Download and install hello latest Azure PowerShell](http://aka.ms/webpi-azps).</span></span>
- <span data-ttu-id="1a299-186">Otwórz program Windows PowerShell i skojarzyć go z Twoim kontem.</span><span class="sxs-lookup"><span data-stu-id="1a299-186">Open Windows PowerShell and associate it with your account.</span></span> <span data-ttu-id="1a299-187">Aby to zrobić, wykonaj czynności hello w hello [skonfiguruj subskrypcję](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) sekcji hello inicjowania obsługi administracyjnej tematu.</span><span class="sxs-lookup"><span data-stu-id="1a299-187">You can do this by following hello steps in hello [Configure your subscription](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) section of hello provisioning topic.</span></span>

### <a name="install-hello-sql-iaas-extension"></a><span data-ttu-id="1a299-188">Zainstaluj hello rozszerzenia IaaS SQL</span><span class="sxs-lookup"><span data-stu-id="1a299-188">Install hello SQL IaaS Extension</span></span>
<span data-ttu-id="1a299-189">Jeśli aprowizowanej maszyny wirtualnej programu SQL Server z portalu Azure hello hello rozszerzenie IaaS serwera SQL powinno być już zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="1a299-189">If you provisioned a SQL Server virtual machine from hello Azure portal, hello SQL Server IaaS Extension should already be installed.</span></span> <span data-ttu-id="1a299-190">Można określić, czy jest ona instalowana dla maszyny Wirtualnej przez wywołanie metody **Get-AzureRmVM** polecenia i sprawdzeniu hello **rozszerzenia** właściwości.</span><span class="sxs-lookup"><span data-stu-id="1a299-190">You can determine if it is installed for your VM by calling **Get-AzureRmVM** command and examining hello **Extensions** property.</span></span>

```powershell
$vmname = "vmname"
$resourcegroupname = "resourcegroupname"

(Get-AzureRmVM -Name $vmname -ResourceGroupName $resourcegroupname).Extensions
```

<span data-ttu-id="1a299-191">Jeśli zainstalowano hello rozszerzenia SQL Server IaaS Agent, powinien pojawić się wymienionym "SqlIaaSAgent" lub "SQLIaaSExtension".</span><span class="sxs-lookup"><span data-stu-id="1a299-191">If hello SQL Server IaaS Agent extension is installed, you should see it listed as “SqlIaaSAgent” or “SQLIaaSExtension”.</span></span> <span data-ttu-id="1a299-192">**ProvisioningState** dla rozszerzenia hello również powinny być widoczne "Powodzenie".</span><span class="sxs-lookup"><span data-stu-id="1a299-192">**ProvisioningState** for hello extension should also show “Succeeded”.</span></span>

<span data-ttu-id="1a299-193">Jeśli nie jest zainstalowany lub nie można zainicjować obsługi administracyjnej toobe, należy zainstalować go z hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="1a299-193">If it is not installed or failed toobe provisioned, you can install it with hello following command.</span></span> <span data-ttu-id="1a299-194">Dodanie toohello wirtualna Nazwa zasobu grupy i, należy także określić hello region (**$region**) maszyny Wirtualnej znajdujący się w.</span><span class="sxs-lookup"><span data-stu-id="1a299-194">In addition toohello VM name and resource group, you must also specify hello region (**$region**) that your VM is located in.</span></span>

```powershell
$region = “EASTUS2”
Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region
```

### <span data-ttu-id="1a299-195"><a id="verifysettings"></a>Sprawdź bieżące ustawienia</span><span class="sxs-lookup"><span data-stu-id="1a299-195"><a id="verifysettings"></a> Verify current settings</span></span>

<span data-ttu-id="1a299-196">Jeśli włączono automatyczne kopie zapasowe podczas inicjowania obsługi, można użyć programu PowerShell toocheck bieżącej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="1a299-196">If you enabled automated backup during provisioning, you can use PowerShell toocheck your current configuration.</span></span> <span data-ttu-id="1a299-197">Uruchom hello **Get-AzureRmVMSqlServerExtension** polecenia i sprawdź, czy hello **AutoBackupSettings** właściwości:</span><span class="sxs-lookup"><span data-stu-id="1a299-197">Run hello **Get-AzureRmVMSqlServerExtension** command and examine hello **AutoBackupSettings** property:</span></span>

```powershell
(Get-AzureRmVMSqlServerExtension -VMName $vmname -ResourceGroupName $resourcegroupname).AutoBackupSettings
```

<span data-ttu-id="1a299-198">Należy pobrać dane wyjściowe podobne toohello poniżej:</span><span class="sxs-lookup"><span data-stu-id="1a299-198">You should get output similar toohello following:</span></span>

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

<span data-ttu-id="1a299-199">Jeśli dane wyjściowe wskazuje, że **włączyć** ustawiono zbyt**False**, następnie tooenable automatyczne kopie zapasowe.</span><span class="sxs-lookup"><span data-stu-id="1a299-199">If your output shows that **Enable** is set too**False**, then you have tooenable automated backup.</span></span> <span data-ttu-id="1a299-200">Witaj szczęście jest włączone, a następnie skonfiguruj automatyczne kopie zapasowe w hello tak samo.</span><span class="sxs-lookup"><span data-stu-id="1a299-200">hello good news is that you enable and configure Automated Backup in hello same way.</span></span> <span data-ttu-id="1a299-201">Zobacz następną sekcję hello tych informacji.</span><span class="sxs-lookup"><span data-stu-id="1a299-201">See hello next section for this information.</span></span>

> [!NOTE] 
> <span data-ttu-id="1a299-202">Jeśli natychmiast po wprowadzeniu zmiany można sprawdzić ustawienia hello, istnieje możliwość, że wystąpi ponownie hello starych wartości konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="1a299-202">If you check hello settings immediately after making a change, it is possible that you will get back hello old configuration values.</span></span> <span data-ttu-id="1a299-203">Poczekaj kilka minut i sprawdź ustawienia hello ponownie toomake się upewnić, że zmiany zostały zastosowane.</span><span class="sxs-lookup"><span data-stu-id="1a299-203">Wait a few minutes and check hello settings again toomake sure that your changes were applied.</span></span>

### <a name="configure-automated-backup"></a><span data-ttu-id="1a299-204">Skonfiguruj automatyczne kopie zapasowe</span><span class="sxs-lookup"><span data-stu-id="1a299-204">Configure Automated Backup</span></span>
<span data-ttu-id="1a299-205">Umożliwia tooenable PowerShell automatyczne kopie zapasowe, a także toomodify jego konfiguracji i zachowania w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="1a299-205">You can use PowerShell tooenable Automated Backup as well as toomodify its configuration and behavior at any time.</span></span>

<span data-ttu-id="1a299-206">Najpierw wybierz lub Utwórz konto magazynu dla hello pliki kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="1a299-206">First, select or create a storage account for hello backup files.</span></span> <span data-ttu-id="1a299-207">Witaj poniższy skrypt wybiera konto magazynu lub utworzenie go, jeśli nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="1a299-207">hello following script selects a storage account or creates it if it does not exist.</span></span>

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
> <span data-ttu-id="1a299-208">Automatyczne kopie zapasowe nie obsługuje przechowywania kopii zapasowych w magazynie premium, ale może potrwać kopii zapasowych z dysków maszyny Wirtualnej, które używają magazyn w warstwie Premium.</span><span class="sxs-lookup"><span data-stu-id="1a299-208">Automated Backup does not support storing backups in premium storage, but it can take backups from VM disks which use Premium Storage.</span></span>

<span data-ttu-id="1a299-209">Następnie użyj hello **AzureRmVMSqlServerAutoBackupConfig nowy** polecenia tooenable i skonfigurować hello automatyczna usługa Backup ustawienia toostore tworzenia kopii zapasowych w hello kontem magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1a299-209">Then use hello **New-AzureRmVMSqlServerAutoBackupConfig** command tooenable and configure hello Automated Backup settings toostore backups in hello Azure storage account.</span></span> <span data-ttu-id="1a299-210">W tym przykładzie hello kopie zapasowe są ustawiane toobe przechowywane przez 10 dni.</span><span class="sxs-lookup"><span data-stu-id="1a299-210">In this example, hello backups are set toobe retained for 10 days.</span></span> <span data-ttu-id="1a299-211">drugie polecenie Hello **AzureRmVMSqlServerExtension zestaw**, hello aktualizacji określonej maszyny Wirtualnej platformy Azure przy użyciu tych ustawień.</span><span class="sxs-lookup"><span data-stu-id="1a299-211">hello second command, **Set-AzureRmVMSqlServerExtension**, updates hello specified Azure VM with these settings.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

<span data-ttu-id="1a299-212">Go może potrwać kilka minut tooinstall i skonfiguruj hello Agent środowiska IaaS programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="1a299-212">It could take several minutes tooinstall and configure hello SQL Server IaaS Agent.</span></span>

> [!NOTE]
> <span data-ttu-id="1a299-213">Istnieją inne ustawienia **AzureRmVMSqlServerAutoBackupConfig nowy** przeznaczonych tylko tooSQL Server 2016 i v2 automatycznego tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="1a299-213">There are other settings for **New-AzureRmVMSqlServerAutoBackupConfig** that apply only tooSQL Server 2016 and Automated Backup v2.</span></span> <span data-ttu-id="1a299-214">SQL Server 2014 nie obsługuje hello następujące ustawienia: **BackupSystemDbs**, **BackupScheduleType**, **FullBackupFrequency**,  **FullBackupStartHour**, **FullBackupWindowInHours**, i **LogBackupFrequencyInMinutes**.</span><span class="sxs-lookup"><span data-stu-id="1a299-214">SQL Server 2014 does not support hello following settings: **BackupSystemDbs**, **BackupScheduleType**, **FullBackupFrequency**, **FullBackupStartHour**, **FullBackupWindowInHours**, and **LogBackupFrequencyInMinutes**.</span></span> <span data-ttu-id="1a299-215">Jeśli próba tooconfigure tych ustawień na maszynę wirtualną programu SQL Server 2014 nie było błędu, ale nie zostać zastosowane ustawienia hello.</span><span class="sxs-lookup"><span data-stu-id="1a299-215">If you attempt tooconfigure these settings on a SQL Server 2014 virtual machine, there is no error, but hello settings do not get applied.</span></span> <span data-ttu-id="1a299-216">Jeśli chcesz toouse tych ustawień na maszynę wirtualną programu SQL Server 2016, zobacz [v2 automatyczna usługa Backup SQL Server 2016 maszyn wirtualnych platformy Azure](virtual-machines-windows-sql-automated-backup-v2.md).</span><span class="sxs-lookup"><span data-stu-id="1a299-216">If you want toouse these settings on a SQL Server 2016 virtual machine, see [Automated Backup v2 for SQL Server 2016 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup-v2.md).</span></span>

<span data-ttu-id="1a299-217">szyfrowania tooenable zmodyfikować hello poprzedniej skryptu toopass hello **EnableEncryption** parametru wraz z hasła (bezpieczny ciąg) hello **CertificatePassword** parametru.</span><span class="sxs-lookup"><span data-stu-id="1a299-217">tooenable encryption, modify hello previous script toopass hello **EnableEncryption** parameter along with a password (secure string) for hello **CertificatePassword** parameter.</span></span> <span data-ttu-id="1a299-218">Witaj poniższy skrypt umożliwia hello ustawienia automatycznego tworzenia kopii zapasowej w poprzednim przykładzie hello i dodaje szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="1a299-218">hello following script enables hello Automated Backup settings in hello previous example and adds encryption.</span></span>

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

<span data-ttu-id="1a299-219">ustawienia są stosowane, tooconfirm [Sprawdź konfigurację automatycznego tworzenia kopii zapasowej hello](#verifysettings).</span><span class="sxs-lookup"><span data-stu-id="1a299-219">tooconfirm your settings are applied, [verify hello Automated Backup configuration](#verifysettings).</span></span>

### <a name="disable-automated-backup"></a><span data-ttu-id="1a299-220">Wyłącz automatyczne kopie zapasowe</span><span class="sxs-lookup"><span data-stu-id="1a299-220">Disable Automated Backup</span></span>

<span data-ttu-id="1a299-221">toodisable automatyczne kopie zapasowe, uruchom hello sam skrypt bez hello **-Włącz** toohello parametru **AzureRmVMSqlServerAutoBackupConfig nowy** polecenia.</span><span class="sxs-lookup"><span data-stu-id="1a299-221">toodisable Automated Backup, run hello same script without hello **-Enable** parameter toohello **New-AzureRmVMSqlServerAutoBackupConfig** command.</span></span> <span data-ttu-id="1a299-222">Witaj braku hello **-Włącz** parametru sygnały hello polecenia toodisable hello funkcji.</span><span class="sxs-lookup"><span data-stu-id="1a299-222">hello absence of hello **-Enable** parameter signals hello command toodisable hello feature.</span></span> <span data-ttu-id="1a299-223">Podobnie jak w przypadku instalacji, może upłynąć kilka minut toodisable automatyczne kopie zapasowe.</span><span class="sxs-lookup"><span data-stu-id="1a299-223">As with installation, it can take several minutes toodisable Automated Backup.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

### <a name="example-script"></a><span data-ttu-id="1a299-224">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="1a299-224">Example script</span></span>

<span data-ttu-id="1a299-225">Witaj poniższy skrypt zawiera zestaw zmiennych można dostosować tooenable i skonfiguruj automatyczne kopie zapasowe dla maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1a299-225">hello following script provides a set of variables that you can customize tooenable and configure Automated Backup for your VM.</span></span> <span data-ttu-id="1a299-226">W Twoim przypadku może być konieczne skryptu hello toocustomize zgodnie z wymaganiami.</span><span class="sxs-lookup"><span data-stu-id="1a299-226">In your case, you might need toocustomize hello script based on your requirements.</span></span> <span data-ttu-id="1a299-227">Na przykład czy mają toomake zmiany, jeśli potrzebujesz kopii zapasowej hello toodisable systemowych baz danych lub włączyć szyfrowanie.</span><span class="sxs-lookup"><span data-stu-id="1a299-227">For example, you would have toomake changes if you wanted toodisable hello backup of system databases or enable encryption.</span></span>

```powershell
$vmname = "yourvmname"
$resourcegroupname = "vmresourcegroupname"
$region = “Azure region name such as EASTUS2”
$storage_accountname = “storageaccountname”
$storage_resourcegroupname = $resourcegroupname
$retentionperiod = 10

# ResourceGroupName is hello resource group which is hosting hello VM where you are deploying hello SQL IaaS Extension

Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region

# Creates/use a storage account toostore hello backups

$storage = Get-AzureRmStorageAccount -ResourceGroupName $resourcegroupname `
    -Name $storage_accountname -ErrorAction SilentlyContinue
If (-Not $storage)
    { $storage = New-AzureRmStorageAccount -ResourceGroupName $storage_resourcegroupname `
    -Name $storage_accountname -SkuName Standard_GRS -Location $region }

# Configure Automated Backup settings

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays $retentionperiod -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

# Apply hello Automated Backup settings toohello VM

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="1a299-228">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1a299-228">Next steps</span></span>

<span data-ttu-id="1a299-229">Automatyczne kopie zapasowe konfiguruje zarządzanej kopii zapasowej na maszynach wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1a299-229">Automated Backup configures Managed Backup on Azure VMs.</span></span> <span data-ttu-id="1a299-230">Dlatego ważne jest zbyt[hello dokumentacji zarządzanej kopii zapasowej](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello zachowanie i skutki.</span><span class="sxs-lookup"><span data-stu-id="1a299-230">So it is important too[review hello documentation for Managed Backup](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello behavior and implications.</span></span>

<span data-ttu-id="1a299-231">Można znaleźć dodatkowe kopii zapasowej i przywracanie wskazówki dotyczące programu SQL Server na maszynach wirtualnych Azure w hello kolejny temat: [kopii zapasowej i przywracania dla programu SQL Server w usłudze Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="1a299-231">You can find additional backup and restore guidance for SQL Server on Azure VMs in hello following topic: [Backup and Restore for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md).</span></span>

<span data-ttu-id="1a299-232">Informacje o innych zadaniach automatyzacji dostępny, zobacz [rozszerzenia agenta programu SQL Server IaaS](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="1a299-232">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

<span data-ttu-id="1a299-233">Aby uzyskać więcej informacji na temat uruchamiania programu SQL Server na maszynach wirtualnych Azure, zobacz [programu SQL Server na maszynach wirtualnych platformy Azure — omówienie](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1a299-233">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

