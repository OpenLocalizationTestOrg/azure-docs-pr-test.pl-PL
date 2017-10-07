---
title: aaaAutomated v2 kopii zapasowej programu SQL Server 2016 maszyn wirtualnych platformy Azure | Dokumentacja firmy Microsoft
description: "Zawiera opis funkcji automatycznego tworzenia kopii zapasowej powitania dla programu SQL Server 2016 maszyn wirtualnych działających na platformie Azure. W tym artykule jest tooVMs określonego za pomocą hello Menedżera zasobów."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: ebd23868-821c-475b-b867-06d4a2e310c7
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 04/05/2017
ms.author: jroth
ms.openlocfilehash: a322792fb22c76bfa74fafb711b8b1927a6e2b3a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="automated-backup-v2-for-sql-server-2016-azure-virtual-machines-resource-manager"></a><span data-ttu-id="29acd-104">Automatycznego tworzenia kopii zapasowej w wersji 2 dla programu SQL Server 2016 maszyn wirtualnych platformy Azure (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="29acd-104">Automated Backup v2 for SQL Server 2016 Azure Virtual Machines (Resource Manager)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="29acd-105">Program SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="29acd-105">SQL Server 2014</span></span>](virtual-machines-windows-sql-automated-backup.md)
> * [<span data-ttu-id="29acd-106">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="29acd-106">SQL Server 2016</span></span>](virtual-machines-windows-sql-automated-backup-v2.md)

<span data-ttu-id="29acd-107">Automatyczne v2 kopii zapasowej automatycznie konfiguruje [tooMicrosoft zarządzanej kopii zapasowej Azure](https://msdn.microsoft.com/library/dn449496.aspx) dla wszystkich istniejących i nowych baz danych na maszynie Wirtualnej platformy Azure, uruchomione wersje programu SQL Server 2016 Standard, Enterprise lub dewelopera.</span><span class="sxs-lookup"><span data-stu-id="29acd-107">Automated Backup v2 automatically configures [Managed Backup tooMicrosoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) for all existing and new databases on an Azure VM running SQL Server 2016 Standard, Enterprise, or Developer editions.</span></span> <span data-ttu-id="29acd-108">Dzięki temu tooconfigure kopie zapasowe zwykłej bazy danych, które korzystać z magazynu trwałego obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="29acd-108">This enables you tooconfigure regular database backups that utilize durable Azure blob storage.</span></span> <span data-ttu-id="29acd-109">Automatyczne v2 kopii zapasowej zależy od hello [rozszerzenia agenta programu SQL Server IaaS](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="29acd-109">Automated Backup v2 depends on hello [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="29acd-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="29acd-110">Prerequisites</span></span>
<span data-ttu-id="29acd-111">toouse v2 automatyczna usługa Backup hello Przejrzyj następujące wymagania wstępne:</span><span class="sxs-lookup"><span data-stu-id="29acd-111">toouse Automated Backup v2, review hello following prerequisites:</span></span>

<span data-ttu-id="29acd-112">**System operacyjny**:</span><span class="sxs-lookup"><span data-stu-id="29acd-112">**Operating System**:</span></span>

- <span data-ttu-id="29acd-113">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="29acd-113">Windows Server 2012 R2</span></span>
- <span data-ttu-id="29acd-114">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="29acd-114">Windows Server 2016</span></span>

<span data-ttu-id="29acd-115">**Wydanie wersji programu SQL Server**:</span><span class="sxs-lookup"><span data-stu-id="29acd-115">**SQL Server version/edition**:</span></span>

- <span data-ttu-id="29acd-116">SQL Server 2016 Standard</span><span class="sxs-lookup"><span data-stu-id="29acd-116">SQL Server 2016 Standard</span></span>
- <span data-ttu-id="29acd-117">SQL Server 2016 Enterprise</span><span class="sxs-lookup"><span data-stu-id="29acd-117">SQL Server 2016 Enterprise</span></span>
- <span data-ttu-id="29acd-118">SQL Server 2016 Developer</span><span class="sxs-lookup"><span data-stu-id="29acd-118">SQL Server 2016 Developer</span></span>

> [!IMPORTANT]
> <span data-ttu-id="29acd-119">Automatyczne v2 kopii zapasowej działa z programem SQL Server 2016.</span><span class="sxs-lookup"><span data-stu-id="29acd-119">Automated Backup v2 works with SQL Server 2016.</span></span> <span data-ttu-id="29acd-120">Jeśli używasz programu SQL Server 2014, można użyć automatycznego tworzenia kopii zapasowej v1 tooback zapasową baz danych.</span><span class="sxs-lookup"><span data-stu-id="29acd-120">If you are using SQL Server 2014, you can use Automated Backup v1 tooback up your databases.</span></span> <span data-ttu-id="29acd-121">Aby uzyskać więcej informacji, zobacz [automatyczna usługa Backup SQL Server 2014 maszyn wirtualnych platformy Azure](virtual-machines-windows-sql-automated-backup.md).</span><span class="sxs-lookup"><span data-stu-id="29acd-121">For more information, see [Automated Backup for SQL Server 2014 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup.md).</span></span>

<span data-ttu-id="29acd-122">**Baza danych konfiguracji**:</span><span class="sxs-lookup"><span data-stu-id="29acd-122">**Database configuration**:</span></span>

- <span data-ttu-id="29acd-123">Docelowymi bazami danych, należy użyć hello modelu odzyskiwania pełnego.</span><span class="sxs-lookup"><span data-stu-id="29acd-123">Target databases must use hello full recovery model.</span></span> <span data-ttu-id="29acd-124">Aby uzyskać więcej informacji dotyczących wpływu hello modelu odzyskiwania pełnego hello na wykonywanie kopii zapasowych, zobacz [hello kopii zapasowych w ramach modelu odzyskiwania pełnego](https://technet.microsoft.com/library/ms190217.aspx).</span><span class="sxs-lookup"><span data-stu-id="29acd-124">For more information about hello impact of hello full recovery model on backups, see [Backup Under hello Full Recovery Model](https://technet.microsoft.com/library/ms190217.aspx).</span></span>
- <span data-ttu-id="29acd-125">Bazy danych systemu nie mają toouse modelu odzyskiwania pełnego.</span><span class="sxs-lookup"><span data-stu-id="29acd-125">System databases do not have toouse full recovery model.</span></span> <span data-ttu-id="29acd-126">Jeśli potrzebujesz toobe kopii zapasowych dziennika poświęcony Model i MSDB, musi jednak używać modelu odzyskiwania pełnego.</span><span class="sxs-lookup"><span data-stu-id="29acd-126">However, if you require log backups toobe taken for Model or MSDB, you must use full recovery model.</span></span>
- <span data-ttu-id="29acd-127">Docelowymi bazami danych musi znajdować się na powitania domyślnego wystąpienia programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="29acd-127">Target databases must be on hello default SQL Server instance.</span></span> <span data-ttu-id="29acd-128">Witaj IaaS rozszerzenie dotyczące programu SQL Server nie obsługuje nazwanych wystąpień.</span><span class="sxs-lookup"><span data-stu-id="29acd-128">hello SQL Server IaaS Extension does not support named instances.</span></span>

<span data-ttu-id="29acd-129">**Model wdrożenia usługi Azure**:</span><span class="sxs-lookup"><span data-stu-id="29acd-129">**Azure deployment model**:</span></span>

- <span data-ttu-id="29acd-130">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="29acd-130">Resource Manager</span></span>

> [!NOTE]
> <span data-ttu-id="29acd-131">Automatyczne kopie zapasowe opiera się na powitania **rozszerzenia agenta programu SQL Server IaaS**.</span><span class="sxs-lookup"><span data-stu-id="29acd-131">Automated Backup relies on hello **SQL Server IaaS Agent Extension**.</span></span> <span data-ttu-id="29acd-132">Bieżący obrazów Galeria maszyny wirtualnej SQL dodać to rozszerzenie domyślnie.</span><span class="sxs-lookup"><span data-stu-id="29acd-132">Current SQL virtual machine gallery images add this extension by default.</span></span> <span data-ttu-id="29acd-133">Aby uzyskać więcej informacji, zobacz [rozszerzenia agenta programu SQL Server IaaS](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="29acd-133">For more information, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="29acd-134">Ustawienia</span><span class="sxs-lookup"><span data-stu-id="29acd-134">Settings</span></span>
<span data-ttu-id="29acd-135">Witaj poniższej tabeli opisano opcje hello, które można skonfigurować do automatycznego tworzenia kopii zapasowej w wersji 2.</span><span class="sxs-lookup"><span data-stu-id="29acd-135">hello following table describes hello options that can be configured for Automated Backup v2.</span></span> <span data-ttu-id="29acd-136">kroki rzeczywista konfiguracja Hello się różnić w zależności od tego, czy używać hello portalu Azure lub poleceń programu Windows PowerShell dla usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="29acd-136">hello actual configuration steps vary depending on whether you use hello Azure portal or Azure Windows PowerShell commands.</span></span>

### <a name="basic-settings"></a><span data-ttu-id="29acd-137">Ustawienia podstawowe</span><span class="sxs-lookup"><span data-stu-id="29acd-137">Basic Settings</span></span>

| <span data-ttu-id="29acd-138">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="29acd-138">Setting</span></span> | <span data-ttu-id="29acd-139">Zakres (ustawienie domyślne)</span><span class="sxs-lookup"><span data-stu-id="29acd-139">Range (Default)</span></span> | <span data-ttu-id="29acd-140">Opis</span><span class="sxs-lookup"><span data-stu-id="29acd-140">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="29acd-141">**Automatyczne kopie zapasowe**</span><span class="sxs-lookup"><span data-stu-id="29acd-141">**Automated Backup**</span></span> | <span data-ttu-id="29acd-142">Włącza/wyłącza (wyłączone)</span><span class="sxs-lookup"><span data-stu-id="29acd-142">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="29acd-143">Włącza lub wyłącza funkcję automatycznego tworzenia kopii zapasowej dla maszyny Wirtualnej platformy Azure, programem SQL Server 2016 Standard lub Enterprise.</span><span class="sxs-lookup"><span data-stu-id="29acd-143">Enables or disables Automated Backup for an Azure VM running SQL Server 2016 Standard or Enterprise.</span></span> |
| <span data-ttu-id="29acd-144">**Okres przechowywania**</span><span class="sxs-lookup"><span data-stu-id="29acd-144">**Retention Period**</span></span> | <span data-ttu-id="29acd-145">1 do 30 dni (30 dni)</span><span class="sxs-lookup"><span data-stu-id="29acd-145">1-30 days (30 days)</span></span> | <span data-ttu-id="29acd-146">Witaj liczbę kopii zapasowych tooretain dni.</span><span class="sxs-lookup"><span data-stu-id="29acd-146">hello number of days tooretain backups.</span></span> |
| <span data-ttu-id="29acd-147">**Konto magazynu**</span><span class="sxs-lookup"><span data-stu-id="29acd-147">**Storage Account**</span></span> | <span data-ttu-id="29acd-148">Konto magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="29acd-148">Azure storage account</span></span> | <span data-ttu-id="29acd-149">Toouse konto magazynu Azure do przechowywania plików automatycznego tworzenia kopii zapasowej w magazynie obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="29acd-149">An Azure storage account toouse for storing Automated Backup files in blob storage.</span></span> <span data-ttu-id="29acd-150">Kontener jest tworzony w tej lokalizacji toostore wszystkie pliki kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="29acd-150">A container is created at this location toostore all backup files.</span></span> <span data-ttu-id="29acd-151">Plik kopii zapasowej Hello konwencji nazewnictwa obejmuje hello daty, godziny i identyfikator GUID bazy danych.</span><span class="sxs-lookup"><span data-stu-id="29acd-151">hello backup file naming convention includes hello date, time, and database GUID.</span></span> |
| <span data-ttu-id="29acd-152">**Szyfrowanie**</span><span class="sxs-lookup"><span data-stu-id="29acd-152">**Encryption**</span></span> |<span data-ttu-id="29acd-153">Włącza/wyłącza (wyłączone)</span><span class="sxs-lookup"><span data-stu-id="29acd-153">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="29acd-154">Włącza lub wyłącza funkcję szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="29acd-154">Enables or disables encryption.</span></span> <span data-ttu-id="29acd-155">Po włączeniu szyfrowania hello używane certyfikaty toorestore hello w kopii zapasowej znajdują się w hello określony magazynu konta w hello sam **automaticbackup** przy użyciu kontenera hello tej samej konwencji nazewnictwa.</span><span class="sxs-lookup"><span data-stu-id="29acd-155">When encryption is enabled, hello certificates used toorestore hello backup are located in hello specified storage account in hello same **automaticbackup** container using hello same naming convention.</span></span> <span data-ttu-id="29acd-156">Zmiana hasła hello nowego certyfikatu jest generowana za pomocą tego hasła, ale hello stary certyfikat pozostaje toorestore poprzednich kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="29acd-156">If hello password changes, a new certificate is generated with that password, but hello old certificate remains toorestore prior backups.</span></span> |
| <span data-ttu-id="29acd-157">**Hasło**</span><span class="sxs-lookup"><span data-stu-id="29acd-157">**Password**</span></span> |<span data-ttu-id="29acd-158">Tekst hasła</span><span class="sxs-lookup"><span data-stu-id="29acd-158">Password text</span></span> | <span data-ttu-id="29acd-159">Hasło dla kluczy szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="29acd-159">A password for encryption keys.</span></span> <span data-ttu-id="29acd-160">Jest to tylko wymagane, jeśli jest włączone szyfrowanie.</span><span class="sxs-lookup"><span data-stu-id="29acd-160">This is only required if encryption is enabled.</span></span> <span data-ttu-id="29acd-161">W kolejności toorestore zaszyfrowanej kopii zapasowej, trzeba hello prawidłowe hasło i powiązane certyfikatu, który został użyty w czasie hello hello tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="29acd-161">In order toorestore an encrypted backup, you must have hello correct password and related certificate that was used at hello time hello backup was taken.</span></span> |

### <a name="advanced-settings"></a><span data-ttu-id="29acd-162">Ustawienia zaawansowane</span><span class="sxs-lookup"><span data-stu-id="29acd-162">Advanced Settings</span></span>

| <span data-ttu-id="29acd-163">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="29acd-163">Setting</span></span> | <span data-ttu-id="29acd-164">Zakres (ustawienie domyślne)</span><span class="sxs-lookup"><span data-stu-id="29acd-164">Range (Default)</span></span> | <span data-ttu-id="29acd-165">Opis</span><span class="sxs-lookup"><span data-stu-id="29acd-165">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="29acd-166">**Kopie zapasowe bazy danych systemu**</span><span class="sxs-lookup"><span data-stu-id="29acd-166">**System Database Backups**</span></span> | <span data-ttu-id="29acd-167">Włącza/wyłącza (wyłączone)</span><span class="sxs-lookup"><span data-stu-id="29acd-167">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="29acd-168">Po włączeniu tej funkcji będzie również wykonać kopię zapasową hello systemowych baz danych: Master, MSDB i modelu.</span><span class="sxs-lookup"><span data-stu-id="29acd-168">When enabled, this feature will also back up hello system databases: Master, MSDB, and Model.</span></span> <span data-ttu-id="29acd-169">Witaj MSDB i baz danych modelu Sprawdź, czy są w trybie odzyskiwania pełnego Jeśli chcesz, aby podjąć toobe kopii zapasowych dziennika.</span><span class="sxs-lookup"><span data-stu-id="29acd-169">For hello MSDB and Model databases, verify that they are in full recovery mode if you want log backups toobe taken.</span></span> <span data-ttu-id="29acd-170">Kopie zapasowe dziennika nigdy nie są wykonywane dla głównego.</span><span class="sxs-lookup"><span data-stu-id="29acd-170">Log backups are never taken for Master.</span></span> <span data-ttu-id="29acd-171">A nie kopii zapasowych są wykonywane dla bazy danych TempDB.</span><span class="sxs-lookup"><span data-stu-id="29acd-171">And no backups are taken for TempDB.</span></span> |
| <span data-ttu-id="29acd-172">**Harmonogram tworzenia kopii zapasowych**</span><span class="sxs-lookup"><span data-stu-id="29acd-172">**Backup Schedule**</span></span> | <span data-ttu-id="29acd-173">Ręczne/automatycznego (automatycznego)</span><span class="sxs-lookup"><span data-stu-id="29acd-173">Manual/Automated (Automated)</span></span> | <span data-ttu-id="29acd-174">Domyślnie hello harmonogram tworzenia kopii zapasowych będzie automatycznie ustalana na podstawie hello wzrostu dziennika.</span><span class="sxs-lookup"><span data-stu-id="29acd-174">By default, hello backup schedule will be automatically determined based on hello log growth.</span></span> <span data-ttu-id="29acd-175">Ręczne harmonogram tworzenia kopii zapasowych umożliwia przedział czasu hello hello użytkownika toospecify kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="29acd-175">Manual backup schedule allows hello user toospecify hello time window for backups.</span></span> <span data-ttu-id="29acd-176">W takim przypadku tylko potrwa kopii zapasowych stosowane na powitania określona częstotliwość i podczas hello określony przedział czasu danego dnia.</span><span class="sxs-lookup"><span data-stu-id="29acd-176">In this case, backups will only ever take place at hello specified frequency and during hello specified time window of a given day.</span></span> |
| <span data-ttu-id="29acd-177">**Częstotliwość tworzenia pełnej kopii zapasowej**</span><span class="sxs-lookup"><span data-stu-id="29acd-177">**Full backup frequency**</span></span> | <span data-ttu-id="29acd-178">Codziennie/co tydzień</span><span class="sxs-lookup"><span data-stu-id="29acd-178">Daily/Weekly</span></span> | <span data-ttu-id="29acd-179">Częstotliwość tworzenia pełnych kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="29acd-179">Frequency of full backups.</span></span> <span data-ttu-id="29acd-180">W obu przypadkach pełne kopie zapasowe rozpocznie się podczas następnego okna zaplanowanej czasie hello.</span><span class="sxs-lookup"><span data-stu-id="29acd-180">In both cases, full backups will begin during hello next scheduled time window.</span></span> <span data-ttu-id="29acd-181">Po wybraniu co tydzień kopii zapasowych może obejmować wiele dni, dopóki wszystkie bazy danych pomyślnie wykonano kopię zapasową.</span><span class="sxs-lookup"><span data-stu-id="29acd-181">When weekly is selected, backups could span multiple days until all databases have successfully backed up.</span></span> |
| <span data-ttu-id="29acd-182">**Czas rozpoczęcia pełnej kopii zapasowej**</span><span class="sxs-lookup"><span data-stu-id="29acd-182">**Full backup start time**</span></span> | <span data-ttu-id="29acd-183">00:00 – 23:00 (01:00)</span><span class="sxs-lookup"><span data-stu-id="29acd-183">00:00 – 23:00 (01:00)</span></span> | <span data-ttu-id="29acd-184">Godzina rozpoczęcia dotyczącego danego dnia, w którym pełnych kopii zapasowych może mieć miejsce.</span><span class="sxs-lookup"><span data-stu-id="29acd-184">Start time of a given day during which full backups can take place.</span></span> |
| <span data-ttu-id="29acd-185">**Przedział czasu tworzenia pełnej kopii zapasowej**</span><span class="sxs-lookup"><span data-stu-id="29acd-185">**Full backup time window**</span></span> | <span data-ttu-id="29acd-186">1 – 23 godzin (1 godz.)</span><span class="sxs-lookup"><span data-stu-id="29acd-186">1 – 23 hours (1 hour)</span></span> | <span data-ttu-id="29acd-187">Czas trwania okna czasu hello danego dnia, w którym pełnych kopii zapasowych może mieć miejsce.</span><span class="sxs-lookup"><span data-stu-id="29acd-187">Duration of hello time window of a given day during which full backups can take place.</span></span> |
| <span data-ttu-id="29acd-188">**Częstotliwość wykonywania kopii zapasowych dziennika**</span><span class="sxs-lookup"><span data-stu-id="29acd-188">**Log backup frequency**</span></span> | <span data-ttu-id="29acd-189">5 – 60 minut (60 minut)</span><span class="sxs-lookup"><span data-stu-id="29acd-189">5 – 60 minutes (60 minutes)</span></span> | <span data-ttu-id="29acd-190">Częstotliwość tworzenia kopii zapasowych dziennika.</span><span class="sxs-lookup"><span data-stu-id="29acd-190">Frequency of log backups.</span></span> |

## <a name="understanding-full-backup-frequency"></a><span data-ttu-id="29acd-191">Opis częstotliwość tworzenia pełnej kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="29acd-191">Understanding full backup frequency</span></span>
<span data-ttu-id="29acd-192">Jest ważne toounderstand hello różnica między codziennie i cotygodniowych pełnych kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="29acd-192">It is important toounderstand hello difference between daily and weekly full backups.</span></span> <span data-ttu-id="29acd-193">W tym wysiłku opisano dwa przykładowe scenariusze.</span><span class="sxs-lookup"><span data-stu-id="29acd-193">In this effort, we will walk through two example scenarios.</span></span>

### <a name="scenario-1-weekly-backups"></a><span data-ttu-id="29acd-194">Scenariusz 1: Cotygodniowe kopie zapasowe</span><span class="sxs-lookup"><span data-stu-id="29acd-194">Scenario 1: Weekly backups</span></span>
<span data-ttu-id="29acd-195">Masz zawierającą liczbę bardzo dużych baz danych maszyny Wirtualnej serwera SQL.</span><span class="sxs-lookup"><span data-stu-id="29acd-195">You have a SQL Server VM which contains a number of very large databases.</span></span>

<span data-ttu-id="29acd-196">W poniedziałek możesz włączyć automatyczna usługa Backup v2 z hello następujące ustawienia:</span><span class="sxs-lookup"><span data-stu-id="29acd-196">On Monday, you enable Automated Backup v2 with hello following settings:</span></span>

- <span data-ttu-id="29acd-197">Harmonogram tworzenia kopii zapasowych: **ręczne**</span><span class="sxs-lookup"><span data-stu-id="29acd-197">Backup schedule: **Manual**</span></span>
- <span data-ttu-id="29acd-198">Pełnej kopii zapasowej częstotliwości: **co tydzień**</span><span class="sxs-lookup"><span data-stu-id="29acd-198">Full backup frequency: **Weekly**</span></span>
- <span data-ttu-id="29acd-199">Czas rozpoczęcia tworzenia kopii zapasowej pełnej: **01:00**</span><span class="sxs-lookup"><span data-stu-id="29acd-199">Full backup start time: **01:00**</span></span>
- <span data-ttu-id="29acd-200">Przedział czasu tworzenia pełnej kopii zapasowej: **1 godzina**</span><span class="sxs-lookup"><span data-stu-id="29acd-200">Full backup time window: **1 hour**</span></span>

<span data-ttu-id="29acd-201">Oznacza to, że ten hello dalej dostępne okna kopii zapasowej jest wtorek na 1: 00 1 godziny.</span><span class="sxs-lookup"><span data-stu-id="29acd-201">This means that hello next available backup window is Tuesday at 1 AM for 1 hour.</span></span> <span data-ttu-id="29acd-202">W tym czasie automatyczna usługa Backup rozpocznie się wykonywanie kopii zapasowych baz danych jednego naraz.</span><span class="sxs-lookup"><span data-stu-id="29acd-202">At that time, Automated Backup will begin backing up your databases one at a time.</span></span> <span data-ttu-id="29acd-203">W tym scenariuszu baz danych są wystarczająco duże, ukończy pełne kopie zapasowe baz danych hello pierwszy kilku.</span><span class="sxs-lookup"><span data-stu-id="29acd-203">In this scenario, your databases are large enough that full backups will complete for hello first couple databases.</span></span> <span data-ttu-id="29acd-204">Jednak po godzinie nie wszystkie bazy danych hello utworzone kopie zapasowe.</span><span class="sxs-lookup"><span data-stu-id="29acd-204">However, after one hour not all of hello databases have been backed up.</span></span>

<span data-ttu-id="29acd-205">W takim przypadku automatyczna usługa Backup rozpocznie się wykonywanie kopii zapasowych hello pozostałych hello baz danych z następnego dnia, środę o godzinie 1: 00 1 godziny.</span><span class="sxs-lookup"><span data-stu-id="29acd-205">When this happens, Automated Backup will begin backing up hello remaining databases hello next day, Wednesday at 1 AM for 1 hour.</span></span> <span data-ttu-id="29acd-206">Jeśli nie wszystkie bazy danych utworzone kopie zapasowe w tym czasie, spróbuje następnego dnia o hello ponownie Witaj, sam czas.</span><span class="sxs-lookup"><span data-stu-id="29acd-206">If not all databases have been backed up in that time, it will try again hello next day at hello same time.</span></span> <span data-ttu-id="29acd-207">Operacja będzie kontynuowana, dopóki wszystkie bazy danych zostały pomyślnie kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="29acd-207">This will continue until all databases have been successfully backed up.</span></span>

<span data-ttu-id="29acd-208">Gdy osiągnie ona wtorek ponownie, automatyczna usługa Backup rozpocznie się wykonywanie kopii zapasowych wszystkich baz danych ponownie.</span><span class="sxs-lookup"><span data-stu-id="29acd-208">Once it reaches Tuesday again, Automated Backup will begin backing up all databases once again.</span></span>

<span data-ttu-id="29acd-209">W tym scenariuszu pokazano, że automatyczna usługa Backup działa jedynie w hello określone okno czasu, a każda baza danych zostaną skopiowane nawet, jeden raz w tygodniu.</span><span class="sxs-lookup"><span data-stu-id="29acd-209">This scenario shows that Automated Backup will only operate within hello specified time window, and each database will be backed up once per week.</span></span> <span data-ttu-id="29acd-210">To także wskazuje, że jest to możliwe dla toospan kopie zapasowe wielu dni w hello przypadek gdy nie jest możliwe toocomplete wszystkie kopie zapasowe w jednym dniu.</span><span class="sxs-lookup"><span data-stu-id="29acd-210">This also shows that it is possible for backups toospan multiple days in hello case where it is not possible toocomplete all backups in a single day.</span></span>

### <a name="scenario-2-daily-backups"></a><span data-ttu-id="29acd-211">Scenariusz 2: Codzienne wykonywanie kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="29acd-211">Scenario 2: Daily backups</span></span>
<span data-ttu-id="29acd-212">Masz zawierającą liczbę bardzo dużych baz danych maszyny Wirtualnej serwera SQL.</span><span class="sxs-lookup"><span data-stu-id="29acd-212">You have a SQL Server VM which contains a number of very large databases.</span></span>

<span data-ttu-id="29acd-213">W poniedziałek możesz włączyć automatyczna usługa Backup v2 z hello następujące ustawienia:</span><span class="sxs-lookup"><span data-stu-id="29acd-213">On Monday, you enable Automated Backup v2 with hello following settings:</span></span>

- <span data-ttu-id="29acd-214">Harmonogram tworzenia kopii zapasowych: ręczne</span><span class="sxs-lookup"><span data-stu-id="29acd-214">Backup schedule: Manual</span></span>
- <span data-ttu-id="29acd-215">Pełnej kopii zapasowej częstotliwości: codziennie</span><span class="sxs-lookup"><span data-stu-id="29acd-215">Full backup frequency: Daily</span></span>
- <span data-ttu-id="29acd-216">Czas rozpoczęcia tworzenia kopii zapasowej pełnej: 22:00</span><span class="sxs-lookup"><span data-stu-id="29acd-216">Full backup start time: 22:00</span></span>
- <span data-ttu-id="29acd-217">Przedział czasu tworzenia pełnej kopii zapasowej: 6 godzin</span><span class="sxs-lookup"><span data-stu-id="29acd-217">Full backup time window: 6 hours</span></span>

<span data-ttu-id="29acd-218">Oznacza to, że ten hello dalej dostępne okna kopii zapasowej jest poniedziałek godzinie 10 przez 6 godzin.</span><span class="sxs-lookup"><span data-stu-id="29acd-218">This means that hello next available backup window is Monday at 10 PM for 6 hours.</span></span> <span data-ttu-id="29acd-219">W tym czasie automatyczna usługa Backup rozpocznie się wykonywanie kopii zapasowych baz danych jednego naraz.</span><span class="sxs-lookup"><span data-stu-id="29acd-219">At that time, Automated Backup will begin backing up your databases one at a time.</span></span>

<span data-ttu-id="29acd-220">Następnie wtorek 10 przez 6 godzin, pełne kopie zapasowe wszystkich baz danych zostanie uruchomiony ponownie.</span><span class="sxs-lookup"><span data-stu-id="29acd-220">Then, on Tuesday at 10 for 6 hours, full backups of all databases will start again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="29acd-221">Podczas planowania codzienne wykonywanie kopii zapasowych, zaleca się zaplanowanie tooensure okno czasu szerokości, wszystkie bazy danych można kopii zapasowej, w tym czasie.</span><span class="sxs-lookup"><span data-stu-id="29acd-221">When scheduling daily backups, it is recommended that you schedule a wide time window tooensure all databases can be backed up within this time.</span></span> <span data-ttu-id="29acd-222">Jest to szczególnie ważne w przypadku hello, w którym znajduje się duża ilość danych tooback się.</span><span class="sxs-lookup"><span data-stu-id="29acd-222">This is especially important in hello case where you have a large amount of data tooback up.</span></span>

## <a name="configuration-in-hello-portal"></a><span data-ttu-id="29acd-223">Konfiguracja w hello portalu</span><span class="sxs-lookup"><span data-stu-id="29acd-223">Configuration in hello Portal</span></span>

<span data-ttu-id="29acd-224">Możesz użyć hello Azure tooconfigure portalu automatyczna usługa Backup v2 podczas inicjowania obsługi lub dla maszyn wirtualnych istniejącego programu SQL Server 2016.</span><span class="sxs-lookup"><span data-stu-id="29acd-224">You can use hello Azure portal tooconfigure Automated Backup v2 during provisioning or for existing SQL Server 2016 VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="29acd-225">Nowe maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="29acd-225">New VMs</span></span>

<span data-ttu-id="29acd-226">Podczas tworzenia nowej maszyny wirtualnej 2016 serwera SQL w modelu wdrażania usługi Resource Manager hello, należy użyć hello automatyczna usługa Backup tooconfigure portalu Azure w wersji 2.</span><span class="sxs-lookup"><span data-stu-id="29acd-226">Use hello Azure portal tooconfigure Automated Backup v2 when you create a new SQL Server 2016 Virtual Machine in hello Resource Manager deployment model.</span></span> 

<span data-ttu-id="29acd-227">W hello **ustawienia programu SQL Server** bloku, wybierz opcję **automatyczne kopie zapasowe**.</span><span class="sxs-lookup"><span data-stu-id="29acd-227">In hello **SQL Server settings** blade, select **Automated backup**.</span></span> <span data-ttu-id="29acd-228">Witaj Poniższy zrzut ekranu portalu Azure zawiera hello **SQL automatyczna usługa Backup** bloku.</span><span class="sxs-lookup"><span data-stu-id="29acd-228">hello following Azure portal screenshot shows hello **SQL Automated Backup** blade.</span></span>

![Konfiguracja SQL automatyczna usługa Backup w portalu Azure](./media/virtual-machines-windows-sql-automated-backup-v2/automated-backup-blade.png)

> [!NOTE]
> <span data-ttu-id="29acd-230">Automatycznego tworzenia kopii zapasowej v2 jest domyślnie wyłączona.</span><span class="sxs-lookup"><span data-stu-id="29acd-230">Automated Backup v2 is disabled by default.</span></span>

<span data-ttu-id="29acd-231">Dla kontekstu, zobacz temat pełną hello na [obsługi maszyny wirtualnej programu SQL Server na platformie Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="29acd-231">For context, see hello complete topic on [provisioning a SQL Server virtual machine in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="29acd-232">Istniejące maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="29acd-232">Existing VMs</span></span>

<span data-ttu-id="29acd-233">W przypadku istniejących maszyn wirtualnych programu SQL Server należy wybrać maszyny wirtualnej programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="29acd-233">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="29acd-234">Następnie wybierz hello **konfigurację programu SQL Server** sekcji hello **ustawienia** bloku.</span><span class="sxs-lookup"><span data-stu-id="29acd-234">Then select hello **SQL Server configuration** section of hello **Settings** blade.</span></span>

![SQL automatyczna usługa Backup dla istniejących maszyn wirtualnych](./media/virtual-machines-windows-sql-automated-backup-v2/sql-server-configuration.png)

<span data-ttu-id="29acd-236">W hello **konfigurację programu SQL Server** bloku, kliknij hello **Edytuj** przycisku na powitania automatycznego tworzenia kopii zapasowej sekcji.</span><span class="sxs-lookup"><span data-stu-id="29acd-236">In hello **SQL Server configuration** blade, click hello **Edit** button in hello Automated backup section.</span></span>

![Konfigurowanie kopii zapasowej SQL automatycznego dla istniejących maszyn wirtualnych](./media/virtual-machines-windows-sql-automated-backup-v2/sql-server-configuration-edit.png)

<span data-ttu-id="29acd-238">Po zakończeniu kliknij przycisk hello **OK** przycisk u dołu hello hello **konfigurację programu SQL Server** toosave bloku zmiany.</span><span class="sxs-lookup"><span data-stu-id="29acd-238">When finished, click hello **OK** button on hello bottom of hello **SQL Server configuration** blade toosave your changes.</span></span>

<span data-ttu-id="29acd-239">Jeśli włączasz automatyczna usługa Backup dla powitania po raz pierwszy, Azure konfiguruje hello Agent środowiska IaaS programu SQL Server w tle hello.</span><span class="sxs-lookup"><span data-stu-id="29acd-239">If you are enabling Automated Backup for hello first time, Azure configures hello SQL Server IaaS Agent in hello background.</span></span> <span data-ttu-id="29acd-240">W tym czasie hello portalu Azure może nie informować, że skonfigurowano automatycznego tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="29acd-240">During this time, hello Azure portal might not show that Automated Backup is configured.</span></span> <span data-ttu-id="29acd-241">Poczekaj kilka minut dla hello toobe agent zainstalowany, skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="29acd-241">Wait several minutes for hello agent toobe installed, configured.</span></span> <span data-ttu-id="29acd-242">Po tym hello Azure portalu będzie odzwierciedlać hello nowych ustawień.</span><span class="sxs-lookup"><span data-stu-id="29acd-242">After that hello Azure portal will reflect hello new settings.</span></span>

## <a name="configuration-with-powershell"></a><span data-ttu-id="29acd-243">Konfiguracja przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="29acd-243">Configuration with PowerShell</span></span>

<span data-ttu-id="29acd-244">Można użyć programu PowerShell tooconfigure v2 automatycznego tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="29acd-244">You can use PowerShell tooconfigure Automated Backup v2.</span></span> <span data-ttu-id="29acd-245">Przed rozpoczęciem należy:</span><span class="sxs-lookup"><span data-stu-id="29acd-245">Before you begin, you must:</span></span>

- <span data-ttu-id="29acd-246">[Pobierz i zainstaluj najnowsze programu Azure PowerShell hello](http://aka.ms/webpi-azps).</span><span class="sxs-lookup"><span data-stu-id="29acd-246">[Download and install hello latest Azure PowerShell](http://aka.ms/webpi-azps).</span></span>
- <span data-ttu-id="29acd-247">Otwórz program Windows PowerShell i skojarzyć go z Twoim kontem.</span><span class="sxs-lookup"><span data-stu-id="29acd-247">Open Windows PowerShell and associate it with your account.</span></span> <span data-ttu-id="29acd-248">Aby to zrobić, wykonaj czynności hello w hello [skonfiguruj subskrypcję](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) sekcji hello inicjowania obsługi administracyjnej tematu.</span><span class="sxs-lookup"><span data-stu-id="29acd-248">You can do this by following hello steps in hello [Configure your subscription](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) section of hello provisioning topic.</span></span>

### <a name="install-hello-sql-iaas-extension"></a><span data-ttu-id="29acd-249">Zainstaluj hello rozszerzenia IaaS SQL</span><span class="sxs-lookup"><span data-stu-id="29acd-249">Install hello SQL IaaS Extension</span></span>
<span data-ttu-id="29acd-250">Jeśli aprowizowanej maszyny wirtualnej programu SQL Server z portalu Azure hello hello rozszerzenie IaaS serwera SQL powinno być już zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="29acd-250">If you provisioned a SQL Server virtual machine from hello Azure portal, hello SQL Server IaaS Extension should already be installed.</span></span> <span data-ttu-id="29acd-251">Można określić, czy jest ona instalowana dla maszyny Wirtualnej przez wywołanie metody **Get-AzureRmVM** polecenia i sprawdzeniu hello **rozszerzenia** właściwości.</span><span class="sxs-lookup"><span data-stu-id="29acd-251">You can determine if it is installed for your VM by calling **Get-AzureRmVM** command and examining hello **Extensions** property.</span></span>

```powershell
$vmname = "vmname"
$resourcegroupname = "resourcegroupname"

(Get-AzureRmVM -Name $vmname -ResourceGroupName $resourcegroupname).Extensions 
```

<span data-ttu-id="29acd-252">Jeśli zainstalowano hello rozszerzenia SQL Server IaaS Agent, powinien pojawić się wymienionym "SqlIaaSAgent" lub "SQLIaaSExtension".</span><span class="sxs-lookup"><span data-stu-id="29acd-252">If hello SQL Server IaaS Agent extension is installed, you should see it listed as “SqlIaaSAgent” or “SQLIaaSExtension”.</span></span> <span data-ttu-id="29acd-253">**ProvisioningState** dla rozszerzenia hello również powinny być widoczne "Powodzenie".</span><span class="sxs-lookup"><span data-stu-id="29acd-253">**ProvisioningState** for hello extension should also show “Succeeded”.</span></span> 

<span data-ttu-id="29acd-254">Jeśli nie jest zainstalowany lub nie można zainicjować obsługi administracyjnej toobe, należy zainstalować go z hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="29acd-254">If it is not installed or failed toobe provisioned, you can install it with hello following command.</span></span> <span data-ttu-id="29acd-255">Dodanie toohello wirtualna Nazwa zasobu grupy i, należy także określić hello region (**$region**) maszyny Wirtualnej znajdujący się w.</span><span class="sxs-lookup"><span data-stu-id="29acd-255">In addition toohello VM name and resource group, you must also specify hello region (**$region**) that your VM is located in.</span></span>

```powershell
$region = “EASTUS2”
Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region 
```

### <span data-ttu-id="29acd-256"><a id="verifysettings"></a>Sprawdź bieżące ustawienia</span><span class="sxs-lookup"><span data-stu-id="29acd-256"><a id="verifysettings"></a> Verify current settings</span></span>
<span data-ttu-id="29acd-257">Jeśli włączono automatyczne kopie zapasowe podczas inicjowania obsługi, można użyć programu PowerShell toocheck bieżącej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="29acd-257">If you enabled automated backup during provisioning, you can use PowerShell toocheck your current configuration.</span></span> <span data-ttu-id="29acd-258">Uruchom hello **Get-AzureRmVMSqlServerExtension** polecenia i sprawdź, czy hello **AutoBackupSettings** właściwości:</span><span class="sxs-lookup"><span data-stu-id="29acd-258">Run hello **Get-AzureRmVMSqlServerExtension** command and examine hello **AutoBackupSettings** property:</span></span>

```powershell
(Get-AzureRmVMSqlServerExtension -VMName $vmname -ResourceGroupName $resourcegroupname).AutoBackupSettings
```

<span data-ttu-id="29acd-259">Należy pobrać dane wyjściowe podobne toohello poniżej:</span><span class="sxs-lookup"><span data-stu-id="29acd-259">You should get output similar toohello following:</span></span>

```
Enable                      : True
EnableEncryption            : False
RetentionPeriod             : 30
StorageUrl                  : https://test.blob.core.windows.net/
StorageAccessKey            :  
Password                    : 
BackupSystemDbs             : False
BackupScheduleType          : Manual
FullBackupFrequency         : WEEKLY
FullBackupStartTime         : 2
FullBackupWindowHours       : 2
LogBackupFrequency          : 60
```

<span data-ttu-id="29acd-260">Jeśli dane wyjściowe wskazuje, że **włączyć** ustawiono zbyt**False**, następnie tooenable automatyczne kopie zapasowe.</span><span class="sxs-lookup"><span data-stu-id="29acd-260">If your output shows that **Enable** is set too**False**, then you have tooenable automated backup.</span></span> <span data-ttu-id="29acd-261">Witaj szczęście jest włączone, a następnie skonfiguruj automatyczne kopie zapasowe w hello tak samo.</span><span class="sxs-lookup"><span data-stu-id="29acd-261">hello good news is that you enable and configure Automated Backup in hello same way.</span></span> <span data-ttu-id="29acd-262">Zobacz następną sekcję hello tych informacji.</span><span class="sxs-lookup"><span data-stu-id="29acd-262">See hello next section for this information.</span></span>

> [!NOTE] 
> <span data-ttu-id="29acd-263">Jeśli natychmiast po wprowadzeniu zmiany można sprawdzić ustawienia hello, istnieje możliwość, że wystąpi ponownie hello starych wartości konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="29acd-263">If you check hello settings immediately after making a change, it is possible that you will get back hello old configuration values.</span></span> <span data-ttu-id="29acd-264">Poczekaj kilka minut i sprawdź ustawienia hello ponownie toomake się upewnić, że zmiany zostały zastosowane.</span><span class="sxs-lookup"><span data-stu-id="29acd-264">Wait a few minutes and check hello settings again toomake sure that your changes were applied.</span></span>

### <a name="configure-automated-backup-v2"></a><span data-ttu-id="29acd-265">Konfigurowanie automatycznego tworzenia kopii zapasowej v2</span><span class="sxs-lookup"><span data-stu-id="29acd-265">Configure Automated Backup v2</span></span>
<span data-ttu-id="29acd-266">Umożliwia tooenable PowerShell automatyczne kopie zapasowe, a także toomodify jego konfiguracji i zachowania w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="29acd-266">You can use PowerShell tooenable Automated Backup as well as toomodify its configuration and behavior at any time.</span></span> 

<span data-ttu-id="29acd-267">Najpierw wybierz lub Utwórz konto magazynu dla hello pliki kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="29acd-267">First, select or create a storage account for hello backup files.</span></span> <span data-ttu-id="29acd-268">Witaj poniższy skrypt wybiera konto magazynu lub utworzenie go, jeśli nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="29acd-268">hello following script selects a storage account or creates it if it does not exist.</span></span>

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
> <span data-ttu-id="29acd-269">Automatyczne kopie zapasowe nie obsługuje przechowywania kopii zapasowych w magazynie premium, ale może potrwać kopii zapasowych z dysków maszyny Wirtualnej, które używają magazyn w warstwie Premium.</span><span class="sxs-lookup"><span data-stu-id="29acd-269">Automated Backup does not support storing backups in premium storage, but it can take backups from VM disks which use Premium Storage.</span></span>

<span data-ttu-id="29acd-270">Następnie użyj hello **AzureRmVMSqlServerAutoBackupConfig nowy** polecenia tooenable i skonfigurować kopie zapasowe toostore ustawienia hello v2 automatycznego tworzenia kopii zapasowej w hello kontem magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="29acd-270">Then use hello **New-AzureRmVMSqlServerAutoBackupConfig** command tooenable and configure hello Automated Backup v2 settings toostore backups in hello Azure storage account.</span></span> <span data-ttu-id="29acd-271">W tym przykładzie hello kopie zapasowe są ustawiane toobe przechowywane przez 10 dni.</span><span class="sxs-lookup"><span data-stu-id="29acd-271">In this example, hello backups are set toobe retained for 10 days.</span></span> <span data-ttu-id="29acd-272">Kopie zapasowe bazy danych systemu są włączone.</span><span class="sxs-lookup"><span data-stu-id="29acd-272">System database backups are enabled.</span></span> <span data-ttu-id="29acd-273">Pełne kopie zapasowe są zaplanowane co tydzień w oknie Uruchamianie 20:00 do dwóch godzin.</span><span class="sxs-lookup"><span data-stu-id="29acd-273">Full backups are scheduled for weekly with a time window starting at 20:00 for two hours.</span></span> <span data-ttu-id="29acd-274">Zaplanowane kopie zapasowe dziennika co 30 minut.</span><span class="sxs-lookup"><span data-stu-id="29acd-274">Log backups are scheduled for every 30 minutes.</span></span> <span data-ttu-id="29acd-275">drugie polecenie Hello **AzureRmVMSqlServerExtension zestaw**, hello aktualizacji określonej maszyny Wirtualnej platformy Azure przy użyciu tych ustawień.</span><span class="sxs-lookup"><span data-stu-id="29acd-275">hello second command, **Set-AzureRmVMSqlServerExtension**, updates hello specified Azure VM with these settings.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType Manual -FullBackupFrequency Weekly `
    -FullBackupStartHour 20 -FullBackupWindowInHours 2 `
    -LogBackupFrequencyInMinutes 30 

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname 
```

<span data-ttu-id="29acd-276">Go może potrwać kilka minut tooinstall i skonfiguruj hello Agent środowiska IaaS programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="29acd-276">It could take several minutes tooinstall and configure hello SQL Server IaaS Agent.</span></span> 

<span data-ttu-id="29acd-277">szyfrowania tooenable zmodyfikować hello poprzedniej skryptu toopass hello **EnableEncryption** parametru wraz z hasła (bezpieczny ciąg) hello **CertificatePassword** parametru.</span><span class="sxs-lookup"><span data-stu-id="29acd-277">tooenable encryption, modify hello previous script toopass hello **EnableEncryption** parameter along with a password (secure string) for hello **CertificatePassword** parameter.</span></span> <span data-ttu-id="29acd-278">Witaj poniższy skrypt umożliwia hello ustawienia automatycznego tworzenia kopii zapasowej w poprzednim przykładzie hello i dodaje szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="29acd-278">hello following script enables hello Automated Backup settings in hello previous example and adds encryption.</span></span>

```powershell
$password = "P@ssw0rd"
$encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force  

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -EnableEncryption -CertificatePassword $encryptionpassword `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType Manual -FullBackupFrequency Weekly `
    -FullBackupStartHour 20 -FullBackupWindowInHours 2 `
    -LogBackupFrequencyInMinutes 30 

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

<span data-ttu-id="29acd-279">ustawienia są stosowane, tooconfirm [Sprawdź konfigurację automatycznego tworzenia kopii zapasowej hello](#verifysettings).</span><span class="sxs-lookup"><span data-stu-id="29acd-279">tooconfirm your settings are applied, [verify hello Automated Backup configuration](#verifysettings).</span></span>

### <a name="disable-automated-backup"></a><span data-ttu-id="29acd-280">Wyłącz automatyczne kopie zapasowe</span><span class="sxs-lookup"><span data-stu-id="29acd-280">Disable Automated Backup</span></span>
<span data-ttu-id="29acd-281">toodisable automatyczne kopie zapasowe, uruchom hello sam skrypt bez hello **-Włącz** toohello parametru **AzureRmVMSqlServerAutoBackupConfig nowy** polecenia.</span><span class="sxs-lookup"><span data-stu-id="29acd-281">toodisable Automated Backup, run hello same script without hello **-Enable** parameter toohello **New-AzureRmVMSqlServerAutoBackupConfig** command.</span></span> <span data-ttu-id="29acd-282">Witaj braku hello **-Włącz** parametru sygnały hello polecenia toodisable hello funkcji.</span><span class="sxs-lookup"><span data-stu-id="29acd-282">hello absence of hello **-Enable** parameter signals hello command toodisable hello feature.</span></span> <span data-ttu-id="29acd-283">Podobnie jak w przypadku instalacji, może upłynąć kilka minut toodisable automatyczne kopie zapasowe.</span><span class="sxs-lookup"><span data-stu-id="29acd-283">As with installation, it can take several minutes toodisable Automated Backup.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

### <a name="example-script"></a><span data-ttu-id="29acd-284">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="29acd-284">Example script</span></span>
<span data-ttu-id="29acd-285">Witaj poniższy skrypt zawiera zestaw zmiennych można dostosować tooenable i skonfiguruj automatyczne kopie zapasowe dla maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="29acd-285">hello following script provides a set of variables that you can customize tooenable and configure Automated Backup for your VM.</span></span> <span data-ttu-id="29acd-286">W Twoim przypadku może być konieczne skryptu hello toocustomize zgodnie z wymaganiami.</span><span class="sxs-lookup"><span data-stu-id="29acd-286">In your case, you might need toocustomize hello script based on your requirements.</span></span> <span data-ttu-id="29acd-287">Na przykład czy mają toomake zmiany, jeśli potrzebujesz kopii zapasowej hello toodisable systemowych baz danych lub włączyć szyfrowanie.</span><span class="sxs-lookup"><span data-stu-id="29acd-287">For example, you would have toomake changes if you wanted toodisable hello backup of system databases or enable encryption.</span></span>

```powershell
$vmname = "yourvmname"
$resourcegroupname = "vmresourcegroupname"
$region = “Azure region name such as EASTUS2”
$storage_accountname = “storageaccountname”
$storage_resourcegroupname = $resourcegroupname
$retentionperiod = 10
$backupscheduletype = "Manual"
$fullbackupfrequency = "Weekly"
$fullbackupstarthour = "20"
$fullbackupwindow = "2"
$logbackupfrequency = "30"

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
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType $backupscheduletype -FullBackupFrequency $fullbackupfrequency `
    -FullBackupStartHour $fullbackupstarthour -FullBackupWindowInHours $fullbackupwindow `
    -LogBackupFrequencyInMinutes $logbackupfrequency

# Apply hello Automated Backup settings toohello VM

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="29acd-288">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="29acd-288">Next steps</span></span>
<span data-ttu-id="29acd-289">Automatyczne v2 kopii zapasowej konfiguruje zarządzanej kopii zapasowej na maszynach wirtualnych Azure.</span><span class="sxs-lookup"><span data-stu-id="29acd-289">Automated Backup v2 configures Managed Backup on Azure VMs.</span></span> <span data-ttu-id="29acd-290">Dlatego ważne jest zbyt[hello dokumentacji zarządzanej kopii zapasowej](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello zachowanie i skutki.</span><span class="sxs-lookup"><span data-stu-id="29acd-290">So it is important too[review hello documentation for Managed Backup](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello behavior and implications.</span></span>

<span data-ttu-id="29acd-291">Można znaleźć dodatkowe kopii zapasowej i przywracanie wskazówki dotyczące programu SQL Server na maszynach wirtualnych Azure w hello kolejny temat: [kopii zapasowej i przywracania dla programu SQL Server w usłudze Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="29acd-291">You can find additional backup and restore guidance for SQL Server on Azure VMs in hello following topic: [Backup and Restore for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md).</span></span>

<span data-ttu-id="29acd-292">Informacje o innych zadaniach automatyzacji dostępny, zobacz [rozszerzenia agenta programu SQL Server IaaS](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="29acd-292">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

<span data-ttu-id="29acd-293">Aby uzyskać więcej informacji na temat uruchamiania programu SQL Server na maszynach wirtualnych Azure, zobacz [programu SQL Server na maszynach wirtualnych platformy Azure — omówienie](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="29acd-293">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

