---
title: "Kopia zapasowa Azure: Użyj programu PowerShell tooback zapasowej obciążeń programu DPM | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toodeploy i zarządzanie nimi dla Data Protection Manager (DPM) przy użyciu programu PowerShell usługi Kopia zapasowa Azure"
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
ms.openlocfilehash: 48ebe6b520857836e89749ffb6fe83d1f14c5597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-backup-tooazure-for-data-protection-manager-dpm-servers-using-powershell"></a><span data-ttu-id="3c6cc-103">Wdrażanie i zarządzanie nimi tooAzure kopii zapasowej na serwerach Data Protection Manager (DPM) przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="3c6cc-103">Deploy and manage backup tooAzure for Data Protection Manager (DPM) servers using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3c6cc-104">ARM</span><span class="sxs-lookup"><span data-stu-id="3c6cc-104">ARM</span></span>](backup-dpm-automation.md)
> * [<span data-ttu-id="3c6cc-105">Wdrożenie klasyczne</span><span class="sxs-lookup"><span data-stu-id="3c6cc-105">Classic</span></span>](backup-dpm-automation-classic.md)
>
>

<span data-ttu-id="3c6cc-106">W tym artykule opisano sposób toouse PowerShell tooback Konfigurowanie i odzyskiwanie danych programu DPM z magazynu kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-106">This article explains how toouse PowerShell tooback up and recover DPM data from a backup vault.</span></span> <span data-ttu-id="3c6cc-107">Firma Microsoft zaleca używanie Magazyny usług odzyskiwania dla wszystkich nowych wdrożeń.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-107">Microsoft recommends using Recovery Services vaults for all new deployments.</span></span> <span data-ttu-id="3c6cc-108">Nowy użytkownik kopia zapasowa Azure, za pomocą hello artykułu, [wdrażanie i zarządzanie nimi przy użyciu programu PowerShell tooAzure danych programu Data Protection Manager](backup-dpm-automation.md), więc dane są przechowywane w magazynie usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-108">If you are a new Azure Backup user, use hello article, [Deploy and manage Data Protection Manager data tooAzure using PowerShell](backup-dpm-automation.md), so you store your data in a Recovery Services vault.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3c6cc-109">Teraz można uaktualnić Twoje Magazyny usług tooRecovery magazynów kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-109">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="3c6cc-110">Aby uzyskać więcej informacji, zobacz artykuł hello [uaktualnienia tooa magazynu kopii zapasowej, Magazyn usług odzyskiwania i](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="3c6cc-110">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="3c6cc-111">Firma Microsoft zachęca tooupgrade Magazyny usług tooRecovery magazyny kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-111">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="3c6cc-112">Po 15 października 2017 nie można użyć magazyny kopii zapasowych toocreate środowiska PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-112">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="3c6cc-113">**Do 1 listopada 2017 r.**:</span><span class="sxs-lookup"><span data-stu-id="3c6cc-113">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="3c6cc-114">Wszystkie pozostałe magazyny kopii zapasowych zostanie automatycznie uaktualniony tooRecovery Magazyny usług.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-114">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="3c6cc-115">Użytkownik nie będzie możliwe tooaccess danych kopii zapasowych w portalu klasycznym hello.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-115">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="3c6cc-116">Zamiast tego użyj hello Azure tooaccess portalu tej kopii zapasowej w Magazyny usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-116">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

## <a name="setting-up-hello-powershell-environment"></a><span data-ttu-id="3c6cc-117">Konfigurowanie środowiska PowerShell hello</span><span class="sxs-lookup"><span data-stu-id="3c6cc-117">Setting up hello PowerShell environment</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="3c6cc-118">Przed użyciem programu PowerShell toomanage tworzenia kopii zapasowych z tooAzure programu Data Protection Manager, należy toohave hello prawo środowiska PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-118">Before you can use PowerShell toomanage backups from Data Protection Manager tooAzure, you will need toohave hello right environment in PowerShell.</span></span> <span data-ttu-id="3c6cc-119">Na początku hello hello sesji programu PowerShell upewnij się, uruchom hello następujące polecenia tooimport hello prawo modułów i pozwala toocorrectly poleceń cmdlet DPM powitania dla odwołania:</span><span class="sxs-lookup"><span data-stu-id="3c6cc-119">At hello start of hello PowerShell session, ensure that you run hello following command tooimport hello right modules and allow you toocorrectly reference hello DPM cmdlets:</span></span>

```
PS C:> & "C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin\DpmCliInitScript.ps1"

Welcome toohello DPM Management Shell!

Full list of cmdlets: Get-Command
Only DPM cmdlets: Get-DPMCommand
Get general help: help
Get help for a cmdlet: help <cmdlet-name> or <cmdlet-name> -?
Get definition of a cmdlet: Get-Command <cmdlet-name> -Syntax
Sample DPM scripts: Get-DPMSampleScript
```

## <a name="setup-and-registration"></a><span data-ttu-id="3c6cc-120">Instalację i rejestrację</span><span class="sxs-lookup"><span data-stu-id="3c6cc-120">Setup and Registration</span></span>
<span data-ttu-id="3c6cc-121">toobegin:</span><span class="sxs-lookup"><span data-stu-id="3c6cc-121">toobegin:</span></span>

1. <span data-ttu-id="3c6cc-122">[Pobierz najnowsze PowerShell](https://github.com/Azure/azure-powershell/releases) (minimalna wersja wymagana jest: 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="3c6cc-122">[Download latest PowerShell](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>
2. <span data-ttu-id="3c6cc-123">Włącz polecenia cmdlet usługi Kopia zapasowa Azure hello przełączając zbyt*AzureResourceManager* trybie przy użyciu hello **Switch-AzureMode** apletu polecenia:</span><span class="sxs-lookup"><span data-stu-id="3c6cc-123">Enable hello Azure Backup commandlets by switching too*AzureResourceManager* mode by using hello **Switch-AzureMode** commandlet:</span></span>

```
PS C:\> Switch-AzureMode AzureResourceManager
```

<span data-ttu-id="3c6cc-124">Witaj następujące ustawienia i zadania rejestracji można zautomatyzować przy użyciu programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="3c6cc-124">hello following setup and registration tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="3c6cc-125">Tworzenie magazynu kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="3c6cc-125">Create a backup vault</span></span>
* <span data-ttu-id="3c6cc-126">Instalowanie agenta usługi Kopia zapasowa Azure hello</span><span class="sxs-lookup"><span data-stu-id="3c6cc-126">Installing hello Azure Backup agent</span></span>
* <span data-ttu-id="3c6cc-127">Rejestrowanie w hello usługi Kopia zapasowa Azure</span><span class="sxs-lookup"><span data-stu-id="3c6cc-127">Registering with hello Azure Backup service</span></span>
* <span data-ttu-id="3c6cc-128">Ustawienia sieciowe</span><span class="sxs-lookup"><span data-stu-id="3c6cc-128">Networking settings</span></span>
* <span data-ttu-id="3c6cc-129">Ustawienia szyfrowania</span><span class="sxs-lookup"><span data-stu-id="3c6cc-129">Encryption settings</span></span>

### <a name="create-a-backup-vault"></a><span data-ttu-id="3c6cc-130">Tworzenie magazynu kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="3c6cc-130">Create a backup vault</span></span>
> [!WARNING]
> <span data-ttu-id="3c6cc-131">W przypadku klientów przy kopia zapasowa Azure powitania po raz pierwszy należy tooregister hello kopia zapasowa Azure dostawcy toobe używane w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-131">For customers using Azure Backup for hello first time, you need tooregister hello Azure Backup provider toobe used with your subscription.</span></span> <span data-ttu-id="3c6cc-132">Można to zrobić, uruchamiając następujące polecenie hello: Register-AzureProvider - ProviderNamespace "Microsoft.Backup"</span><span class="sxs-lookup"><span data-stu-id="3c6cc-132">This can be done by running hello following command: Register-AzureProvider -ProviderNamespace "Microsoft.Backup"</span></span>
>
>

<span data-ttu-id="3c6cc-133">Można utworzyć nowy magazyn kopii zapasowych za pomocą hello **AzureRMBackupVault nowy** apletu polecenia.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-133">You can create a new backup vault using hello **New-AzureRMBackupVault** commandlet.</span></span> <span data-ttu-id="3c6cc-134">Hello magazynu kopii zapasowych jest zasobem ARM, więc należy tooplace go w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-134">hello backup vault is an ARM resource, so you need tooplace it within a Resource Group.</span></span> <span data-ttu-id="3c6cc-135">W konsoli programu Azure PowerShell z podwyższonym poziomem uprawnień uruchom następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="3c6cc-135">In an elevated Azure PowerShell console, run hello following commands:</span></span>

```
PS C:\> New-AzureResourceGroup –Name “test-rg” -Region “West US”
PS C:\> $backupvault = New-AzureRMBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GRS
```

<span data-ttu-id="3c6cc-136">Można uzyskać listę wszystkich magazynów kopii zapasowych hello w ramach danej subskrypcji przy użyciu hello **Get AzureRMBackupVault** apletu polecenia.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-136">You can get a list of all hello backup vaults in a given subscription using hello **Get-AzureRMBackupVault** commandlet.</span></span>

### <a name="installing-hello-azure-backup-agent-on-a-dpm-server"></a><span data-ttu-id="3c6cc-137">Instalowanie agenta usługi Kopia zapasowa Azure hello na serwerze programu DPM</span><span class="sxs-lookup"><span data-stu-id="3c6cc-137">Installing hello Azure Backup agent on a DPM Server</span></span>
<span data-ttu-id="3c6cc-138">Przed zainstalowaniem agenta usługi Kopia zapasowa Azure hello należy toohave hello Instalatora, pobranych i znajdują się na powitania serwera systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-138">Before you install hello Azure Backup agent, you need toohave hello installer downloaded and present on hello Windows Server.</span></span> <span data-ttu-id="3c6cc-139">Możesz pobrać najnowszą wersję Instalatora hello hello ze hello [Microsoft Download Center](http://aka.ms/azurebackup_agent) lub ze strony pulpitu nawigacyjnego hello magazynu kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-139">You can get hello latest version of hello installer from hello [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from hello backup vault's Dashboard page.</span></span> <span data-ttu-id="3c6cc-140">Zapisz Instalator hello tooan łatwo dostępnej lokalizacji, takich jak * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-140">Save hello installer tooan easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="3c6cc-141">tooinstall hello agenta, uruchom następujące polecenie w konsoli programu PowerShell z podwyższonym poziomem uprawnień hello **na serwerze DPM hello**:</span><span class="sxs-lookup"><span data-stu-id="3c6cc-141">tooinstall hello agent, run hello following command in an elevated PowerShell console **on hello DPM server**:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="3c6cc-142">Spowoduje to zainstalowanie agenta hello z wszystkich opcji domyślnych hello.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-142">This installs hello agent with all hello default options.</span></span> <span data-ttu-id="3c6cc-143">Instalacja Hello zajmuje kilka minut w tle hello.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-143">hello installation takes a few minutes in hello background.</span></span> <span data-ttu-id="3c6cc-144">Jeśli nie określisz hello */nu* hello opcja **usługi Windows Update** na końcu hello hello toocheck instalacji dla wszystkich aktualizacji, zostanie otwarte okno.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-144">If you do not specify hello */nu* option hello **Windows Update** window will open at hello end of hello installation toocheck for any updates.</span></span>

<span data-ttu-id="3c6cc-145">Hello agent wyświetli hello listy zainstalowanych programów.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-145">hello agent will show in hello list of installed programs.</span></span> <span data-ttu-id="3c6cc-146">toosee hello listy zainstalowanych programów, należy przejść za**Panelu sterowania** > **programy** > **programy i funkcje**.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-146">toosee hello list of installed programs, go too**Control Panel** > **Programs** > **Programs and Features**.</span></span>

![Agent został zainstalowany](./media/backup-dpm-automation/installed-agent-listing.png)

#### <a name="installation-options"></a><span data-ttu-id="3c6cc-148">Opcje instalacji</span><span class="sxs-lookup"><span data-stu-id="3c6cc-148">Installation options</span></span>
<span data-ttu-id="3c6cc-149">toosee, który hello wszystkie opcje dostępne za pośrednictwem hello wiersza polecenia, użyj następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="3c6cc-149">toosee all hello options available via hello command-line, use hello following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="3c6cc-150">Witaj dostępne opcje to:</span><span class="sxs-lookup"><span data-stu-id="3c6cc-150">hello available options include:</span></span>

| <span data-ttu-id="3c6cc-151">Opcja</span><span class="sxs-lookup"><span data-stu-id="3c6cc-151">Option</span></span> | <span data-ttu-id="3c6cc-152">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="3c6cc-152">Details</span></span> | <span data-ttu-id="3c6cc-153">Domyślne</span><span class="sxs-lookup"><span data-stu-id="3c6cc-153">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3c6cc-154">/q</span><span class="sxs-lookup"><span data-stu-id="3c6cc-154">/q</span></span> |<span data-ttu-id="3c6cc-155">Instalację cichą</span><span class="sxs-lookup"><span data-stu-id="3c6cc-155">Quiet installation</span></span> |- |
| <span data-ttu-id="3c6cc-156">/ p: "Lokalizacja"</span><span class="sxs-lookup"><span data-stu-id="3c6cc-156">/p:"location"</span></span> |<span data-ttu-id="3c6cc-157">Ścieżka folderu instalacji toohello hello Azure Backup Agent.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-157">Path toohello installation folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="3c6cc-158">C:\Program Files\Microsoft Azure Recovery usługi agenta</span><span class="sxs-lookup"><span data-stu-id="3c6cc-158">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="3c6cc-159">/ s: "Lokalizacja"</span><span class="sxs-lookup"><span data-stu-id="3c6cc-159">/s:"location"</span></span> |<span data-ttu-id="3c6cc-160">Ścieżka folderu pamięci podręcznej toohello hello Azure Backup Agent.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-160">Path toohello cache folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="3c6cc-161">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="3c6cc-161">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="3c6cc-162">/m</span><span class="sxs-lookup"><span data-stu-id="3c6cc-162">/m</span></span> |<span data-ttu-id="3c6cc-163">TooMicrosoft opcjonalnych aktualizacji</span><span class="sxs-lookup"><span data-stu-id="3c6cc-163">Opt-in tooMicrosoft Update</span></span> |- |
| <span data-ttu-id="3c6cc-164">/nu</span><span class="sxs-lookup"><span data-stu-id="3c6cc-164">/nu</span></span> |<span data-ttu-id="3c6cc-165">Nie sprawdzaj aktualizacji po ukończeniu instalacji</span><span class="sxs-lookup"><span data-stu-id="3c6cc-165">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="3c6cc-166">/d</span><span class="sxs-lookup"><span data-stu-id="3c6cc-166">/d</span></span> |<span data-ttu-id="3c6cc-167">Odinstalowuje agenta usług odzyskiwania Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="3c6cc-167">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="3c6cc-168">/pH</span><span class="sxs-lookup"><span data-stu-id="3c6cc-168">/ph</span></span> |<span data-ttu-id="3c6cc-169">Adres hosta serwera proxy</span><span class="sxs-lookup"><span data-stu-id="3c6cc-169">Proxy Host Address</span></span> |- |
| <span data-ttu-id="3c6cc-170">/Po</span><span class="sxs-lookup"><span data-stu-id="3c6cc-170">/po</span></span> |<span data-ttu-id="3c6cc-171">Numer portu hosta serwera proxy</span><span class="sxs-lookup"><span data-stu-id="3c6cc-171">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="3c6cc-172">/Pu</span><span class="sxs-lookup"><span data-stu-id="3c6cc-172">/pu</span></span> |<span data-ttu-id="3c6cc-173">Nazwa użytkownika serwera proxy hosta</span><span class="sxs-lookup"><span data-stu-id="3c6cc-173">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="3c6cc-174">/PW</span><span class="sxs-lookup"><span data-stu-id="3c6cc-174">/pw</span></span> |<span data-ttu-id="3c6cc-175">Hasło serwera proxy</span><span class="sxs-lookup"><span data-stu-id="3c6cc-175">Proxy Password</span></span> |- |

### <a name="registering-with-hello-azure-backup-service"></a><span data-ttu-id="3c6cc-176">Rejestrowanie w hello usługi Kopia zapasowa Azure</span><span class="sxs-lookup"><span data-stu-id="3c6cc-176">Registering with hello Azure Backup service</span></span>
<span data-ttu-id="3c6cc-177">Przed zarejestrowaniem z hello usługi Kopia zapasowa Azure, należy tooensure tego hello [wymagania wstępne](backup-azure-dpm-introduction.md) są spełnione.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-177">Before you can register with hello Azure Backup service, you need tooensure that hello [prerequisites](backup-azure-dpm-introduction.md) are met.</span></span> <span data-ttu-id="3c6cc-178">Należy:</span><span class="sxs-lookup"><span data-stu-id="3c6cc-178">You must:</span></span>

* <span data-ttu-id="3c6cc-179">Masz ważną subskrypcję platformy Azure</span><span class="sxs-lookup"><span data-stu-id="3c6cc-179">Have a valid Azure subscription</span></span>
* <span data-ttu-id="3c6cc-180">Masz magazyn kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="3c6cc-180">Have a backup vault</span></span>

<span data-ttu-id="3c6cc-181">poświadczenia magazynu hello toodownload Uruchom hello **Get-AzureBackupVaultCredentials** polecenia w konsoli programu PowerShell systemu Azure i zapisać go w dogodnym miejscu, takich jak * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-181">toodownload hello vault credentials, run hello **Get-AzureBackupVaultCredentials** commandlet in an Azure PowerShell console and store it in a convenient location like *C:\Downloads\*.</span></span>

```
PS C:\> $credspath = "C:\"
PS C:\> $credsfilename = Get-AzureRMBackupVaultCredentials -Vault $backupvault -TargetLocation $credspath
PS C:\> $credsfilename
f5303a0b-fae4-4cdb-b44d-0e4c032dde26_backuprg_backuprn_2015-08-11--06-22-35.VaultCredentials
```

<span data-ttu-id="3c6cc-182">Rejestracji hello maszyny z magazynem hello jest wykonywane przy użyciu hello [Start DPMCloudRegistration](https://technet.microsoft.com/library/jj612787) polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="3c6cc-182">Registering hello machine with hello vault is done using hello [Start-DPMCloudRegistration](https://technet.microsoft.com/library/jj612787) cmdlet:</span></span>

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-DPMCloudRegistration -DPMServerName "TestingServer" -VaultCredentialsFilePath $cred
```

<span data-ttu-id="3c6cc-183">To zarejestruje hello o nazwie "Serwerach" serwera DPM w magazynie usługi Microsoft Azure przy użyciu hello określone poświadczenia magazynu.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-183">This will register hello DPM Server named “TestingServer” with Microsoft Azure Vault using hello specified vault credentials.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3c6cc-184">Nie należy używać pliku poświadczeń magazynu hello toospecify ścieżek względnych.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-184">Do not use relative paths toospecify hello vault credentials file.</span></span> <span data-ttu-id="3c6cc-185">Należy podać ścieżkę bezwzględną jako polecenia cmdlet toohello wejściowego.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-185">You must provide an absolute path as an input toohello cmdlet.</span></span>
>
>

### <a name="initial-configuration-settings"></a><span data-ttu-id="3c6cc-186">Ustawienia konfiguracji początkowej</span><span class="sxs-lookup"><span data-stu-id="3c6cc-186">Initial configuration settings</span></span>
<span data-ttu-id="3c6cc-187">Po hello serwer DPM jest zarejestrowany w magazynie usługi Kopia zapasowa Azure hello, rozpoczyna się od domyślnego ustawienia subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-187">Once hello DPM Server is registered with hello Azure Backup vault, it will start with default subscription settings.</span></span> <span data-ttu-id="3c6cc-188">Te ustawienia subskrypcji obejmują sieci, szyfrowania i hello obszaru przemieszczania.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-188">These subscription settings include Networking, Encryption and hello Staging area.</span></span> <span data-ttu-id="3c6cc-189">toobegin zmiana hello subskrypcji ustawień należy toofirst uzyskać dojścia do na powitania istniejące ustawienia (ustawienie domyślne) przy użyciu hello [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="3c6cc-189">toobegin changing hello subscription settings you need toofirst get a handle on hello existing (default) settings using hello [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet:</span></span>

```
$setting = Get-DPMCloudSubscriptionSetting -DPMServerName "TestingServer"
```

<span data-ttu-id="3c6cc-190">Wszystkie modyfikacje są wykonane toothis lokalnego środowiska PowerShell obiektu ```$setting``` , a następnie obiektowego hello jest tooDPM zatwierdzone i kopia zapasowa Azure toosave je przy użyciu hello [DPMCloudSubscriptionSetting zestaw](https://technet.microsoft.com/library/jj612791) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-190">All modifications are made toothis local PowerShell object ```$setting```  and then hello full object is committed tooDPM and Azure Backup toosave them using hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="3c6cc-191">Należy toouse hello ```–Commit``` tooensure flagę, która hello zmiany są zachowywane.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-191">You need toouse hello ```–Commit``` flag tooensure that hello changes are persisted.</span></span> <span data-ttu-id="3c6cc-192">Witaj ustawienia nie będą stosowane i używane przez usługi Kopia zapasowa Azure, chyba że zostało zatwierdzone.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-192">hello settings will not be applied and used by Azure Backup unless committed.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

### <a name="networking"></a><span data-ttu-id="3c6cc-193">Sieć</span><span class="sxs-lookup"><span data-stu-id="3c6cc-193">Networking</span></span>
<span data-ttu-id="3c6cc-194">W przypadku łączności hello hello DPM maszyny toohello usługi Azure Backup na powitania internet za pośrednictwem serwera proxy, ustawienia serwera proxy hello należy podać dla toosucceed kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-194">If hello connectivity of hello DPM machine toohello Azure Backup service on hello internet is through a proxy server, then hello proxy server settings should be provided for backups toosucceed.</span></span> <span data-ttu-id="3c6cc-195">Jest to zrobić za pomocą hello ```-ProxyServer```, ```-ProxyPort```, ```-ProxyUsername``` i hello ```ProxyPassword``` parametrów z hello [DPMCloudSubscriptionSetting zestaw](https://technet.microsoft.com/library/jj612791) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-195">This is done by using hello ```-ProxyServer```, ```-ProxyPort```, ```-ProxyUsername``` and hello ```ProxyPassword``` parameters with hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="3c6cc-196">W tym przykładzie nie żadnego serwera proxy, dlatego firma Microsoft są jawnie wyczyszczenie żadnych informacji dotyczących serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-196">In this example, there is no proxy server so we are explicitly clearing any proxy-related information.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoProxy
```

<span data-ttu-id="3c6cc-197">Wykorzystanie przepustowości można również sterować za pomocą opcji ```-WorkHourBandwidth``` i ```-NonWorkHourBandwidth``` dla danego zestawu dni tygodnia hello.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-197">Bandwidth usage can also be controlled with options of ```-WorkHourBandwidth``` and ```-NonWorkHourBandwidth``` for a given set of days of hello week.</span></span> <span data-ttu-id="3c6cc-198">W tym przykładzie firma Microsoft nie ustawienia dowolnej ograniczania.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-198">In this example we are not setting any throttling.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoThrottle
```

### <a name="configuring-hello-staging-area"></a><span data-ttu-id="3c6cc-199">Konfigurowanie hello obszaru przemieszczania</span><span class="sxs-lookup"><span data-stu-id="3c6cc-199">Configuring hello staging Area</span></span>
<span data-ttu-id="3c6cc-200">agent usługi Kopia zapasowa Azure Hello działającej na serwerze DPM hello wymaga tymczasowego magazynu dla danych przywróconych z chmury hello (lokalny obszar przemieszczania).</span><span class="sxs-lookup"><span data-stu-id="3c6cc-200">hello Azure Backup agent running on hello DPM server needs temporary storage for data restored from hello cloud (local staging area).</span></span> <span data-ttu-id="3c6cc-201">Konfigurowanie przy użyciu hello obszaru przemieszczania hello [DPMCloudSubscriptionSetting zestaw](https://technet.microsoft.com/library/jj612791) polecenia cmdlet i hello ```-StagingAreaPath``` parametru.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-201">Configure hello staging area using hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet and hello ```-StagingAreaPath``` parameter.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -StagingAreaPath "C:\StagingArea"
```

<span data-ttu-id="3c6cc-202">W powyższym przykładzie hello, obszaru przemieszczania hello zostanie ustawiona zbyt*C:\StagingArea* w obiekcie środowiska PowerShell hello ```$setting```.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-202">In hello example above, hello staging area will be set too*C:\StagingArea* in hello PowerShell object ```$setting```.</span></span> <span data-ttu-id="3c6cc-203">Upewnij się, że hello określony folder już istnieje, w przeciwnym razie hello końcowego zatwierdzania ustawienia subskrypcji hello zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-203">Ensure that hello specified folder already exists, or else hello final commit of hello subscription settings will fail.</span></span>

### <a name="encryption-settings"></a><span data-ttu-id="3c6cc-204">Ustawienia szyfrowania</span><span class="sxs-lookup"><span data-stu-id="3c6cc-204">Encryption settings</span></span>
<span data-ttu-id="3c6cc-205">tooAzure wysyłane dane kopii zapasowej Hello kopii zapasowej jest zaszyfrowany tooprotect hello poufność danych hello.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-205">hello backup data sent tooAzure Backup is encrypted tooprotect hello confidentiality of hello data.</span></span> <span data-ttu-id="3c6cc-206">hasło szyfrowania Hello jest hello "password" toodecrypt hello danych w czasie hello przywracania.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-206">hello encryption passphrase is hello "password" toodecrypt hello data at hello time of restore.</span></span> <span data-ttu-id="3c6cc-207">Jest to bezpieczne informacje ważne tookeep i secure po ustawieniu.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-207">It is important tookeep this information safe and secure once it is set.</span></span>

<span data-ttu-id="3c6cc-208">W poniższym przykładzie hello, pierwsze polecenie hello konwertuje ciąg hello ```passphrase123456789``` tooa bezpieczny ciąg i przypisuje hello bezpieczny ciąg toohello zmiennej o nazwie ```$Passphrase```.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-208">In hello example below, hello first command converts hello string ```passphrase123456789``` tooa secure string and assigns hello secure string toohello variable named ```$Passphrase```.</span></span> <span data-ttu-id="3c6cc-209">drugie polecenie Hello ustawia bezpieczny ciąg hello w ```$Passphrase``` jako hello hasła do szyfrowania kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-209">hello second command sets hello secure string in ```$Passphrase``` as hello password for encrypting backups.</span></span>

```
PS C:\> $Passphrase = ConvertTo-SecureString -string "passphrase123456789" -AsPlainText -Force

PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -EncryptionPassphrase $Passphrase
```

> [!IMPORTANT]
> <span data-ttu-id="3c6cc-210">Zachowaj informacje hasło hello bezpieczne po ustawieniu.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-210">Keep hello passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="3c6cc-211">Nie będzie możliwe toorestore danych z platformy Azure bez tego hasła.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-211">You will not be able toorestore data from Azure without this passphrase.</span></span>
>
>

<span data-ttu-id="3c6cc-212">W tym momencie powinien wprowadzone wszystkie hello wymagane zmiany toohello ```$setting``` obiektu.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-212">At this point, you should have made all hello required changes toohello ```$setting``` object.</span></span> <span data-ttu-id="3c6cc-213">Należy pamiętać, toocommit hello zmiany.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-213">Remember toocommit hello changes.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="protect-data-tooazure-backup"></a><span data-ttu-id="3c6cc-214">Ochrona danych tooAzure kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="3c6cc-214">Protect data tooAzure Backup</span></span>
<span data-ttu-id="3c6cc-215">W tej sekcji możesz dodać tooDPM serwera produkcyjnego i chronić magazynu programu DPM toolocal danych hello, a następnie tooAzure kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-215">In this section, you will add a production server tooDPM and then protect hello data toolocal DPM storage and then tooAzure Backup.</span></span> <span data-ttu-id="3c6cc-216">W przykładach hello przedstawiony zostanie sposób tooback zapasowe plików i folderów.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-216">In hello examples we will demonstrate how tooback up files and folders.</span></span> <span data-ttu-id="3c6cc-217">Witaj logiki można łatwo można toobackup rozszerzonej z dowolnego źródła danych obsługiwane przez program DPM.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-217">hello logic can easily be extended toobackup any DPM-supported data source.</span></span> <span data-ttu-id="3c6cc-218">Kopii zapasowych programu DPM są regulowane przez ochronę grupy (PG) z czterech części:</span><span class="sxs-lookup"><span data-stu-id="3c6cc-218">All your DPM backups are governed by a Protection Group (PG) with four parts:</span></span>

1. <span data-ttu-id="3c6cc-219">**Członków grupy** znajduje się lista wszystkich hello obiekty chronione (nazywane również *źródeł danych* w programie DPM), które mają tooprotect w hello tej samej grupy ochrony.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-219">**Group members** is a list of all hello protectable objects (also known as *Datasources* in DPM) that you want tooprotect in hello same protection group.</span></span> <span data-ttu-id="3c6cc-220">Na przykład można tooprotect produkcji maszyny wirtualne w jednej grupy ochrony i baz danych programu SQL Server w innej grupy ochrony jako mogą mieć różne wymagania kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-220">For example, you may want tooprotect production VMs in one protection group and SQL Server databases in another protection group as they may have different backup requirements.</span></span> <span data-ttu-id="3c6cc-221">Przed utworzeniem kopii zapasowej żadnego źródła danych na serwerze produkcyjnym należy toomake hello się, że Agent programu DPM jest zainstalowany na serwerze hello i jest zarządzany przez program DPM.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-221">Before you can back up any datasource on a production server you need toomake sure hello DPM Agent is installed on hello server and is managed by DPM.</span></span> <span data-ttu-id="3c6cc-222">Wykonaj procedurę hello [instalowanie hello agenta DPM](https://technet.microsoft.com/library/bb870935.aspx) i połączenie go toohello odpowiednie serwera DPM.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-222">Follow hello steps for [installing hello DPM Agent](https://technet.microsoft.com/library/bb870935.aspx) and linking it toohello appropriate DPM Server.</span></span>
2. <span data-ttu-id="3c6cc-223">**Metoda ochrony danych** określa hello docelowej lokalizacji kopii zapasowych — taśma, dysk i chmura.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-223">**Data protection method** specifies hello target backup locations - tape, disk, and cloud.</span></span> <span data-ttu-id="3c6cc-224">W naszym przykładzie będzie chronić danych toohello lokalny dysk i toohello w chmurze.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-224">In our example we will protect data toohello local disk and toohello cloud.</span></span>
3. <span data-ttu-id="3c6cc-225">A **harmonogram tworzenia kopii zapasowych** , który określa podczas tworzenia kopii zapasowych należy toobe podjęte i jak często hello dane mają być synchronizowane między hello serwera programu DPM i serwerze produkcyjnym hello.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-225">A **backup schedule** that specifies when backups need toobe taken and how often hello data should be synchronized between hello DPM Server and hello production server.</span></span>
4. <span data-ttu-id="3c6cc-226">A **harmonogramu przechowywania** Określa, jak długo punkty odzyskiwania hello tooretain na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-226">A **retention schedule** that specifies how long tooretain hello recovery points in Azure.</span></span>

### <a name="creating-a-protection-group"></a><span data-ttu-id="3c6cc-227">Utworzenie grupy ochrony</span><span class="sxs-lookup"><span data-stu-id="3c6cc-227">Creating a protection group</span></span>
<span data-ttu-id="3c6cc-228">Rozpocznij od utworzenia nowej grupy ochrony za pomocą hello [DPMProtectionGroup nowy](https://technet.microsoft.com/library/hh881722) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-228">Start by creating a new Protection Group using hello [New-DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) cmdlet.</span></span>

```
PS C:\> $PG = New-DPMProtectionGroup -DPMServerName " TestingServer " -Name "ProtectGroup01"
```

<span data-ttu-id="3c6cc-229">Witaj powyżej polecenie cmdlet spowoduje utworzenie grupy ochrony o nazwie *ProtectGroup01*.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-229">hello above cmdlet will create a Protection Group named *ProtectGroup01*.</span></span> <span data-ttu-id="3c6cc-230">Istniejącej grupy ochrony można także modyfikować nowszych kopii zapasowej tooadd toohello chmury Azure.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-230">An existing protection group can also be modified later tooadd backup toohello Azure cloud.</span></span> <span data-ttu-id="3c6cc-231">Jednak toomake zmiany toohello grupy ochrony — nowy lub istniejący - potrzebujemy tooget dojścia na *modyfikowalnymi* obiektu przy użyciu hello [Get DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-231">However, toomake any changes toohello Protection Group - new or existing - we need tooget a handle on a *modifiable* object using hello [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) cmdlet.</span></span>

```
PS C:\> $MPG = Get-ModifiableProtectionGroup $PG
```

### <a name="adding-group-members-toohello-protection-group"></a><span data-ttu-id="3c6cc-232">Dodawanie grupy toohello członków grupy ochrony</span><span class="sxs-lookup"><span data-stu-id="3c6cc-232">Adding group members toohello Protection Group</span></span>
<span data-ttu-id="3c6cc-233">Każdy Agent programu DPM wie hello listy źródeł danych na powitania serwera, który jest zainstalowany na.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-233">Each DPM Agent knows hello list of datasources on hello server that it is installed on.</span></span> <span data-ttu-id="3c6cc-234">tooadd toohello datasource grupy ochrony, hello toofirst potrzeb agenta DPM wysyła listę hello źródeł danych toohello zapasowego serwera programu DPM.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-234">tooadd a datasource toohello Protection Group, hello DPM Agent needs toofirst send a list of hello datasources back toohello DPM server.</span></span> <span data-ttu-id="3c6cc-235">Jeden lub więcej źródeł danych są, a następnie wybrać i dodać toohello grupy ochrony.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-235">One or more datasources are then selected and added toohello Protection Group.</span></span> <span data-ttu-id="3c6cc-236">tooget kroki niezbędne PowerShell Hello osiągnięcia się to:</span><span class="sxs-lookup"><span data-stu-id="3c6cc-236">hello PowerShell steps needed tooget achieve this are:</span></span>

1. <span data-ttu-id="3c6cc-237">Pobierz listę wszystkich serwerów zarządzanych przez program DPM za pomocą hello agenta programu DPM.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-237">Fetch a list of all servers managed by DPM through hello DPM Agent.</span></span>
2. <span data-ttu-id="3c6cc-238">Wybierz określonego serwera.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-238">Choose a specific server.</span></span>
3. <span data-ttu-id="3c6cc-239">Pobranie listy wszystkich źródeł danych na powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-239">Fetch a list of all datasources on hello server.</span></span>
4. <span data-ttu-id="3c6cc-240">Wybierz co najmniej jednego źródła danych, a następnie dodać toohello grupy ochrony</span><span class="sxs-lookup"><span data-stu-id="3c6cc-240">Choose one or more datasources and add them toohello Protection Group</span></span>

<span data-ttu-id="3c6cc-241">Hello listy serwerów, na które hello agenta programu DPM jest zainstalowany i jest zarządzany przez powitania serwera programu DPM są uzyskiwane z hello [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-241">hello list of servers on which hello DPM Agent is installed and is being managed by hello DPM Server is acquired with hello [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet.</span></span> <span data-ttu-id="3c6cc-242">W tym przykładzie firma Microsoft będzie filtrowania i skonfigurować tylko PS o nazwie *productionserver01* do utworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-242">In this example we will filter and only configure PS with name *productionserver01* for backup.</span></span>

```
PS C:\> $server = Get-ProductionServer -DPMServerName "TestingServer" | where {($_.servername) –contains “productionserver01”
```

<span data-ttu-id="3c6cc-243">Teraz pobrać hello listy źródeł danych na ```$server``` przy użyciu hello [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-243">Now fetch hello list of datasources on ```$server``` using hello [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet.</span></span> <span data-ttu-id="3c6cc-244">W tym przykładzie mamy filtrowania dla woluminu hello * D:\* którego chcemy tooconfigure do utworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-244">In this example we are filtering for hello volume *D:\* which we want tooconfigure for backup.</span></span> <span data-ttu-id="3c6cc-245">To źródło danych jest następnie dodawana toohello grupy ochrony za pomocą hello [DPMChildDatasource Dodaj](https://technet.microsoft.com/library/hh881732) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-245">This datasource is then added toohello Protection Group using hello [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet.</span></span> <span data-ttu-id="3c6cc-246">Pamiętaj toouse hello *modifable* obiektu grupy ochrony ```$MPG``` toomake hello dodatków.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-246">Remember toouse hello *modifable* protection group object ```$MPG``` toomake hello additions.</span></span>

```
PS C:\> $DS = Get-Datasource -ProductionServer $server -Inquire | where { $_.Name -contains “D:\” }

PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS
```

<span data-ttu-id="3c6cc-247">Powtórz ten krok liczbę razy, aż zostaną dodane wszystkie hello wybrane grupy ochrony toohello źródeł danych.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-247">Repeat this step as many times as required, until you have added all hello chosen datasources toohello protection group.</span></span> <span data-ttu-id="3c6cc-248">Można również uruchomić tylko jedno źródło danych i hello pełny przepływ pracy tworzenia hello grupy ochrony i w późniejszym czasie dodać więcej źródeł danych toohello grupy ochrony.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-248">You can also start with just one datasource, and complete hello workflow for creating hello Protection Group, and at a later point add more datasources toohello Protection Group.</span></span>

### <a name="selecting-hello-data-protection-method"></a><span data-ttu-id="3c6cc-249">Wybieranie metody ochrony danych hello</span><span class="sxs-lookup"><span data-stu-id="3c6cc-249">Selecting hello data protection method</span></span>
<span data-ttu-id="3c6cc-250">Po dodaniu źródła danych hello toohello grupy ochrony, hello następnym krokiem jest metoda ochrony hello toospecify przy użyciu hello [DPMProtectionType zestaw](https://technet.microsoft.com/library/hh881725) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-250">Once hello datasources have been added toohello Protection Group, hello next step is toospecify hello protection method using hello [Set-DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet.</span></span> <span data-ttu-id="3c6cc-251">W tym przykładzie hello grupy ochrony będzie instalacji na dysku lokalnym, a kopia zapasowa w chmurze.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-251">In this example, hello Protection Group will be setup for local disk and cloud backup.</span></span> <span data-ttu-id="3c6cc-252">Należy również toospecify hello datasource, które mają toocloud tooprotect przy użyciu hello [DPMChildDatasource Dodaj](https://technet.microsoft.com/library/hh881732.aspx) polecenia cmdlet flagą - Online.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-252">You also need toospecify hello datasource that you want tooprotect toocloud using hello [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet with -Online flag.</span></span>

```
PS C:\> Set-DPMProtectionType -ProtectionGroup $MPG -ShortTerm Disk –LongTerm Online
PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS –Online
```

### <a name="setting-hello-retention-range"></a><span data-ttu-id="3c6cc-253">Ustawianie zakresu przechowywania hello</span><span class="sxs-lookup"><span data-stu-id="3c6cc-253">Setting hello retention range</span></span>
<span data-ttu-id="3c6cc-254">Ustawienia przechowywania hello hello punktów kopii zapasowej za pomocą hello [DPMPolicyObjective zestaw](https://technet.microsoft.com/library/hh881762) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-254">Set hello retention for hello backup points using hello [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span> <span data-ttu-id="3c6cc-255">Gdy może wydawać się przechowywania hello nieparzysta tooset przed zdefiniowaniem hello harmonogram tworzenia kopii zapasowych, przy użyciu hello ```Set-DPMPolicyObjective``` polecenie cmdlet automatycznie ustawia domyślny harmonogram tworzenia kopii zapasowej, który może być modyfikowany.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-255">While it might seem odd tooset hello retention before hello backup schedule has been defined, using hello ```Set-DPMPolicyObjective``` cmdlet automatically sets a default backup schedule that can then be modified.</span></span> <span data-ttu-id="3c6cc-256">Jest zawsze harmonogram tworzenia kopii zapasowych hello możliwe tooset najpierw i hello zasady przechowywania po.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-256">It is always possible tooset hello backup schedule first and hello retention policy after.</span></span>

<span data-ttu-id="3c6cc-257">W poniższym przykładzie hello polecenia cmdlet hello ustawia hello parametry przechowywania kopii zapasowych na dysku.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-257">In hello example below, hello cmdlet sets hello retention parameters for disk backups.</span></span> <span data-ttu-id="3c6cc-258">To zachowują kopie zapasowe 10 dni i synchronizowanie danych co 6 godzin między serwerem produkcyjnym hello i hello programu DPM.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-258">This will retain backups for 10 days, and sync data every 6 hours between hello production server and hello DPM server.</span></span> <span data-ttu-id="3c6cc-259">Witaj ```SynchronizationFrequencyMinutes``` nie definiuje, jak często punktu kopii zapasowej jest tworzony, ale jak często dane serwera DPM toohello skopiowanych; zapobiega to kopie zapasowe za duży.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-259">hello ```SynchronizationFrequencyMinutes``` doesn't define how often a backup point is created, but how often data is copied toohello DPM server; this prevents backups from becoming too large.</span></span>

```
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -RetentionRangeInDays 10 -SynchronizationFrequencyMinutes 360
```

<span data-ttu-id="3c6cc-260">Kopii zapasowych będzie tooAzure (Program DPM stosowany jest wspólny termin toothese kopii zapasowych Online) można skonfigurować dla zakresów przechowywania hello [długoterminowych przechowywania użyciu schematu dziadek-ojciec-syn. (GFS)](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="3c6cc-260">For backups going tooAzure (DPM refers toothese as Online backups) hello retention ranges can be configured for [long term retention using a Grandfather-Father-Son scheme (GFS)](backup-azure-backup-cloud-as-tape.md).</span></span> <span data-ttu-id="3c6cc-261">Oznacza to można zdefiniować zasady przechowywania Scalonej obejmujące codziennie, co tydzień, miesięcznych i rocznych zasady przechowywania.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-261">That is, you can define a combined retention policy involving daily, weekly, monthly and yearly retention policies.</span></span> <span data-ttu-id="3c6cc-262">W tym przykładzie firma Microsoft utworzenia tablicy reprezentujący schemat przechowywania złożonych hello chcemy, a następnie skonfiguruj zakres przechowywania hello za pomocą hello [DPMPolicyObjective zestaw](https://technet.microsoft.com/library/hh881762) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-262">In this example, we create an array representing hello complex retention scheme that we want, and then configure hello retention range using hello [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span>

```
PS C:\> $RRlist = @()
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 180, Days)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 104, Weeks)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 60, Month)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 10, Years)
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -OnlineRetentionRangeList $RRlist
```

### <a name="set-hello-backup-schedule"></a><span data-ttu-id="3c6cc-263">Harmonogram tworzenia kopii zapasowych hello zestawu</span><span class="sxs-lookup"><span data-stu-id="3c6cc-263">Set hello backup schedule</span></span>
<span data-ttu-id="3c6cc-264">Program DPM ustawia automatycznie domyślny harmonogram tworzenia kopii zapasowej, jeśli Określ cel ochrony hello przy użyciu hello ```Set-DPMPolicyObjective``` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-264">DPM sets a default backup schedule automatically if you specify hello protection objective using hello ```Set-DPMPolicyObjective``` cmdlet.</span></span> <span data-ttu-id="3c6cc-265">toochange hello domyślne harmonogramy, użyj hello [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) polecenia cmdlet następuje hello [DPMPolicySchedule zestaw](https://technet.microsoft.com/library/hh881723) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-265">toochange hello default schedules, use hello [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet followed by hello [Set-DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) cmdlet.</span></span>

```
PS C:\> $onlineSch = Get-DPMPolicySchedule -ProtectionGroup $mpg -LongTerm Online
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[0] -TimesOfDay 02:00
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[1] -TimesOfDay 02:00 -DaysOfWeek Sa,Su –Interval 1
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[2] -TimesOfDay 02:00 -RelativeIntervals First,Third –DaysOfWeek Sa
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[3] -TimesOfDay 02:00 -DaysOfMonth 2,5,8,9 -Months Jan,Jul
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```

<span data-ttu-id="3c6cc-266">W powyższym przykładzie hello ```$onlineSch``` jest tablicy z czterech elementów, które zawierają hello istniejący harmonogram ochrony w trybie online dla hello grupy ochrony w schemacie GFS hello:</span><span class="sxs-lookup"><span data-stu-id="3c6cc-266">In hello example above, ```$onlineSch``` is an array with four elements that contains hello existing online protection schedule for hello Protection Group in hello GFS scheme:</span></span>

1. <span data-ttu-id="3c6cc-267">```$onlineSch[0]```będzie zawierać harmonogramu dziennego hello</span><span class="sxs-lookup"><span data-stu-id="3c6cc-267">```$onlineSch[0]``` will contain hello daily schedule</span></span>
2. <span data-ttu-id="3c6cc-268">```$onlineSch[1]```będzie zawierać hello harmonogramu tygodniowego</span><span class="sxs-lookup"><span data-stu-id="3c6cc-268">```$onlineSch[1]``` will contain hello weekly schedule</span></span>
3. <span data-ttu-id="3c6cc-269">```$onlineSch[2]```będzie zawierać hello harmonogramu miesięcznego</span><span class="sxs-lookup"><span data-stu-id="3c6cc-269">```$onlineSch[2]``` will contain hello monthly schedule</span></span>
4. <span data-ttu-id="3c6cc-270">```$onlineSch[3]```będzie zawierać hello corocznych harmonogramu</span><span class="sxs-lookup"><span data-stu-id="3c6cc-270">```$onlineSch[3]``` will contain hello yearly schedule</span></span>

<span data-ttu-id="3c6cc-271">Więc jeśli potrzebujesz harmonogramu tygodniowego hello toomodify należy toorefer toohello ```$onlineSch[1]```.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-271">So if you need toomodify hello weekly schedule, you need toorefer toohello ```$onlineSch[1]```.</span></span>

### <a name="initial-backup"></a><span data-ttu-id="3c6cc-272">Początkowa kopia zapasowa</span><span class="sxs-lookup"><span data-stu-id="3c6cc-272">Initial backup</span></span>
<span data-ttu-id="3c6cc-273">Podczas wykonywania kopii zapasowej źródła danych powitania po raz pierwszy, program DPM musi toocreate repliki początkowej, co spowoduje utworzenie kopii hello toobe źródeł danych chronionych na woluminie repliki programu DPM.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-273">When backing up a datasource for hello first time, DPM needs toocreate an initial replica which will create a copy of hello datasource toobe protected on DPM replica volume.</span></span> <span data-ttu-id="3c6cc-274">To działanie albo mogą być planowane na określoną godzinę lub mogą być wyzwalane ręcznie, używając hello [DPMReplicaCreationMethod zestaw](https://technet.microsoft.com/library/hh881715) polecenia cmdlet z parametrem hello ```-NOW```.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-274">This activity can either be scheduled for a specific time, or can be triggered manually, using hello [Set-DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet with hello parameter ```-NOW```.</span></span>

```
PS C:\> Set-DPMReplicaCreationMethod -ProtectionGroup $MPG -NOW
```
### <a name="changing-hello-size-of-dpm-replica--recovery-point-volume"></a><span data-ttu-id="3c6cc-275">Zmiana rozmiaru hello repliki programu DPM i wolumin punktu odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="3c6cc-275">Changing hello size of DPM Replica & recovery point volume</span></span>
<span data-ttu-id="3c6cc-276">Możesz również zmienić rozmiar woluminu repliki programu DPM, a także kopii w tle woluminu przy użyciu hello [DPMDatasourceDiskAllocation zestaw](https://technet.microsoft.com/library/hh881618.aspx) jak hello w poniższym przykładzie polecenie cmdlet: Get-DatasourceDiskAllocation - Datasource $DS Set-DatasourceDiskAllocation - Datasource $DS - ProtectionGroup $MPG-ręczne - ReplicaArea (2 gb) — ShadowCopyArea (2 gb)</span><span class="sxs-lookup"><span data-stu-id="3c6cc-276">You can also change hello size of DPM Replica volume as well as Shadow Copy volume using [Set-DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) cmdlet as in hello below example: Get-DatasourceDiskAllocation -Datasource $DS Set-DatasourceDiskAllocation -Datasource $DS -ProtectionGroup $MPG -manual -ReplicaArea (2gb) -ShadowCopyArea (2gb)</span></span>

### <a name="committing-hello-changes-toohello-protection-group"></a><span data-ttu-id="3c6cc-277">Przekazywanie hello toohello zmiany grupy ochrony</span><span class="sxs-lookup"><span data-stu-id="3c6cc-277">Committing hello changes toohello Protection Group</span></span>
<span data-ttu-id="3c6cc-278">Na koniec hello zmiany muszą toobe zatwierdzona przed programu DPM można wykonać kopię zapasową hello na powitania nowej konfiguracji grupy ochrony.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-278">Finally, hello changes need toobe committed before DPM can take hello backup per hello new Protection Group configuration.</span></span> <span data-ttu-id="3c6cc-279">Jest to realizowane przy użyciu hello [DPMProtectionGroup zestaw](https://technet.microsoft.com/library/hh881758) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-279">This is done using hello [Set-DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet.</span></span>

```
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```
## <a name="view-hello-backup-points"></a><span data-ttu-id="3c6cc-280">Wyświetlanie hello punktów kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="3c6cc-280">View hello backup points</span></span>
<span data-ttu-id="3c6cc-281">Można użyć hello [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) tooget polecenia cmdlet listę wszystkich punktów odzyskiwania dla źródła danych.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-281">You can use hello [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) cmdlet tooget a list of all recovery points for a datasource.</span></span> <span data-ttu-id="3c6cc-282">W tym przykładzie zostaną wykonane następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="3c6cc-282">In this example, we will:</span></span>

* <span data-ttu-id="3c6cc-283">Pobierz wszystkie PGA hello na powitania serwera DPM, które będą przechowywane w tablicy```$PG```</span><span class="sxs-lookup"><span data-stu-id="3c6cc-283">fetch all hello PGs on hello DPM server which will be stored in an array ```$PG```</span></span>
* <span data-ttu-id="3c6cc-284">Pobierz toohello odpowiedniego hello źródeł danych```$PG[0]```</span><span class="sxs-lookup"><span data-stu-id="3c6cc-284">get hello datasources corresponding toohello ```$PG[0]```</span></span>
* <span data-ttu-id="3c6cc-285">Pobierz wszystkie hello punkty odzyskiwania dla źródła danych.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-285">get all hello recovery points for a datasource.</span></span>

```
PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online
```

## <a name="restore-data-protected-on-azure"></a><span data-ttu-id="3c6cc-286">Przywracanie danych chronionych na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="3c6cc-286">Restore data protected on Azure</span></span>
<span data-ttu-id="3c6cc-287">Przywracanie danych jest kombinacją ```RecoverableItem``` obiektu i ```RecoveryOption``` obiektu.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-287">Restoring data is a combination of a ```RecoverableItem``` object and a ```RecoveryOption``` object.</span></span> <span data-ttu-id="3c6cc-288">W poprzedniej sekcji hello dotarliśmy listę hello punktów kopii zapasowej dla źródła danych.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-288">In hello previous section, we got a list of hello backup points for a datasource.</span></span>

<span data-ttu-id="3c6cc-289">W poniższym przykładzie hello przedstawiony sposób toorestore funkcji Hyper-V maszyny wirtualnej z kopii zapasowej Azure za pomocą punktów kopii zapasowej łączenie z hello docelowe dla odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-289">In hello example below, we demonstrate how toorestore a Hyper-V virtual machine from Azure Backup by combining backup points with hello target for recovery.</span></span> <span data-ttu-id="3c6cc-290">Obejmuje to:</span><span class="sxs-lookup"><span data-stu-id="3c6cc-290">This includes:</span></span>

* <span data-ttu-id="3c6cc-291">Tworzenie opcję odzyskiwania przy użyciu hello [DPMRecoveryOption nowy](https://technet.microsoft.com/library/hh881592) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-291">Creating a recovery option using hello  [New-DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) cmdlet.</span></span>
* <span data-ttu-id="3c6cc-292">Pobrano tablicy hello punktów kopii zapasowej za pomocą hello ```Get-DPMRecoveryPoint``` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-292">Fetching hello array of backup points using hello ```Get-DPMRecoveryPoint``` cmdlet.</span></span>
* <span data-ttu-id="3c6cc-293">Po wybraniu opcji tworzenia kopii zapasowej toorestore punktu z.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-293">Choosing a backup point toorestore from.</span></span>

```
PS C:\> $RecoveryOption = New-DPMRecoveryOption -HyperVDatasource -TargetServer "HVDCenter02" -RecoveryLocation AlternateHyperVServer -RecoveryType Recover -TargetLocation “C:\VMRecovery”

PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online

PS C:\> Restore-DPMRecoverableItem -RecoverableItem $RecoveryPoints[0] -RecoveryOption $RecoveryOption
```

<span data-ttu-id="3c6cc-294">polecenia Hello można z łatwością rozszerzyć dla dowolnego typu źródła danych.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-294">hello commands can easily be extended for any datasource type.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3c6cc-295">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3c6cc-295">Next steps</span></span>
* <span data-ttu-id="3c6cc-296">Aby uzyskać więcej informacji na temat tworzenia kopii zapasowej Azure dla programu DPM zobacz [tooDPM wprowadzenie kopii zapasowej](backup-azure-dpm-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="3c6cc-296">For more information about Azure Backup for DPM see [Introduction tooDPM Backup](backup-azure-dpm-introduction.md)</span></span>
