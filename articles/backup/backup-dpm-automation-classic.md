---
title: "Kopia zapasowa Azure: Użyj programu PowerShell do tworzenia kopii zapasowej obciążeń programu DPM | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie wdrażania i zarządzania nimi kopia zapasowa Azure dla Data Protection Manager (DPM) przy użyciu programu PowerShell"
services: backup
documentationcenter: 
author: Nkolli1
manager: shreeshd
editor: 
ms.assetid: bcbcef79-9d33-4e84-a558-9866614f2cae
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: nkolli;trinadhk;anuragm;markgal
ms.openlocfilehash: 943a12dcba49a114d206b9dab968da332ea99926
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-and-manage-backup-to-azure-for-data-protection-manager-dpm-servers-using-powershell"></a><span data-ttu-id="bdfd1-103">Wdrażanie kopii zapasowych serwerów Data Protection Manager (DPM) na platformie Azure i zarządzanie nimi przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="bdfd1-103">Deploy and manage backup to Azure for Data Protection Manager (DPM) servers using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bdfd1-104">ARM</span><span class="sxs-lookup"><span data-stu-id="bdfd1-104">ARM</span></span>](backup-dpm-automation.md)
> * [<span data-ttu-id="bdfd1-105">Wdrożenie klasyczne</span><span class="sxs-lookup"><span data-stu-id="bdfd1-105">Classic</span></span>](backup-dpm-automation-classic.md)
>
>

<span data-ttu-id="bdfd1-106">W tym artykule opisano sposób tworzenia kopii zapasowej i odzyskiwania danych programu DPM z magazynu kopii zapasowych za pomocą programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-106">This article explains how to use PowerShell to back up and recover DPM data from a backup vault.</span></span> <span data-ttu-id="bdfd1-107">Firma Microsoft zaleca używanie Magazyny usług odzyskiwania dla wszystkich nowych wdrożeń.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-107">Microsoft recommends using Recovery Services vaults for all new deployments.</span></span> <span data-ttu-id="bdfd1-108">Jeśli nowy użytkownik kopia zapasowa Azure, użyj tego artykułu [Wdróż danych programu Data Protection Manager przy użyciu programu PowerShell Azure i zarządzać nimi](backup-dpm-automation.md), więc dane są przechowywane w magazynie usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-108">If you are a new Azure Backup user, use the article, [Deploy and manage Data Protection Manager data to Azure using PowerShell](backup-dpm-automation.md), so you store your data in a Recovery Services vault.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bdfd1-109">Magazyny kopii zapasowych możesz teraz uaktualnić do magazynów usługi Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-109">You can now upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="bdfd1-110">Więcej szczegółów znajduje się w artykule [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md) (Uaktualnianie magazynu kopii zapasowych do magazynu usługi Recovery Services).</span><span class="sxs-lookup"><span data-stu-id="bdfd1-110">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="bdfd1-111">Firma Microsoft zachęca do przeprowadzenia uaktualnienia magazynów kopii zapasowych do magazynów usługi Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-111">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="bdfd1-112">Po 15 października 2017 r. nie będzie można tworzyć magazynów kopii zapasowych za pomocą programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-112">After October 15, 2017, you can’t use PowerShell to create Backup vaults.</span></span> <span data-ttu-id="bdfd1-113">**Do 1 listopada 2017 r.**:</span><span class="sxs-lookup"><span data-stu-id="bdfd1-113">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="bdfd1-114">Wszystkie pozostałe magazyny kopii zapasowych zostaną automatycznie uaktualnione do magazynów usługi Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-114">All remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="bdfd1-115">Nie będzie możliwe uzyskanie dostępu do danych kopii zapasowych w portalu klasycznym.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-115">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="bdfd1-116">Zamiast tego należy użyć witryny Azure Portal, aby uzyskać dostęp do danych kopii zapasowych w magazynach usługi Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-116">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>
>

## <a name="setting-up-the-powershell-environment"></a><span data-ttu-id="bdfd1-117">Konfigurowanie środowiska PowerShell</span><span class="sxs-lookup"><span data-stu-id="bdfd1-117">Setting up the PowerShell environment</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="bdfd1-118">Przed użyciem programu PowerShell do zarządzania kopiami zapasowymi z programu Data Protection Manager na platformie Azure, musisz mieć prawo środowiska w programie PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-118">Before you can use PowerShell to manage backups from Data Protection Manager to Azure, you will need to have the right environment in PowerShell.</span></span> <span data-ttu-id="bdfd1-119">Na początku sesji programu PowerShell upewnij się, że uruchom następujące polecenie, aby zaimportować moduły, prawym i pozwalają na poprawnie odwołują się następujące polecenia cmdlet programu DPM:</span><span class="sxs-lookup"><span data-stu-id="bdfd1-119">At the start of the PowerShell session, ensure that you run the following command to import the right modules and allow you to correctly reference the DPM cmdlets:</span></span>

```
PS C:> & "C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin\DpmCliInitScript.ps1"

Welcome to the DPM Management Shell!

Full list of cmdlets: Get-Command
Only DPM cmdlets: Get-DPMCommand
Get general help: help
Get help for a cmdlet: help <cmdlet-name> or <cmdlet-name> -?
Get definition of a cmdlet: Get-Command <cmdlet-name> -Syntax
Sample DPM scripts: Get-DPMSampleScript
```

## <a name="setup-and-registration"></a><span data-ttu-id="bdfd1-120">Instalację i rejestrację</span><span class="sxs-lookup"><span data-stu-id="bdfd1-120">Setup and Registration</span></span>
<span data-ttu-id="bdfd1-121">Aby rozpocząć:</span><span class="sxs-lookup"><span data-stu-id="bdfd1-121">To begin:</span></span>

1. <span data-ttu-id="bdfd1-122">[Pobierz najnowsze PowerShell](https://github.com/Azure/azure-powershell/releases) (minimalna wersja wymagana jest: 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="bdfd1-122">[Download latest PowerShell](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>
2. <span data-ttu-id="bdfd1-123">Włącz przez przełączenie do polecenia cmdlet usługi Kopia zapasowa Azure *AzureResourceManager* trybie przy użyciu **Switch-AzureMode** apletu polecenia:</span><span class="sxs-lookup"><span data-stu-id="bdfd1-123">Enable the Azure Backup commandlets by switching to *AzureResourceManager* mode by using the **Switch-AzureMode** commandlet:</span></span>

```
PS C:\> Switch-AzureMode AzureResourceManager
```

<span data-ttu-id="bdfd1-124">Następujące zadania instalację i rejestrację można zautomatyzować przy użyciu programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="bdfd1-124">The following setup and registration tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="bdfd1-125">Tworzenie magazynu kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="bdfd1-125">Create a backup vault</span></span>
* <span data-ttu-id="bdfd1-126">Instalowanie agenta usługi Kopia zapasowa Azure</span><span class="sxs-lookup"><span data-stu-id="bdfd1-126">Installing the Azure Backup agent</span></span>
* <span data-ttu-id="bdfd1-127">Rejestrowanie w usłudze Kopia zapasowa Azure</span><span class="sxs-lookup"><span data-stu-id="bdfd1-127">Registering with the Azure Backup service</span></span>
* <span data-ttu-id="bdfd1-128">Ustawienia sieciowe</span><span class="sxs-lookup"><span data-stu-id="bdfd1-128">Networking settings</span></span>
* <span data-ttu-id="bdfd1-129">Ustawienia szyfrowania</span><span class="sxs-lookup"><span data-stu-id="bdfd1-129">Encryption settings</span></span>

### <a name="create-a-backup-vault"></a><span data-ttu-id="bdfd1-130">Tworzenie magazynu kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="bdfd1-130">Create a backup vault</span></span>
> [!WARNING]
> <span data-ttu-id="bdfd1-131">Dla klientów korzystających z usługi Kopia zapasowa Azure po raz pierwszy należy zarejestrować dostawcę usługi Kopia zapasowa Azure do użycia w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-131">For customers using Azure Backup for the first time, you need to register the Azure Backup provider to be used with your subscription.</span></span> <span data-ttu-id="bdfd1-132">Można to zrobić, uruchamiając następujące polecenie: Register AzureProvider - ProviderNamespace "Microsoft.Backup"</span><span class="sxs-lookup"><span data-stu-id="bdfd1-132">This can be done by running the following command: Register-AzureProvider -ProviderNamespace "Microsoft.Backup"</span></span>
>
>

<span data-ttu-id="bdfd1-133">Można utworzyć nowego magazynu kopii zapasowych przy użyciu **AzureRMBackupVault nowy** apletu polecenia.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-133">You can create a new backup vault using the **New-AzureRMBackupVault** commandlet.</span></span> <span data-ttu-id="bdfd1-134">Magazyn kopii zapasowych jest zasobem ARM, więc należy umieścić w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-134">The backup vault is an ARM resource, so you need to place it within a Resource Group.</span></span> <span data-ttu-id="bdfd1-135">W konsoli programu Azure PowerShell z podwyższonym poziomem uprawnień uruchom następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="bdfd1-135">In an elevated Azure PowerShell console, run the following commands:</span></span>

```
PS C:\> New-AzureResourceGroup –Name “test-rg” -Region “West US”
PS C:\> $backupvault = New-AzureRMBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GRS
```

<span data-ttu-id="bdfd1-136">Można uzyskać listę wszystkich magazynów kopii zapasowych w danej subskrypcji przy użyciu **Get AzureRMBackupVault** apletu polecenia.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-136">You can get a list of all the backup vaults in a given subscription using the **Get-AzureRMBackupVault** commandlet.</span></span>

### <a name="installing-the-azure-backup-agent-on-a-dpm-server"></a><span data-ttu-id="bdfd1-137">Instalowanie agenta usługi Kopia zapasowa Azure na serwerze programu DPM</span><span class="sxs-lookup"><span data-stu-id="bdfd1-137">Installing the Azure Backup agent on a DPM Server</span></span>
<span data-ttu-id="bdfd1-138">Przed zainstalowaniem agenta usługi Kopia zapasowa Azure, musisz mieć Instalator pobrane i są obecne w systemie Windows Server.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-138">Before you install the Azure Backup agent, you need to have the installer downloaded and present on the Windows Server.</span></span> <span data-ttu-id="bdfd1-139">Możesz pobrać najnowszą wersję Instalatora z [Microsoft Download Center](http://aka.ms/azurebackup_agent) lub ze strony pulpitu nawigacyjnego magazynu kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-139">You can get the latest version of the installer from the [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from the backup vault's Dashboard page.</span></span> <span data-ttu-id="bdfd1-140">Zapisanie Instalatora, aby łatwo dostępnej lokalizacji, takich jak * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-140">Save the installer to an easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="bdfd1-141">Aby zainstalować agenta, uruchom następujące polecenie w konsoli programu PowerShell z podwyższonym poziomem uprawnień **na serwerze programu DPM**:</span><span class="sxs-lookup"><span data-stu-id="bdfd1-141">To install the agent, run the following command in an elevated PowerShell console **on the DPM server**:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="bdfd1-142">Spowoduje to zainstalowanie agenta przy użyciu opcji domyślnej.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-142">This installs the agent with all the default options.</span></span> <span data-ttu-id="bdfd1-143">Instalacja trwa kilka minut w tle.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-143">The installation takes a few minutes in the background.</span></span> <span data-ttu-id="bdfd1-144">Jeśli nie określisz */nu* opcji **usługi Windows Update** zostanie otwarte okno po zakończeniu instalacji sprawdź, czy wszystkie aktualizacje.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-144">If you do not specify the */nu* option the **Windows Update** window will open at the end of the installation to check for any updates.</span></span>

<span data-ttu-id="bdfd1-145">Agent zostaną wyświetlone na liście zainstalowanych programów.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-145">The agent will show in the list of installed programs.</span></span> <span data-ttu-id="bdfd1-146">Aby wyświetlić listę zainstalowanych programów, przejdź do **Panelu sterowania** > **programy** > **programy i funkcje**.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-146">To see the list of installed programs, go to **Control Panel** > **Programs** > **Programs and Features**.</span></span>

![Agent został zainstalowany](./media/backup-dpm-automation/installed-agent-listing.png)

#### <a name="installation-options"></a><span data-ttu-id="bdfd1-148">Opcje instalacji</span><span class="sxs-lookup"><span data-stu-id="bdfd1-148">Installation options</span></span>
<span data-ttu-id="bdfd1-149">Aby wyświetlić wszystkie opcje dostępne za pomocą wiersza polecenia, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="bdfd1-149">To see all the options available via the command-line, use the following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="bdfd1-150">Dostępne opcje to:</span><span class="sxs-lookup"><span data-stu-id="bdfd1-150">The available options include:</span></span>

| <span data-ttu-id="bdfd1-151">Opcja</span><span class="sxs-lookup"><span data-stu-id="bdfd1-151">Option</span></span> | <span data-ttu-id="bdfd1-152">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="bdfd1-152">Details</span></span> | <span data-ttu-id="bdfd1-153">Domyślne</span><span class="sxs-lookup"><span data-stu-id="bdfd1-153">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bdfd1-154">/q</span><span class="sxs-lookup"><span data-stu-id="bdfd1-154">/q</span></span> |<span data-ttu-id="bdfd1-155">Instalację cichą</span><span class="sxs-lookup"><span data-stu-id="bdfd1-155">Quiet installation</span></span> |- |
| <span data-ttu-id="bdfd1-156">/ p: "Lokalizacja"</span><span class="sxs-lookup"><span data-stu-id="bdfd1-156">/p:"location"</span></span> |<span data-ttu-id="bdfd1-157">Ścieżka do folderu instalacji agenta usługi Kopia zapasowa Azure.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-157">Path to the installation folder for the Azure Backup agent.</span></span> |<span data-ttu-id="bdfd1-158">C:\Program Files\Microsoft Azure Recovery usługi agenta</span><span class="sxs-lookup"><span data-stu-id="bdfd1-158">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="bdfd1-159">/ s: "Lokalizacja"</span><span class="sxs-lookup"><span data-stu-id="bdfd1-159">/s:"location"</span></span> |<span data-ttu-id="bdfd1-160">Ścieżka do folderu pamięci podręcznej agenta usługi Kopia zapasowa Azure.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-160">Path to the cache folder for the Azure Backup agent.</span></span> |<span data-ttu-id="bdfd1-161">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="bdfd1-161">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="bdfd1-162">/m</span><span class="sxs-lookup"><span data-stu-id="bdfd1-162">/m</span></span> |<span data-ttu-id="bdfd1-163">Zezwól na usługi Microsoft Update</span><span class="sxs-lookup"><span data-stu-id="bdfd1-163">Opt-in to Microsoft Update</span></span> |- |
| <span data-ttu-id="bdfd1-164">/nu</span><span class="sxs-lookup"><span data-stu-id="bdfd1-164">/nu</span></span> |<span data-ttu-id="bdfd1-165">Nie sprawdzaj aktualizacji po ukończeniu instalacji</span><span class="sxs-lookup"><span data-stu-id="bdfd1-165">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="bdfd1-166">/d</span><span class="sxs-lookup"><span data-stu-id="bdfd1-166">/d</span></span> |<span data-ttu-id="bdfd1-167">Odinstalowuje agenta usług odzyskiwania Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="bdfd1-167">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="bdfd1-168">/pH</span><span class="sxs-lookup"><span data-stu-id="bdfd1-168">/ph</span></span> |<span data-ttu-id="bdfd1-169">Adres hosta serwera proxy</span><span class="sxs-lookup"><span data-stu-id="bdfd1-169">Proxy Host Address</span></span> |- |
| <span data-ttu-id="bdfd1-170">/Po</span><span class="sxs-lookup"><span data-stu-id="bdfd1-170">/po</span></span> |<span data-ttu-id="bdfd1-171">Numer portu hosta serwera proxy</span><span class="sxs-lookup"><span data-stu-id="bdfd1-171">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="bdfd1-172">/Pu</span><span class="sxs-lookup"><span data-stu-id="bdfd1-172">/pu</span></span> |<span data-ttu-id="bdfd1-173">Nazwa użytkownika serwera proxy hosta</span><span class="sxs-lookup"><span data-stu-id="bdfd1-173">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="bdfd1-174">/PW</span><span class="sxs-lookup"><span data-stu-id="bdfd1-174">/pw</span></span> |<span data-ttu-id="bdfd1-175">Hasło serwera proxy</span><span class="sxs-lookup"><span data-stu-id="bdfd1-175">Proxy Password</span></span> |- |

### <a name="registering-with-the-azure-backup-service"></a><span data-ttu-id="bdfd1-176">Rejestrowanie w usłudze Kopia zapasowa Azure</span><span class="sxs-lookup"><span data-stu-id="bdfd1-176">Registering with the Azure Backup service</span></span>
<span data-ttu-id="bdfd1-177">Przed zarejestrowaniem w usłudze Kopia zapasowa Azure, należy upewnić się, że [wymagania wstępne](backup-azure-dpm-introduction.md) są spełnione.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-177">Before you can register with the Azure Backup service, you need to ensure that the [prerequisites](backup-azure-dpm-introduction.md) are met.</span></span> <span data-ttu-id="bdfd1-178">Należy:</span><span class="sxs-lookup"><span data-stu-id="bdfd1-178">You must:</span></span>

* <span data-ttu-id="bdfd1-179">Masz ważną subskrypcję platformy Azure</span><span class="sxs-lookup"><span data-stu-id="bdfd1-179">Have a valid Azure subscription</span></span>
* <span data-ttu-id="bdfd1-180">Masz magazyn kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="bdfd1-180">Have a backup vault</span></span>

<span data-ttu-id="bdfd1-181">Aby pobrać poświadczenia magazynu, uruchom **Get-AzureBackupVaultCredentials** polecenia w konsoli programu PowerShell systemu Azure i zapisać go w dogodnym miejscu, takich jak * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-181">To download the vault credentials, run the **Get-AzureBackupVaultCredentials** commandlet in an Azure PowerShell console and store it in a convenient location like *C:\Downloads\*.</span></span>

```
PS C:\> $credspath = "C:\"
PS C:\> $credsfilename = Get-AzureRMBackupVaultCredentials -Vault $backupvault -TargetLocation $credspath
PS C:\> $credsfilename
f5303a0b-fae4-4cdb-b44d-0e4c032dde26_backuprg_backuprn_2015-08-11--06-22-35.VaultCredentials
```

<span data-ttu-id="bdfd1-182">Rejestrowanie w magazynie komputera jest wykonywane przy użyciu [Start DPMCloudRegistration](https://technet.microsoft.com/library/jj612787) polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="bdfd1-182">Registering the machine with the vault is done using the [Start-DPMCloudRegistration](https://technet.microsoft.com/library/jj612787) cmdlet:</span></span>

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-DPMCloudRegistration -DPMServerName "TestingServer" -VaultCredentialsFilePath $cred
```

<span data-ttu-id="bdfd1-183">Spowoduje to rejestrowania serwera DPM, o nazwie "Serwerach" o magazynie usługi Microsoft Azure przy użyciu poświadczeń określonego magazynu.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-183">This will register the DPM Server named “TestingServer” with Microsoft Azure Vault using the specified vault credentials.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bdfd1-184">Aby określić plik poświadczeń magazynu nie należy używać ścieżek względnych.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-184">Do not use relative paths to specify the vault credentials file.</span></span> <span data-ttu-id="bdfd1-185">Należy podać ścieżkę bezwzględną jako dane wejściowe polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-185">You must provide an absolute path as an input to the cmdlet.</span></span>
>
>

### <a name="initial-configuration-settings"></a><span data-ttu-id="bdfd1-186">Ustawienia konfiguracji początkowej</span><span class="sxs-lookup"><span data-stu-id="bdfd1-186">Initial configuration settings</span></span>
<span data-ttu-id="bdfd1-187">Gdy serwer DPM jest zarejestrowany w magazynie usługi Kopia zapasowa Azure, rozpoczyna się od domyślnego ustawienia subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-187">Once the DPM Server is registered with the Azure Backup vault, it will start with default subscription settings.</span></span> <span data-ttu-id="bdfd1-188">Te ustawienia subskrypcji obejmują sieci, szyfrowania i obszaru przemieszczania.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-188">These subscription settings include Networking, Encryption and the Staging area.</span></span> <span data-ttu-id="bdfd1-189">Aby rozpocząć, zmiana ustawień subskrypcji, należy najpierw uzyskać uchwytu na istniejące ustawienia (ustawienie domyślne), za pomocą [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="bdfd1-189">To begin changing the subscription settings you need to first get a handle on the existing (default) settings using the [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet:</span></span>

```
$setting = Get-DPMCloudSubscriptionSetting -DPMServerName "TestingServer"
```

<span data-ttu-id="bdfd1-190">Wszystkie modyfikacje są dokonywane na ten obiekt programu PowerShell ```$setting``` , a następnie pełne obiektu jest przekazane do programu DPM i kopia zapasowa Azure, aby zapisać je przy użyciu [DPMCloudSubscriptionSetting zestaw](https://technet.microsoft.com/library/jj612791) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-190">All modifications are made to this local PowerShell object ```$setting```  and then the full object is committed to DPM and Azure Backup to save them using the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="bdfd1-191">Należy użyć ```–Commit``` flagę, aby upewnić się, że zmiany są zachowywane.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-191">You need to use the ```–Commit``` flag to ensure that the changes are persisted.</span></span> <span data-ttu-id="bdfd1-192">Ustawienia nie będą stosowane i używane przez usługi Kopia zapasowa Azure, chyba że zostało zatwierdzone.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-192">The settings will not be applied and used by Azure Backup unless committed.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

### <a name="networking"></a><span data-ttu-id="bdfd1-193">Sieć</span><span class="sxs-lookup"><span data-stu-id="bdfd1-193">Networking</span></span>
<span data-ttu-id="bdfd1-194">W przypadku łączności maszyny programu DPM z usługą kopia zapasowa Azure w sieci internet za pośrednictwem serwera proxy, ustawienia serwera proxy należy podać dla kopii zapasowych powiodło się.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-194">If the connectivity of the DPM machine to the Azure Backup service on the internet is through a proxy server, then the proxy server settings should be provided for backups to succeed.</span></span> <span data-ttu-id="bdfd1-195">Jest to zrobić za pomocą ```-ProxyServer```, ```-ProxyPort```, ```-ProxyUsername``` i ```ProxyPassword``` parametrów z [DPMCloudSubscriptionSetting zestaw](https://technet.microsoft.com/library/jj612791) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-195">This is done by using the ```-ProxyServer```, ```-ProxyPort```, ```-ProxyUsername``` and the ```ProxyPassword``` parameters with the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="bdfd1-196">W tym przykładzie nie żadnego serwera proxy, dlatego firma Microsoft są jawnie wyczyszczenie żadnych informacji dotyczących serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-196">In this example, there is no proxy server so we are explicitly clearing any proxy-related information.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoProxy
```

<span data-ttu-id="bdfd1-197">Wykorzystanie przepustowości można również sterować za pomocą opcji ```-WorkHourBandwidth``` i ```-NonWorkHourBandwidth``` dla danego zestawu dni tygodnia.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-197">Bandwidth usage can also be controlled with options of ```-WorkHourBandwidth``` and ```-NonWorkHourBandwidth``` for a given set of days of the week.</span></span> <span data-ttu-id="bdfd1-198">W tym przykładzie firma Microsoft nie ustawienia dowolnej ograniczania.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-198">In this example we are not setting any throttling.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoThrottle
```

### <a name="configuring-the-staging-area"></a><span data-ttu-id="bdfd1-199">Konfigurowanie obszaru przemieszczania</span><span class="sxs-lookup"><span data-stu-id="bdfd1-199">Configuring the staging Area</span></span>
<span data-ttu-id="bdfd1-200">Agent usługi Kopia zapasowa Azure uruchomionych na serwerze programu DPM wymaga tymczasowego magazynu dla danych przywróconych z chmury (lokalny obszar przemieszczania).</span><span class="sxs-lookup"><span data-stu-id="bdfd1-200">The Azure Backup agent running on the DPM server needs temporary storage for data restored from the cloud (local staging area).</span></span> <span data-ttu-id="bdfd1-201">Konfigurowanie przy użyciu obszaru przemieszczania [DPMCloudSubscriptionSetting zestaw](https://technet.microsoft.com/library/jj612791) polecenia cmdlet i ```-StagingAreaPath``` parametru.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-201">Configure the staging area using the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet and the ```-StagingAreaPath``` parameter.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -StagingAreaPath "C:\StagingArea"
```

<span data-ttu-id="bdfd1-202">W powyższym przykładzie obszar tymczasowy zostanie ustawiona do *C:\StagingArea* w obiekcie środowiska PowerShell ```$setting```.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-202">In the example above, the staging area will be set to *C:\StagingArea* in the PowerShell object ```$setting```.</span></span> <span data-ttu-id="bdfd1-203">Upewnij się, że podany folder już istnieje, w przeciwnym razie końcowego zatwierdzania ustawień subskrypcji zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-203">Ensure that the specified folder already exists, or else the final commit of the subscription settings will fail.</span></span>

### <a name="encryption-settings"></a><span data-ttu-id="bdfd1-204">Ustawienia szyfrowania</span><span class="sxs-lookup"><span data-stu-id="bdfd1-204">Encryption settings</span></span>
<span data-ttu-id="bdfd1-205">Dane kopii zapasowej wysyłane do usługi Kopia zapasowa Azure są szyfrowane w chronieniu poufności danych.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-205">The backup data sent to Azure Backup is encrypted to protect the confidentiality of the data.</span></span> <span data-ttu-id="bdfd1-206">Hasło szyfrowania jest "password" do odszyfrowania danych w czasie przywracania.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-206">The encryption passphrase is the "password" to decrypt the data at the time of restore.</span></span> <span data-ttu-id="bdfd1-207">Należy zachować te informacje bezpieczne po ustawieniu.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-207">It is important to keep this information safe and secure once it is set.</span></span>

<span data-ttu-id="bdfd1-208">W poniższym przykładzie pierwsze polecenie konwertuje ciąg ```passphrase123456789``` ciąg bezpieczny i przypisuje bezpieczny ciąg do zmiennej o nazwie ```$Passphrase```.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-208">In the example below, the first command converts the string ```passphrase123456789``` to a secure string and assigns the secure string to the variable named ```$Passphrase```.</span></span> <span data-ttu-id="bdfd1-209">drugie polecenie ustawia bezpieczny ciąg w ```$Passphrase``` jako hasło do szyfrowania kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-209">the second command sets the secure string in ```$Passphrase``` as the password for encrypting backups.</span></span>

```
PS C:\> $Passphrase = ConvertTo-SecureString -string "passphrase123456789" -AsPlainText -Force

PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -EncryptionPassphrase $Passphrase
```

> [!IMPORTANT]
> <span data-ttu-id="bdfd1-210">Zachowaj informacje hasło bezpieczne po ustawieniu.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-210">Keep the passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="bdfd1-211">Nie można przywrócić dane z platformy Azure bez tego hasła.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-211">You will not be able to restore data from Azure without this passphrase.</span></span>
>
>

<span data-ttu-id="bdfd1-212">W tym momencie powinien wprowadzone wszystkie zmiany wymagane w celu ```$setting``` obiektu.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-212">At this point, you should have made all the required changes to the ```$setting``` object.</span></span> <span data-ttu-id="bdfd1-213">Pamiętaj, aby zatwierdzić zmiany.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-213">Remember to commit the changes.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="protect-data-to-azure-backup"></a><span data-ttu-id="bdfd1-214">Ochrona danych do usługi Kopia zapasowa Azure</span><span class="sxs-lookup"><span data-stu-id="bdfd1-214">Protect data to Azure Backup</span></span>
<span data-ttu-id="bdfd1-215">W tej sekcji zostanie Dodawanie serwera produkcyjnego do programu DPM, a następnie włącz ochronę danych do lokalnego magazynu programu DPM, a następnie kopia zapasowa Azure.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-215">In this section, you will add a production server to DPM and then protect the data to local DPM storage and then to Azure Backup.</span></span> <span data-ttu-id="bdfd1-216">W przykładach przedstawiony zostanie sposób wykonywania kopii zapasowej plików i folderów.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-216">In the examples we will demonstrate how to back up files and folders.</span></span> <span data-ttu-id="bdfd1-217">Logika można z łatwością rozszerzyć kopii zapasowej dowolnych źródeł danych obsługiwane przez program DPM.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-217">The logic can easily be extended to backup any DPM-supported data source.</span></span> <span data-ttu-id="bdfd1-218">Kopii zapasowych programu DPM są regulowane przez ochronę grupy (PG) z czterech części:</span><span class="sxs-lookup"><span data-stu-id="bdfd1-218">All your DPM backups are governed by a Protection Group (PG) with four parts:</span></span>

1. <span data-ttu-id="bdfd1-219">**Członków grupy** znajduje się lista wszystkich obiekty chronione (nazywane również *źródeł danych* w programie DPM), które mają być chronione w tej samej grupy ochrony.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-219">**Group members** is a list of all the protectable objects (also known as *Datasources* in DPM) that you want to protect in the same protection group.</span></span> <span data-ttu-id="bdfd1-220">Na przykład można chronić produkcji maszyny wirtualne w jednej grupy ochrony i baz danych programu SQL Server w innej grupy ochrony, ponieważ mogą mieć różne wymagania kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-220">For example, you may want to protect production VMs in one protection group and SQL Server databases in another protection group as they may have different backup requirements.</span></span> <span data-ttu-id="bdfd1-221">Przed utworzeniem kopii zapasowej żadnego źródła danych na serwerze produkcyjnym, które należy się upewnić, Agent programu DPM jest zainstalowany na serwerze i jest zarządzany przez program DPM.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-221">Before you can back up any datasource on a production server you need to make sure the DPM Agent is installed on the server and is managed by DPM.</span></span> <span data-ttu-id="bdfd1-222">Wykonaj kroki [zainstalowanie agenta DPM](https://technet.microsoft.com/library/bb870935.aspx) i połączenie go do odpowiedniego serwera programu DPM.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-222">Follow the steps for [installing the DPM Agent](https://technet.microsoft.com/library/bb870935.aspx) and linking it to the appropriate DPM Server.</span></span>
2. <span data-ttu-id="bdfd1-223">**Metoda ochrony danych** Określa docelowy kopii zapasowej lokalizacje - taśmy, dysku i chmury.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-223">**Data protection method** specifies the target backup locations - tape, disk, and cloud.</span></span> <span data-ttu-id="bdfd1-224">W naszym przykładzie będzie chronić dane na dysku lokalnym i w chmurze.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-224">In our example we will protect data to the local disk and to the cloud.</span></span>
3. <span data-ttu-id="bdfd1-225">A **harmonogram tworzenia kopii zapasowych** Określa, kiedy należy podjąć kopii zapasowych i jak często dane powinny być synchronizowane między serwerem DPM i serwerze produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-225">A **backup schedule** that specifies when backups need to be taken and how often the data should be synchronized between the DPM Server and the production server.</span></span>
4. <span data-ttu-id="bdfd1-226">A **harmonogramu przechowywania** określająca czas przechowywania punktów odzyskiwania na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-226">A **retention schedule** that specifies how long to retain the recovery points in Azure.</span></span>

### <a name="creating-a-protection-group"></a><span data-ttu-id="bdfd1-227">Utworzenie grupy ochrony</span><span class="sxs-lookup"><span data-stu-id="bdfd1-227">Creating a protection group</span></span>
<span data-ttu-id="bdfd1-228">Rozpocznij od utworzenia nowej grupy ochrony za pomocą [DPMProtectionGroup nowy](https://technet.microsoft.com/library/hh881722) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-228">Start by creating a new Protection Group using the [New-DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) cmdlet.</span></span>

```
PS C:\> $PG = New-DPMProtectionGroup -DPMServerName " TestingServer " -Name "ProtectGroup01"
```

<span data-ttu-id="bdfd1-229">Powyższe polecenia cmdlet spowoduje utworzenie grupy ochrony o nazwie *ProtectGroup01*.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-229">The above cmdlet will create a Protection Group named *ProtectGroup01*.</span></span> <span data-ttu-id="bdfd1-230">Aby dodać kopii zapasowej w chmurze platformy Azure istniejącej grupy ochrony może być modyfikowany również później.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-230">An existing protection group can also be modified later to add backup to the Azure cloud.</span></span> <span data-ttu-id="bdfd1-231">Jednak wprowadzać żadnych zmian do grupy ochrony — nowy lub istniejący - musimy pobrać dojścia *modyfikowalnymi* przy użyciu [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-231">However, to make any changes to the Protection Group - new or existing - we need to get a handle on a *modifiable* object using the [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) cmdlet.</span></span>

```
PS C:\> $MPG = Get-ModifiableProtectionGroup $PG
```

### <a name="adding-group-members-to-the-protection-group"></a><span data-ttu-id="bdfd1-232">Dodawanie członków grupy do grupy ochrony</span><span class="sxs-lookup"><span data-stu-id="bdfd1-232">Adding group members to the Protection Group</span></span>
<span data-ttu-id="bdfd1-233">Lista źródeł danych na serwerze, na którym jest zainstalowany na wie, każdego agenta programu DPM.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-233">Each DPM Agent knows the list of datasources on the server that it is installed on.</span></span> <span data-ttu-id="bdfd1-234">Aby dodać źródła danych do grupy ochrony, agenta programu DPM musi najpierw wysłać listę źródeł danych na serwer programu DPM.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-234">To add a datasource to the Protection Group, the DPM Agent needs to first send a list of the datasources back to the DPM server.</span></span> <span data-ttu-id="bdfd1-235">Jeden lub więcej źródeł danych są następnie i dodane do grupy ochrony.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-235">One or more datasources are then selected and added to the Protection Group.</span></span> <span data-ttu-id="bdfd1-236">Kroki programu PowerShell, aby zacząć, niezbędne osiągnięcia się to:</span><span class="sxs-lookup"><span data-stu-id="bdfd1-236">The PowerShell steps needed to get achieve this are:</span></span>

1. <span data-ttu-id="bdfd1-237">Pobierz listę wszystkich serwerów zarządzanych przez program DPM za pomocą agenta programu DPM.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-237">Fetch a list of all servers managed by DPM through the DPM Agent.</span></span>
2. <span data-ttu-id="bdfd1-238">Wybierz określonego serwera.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-238">Choose a specific server.</span></span>
3. <span data-ttu-id="bdfd1-239">Pobranie listy wszystkich źródeł danych na serwerze.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-239">Fetch a list of all datasources on the server.</span></span>
4. <span data-ttu-id="bdfd1-240">Wybierz co najmniej jednego źródła danych i dodaj je do grupy ochrony</span><span class="sxs-lookup"><span data-stu-id="bdfd1-240">Choose one or more datasources and add them to the Protection Group</span></span>

<span data-ttu-id="bdfd1-241">Lista serwerów, na których Agent programu DPM jest zainstalowany i jest zarządzany przez serwer programu DPM są uzyskiwane z [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-241">The list of servers on which the DPM Agent is installed and is being managed by the DPM Server is acquired with the [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet.</span></span> <span data-ttu-id="bdfd1-242">W tym przykładzie firma Microsoft będzie filtrowania i skonfigurować tylko PS o nazwie *productionserver01* do utworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-242">In this example we will filter and only configure PS with name *productionserver01* for backup.</span></span>

```
PS C:\> $server = Get-ProductionServer -DPMServerName "TestingServer" | where {($_.servername) –contains “productionserver01”
```

<span data-ttu-id="bdfd1-243">Teraz pobrać listy źródeł danych na ```$server``` przy użyciu [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-243">Now fetch the list of datasources on ```$server``` using the [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet.</span></span> <span data-ttu-id="bdfd1-244">W tym przykładzie mamy filtrowania dla woluminu * D:\* którego chcemy skonfigurować dla kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-244">In this example we are filtering for the volume *D:\* which we want to configure for backup.</span></span> <span data-ttu-id="bdfd1-245">To źródło danych jest dodawane do grupy ochrony za pomocą [DPMChildDatasource Dodaj](https://technet.microsoft.com/library/hh881732) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-245">This datasource is then added to the Protection Group using the [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet.</span></span> <span data-ttu-id="bdfd1-246">Pamiętaj, aby użyć *modifable* obiektu grupy ochrony ```$MPG``` uzupełnianie.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-246">Remember to use the *modifable* protection group object ```$MPG``` to make the additions.</span></span>

```
PS C:\> $DS = Get-Datasource -ProductionServer $server -Inquire | where { $_.Name -contains “D:\” }

PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS
```

<span data-ttu-id="bdfd1-247">Powtórz ten krok liczbę razy, aż zostaną dodane wszystkie wybrane źródła danych do grupy ochrony.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-247">Repeat this step as many times as required, until you have added all the chosen datasources to the protection group.</span></span> <span data-ttu-id="bdfd1-248">Można również uruchomić z tylko jednego źródła danych i ukończenia przepływu pracy tworzenia grupy ochrony i w późniejszym czasie dodać więcej źródeł danych do grupy ochrony.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-248">You can also start with just one datasource, and complete the workflow for creating the Protection Group, and at a later point add more datasources to the Protection Group.</span></span>

### <a name="selecting-the-data-protection-method"></a><span data-ttu-id="bdfd1-249">Wybieranie metody ochrony danych</span><span class="sxs-lookup"><span data-stu-id="bdfd1-249">Selecting the data protection method</span></span>
<span data-ttu-id="bdfd1-250">Po źródła danych zostały dodane do grupy ochrony, następnym krokiem jest określenie, przy użyciu metody ochrony [DPMProtectionType zestaw](https://technet.microsoft.com/library/hh881725) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-250">Once the datasources have been added to the Protection Group, the next step is to specify the protection method using the [Set-DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet.</span></span> <span data-ttu-id="bdfd1-251">W tym przykładzie grupy ochrony będzie instalacji na dysku lokalnym, a kopia zapasowa w chmurze.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-251">In this example, the Protection Group will be setup for local disk and cloud backup.</span></span> <span data-ttu-id="bdfd1-252">Należy również określić źródło danych, które chcesz chronić do chmury przy użyciu [DPMChildDatasource Dodaj](https://technet.microsoft.com/library/hh881732.aspx) polecenia cmdlet flagą - Online.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-252">You also need to specify the datasource that you want to protect to cloud using the [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet with -Online flag.</span></span>

```
PS C:\> Set-DPMProtectionType -ProtectionGroup $MPG -ShortTerm Disk –LongTerm Online
PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS –Online
```

### <a name="setting-the-retention-range"></a><span data-ttu-id="bdfd1-253">Ustawianie zakresu przechowywania</span><span class="sxs-lookup"><span data-stu-id="bdfd1-253">Setting the retention range</span></span>
<span data-ttu-id="bdfd1-254">Ustawienia przechowywania dla punktów kopii zapasowej za pomocą [DPMPolicyObjective zestaw](https://technet.microsoft.com/library/hh881762) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-254">Set the retention for the backup points using the [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span> <span data-ttu-id="bdfd1-255">Gdy może wydawać się nieparzysta ustawień przechowywania, przed rozpoczęciem zdefiniowano harmonogram tworzenia kopii zapasowych, przy użyciu ```Set-DPMPolicyObjective``` polecenie cmdlet automatycznie ustawia domyślny harmonogram tworzenia kopii zapasowej, który może być modyfikowany.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-255">While it might seem odd to set the retention before the backup schedule has been defined, using the ```Set-DPMPolicyObjective``` cmdlet automatically sets a default backup schedule that can then be modified.</span></span> <span data-ttu-id="bdfd1-256">Zawsze jest możliwe zestawu kopii zapasowej najpierw zaplanować, jak i zasady przechowywania po.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-256">It is always possible to set the backup schedule first and the retention policy after.</span></span>

<span data-ttu-id="bdfd1-257">W poniższym przykładzie polecenia cmdlet do ustawiania parametrów przechowywania kopii zapasowych na dyskach.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-257">In the example below, the cmdlet sets the retention parameters for disk backups.</span></span> <span data-ttu-id="bdfd1-258">To zachowują kopie zapasowe 10 dni i synchronizowanie danych co 6 godzin między serwerem produkcyjnym i serwerze programu DPM.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-258">This will retain backups for 10 days, and sync data every 6 hours between the production server and the DPM server.</span></span> <span data-ttu-id="bdfd1-259">```SynchronizationFrequencyMinutes``` Nie definiuje, jak często punktu kopii zapasowej jest tworzony, ale jak często dane są kopiowane do serwera programu DPM; zapobiega to kopie zapasowe za duży.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-259">The ```SynchronizationFrequencyMinutes``` doesn't define how often a backup point is created, but how often data is copied to the DPM server; this prevents backups from becoming too large.</span></span>

```
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -RetentionRangeInDays 10 -SynchronizationFrequencyMinutes 360
```

<span data-ttu-id="bdfd1-260">Kopii zapasowych, przechodząc do platformy Azure (Program DPM odwołuje się do tych kopii zapasowych Online) zakresów przechowywania można skonfigurować dla [długoterminowych przechowywania użyciu schematu dziadek-ojciec-syn. (GFS)](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="bdfd1-260">For backups going to Azure (DPM refers to these as Online backups) the retention ranges can be configured for [long term retention using a Grandfather-Father-Son scheme (GFS)](backup-azure-backup-cloud-as-tape.md).</span></span> <span data-ttu-id="bdfd1-261">Oznacza to można zdefiniować zasady przechowywania Scalonej obejmujące codziennie, co tydzień, miesięcznych i rocznych zasady przechowywania.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-261">That is, you can define a combined retention policy involving daily, weekly, monthly and yearly retention policies.</span></span> <span data-ttu-id="bdfd1-262">W tym przykładzie, możemy utworzyć tablicy reprezentujący schemat przechowywania złożonych, która ma, a następnie skonfiguruj, przy użyciu zakresu przechowywania [DPMPolicyObjective zestaw](https://technet.microsoft.com/library/hh881762) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-262">In this example, we create an array representing the complex retention scheme that we want, and then configure the retention range using the [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span>

```
PS C:\> $RRlist = @()
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 180, Days)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 104, Weeks)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 60, Month)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 10, Years)
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -OnlineRetentionRangeList $RRlist
```

### <a name="set-the-backup-schedule"></a><span data-ttu-id="bdfd1-263">Ustaw harmonogram tworzenia kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="bdfd1-263">Set the backup schedule</span></span>
<span data-ttu-id="bdfd1-264">Program DPM ustawia automatycznie domyślny harmonogram tworzenia kopii zapasowej, jeśli określisz ochronę celu za pomocą ```Set-DPMPolicyObjective``` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-264">DPM sets a default backup schedule automatically if you specify the protection objective using the ```Set-DPMPolicyObjective``` cmdlet.</span></span> <span data-ttu-id="bdfd1-265">Aby zmienić domyślne harmonogramy, użyj [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) polecenia cmdlet następuje [DPMPolicySchedule zestaw](https://technet.microsoft.com/library/hh881723) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-265">To change the default schedules, use the [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet followed by the [Set-DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) cmdlet.</span></span>

```
PS C:\> $onlineSch = Get-DPMPolicySchedule -ProtectionGroup $mpg -LongTerm Online
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[0] -TimesOfDay 02:00
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[1] -TimesOfDay 02:00 -DaysOfWeek Sa,Su –Interval 1
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[2] -TimesOfDay 02:00 -RelativeIntervals First,Third –DaysOfWeek Sa
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[3] -TimesOfDay 02:00 -DaysOfMonth 2,5,8,9 -Months Jan,Jul
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```

<span data-ttu-id="bdfd1-266">W powyższym przykładzie ```$onlineSch``` jest tablicą o czterech elementów zawierający istniejący harmonogram ochrony w trybie online dla grupy ochrony w schemacie GFS:</span><span class="sxs-lookup"><span data-stu-id="bdfd1-266">In the example above, ```$onlineSch``` is an array with four elements that contains the existing online protection schedule for the Protection Group in the GFS scheme:</span></span>

1. <span data-ttu-id="bdfd1-267">```$onlineSch[0]```będzie zawierać harmonogramu dziennego</span><span class="sxs-lookup"><span data-stu-id="bdfd1-267">```$onlineSch[0]``` will contain the daily schedule</span></span>
2. <span data-ttu-id="bdfd1-268">```$onlineSch[1]```będzie zawierać harmonogramu tygodniowego</span><span class="sxs-lookup"><span data-stu-id="bdfd1-268">```$onlineSch[1]``` will contain the weekly schedule</span></span>
3. <span data-ttu-id="bdfd1-269">```$onlineSch[2]```będzie zawierać harmonogramu miesięcznego</span><span class="sxs-lookup"><span data-stu-id="bdfd1-269">```$onlineSch[2]``` will contain the monthly schedule</span></span>
4. <span data-ttu-id="bdfd1-270">```$onlineSch[3]```będzie zawierać corocznych harmonogramu</span><span class="sxs-lookup"><span data-stu-id="bdfd1-270">```$onlineSch[3]``` will contain the yearly schedule</span></span>

<span data-ttu-id="bdfd1-271">Dlatego jeśli trzeba zmodyfikować harmonogram tygodniowy, trzeba odwoływać się do ```$onlineSch[1]```.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-271">So if you need to modify the weekly schedule, you need to refer to the ```$onlineSch[1]```.</span></span>

### <a name="initial-backup"></a><span data-ttu-id="bdfd1-272">Początkowa kopia zapasowa</span><span class="sxs-lookup"><span data-stu-id="bdfd1-272">Initial backup</span></span>
<span data-ttu-id="bdfd1-273">Podczas wykonywania kopii zapasowej źródła danych po raz pierwszy, program DPM potrzebuje do utworzenia repliki początkowej, co spowoduje utworzenie kopii źródła danych mają być chronione na woluminie repliki programu DPM.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-273">When backing up a datasource for the first time, DPM needs to create an initial replica which will create a copy of the datasource to be protected on DPM replica volume.</span></span> <span data-ttu-id="bdfd1-274">To działanie albo mogą być planowane na określoną godzinę lub mogą być wyzwalane ręcznie, używając [DPMReplicaCreationMethod zestaw](https://technet.microsoft.com/library/hh881715) polecenia cmdlet z parametrem ```-NOW```.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-274">This activity can either be scheduled for a specific time, or can be triggered manually, using the [Set-DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet with the parameter ```-NOW```.</span></span>

```
PS C:\> Set-DPMReplicaCreationMethod -ProtectionGroup $MPG -NOW
```
### <a name="changing-the-size-of-dpm-replica--recovery-point-volume"></a><span data-ttu-id="bdfd1-275">Zmiana rozmiaru repliki programu DPM i wolumin punktu odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="bdfd1-275">Changing the size of DPM Replica & recovery point volume</span></span>
<span data-ttu-id="bdfd1-276">Można również zmienić rozmiar woluminu repliki programu DPM, a także kopii w tle woluminu przy użyciu [DPMDatasourceDiskAllocation zestaw](https://technet.microsoft.com/library/hh881618.aspx) polecenia cmdlet, jak w poniższym przykładzie: Get-DatasourceDiskAllocation - Datasource $DS $DS Set-DatasourceDiskAllocation - Datasource - ProtectionGroup $MPG — ręczne - ReplicaArea (2 gb) — ShadowCopyArea (2 gb)</span><span class="sxs-lookup"><span data-stu-id="bdfd1-276">You can also change the size of DPM Replica volume as well as Shadow Copy volume using [Set-DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) cmdlet as in the below example: Get-DatasourceDiskAllocation -Datasource $DS Set-DatasourceDiskAllocation -Datasource $DS -ProtectionGroup $MPG -manual -ReplicaArea (2gb) -ShadowCopyArea (2gb)</span></span>

### <a name="committing-the-changes-to-the-protection-group"></a><span data-ttu-id="bdfd1-277">Zatwierdzenie zmian do grupy ochrony</span><span class="sxs-lookup"><span data-stu-id="bdfd1-277">Committing the changes to the Protection Group</span></span>
<span data-ttu-id="bdfd1-278">Na koniec zmiany muszą być zatwierdzone przed programu DPM można wykonać kopię zapasową na nową konfigurację grupy ochrony.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-278">Finally, the changes need to be committed before DPM can take the backup per the new Protection Group configuration.</span></span> <span data-ttu-id="bdfd1-279">Jest to realizowane przy użyciu [DPMProtectionGroup zestaw](https://technet.microsoft.com/library/hh881758) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-279">This is done using the [Set-DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet.</span></span>

```
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```
## <a name="view-the-backup-points"></a><span data-ttu-id="bdfd1-280">Wyświetlanie punktów kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="bdfd1-280">View the backup points</span></span>
<span data-ttu-id="bdfd1-281">Można użyć [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) polecenia cmdlet, aby uzyskać listę wszystkich punktów odzyskiwania dla źródła danych.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-281">You can use the [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) cmdlet to get a list of all recovery points for a datasource.</span></span> <span data-ttu-id="bdfd1-282">W tym przykładzie zostaną wykonane następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="bdfd1-282">In this example, we will:</span></span>

* <span data-ttu-id="bdfd1-283">Pobierz wszystkie PGA na serwerze programu DPM, w którym będą przechowywane w tablicy```$PG```</span><span class="sxs-lookup"><span data-stu-id="bdfd1-283">fetch all the PGs on the DPM server which will be stored in an array ```$PG```</span></span>
* <span data-ttu-id="bdfd1-284">Pobierz odpowiadający źródeł danych```$PG[0]```</span><span class="sxs-lookup"><span data-stu-id="bdfd1-284">get the datasources corresponding to the ```$PG[0]```</span></span>
* <span data-ttu-id="bdfd1-285">Pobierz wszystkie punkty odzyskiwania dla źródła danych.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-285">get all the recovery points for a datasource.</span></span>

```
PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online
```

## <a name="restore-data-protected-on-azure"></a><span data-ttu-id="bdfd1-286">Przywracanie danych chronionych na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="bdfd1-286">Restore data protected on Azure</span></span>
<span data-ttu-id="bdfd1-287">Przywracanie danych jest kombinacją ```RecoverableItem``` obiektu i ```RecoveryOption``` obiektu.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-287">Restoring data is a combination of a ```RecoverableItem``` object and a ```RecoveryOption``` object.</span></span> <span data-ttu-id="bdfd1-288">W poprzedniej sekcji dotarliśmy listę punktów kopii zapasowej dla źródła danych.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-288">In the previous section, we got a list of the backup points for a datasource.</span></span>

<span data-ttu-id="bdfd1-289">W poniższym przykładzie przedstawiony sposób przywracania maszyny wirtualnej funkcji Hyper-V z kopii zapasowej Azure dzięki połączeniu z elementem docelowym odzyskiwania punktów kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-289">In the example below, we demonstrate how to restore a Hyper-V virtual machine from Azure Backup by combining backup points with the target for recovery.</span></span> <span data-ttu-id="bdfd1-290">Obejmuje to:</span><span class="sxs-lookup"><span data-stu-id="bdfd1-290">This includes:</span></span>

* <span data-ttu-id="bdfd1-291">Utworzenie przy użyciu opcji odzyskiwania [DPMRecoveryOption nowy](https://technet.microsoft.com/library/hh881592) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-291">Creating a recovery option using the  [New-DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) cmdlet.</span></span>
* <span data-ttu-id="bdfd1-292">Tablica punktów kopii zapasowej przy użyciu pobierania ```Get-DPMRecoveryPoint``` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-292">Fetching the array of backup points using the ```Get-DPMRecoveryPoint``` cmdlet.</span></span>
* <span data-ttu-id="bdfd1-293">Wybieranie punktu kopii zapasowej do przywrócenia z.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-293">Choosing a backup point to restore from.</span></span>

```
PS C:\> $RecoveryOption = New-DPMRecoveryOption -HyperVDatasource -TargetServer "HVDCenter02" -RecoveryLocation AlternateHyperVServer -RecoveryType Recover -TargetLocation “C:\VMRecovery”

PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online

PS C:\> Restore-DPMRecoverableItem -RecoverableItem $RecoveryPoints[0] -RecoveryOption $RecoveryOption
```

<span data-ttu-id="bdfd1-294">Polecenia można z łatwością rozszerzyć dla dowolnego typu źródła danych.</span><span class="sxs-lookup"><span data-stu-id="bdfd1-294">The commands can easily be extended for any datasource type.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bdfd1-295">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bdfd1-295">Next steps</span></span>
* <span data-ttu-id="bdfd1-296">Aby uzyskać więcej informacji na temat tworzenia kopii zapasowej Azure dla programu DPM zobacz [wprowadzenie do kopii zapasowej programu DPM](backup-azure-dpm-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="bdfd1-296">For more information about Azure Backup for DPM see [Introduction to DPM Backup](backup-azure-dpm-introduction.md)</span></span>
