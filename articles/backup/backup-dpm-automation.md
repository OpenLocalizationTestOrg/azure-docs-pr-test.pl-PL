---
title: "Kopia zapasowa Azure — tworzenie kopii zapasowej obciążeń programu DPM w programie PowerShell | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie wdrażania i zarządzania nimi kopia zapasowa Azure dla Data Protection Manager (DPM) przy użyciu programu PowerShell"
services: backup
documentationcenter: 
author: NKolli1
manager: shreeshd
editor: 
ms.assetid: e9bd223c-2398-4eb1-9bf3-50e08970fea7
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 1/23/2017
ms.author: adigan;anuragm;trinadhk;markgal
ms.openlocfilehash: 2e3b4a094511a59cfa02917efc2e3e053840af0c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-and-manage-backup-to-azure-for-data-protection-manager-dpm-servers-using-powershell"></a><span data-ttu-id="3d583-103">Wdrażanie kopii zapasowych serwerów Data Protection Manager (DPM) na platformie Azure i zarządzanie nimi przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="3d583-103">Deploy and manage backup to Azure for Data Protection Manager (DPM) servers using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3d583-104">ARM</span><span class="sxs-lookup"><span data-stu-id="3d583-104">ARM</span></span>](backup-dpm-automation.md)
> * [<span data-ttu-id="3d583-105">Wdrożenie klasyczne</span><span class="sxs-lookup"><span data-stu-id="3d583-105">Classic</span></span>](backup-dpm-automation-classic.md)
>
>

<span data-ttu-id="3d583-106">W tym artykule przedstawiono sposób instalacji usługi Kopia zapasowa Azure na serwerze DPM przy użyciu programu PowerShell, a zarządzanie kopii zapasowych i odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="3d583-106">This article shows you how to use PowerShell to setup Azure Backup on a DPM server, and to manage backup and recovery.</span></span>

## <a name="setting-up-the-powershell-environment"></a><span data-ttu-id="3d583-107">Konfigurowanie środowiska PowerShell</span><span class="sxs-lookup"><span data-stu-id="3d583-107">Setting up the PowerShell environment</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="3d583-108">Przed użyciem programu PowerShell do zarządzania kopiami zapasowymi z programu Data Protection Manager na platformie Azure, musisz mieć prawo środowiska w programie PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3d583-108">Before you can use PowerShell to manage backups from Data Protection Manager to Azure, you need to have the right environment in PowerShell.</span></span> <span data-ttu-id="3d583-109">Na początku sesji programu PowerShell upewnij się, że uruchom następujące polecenie, aby zaimportować moduły, prawym i pozwalają na poprawnie odwołują się następujące polecenia cmdlet programu DPM:</span><span class="sxs-lookup"><span data-stu-id="3d583-109">At the start of the PowerShell session, ensure that you run the following command to import the right modules and allow you to correctly reference the DPM cmdlets:</span></span>

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

## <a name="setup-and-registration"></a><span data-ttu-id="3d583-110">Instalację i rejestrację</span><span class="sxs-lookup"><span data-stu-id="3d583-110">Setup and Registration</span></span>
<span data-ttu-id="3d583-111">Aby rozpocząć:</span><span class="sxs-lookup"><span data-stu-id="3d583-111">To begin:</span></span>

1. <span data-ttu-id="3d583-112">[Pobierz najnowsze PowerShell](https://github.com/Azure/azure-powershell/releases) (minimalna wersja wymagana jest: 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="3d583-112">[Download latest PowerShell](https://github.com/Azure/azure-powershell/releases) (minimum version required is: 1.0.0)</span></span>
2. <span data-ttu-id="3d583-113">Włącz przez przełączenie do polecenia cmdlet usługi Kopia zapasowa Azure *AzureResourceManager* trybie przy użyciu **Switch-AzureMode** apletu polecenia:</span><span class="sxs-lookup"><span data-stu-id="3d583-113">Enable the Azure Backup commandlets by switching to *AzureResourceManager* mode by using the **Switch-AzureMode** commandlet:</span></span>

```
PS C:\> Switch-AzureMode AzureResourceManager
```

<span data-ttu-id="3d583-114">Następujące zadania instalację i rejestrację można zautomatyzować przy użyciu programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="3d583-114">The following setup and registration tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="3d583-115">Tworzenie magazynu Usług odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="3d583-115">Create a Recovery Services vault</span></span>
* <span data-ttu-id="3d583-116">Instalowanie agenta usługi Kopia zapasowa Azure</span><span class="sxs-lookup"><span data-stu-id="3d583-116">Installing the Azure Backup agent</span></span>
* <span data-ttu-id="3d583-117">Rejestrowanie w usłudze Kopia zapasowa Azure</span><span class="sxs-lookup"><span data-stu-id="3d583-117">Registering with the Azure Backup service</span></span>
* <span data-ttu-id="3d583-118">Ustawienia sieciowe</span><span class="sxs-lookup"><span data-stu-id="3d583-118">Networking settings</span></span>
* <span data-ttu-id="3d583-119">Ustawienia szyfrowania</span><span class="sxs-lookup"><span data-stu-id="3d583-119">Encryption settings</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="3d583-120">Tworzenie magazynu usługi Recovery Services</span><span class="sxs-lookup"><span data-stu-id="3d583-120">Create a recovery services vault</span></span>
<span data-ttu-id="3d583-121">Poniższe kroki prowadzi przez proces tworzenia magazynu usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="3d583-121">The following steps lead you through creating a Recovery Services vault.</span></span> <span data-ttu-id="3d583-122">Magazyn usług odzyskiwania są inne niż magazynu kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="3d583-122">A Recovery Services vault is different than a Backup vault.</span></span>

1. <span data-ttu-id="3d583-123">Jeśli korzystasz z usługi Kopia zapasowa Azure po raz pierwszy, należy użyć **AzureRMResourceProvider rejestru** polecenia cmdlet, aby zarejestrować dostawcę usług odzyskiwania Azure w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="3d583-123">If you are using Azure Backup for the first time, you must use the **Register-AzureRMResourceProvider** cmdlet to register the Azure Recovery Service provider with your subscription.</span></span>

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. <span data-ttu-id="3d583-124">Magazyn usług odzyskiwania jest zasobem ARM, więc należy umieścić w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="3d583-124">The Recovery Services vault is an ARM resource, so you need to place it within a Resource Group.</span></span> <span data-ttu-id="3d583-125">Użyj istniejącej grupy zasobów lub Utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="3d583-125">You can use an existing resource group, or create a new one.</span></span> <span data-ttu-id="3d583-126">Podczas tworzenia nowej grupy zasobów, określ nazwę i lokalizację dla grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="3d583-126">When creating a new resource group, specify the name and location for the resource group.</span></span>  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "West US"
    ```
3. <span data-ttu-id="3d583-127">Użyj **AzureRmRecoveryServicesVault nowy** , aby utworzyć nowy magazyn.</span><span class="sxs-lookup"><span data-stu-id="3d583-127">Use the **New-AzureRmRecoveryServicesVault** cmdlet to create a new vault.</span></span> <span data-ttu-id="3d583-128">Należy określić tę samą lokalizację dla magazynu, które było używane dla grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="3d583-128">Be sure to specify the same location for the vault as was used for the resource group.</span></span>

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "West US"
    ```
4. <span data-ttu-id="3d583-129">Określ typ nadmiarowość magazynu mają być używane; można użyć [lokalnie nadmiarowego magazynu (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) lub [z magazynu geograficznie nadmiarowego magazynu (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span><span class="sxs-lookup"><span data-stu-id="3d583-129">Specify the type of storage redundancy to use; you can use [Locally Redundant Storage (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) or [Geo Redundant Storage (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span></span> <span data-ttu-id="3d583-130">W poniższym przykładzie przedstawiono, że opcja - BackupStorageRedundancy testVault jest ustawiona na GeoRedundant.</span><span class="sxs-lookup"><span data-stu-id="3d583-130">The following example shows the -BackupStorageRedundancy option for testVault is set to GeoRedundant.</span></span>

   > [!TIP]
   > <span data-ttu-id="3d583-131">Wiele poleceń cmdlet narzędzia Kopia zapasowa Azure wymaga obiektu magazynu usług odzyskiwania jako danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="3d583-131">Many Azure Backup cmdlets require the Recovery Services vault object as an input.</span></span> <span data-ttu-id="3d583-132">Z tego powodu jest wygodne do przechowywania obiektów magazynu usług odzyskiwania kopii zapasowej w zmiennej.</span><span class="sxs-lookup"><span data-stu-id="3d583-132">For this reason, it is convenient to store the Backup Recovery Services vault object in a variable.</span></span>
   >
   >

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testVault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

## <a name="view-the-vaults-in-a-subscription"></a><span data-ttu-id="3d583-133">Wyświetlanie magazynów w ramach subskrypcji</span><span class="sxs-lookup"><span data-stu-id="3d583-133">View the vaults in a subscription</span></span>
<span data-ttu-id="3d583-134">Użyj **Get AzureRmRecoveryServicesVault** Aby wyświetlić listę wszystkich magazynów w bieżącej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="3d583-134">Use **Get-AzureRmRecoveryServicesVault** to view the list of all vaults in the current subscription.</span></span> <span data-ttu-id="3d583-135">Można użyć tego polecenia, aby sprawdzić, czy został utworzony nowy magazyn lub aby zobaczyć, jakie magazyny są dostępne w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="3d583-135">You can use this command to check that a new  vault was created, or to see what vaults are available in the subscription.</span></span>

<span data-ttu-id="3d583-136">Uruchom polecenie Get-AzureRmRecoveryServicesVault i są wyświetlane wszystkie magazyny do subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="3d583-136">Run the command, Get-AzureRmRecoveryServicesVault, and all vaults in the subscription are listed.</span></span>

```
PS C:\> Get-AzureRmRecoveryServicesVault
Name              : Contoso-vault
ID                : /subscriptions/1234
Type              : Microsoft.RecoveryServices/vaults
Location          : WestUS
ResourceGroupName : Contoso-docs-rg
SubscriptionId    : 1234-567f-8910-abc
Properties        : Microsoft.Azure.Commands.RecoveryServices.ARSVaultProperties
```


## <a name="installing-the-azure-backup-agent-on-a-dpm-server"></a><span data-ttu-id="3d583-137">Instalowanie agenta usługi Kopia zapasowa Azure na serwerze programu DPM</span><span class="sxs-lookup"><span data-stu-id="3d583-137">Installing the Azure Backup agent on a DPM Server</span></span>
<span data-ttu-id="3d583-138">Przed zainstalowaniem agenta usługi Kopia zapasowa Azure, musisz mieć Instalator pobrane i są obecne w systemie Windows Server.</span><span class="sxs-lookup"><span data-stu-id="3d583-138">Before you install the Azure Backup agent, you need to have the installer downloaded and present on the Windows Server.</span></span> <span data-ttu-id="3d583-139">Możesz pobrać najnowszą wersję Instalatora z [Microsoft Download Center](http://aka.ms/azurebackup_agent) lub ze strony pulpitu nawigacyjnego magazynu usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="3d583-139">You can get the latest version of the installer from the [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from the Recovery Services vault's Dashboard page.</span></span> <span data-ttu-id="3d583-140">Zapisanie Instalatora, aby łatwo dostępnej lokalizacji, takich jak * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="3d583-140">Save the installer to an easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="3d583-141">Aby zainstalować agenta, uruchom następujące polecenie w konsoli programu PowerShell z podwyższonym poziomem uprawnień **na serwerze programu DPM**:</span><span class="sxs-lookup"><span data-stu-id="3d583-141">To install the agent, run the following command in an elevated PowerShell console **on the DPM server**:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="3d583-142">Spowoduje to zainstalowanie agenta przy użyciu opcji domyślnej.</span><span class="sxs-lookup"><span data-stu-id="3d583-142">This installs the agent with all the default options.</span></span> <span data-ttu-id="3d583-143">Instalacja trwa kilka minut w tle.</span><span class="sxs-lookup"><span data-stu-id="3d583-143">The installation takes a few minutes in the background.</span></span> <span data-ttu-id="3d583-144">Jeśli nie określisz */nu* opcji **usługi Windows Update** zostanie otwarte okno po zakończeniu instalacji sprawdź, czy wszystkie aktualizacje.</span><span class="sxs-lookup"><span data-stu-id="3d583-144">If you do not specify the */nu* option the **Windows Update** window opens at the end of the installation to check for any updates.</span></span>

<span data-ttu-id="3d583-145">Agent zostaną wyświetlone na liście zainstalowanych programów.</span><span class="sxs-lookup"><span data-stu-id="3d583-145">The agent shows up in the list of installed programs.</span></span> <span data-ttu-id="3d583-146">Aby wyświetlić listę zainstalowanych programów, przejdź do **Panelu sterowania** > **programy** > **programy i funkcje**.</span><span class="sxs-lookup"><span data-stu-id="3d583-146">To see the list of installed programs, go to **Control Panel** > **Programs** > **Programs and Features**.</span></span>

![Agent został zainstalowany](./media/backup-dpm-automation/installed-agent-listing.png)

### <a name="installation-options"></a><span data-ttu-id="3d583-148">Opcje instalacji</span><span class="sxs-lookup"><span data-stu-id="3d583-148">Installation options</span></span>
<span data-ttu-id="3d583-149">Aby wyświetlić wszystkie opcje dostępne za pomocą wiersza polecenia, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="3d583-149">To see all the options available via the commandline, use the following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="3d583-150">Dostępne opcje to:</span><span class="sxs-lookup"><span data-stu-id="3d583-150">The available options include:</span></span>

| <span data-ttu-id="3d583-151">Opcja</span><span class="sxs-lookup"><span data-stu-id="3d583-151">Option</span></span> | <span data-ttu-id="3d583-152">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="3d583-152">Details</span></span> | <span data-ttu-id="3d583-153">Domyślne</span><span class="sxs-lookup"><span data-stu-id="3d583-153">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3d583-154">/q</span><span class="sxs-lookup"><span data-stu-id="3d583-154">/q</span></span> |<span data-ttu-id="3d583-155">Instalację cichą</span><span class="sxs-lookup"><span data-stu-id="3d583-155">Quiet installation</span></span> |- |
| <span data-ttu-id="3d583-156">/ p: "Lokalizacja"</span><span class="sxs-lookup"><span data-stu-id="3d583-156">/p:"location"</span></span> |<span data-ttu-id="3d583-157">Ścieżka do folderu instalacji agenta usługi Kopia zapasowa Azure.</span><span class="sxs-lookup"><span data-stu-id="3d583-157">Path to the installation folder for the Azure Backup agent.</span></span> |<span data-ttu-id="3d583-158">C:\Program Files\Microsoft Azure Recovery usługi agenta</span><span class="sxs-lookup"><span data-stu-id="3d583-158">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="3d583-159">/ s: "Lokalizacja"</span><span class="sxs-lookup"><span data-stu-id="3d583-159">/s:"location"</span></span> |<span data-ttu-id="3d583-160">Ścieżka do folderu pamięci podręcznej agenta usługi Kopia zapasowa Azure.</span><span class="sxs-lookup"><span data-stu-id="3d583-160">Path to the cache folder for the Azure Backup agent.</span></span> |<span data-ttu-id="3d583-161">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="3d583-161">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="3d583-162">/m</span><span class="sxs-lookup"><span data-stu-id="3d583-162">/m</span></span> |<span data-ttu-id="3d583-163">Zezwól na usługi Microsoft Update</span><span class="sxs-lookup"><span data-stu-id="3d583-163">Opt-in to Microsoft Update</span></span> |- |
| <span data-ttu-id="3d583-164">/nu</span><span class="sxs-lookup"><span data-stu-id="3d583-164">/nu</span></span> |<span data-ttu-id="3d583-165">Nie sprawdzaj aktualizacji po ukończeniu instalacji</span><span class="sxs-lookup"><span data-stu-id="3d583-165">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="3d583-166">/d</span><span class="sxs-lookup"><span data-stu-id="3d583-166">/d</span></span> |<span data-ttu-id="3d583-167">Odinstalowuje agenta usług odzyskiwania Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="3d583-167">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="3d583-168">/pH</span><span class="sxs-lookup"><span data-stu-id="3d583-168">/ph</span></span> |<span data-ttu-id="3d583-169">Adres hosta serwera proxy</span><span class="sxs-lookup"><span data-stu-id="3d583-169">Proxy Host Address</span></span> |- |
| <span data-ttu-id="3d583-170">/Po</span><span class="sxs-lookup"><span data-stu-id="3d583-170">/po</span></span> |<span data-ttu-id="3d583-171">Numer portu hosta serwera proxy</span><span class="sxs-lookup"><span data-stu-id="3d583-171">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="3d583-172">/Pu</span><span class="sxs-lookup"><span data-stu-id="3d583-172">/pu</span></span> |<span data-ttu-id="3d583-173">Nazwa użytkownika serwera proxy hosta</span><span class="sxs-lookup"><span data-stu-id="3d583-173">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="3d583-174">/PW</span><span class="sxs-lookup"><span data-stu-id="3d583-174">/pw</span></span> |<span data-ttu-id="3d583-175">Hasło serwera proxy</span><span class="sxs-lookup"><span data-stu-id="3d583-175">Proxy Password</span></span> |- |

## <a name="registering-dpm-to-a-recovery-services-vault"></a><span data-ttu-id="3d583-176">Magazyn usługi rejestrowania programu DPM do odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="3d583-176">Registering DPM to a Recovery Services Vault</span></span>
<span data-ttu-id="3d583-177">Po utworzeniu magazynu usług odzyskiwania, Pobierz najnowszą wersję agenta i poświadczenia magazynu i zapisz go w dogodnym miejscu, podobnie jak C:\Downloads.</span><span class="sxs-lookup"><span data-stu-id="3d583-177">After you created the Recovery Services vault, download the latest agent and the vault credentials and store it in a convenient location like C:\Downloads.</span></span>

```
PS C:\> $credspath = "C:\downloads"
PS C:\> $credsfilename = Get-AzureRmRecoveryServicesVaultSettingsFile -Backup -Vault $vault1 -Path  $credspath
PS C:\> $credsfilename
C:\downloads\testvault\_Sun Apr 10 2016.VaultCredentials
```

<span data-ttu-id="3d583-178">Na serwerze programu DPM Uruchom [Start OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) polecenia cmdlet, aby zarejestrować komputer w magazynie.</span><span class="sxs-lookup"><span data-stu-id="3d583-178">On the DPM server, run the [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet to register the machine with the vault.</span></span>

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-OBRegistration-VaultCredentials $cred -Confirm:$false
CertThumbprint      :7a2ef2caa2e74b6ed1222a5e89288ddad438df2
SubscriptionID      : ef4ab577-c2c0-43e4-af80-af49f485f3d1
ServiceResourceName: testvault
Region              :West US
Machine registration succeeded.
```

### <a name="initial-configuration-settings"></a><span data-ttu-id="3d583-179">Ustawienia konfiguracji początkowej</span><span class="sxs-lookup"><span data-stu-id="3d583-179">Initial configuration settings</span></span>
<span data-ttu-id="3d583-180">Gdy serwer DPM jest zarejestrowany w magazynie usług odzyskiwania, rozpoczyna się od domyślnego ustawienia subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="3d583-180">Once the DPM Server is registered with the Recovery Services vault, it starts with default subscription settings.</span></span> <span data-ttu-id="3d583-181">Te ustawienia subskrypcji obejmują sieci, szyfrowania i obszaru przemieszczania.</span><span class="sxs-lookup"><span data-stu-id="3d583-181">These subscription settings include Networking, Encryption and the Staging area.</span></span> <span data-ttu-id="3d583-182">Aby zmienić ustawienia subskrypcji, należy najpierw uzyskać uchwytu na istniejące ustawienia (ustawienie domyślne), za pomocą [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="3d583-182">To change subscription settings you need to first get a handle on the existing (default) settings using the [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet:</span></span>

```
$setting = Get-DPMCloudSubscriptionSetting -DPMServerName "TestingServer"
```

<span data-ttu-id="3d583-183">Wszystkie modyfikacje są dokonywane na ten obiekt programu PowerShell ```$setting``` , a następnie pełne obiektu jest przekazane do programu DPM i kopia zapasowa Azure, aby zapisać je przy użyciu [DPMCloudSubscriptionSetting zestaw](https://technet.microsoft.com/library/jj612791) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3d583-183">All modifications are made to this local PowerShell object ```$setting```  and then the full object is committed to DPM and Azure Backup to save them using the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="3d583-184">Należy użyć ```–Commit``` flagę, aby upewnić się, że zmiany są zachowywane.</span><span class="sxs-lookup"><span data-stu-id="3d583-184">You need to use the ```–Commit``` flag to ensure that the changes are persisted.</span></span> <span data-ttu-id="3d583-185">Ustawienia nie będą stosowane i używane przez usługi Kopia zapasowa Azure, chyba że zostało zatwierdzone.</span><span class="sxs-lookup"><span data-stu-id="3d583-185">The settings will not be applied and used by Azure Backup unless committed.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="networking"></a><span data-ttu-id="3d583-186">Sieć</span><span class="sxs-lookup"><span data-stu-id="3d583-186">Networking</span></span>
<span data-ttu-id="3d583-187">W przypadku łączności maszyny programu DPM z usługą kopia zapasowa Azure w sieci internet za pośrednictwem serwera proxy, ustawienia serwera proxy należy podać dla pomyślnie utworzone kopie zapasowe.</span><span class="sxs-lookup"><span data-stu-id="3d583-187">If the connectivity of the DPM machine to the Azure Backup service on the internet is through a proxy server, then the proxy server settings should be provided for successful backups.</span></span> <span data-ttu-id="3d583-188">Jest to zrobić za pomocą ```-ProxyServer```i ```-ProxyPort```, ```-ProxyUsername``` i ```ProxyPassword``` parametrów z [DPMCloudSubscriptionSetting zestaw](https://technet.microsoft.com/library/jj612791) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3d583-188">This is done by using the ```-ProxyServer```and ```-ProxyPort```, ```-ProxyUsername``` and the ```ProxyPassword``` parameters with the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="3d583-189">W tym przykładzie nie żadnego serwera proxy, dlatego firma Microsoft są jawnie wyczyszczenie żadnych informacji dotyczących serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="3d583-189">In this example, there is no proxy server so we are explicitly clearing any proxy-related information.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoProxy
```

<span data-ttu-id="3d583-190">Wykorzystanie przepustowości można również sterować za pomocą opcji ```-WorkHourBandwidth``` i ```-NonWorkHourBandwidth``` dla danego zestawu dni tygodnia.</span><span class="sxs-lookup"><span data-stu-id="3d583-190">Bandwidth usage can also be controlled with options of ```-WorkHourBandwidth``` and ```-NonWorkHourBandwidth``` for a given set of days of the week.</span></span> <span data-ttu-id="3d583-191">W tym przykładzie firma Microsoft nie ustawienia dowolnej ograniczania.</span><span class="sxs-lookup"><span data-stu-id="3d583-191">In this example, we are not setting any throttling.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoThrottle
```

## <a name="configuring-the-staging-area"></a><span data-ttu-id="3d583-192">Konfigurowanie obszaru przemieszczania</span><span class="sxs-lookup"><span data-stu-id="3d583-192">Configuring the staging Area</span></span>
<span data-ttu-id="3d583-193">Agent usługi Kopia zapasowa Azure uruchomionych na serwerze programu DPM wymaga tymczasowego magazynu dla danych przywróconych z chmury (lokalny obszar przemieszczania).</span><span class="sxs-lookup"><span data-stu-id="3d583-193">The Azure Backup agent running on the DPM server needs temporary storage for data restored from the cloud (local staging area).</span></span> <span data-ttu-id="3d583-194">Konfigurowanie przy użyciu obszaru przemieszczania [DPMCloudSubscriptionSetting zestaw](https://technet.microsoft.com/library/jj612791) polecenia cmdlet i ```-StagingAreaPath``` parametru.</span><span class="sxs-lookup"><span data-stu-id="3d583-194">Configure the staging area using the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet and the ```-StagingAreaPath``` parameter.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -StagingAreaPath "C:\StagingArea"
```

<span data-ttu-id="3d583-195">W powyższym przykładzie obszar tymczasowy zostanie ustawiona do *C:\StagingArea* w obiekcie środowiska PowerShell ```$setting```.</span><span class="sxs-lookup"><span data-stu-id="3d583-195">In the example above, the staging area will be set to *C:\StagingArea* in the PowerShell object ```$setting```.</span></span> <span data-ttu-id="3d583-196">Upewnij się, że podany folder już istnieje, w przeciwnym razie końcowego zatwierdzania ustawień subskrypcji zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="3d583-196">Ensure that the specified folder already exists, or else the final commit of the subscription settings will fail.</span></span>

### <a name="encryption-settings"></a><span data-ttu-id="3d583-197">Ustawienia szyfrowania</span><span class="sxs-lookup"><span data-stu-id="3d583-197">Encryption settings</span></span>
<span data-ttu-id="3d583-198">Dane kopii zapasowej wysyłane do usługi Kopia zapasowa Azure są szyfrowane w chronieniu poufności danych.</span><span class="sxs-lookup"><span data-stu-id="3d583-198">The backup data sent to Azure Backup is encrypted to protect the confidentiality of the data.</span></span> <span data-ttu-id="3d583-199">Hasło szyfrowania jest "password" do odszyfrowania danych w czasie przywracania.</span><span class="sxs-lookup"><span data-stu-id="3d583-199">The encryption passphrase is the "password" to decrypt the data at the time of restore.</span></span> <span data-ttu-id="3d583-200">Należy zachować te informacje bezpieczne po ustawieniu.</span><span class="sxs-lookup"><span data-stu-id="3d583-200">It is important to keep this information safe and secure once it is set.</span></span>

<span data-ttu-id="3d583-201">W poniższym przykładzie pierwsze polecenie konwertuje ciąg ```passphrase123456789``` ciąg bezpieczny i przypisuje bezpieczny ciąg do zmiennej o nazwie ```$Passphrase```.</span><span class="sxs-lookup"><span data-stu-id="3d583-201">In the example below, the first command converts the string ```passphrase123456789``` to a secure string and assigns the secure string to the variable named ```$Passphrase```.</span></span> <span data-ttu-id="3d583-202">drugie polecenie ustawia bezpieczny ciąg w ```$Passphrase``` jako hasło do szyfrowania kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="3d583-202">the second command sets the secure string in ```$Passphrase``` as the password for encrypting backups.</span></span>

```
PS C:\> $Passphrase = ConvertTo-SecureString -string "passphrase123456789" -AsPlainText -Force

PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -EncryptionPassphrase $Passphrase
```

> [!IMPORTANT]
> <span data-ttu-id="3d583-203">Zachowaj informacje hasło bezpieczne po ustawieniu.</span><span class="sxs-lookup"><span data-stu-id="3d583-203">Keep the passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="3d583-204">Nie można przywrócić dane z platformy Azure bez tego hasła.</span><span class="sxs-lookup"><span data-stu-id="3d583-204">You will not be able to restore data from Azure without this passphrase.</span></span>
>
>

<span data-ttu-id="3d583-205">W tym momencie powinien wprowadzone wszystkie zmiany wymagane w celu ```$setting``` obiektu.</span><span class="sxs-lookup"><span data-stu-id="3d583-205">At this point, you should have made all the required changes to the ```$setting``` object.</span></span> <span data-ttu-id="3d583-206">Pamiętaj, aby zatwierdzić zmiany.</span><span class="sxs-lookup"><span data-stu-id="3d583-206">Remember to commit the changes.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="protect-data-to-azure-backup"></a><span data-ttu-id="3d583-207">Ochrona danych do usługi Kopia zapasowa Azure</span><span class="sxs-lookup"><span data-stu-id="3d583-207">Protect data to Azure Backup</span></span>
<span data-ttu-id="3d583-208">W tej sekcji zostanie Dodawanie serwera produkcyjnego do programu DPM, a następnie włącz ochronę danych do lokalnego magazynu programu DPM, a następnie kopia zapasowa Azure.</span><span class="sxs-lookup"><span data-stu-id="3d583-208">In this section, you will add a production server to DPM and then protect the data to local DPM storage and then to Azure Backup.</span></span> <span data-ttu-id="3d583-209">W przykładach przedstawiony zostanie sposób wykonywania kopii zapasowej plików i folderów.</span><span class="sxs-lookup"><span data-stu-id="3d583-209">In the examples, we will demonstrate how to back up files and folders.</span></span> <span data-ttu-id="3d583-210">Logika można z łatwością rozszerzyć kopii zapasowej dowolnych źródeł danych obsługiwane przez program DPM.</span><span class="sxs-lookup"><span data-stu-id="3d583-210">The logic can easily be extended to backup any DPM-supported data source.</span></span> <span data-ttu-id="3d583-211">Kopii zapasowych programu DPM są regulowane przez ochronę grupy (PG) z czterech części:</span><span class="sxs-lookup"><span data-stu-id="3d583-211">All your DPM backups are governed by a Protection Group (PG) with four parts:</span></span>

1. <span data-ttu-id="3d583-212">**Członków grupy** znajduje się lista wszystkich obiekty chronione (nazywane również *źródeł danych* w programie DPM), które mają być chronione w tej samej grupy ochrony.</span><span class="sxs-lookup"><span data-stu-id="3d583-212">**Group members** is a list of all the protectable objects (also known as *Datasources* in DPM) that you want to protect in the same protection group.</span></span> <span data-ttu-id="3d583-213">Na przykład można chronić produkcji maszyny wirtualne w jednej grupy ochrony i baz danych programu SQL Server w innej grupy ochrony, ponieważ mogą mieć różne wymagania kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="3d583-213">For example, you may want to protect production VMs in one protection group and SQL Server databases in another protection group as they may have different backup requirements.</span></span> <span data-ttu-id="3d583-214">Przed utworzeniem kopii zapasowej żadnego źródła danych na serwerze produkcyjnym, które należy się upewnić, Agent programu DPM jest zainstalowany na serwerze i jest zarządzany przez program DPM.</span><span class="sxs-lookup"><span data-stu-id="3d583-214">Before you can back up any datasource on a production server you need to make sure the DPM Agent is installed on the server and is managed by DPM.</span></span> <span data-ttu-id="3d583-215">Wykonaj kroki [zainstalowanie agenta DPM](https://technet.microsoft.com/library/bb870935.aspx) i połączenie go do odpowiedniego serwera programu DPM.</span><span class="sxs-lookup"><span data-stu-id="3d583-215">Follow the steps for [installing the DPM Agent](https://technet.microsoft.com/library/bb870935.aspx) and linking it to the appropriate DPM Server.</span></span>
2. <span data-ttu-id="3d583-216">**Metoda ochrony danych** Określa docelowy kopii zapasowej lokalizacje - taśmy, dysku i chmury.</span><span class="sxs-lookup"><span data-stu-id="3d583-216">**Data protection method** specifies the target backup locations - tape, disk, and cloud.</span></span> <span data-ttu-id="3d583-217">W naszym przykładzie będzie chronić dane na dysku lokalnym i w chmurze.</span><span class="sxs-lookup"><span data-stu-id="3d583-217">In our example we will protect data to the local disk and to the cloud.</span></span>
3. <span data-ttu-id="3d583-218">A **harmonogram tworzenia kopii zapasowych** Określa, kiedy należy podjąć kopii zapasowych i jak często dane powinny być synchronizowane między serwerem DPM i serwerze produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="3d583-218">A **backup schedule** that specifies when backups need to be taken and how often the data should be synchronized between the DPM Server and the production server.</span></span>
4. <span data-ttu-id="3d583-219">A **harmonogramu przechowywania** określająca czas przechowywania punktów odzyskiwania na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="3d583-219">A **retention schedule** that specifies how long to retain the recovery points in Azure.</span></span>

### <a name="creating-a-protection-group"></a><span data-ttu-id="3d583-220">Utworzenie grupy ochrony</span><span class="sxs-lookup"><span data-stu-id="3d583-220">Creating a protection group</span></span>
<span data-ttu-id="3d583-221">Rozpocznij od utworzenia nowej grupy ochrony za pomocą [DPMProtectionGroup nowy](https://technet.microsoft.com/library/hh881722) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3d583-221">Start by creating a new Protection Group using the [New-DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) cmdlet.</span></span>

```
PS C:\> $PG = New-DPMProtectionGroup -DPMServerName " TestingServer " -Name "ProtectGroup01"
```

<span data-ttu-id="3d583-222">Powyższe polecenia cmdlet spowoduje utworzenie grupy ochrony o nazwie *ProtectGroup01*.</span><span class="sxs-lookup"><span data-stu-id="3d583-222">The above cmdlet will create a Protection Group named *ProtectGroup01*.</span></span> <span data-ttu-id="3d583-223">Aby dodać kopii zapasowej w chmurze platformy Azure istniejącej grupy ochrony może być modyfikowany również później.</span><span class="sxs-lookup"><span data-stu-id="3d583-223">An existing protection group can also be modified later to add backup to the Azure cloud.</span></span> <span data-ttu-id="3d583-224">Jednak wprowadzać żadnych zmian do grupy ochrony — nowy lub istniejący - musimy pobrać dojścia *modyfikowalnymi* przy użyciu [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3d583-224">However, to make any changes to the Protection Group - new or existing - we need to get a handle on a *modifiable* object using the [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) cmdlet.</span></span>

```
PS C:\> $MPG = Get-ModifiableProtectionGroup $PG
```

### <a name="adding-group-members-to-the-protection-group"></a><span data-ttu-id="3d583-225">Dodawanie członków grupy do grupy ochrony</span><span class="sxs-lookup"><span data-stu-id="3d583-225">Adding group members to the Protection Group</span></span>
<span data-ttu-id="3d583-226">Lista źródeł danych na serwerze, na którym jest zainstalowany na wie, każdego agenta programu DPM.</span><span class="sxs-lookup"><span data-stu-id="3d583-226">Each DPM Agent knows the list of datasources on the server that it is installed on.</span></span> <span data-ttu-id="3d583-227">Aby dodać źródła danych do grupy ochrony, agenta programu DPM musi najpierw wysłać listę źródeł danych na serwer programu DPM.</span><span class="sxs-lookup"><span data-stu-id="3d583-227">To add a datasource to the Protection Group, the DPM Agent needs to first send a list of the datasources back to the DPM server.</span></span> <span data-ttu-id="3d583-228">Jeden lub więcej źródeł danych są następnie i dodane do grupy ochrony.</span><span class="sxs-lookup"><span data-stu-id="3d583-228">One or more datasources are then selected and added to the Protection Group.</span></span> <span data-ttu-id="3d583-229">Potrzebne w tym kroki programu PowerShell są:</span><span class="sxs-lookup"><span data-stu-id="3d583-229">The PowerShell steps needed to achieve this are:</span></span>

1. <span data-ttu-id="3d583-230">Pobierz listę wszystkich serwerów zarządzanych przez program DPM za pomocą agenta programu DPM.</span><span class="sxs-lookup"><span data-stu-id="3d583-230">Fetch a list of all servers managed by DPM through the DPM Agent.</span></span>
2. <span data-ttu-id="3d583-231">Wybierz określonego serwera.</span><span class="sxs-lookup"><span data-stu-id="3d583-231">Choose a specific server.</span></span>
3. <span data-ttu-id="3d583-232">Pobranie listy wszystkich źródeł danych na serwerze.</span><span class="sxs-lookup"><span data-stu-id="3d583-232">Fetch a list of all datasources on the server.</span></span>
4. <span data-ttu-id="3d583-233">Wybierz co najmniej jednego źródła danych i dodaj je do grupy ochrony</span><span class="sxs-lookup"><span data-stu-id="3d583-233">Choose one or more datasources and add them to the Protection Group</span></span>

<span data-ttu-id="3d583-234">Lista serwerów, na których Agent programu DPM jest zainstalowany i jest zarządzany przez serwer programu DPM są uzyskiwane z [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3d583-234">The list of servers on which the DPM Agent is installed and is being managed by the DPM Server is acquired with the [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet.</span></span> <span data-ttu-id="3d583-235">W tym przykładzie firma Microsoft będzie filtrowania i skonfigurować tylko PS o nazwie *productionserver01* do utworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="3d583-235">In this example we will filter and only configure PS with name *productionserver01* for backup.</span></span>

```
PS C:\> $server = Get-ProductionServer -DPMServerName "TestingServer" | where {($_.servername) –contains “productionserver01”
```

<span data-ttu-id="3d583-236">Teraz pobrać listy źródeł danych na ```$server``` przy użyciu [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3d583-236">Now fetch the list of datasources on ```$server``` using the [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet.</span></span> <span data-ttu-id="3d583-237">W tym przykładzie mamy filtrowania dla woluminu * D:\* interesujące można skonfigurować dla kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="3d583-237">In this example we are filtering for the volume *D:\* that we want to configure for backup.</span></span> <span data-ttu-id="3d583-238">To źródło danych jest dodawane do grupy ochrony za pomocą [DPMChildDatasource Dodaj](https://technet.microsoft.com/library/hh881732) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3d583-238">This datasource is then added to the Protection Group using the [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet.</span></span> <span data-ttu-id="3d583-239">Pamiętaj, aby użyć *modyfikowalnymi* obiektu grupy ochrony ```$MPG``` uzupełnianie.</span><span class="sxs-lookup"><span data-stu-id="3d583-239">Remember to use the *modifiable* protection group object ```$MPG``` to make the additions.</span></span>

```
PS C:\> $DS = Get-Datasource -ProductionServer $server -Inquire | where { $_.Name -contains “D:\” }

PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS
```

<span data-ttu-id="3d583-240">Powtórz ten krok liczbę razy, aż zostaną dodane wszystkie wybrane źródła danych do grupy ochrony.</span><span class="sxs-lookup"><span data-stu-id="3d583-240">Repeat this step as many times as required, until you have added all the chosen datasources to the protection group.</span></span> <span data-ttu-id="3d583-241">Można również uruchomić z tylko jednego źródła danych i ukończenia przepływu pracy tworzenia grupy ochrony i w późniejszym czasie dodać więcej źródeł danych do grupy ochrony.</span><span class="sxs-lookup"><span data-stu-id="3d583-241">You can also start with just one datasource, and complete the workflow for creating the Protection Group, and at a later point add more datasources to the Protection Group.</span></span>

### <a name="selecting-the-data-protection-method"></a><span data-ttu-id="3d583-242">Wybieranie metody ochrony danych</span><span class="sxs-lookup"><span data-stu-id="3d583-242">Selecting the data protection method</span></span>
<span data-ttu-id="3d583-243">Po źródła danych zostały dodane do grupy ochrony, następnym krokiem jest określenie, przy użyciu metody ochrony [DPMProtectionType zestaw](https://technet.microsoft.com/library/hh881725) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3d583-243">Once the datasources have been added to the Protection Group, the next step is to specify the protection method using the [Set-DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet.</span></span> <span data-ttu-id="3d583-244">W tym przykładzie grupy ochrony jest ustawiony na potrzeby dysku lokalnego, a kopia zapasowa w chmurze.</span><span class="sxs-lookup"><span data-stu-id="3d583-244">In this example, the Protection Group is setup for local disk and cloud backup.</span></span> <span data-ttu-id="3d583-245">Należy również określić źródło danych, które chcesz chronić do chmury przy użyciu [DPMChildDatasource Dodaj](https://technet.microsoft.com/library/hh881732.aspx) polecenia cmdlet flagą - Online.</span><span class="sxs-lookup"><span data-stu-id="3d583-245">You also need to specify the datasource that you want to protect to cloud using the [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet with -Online flag.</span></span>

```
PS C:\> Set-DPMProtectionType -ProtectionGroup $MPG -ShortTerm Disk –LongTerm Online
PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS –Online
```

### <a name="setting-the-retention-range"></a><span data-ttu-id="3d583-246">Ustawianie zakresu przechowywania</span><span class="sxs-lookup"><span data-stu-id="3d583-246">Setting the retention range</span></span>
<span data-ttu-id="3d583-247">Ustawienia przechowywania dla punktów kopii zapasowej za pomocą [DPMPolicyObjective zestaw](https://technet.microsoft.com/library/hh881762) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3d583-247">Set the retention for the backup points using the [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span> <span data-ttu-id="3d583-248">Gdy może wydawać się nieparzysta ustawień przechowywania, przed rozpoczęciem zdefiniowano harmonogram tworzenia kopii zapasowych, przy użyciu ```Set-DPMPolicyObjective``` polecenie cmdlet automatycznie ustawia domyślny harmonogram tworzenia kopii zapasowej, który może być modyfikowany.</span><span class="sxs-lookup"><span data-stu-id="3d583-248">While it might seem odd to set the retention before the backup schedule has been defined, using the ```Set-DPMPolicyObjective``` cmdlet automatically sets a default backup schedule that can then be modified.</span></span> <span data-ttu-id="3d583-249">Zawsze jest możliwe zestawu kopii zapasowej najpierw zaplanować, jak i zasady przechowywania po.</span><span class="sxs-lookup"><span data-stu-id="3d583-249">It is always possible to set the backup schedule first and the retention policy after.</span></span>

<span data-ttu-id="3d583-250">W poniższym przykładzie polecenia cmdlet do ustawiania parametrów przechowywania kopii zapasowych na dyskach.</span><span class="sxs-lookup"><span data-stu-id="3d583-250">In the example below, the cmdlet sets the retention parameters for disk backups.</span></span> <span data-ttu-id="3d583-251">To zachowują kopie zapasowe 10 dni i synchronizowanie danych co 6 godzin między serwerem produkcyjnym i serwerze programu DPM.</span><span class="sxs-lookup"><span data-stu-id="3d583-251">This will retain backups for 10 days, and sync data every 6 hours between the production server and the DPM server.</span></span> <span data-ttu-id="3d583-252">```SynchronizationFrequencyMinutes``` Nie definiuje, jak często punktu kopii zapasowej jest tworzony, ale jak często dane są kopiowane do serwera DPM.</span><span class="sxs-lookup"><span data-stu-id="3d583-252">The ```SynchronizationFrequencyMinutes``` doesn't define how often a backup point is created, but how often data is copied to the DPM server.</span></span>  <span data-ttu-id="3d583-253">To ustawienie uniemożliwia tworzenie kopii zapasowych za duży.</span><span class="sxs-lookup"><span data-stu-id="3d583-253">This setting prevents backups from becoming too large.</span></span>

```
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -RetentionRangeInDays 10 -SynchronizationFrequencyMinutes 360
```

<span data-ttu-id="3d583-254">Kopii zapasowych, przechodząc do platformy Azure (Program DPM odwołuje się do nich jako kopii zapasowych Online) zakresów przechowywania można skonfigurować dla [długoterminowych przechowywania użyciu schematu dziadek-ojciec-syn. (GFS)](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="3d583-254">For backups going to Azure (DPM refers to them as Online backups) the retention ranges can be configured for [long term retention using a Grandfather-Father-Son scheme (GFS)](backup-azure-backup-cloud-as-tape.md).</span></span> <span data-ttu-id="3d583-255">Oznacza to można zdefiniować zasady przechowywania Scalonej obejmujące codziennie, co tydzień, miesięcznych i rocznych zasady przechowywania.</span><span class="sxs-lookup"><span data-stu-id="3d583-255">That is, you can define a combined retention policy involving daily, weekly, monthly and yearly retention policies.</span></span> <span data-ttu-id="3d583-256">W tym przykładzie, możemy utworzyć tablicy reprezentujący schemat przechowywania złożonych, która ma, a następnie skonfiguruj, przy użyciu zakresu przechowywania [DPMPolicyObjective zestaw](https://technet.microsoft.com/library/hh881762) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3d583-256">In this example, we create an array representing the complex retention scheme that we want, and then configure the retention range using the [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span>

```
PS C:\> $RRlist = @()
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 180, Days)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 104, Weeks)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 60, Month)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 10, Years)
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -OnlineRetentionRangeList $RRlist
```

### <a name="set-the-backup-schedule"></a><span data-ttu-id="3d583-257">Ustaw harmonogram tworzenia kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="3d583-257">Set the backup schedule</span></span>
<span data-ttu-id="3d583-258">Program DPM ustawia automatycznie domyślny harmonogram tworzenia kopii zapasowej, jeśli określisz ochronę celu za pomocą ```Set-DPMPolicyObjective``` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3d583-258">DPM sets a default backup schedule automatically if you specify the protection objective using the ```Set-DPMPolicyObjective``` cmdlet.</span></span> <span data-ttu-id="3d583-259">Aby zmienić domyślne harmonogramy, użyj [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) polecenia cmdlet następuje [DPMPolicySchedule zestaw](https://technet.microsoft.com/library/hh881723) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3d583-259">To change the default schedules, use the [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet followed by the [Set-DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) cmdlet.</span></span>

```
PS C:\> $onlineSch = Get-DPMPolicySchedule -ProtectionGroup $mpg -LongTerm Online
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[0] -TimesOfDay 02:00
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[1] -TimesOfDay 02:00 -DaysOfWeek Sa,Su –Interval 1
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[2] -TimesOfDay 02:00 -RelativeIntervals First,Third –DaysOfWeek Sa
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[3] -TimesOfDay 02:00 -DaysOfMonth 2,5,8,9 -Months Jan,Jul
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```

<span data-ttu-id="3d583-260">W powyższym przykładzie ```$onlineSch``` jest tablicą o czterech elementów zawierający istniejący harmonogram ochrony w trybie online dla grupy ochrony w schemacie GFS:</span><span class="sxs-lookup"><span data-stu-id="3d583-260">In the above example, ```$onlineSch``` is an array with four elements that contains the existing online protection schedule for the Protection Group in the GFS scheme:</span></span>

1. <span data-ttu-id="3d583-261">```$onlineSch[0]```zawiera harmonogramu dziennego</span><span class="sxs-lookup"><span data-stu-id="3d583-261">```$onlineSch[0]``` contains the daily schedule</span></span>
2. <span data-ttu-id="3d583-262">```$onlineSch[1]```zawiera harmonogramu tygodniowego</span><span class="sxs-lookup"><span data-stu-id="3d583-262">```$onlineSch[1]``` contains the weekly schedule</span></span>
3. <span data-ttu-id="3d583-263">```$onlineSch[2]```zawiera harmonogramu miesięcznego</span><span class="sxs-lookup"><span data-stu-id="3d583-263">```$onlineSch[2]``` contains the monthly schedule</span></span>
4. <span data-ttu-id="3d583-264">```$onlineSch[3]```zawiera corocznych harmonogramu</span><span class="sxs-lookup"><span data-stu-id="3d583-264">```$onlineSch[3]``` contains the yearly schedule</span></span>

<span data-ttu-id="3d583-265">Dlatego jeśli trzeba zmodyfikować harmonogram tygodniowy, trzeba odwoływać się do ```$onlineSch[1]```.</span><span class="sxs-lookup"><span data-stu-id="3d583-265">So if you need to modify the weekly schedule, you need to refer to the ```$onlineSch[1]```.</span></span>

### <a name="initial-backup"></a><span data-ttu-id="3d583-266">Początkowa kopia zapasowa</span><span class="sxs-lookup"><span data-stu-id="3d583-266">Initial backup</span></span>
<span data-ttu-id="3d583-267">Podczas wykonywania kopii zapasowej źródła danych po raz pierwszy, program DPM musi tworzy repliki początkowej który tworzy pełną kopię źródła danych mają być chronione na woluminie repliki programu DPM.</span><span class="sxs-lookup"><span data-stu-id="3d583-267">When backing up a datasource for the first time, DPM needs creates initial replica that creates a full copy of the datasource to be protected on DPM replica volume.</span></span> <span data-ttu-id="3d583-268">To działanie albo mogą być planowane na określoną godzinę lub mogą być wyzwalane ręcznie, używając [DPMReplicaCreationMethod zestaw](https://technet.microsoft.com/library/hh881715) polecenia cmdlet z parametrem ```-NOW```.</span><span class="sxs-lookup"><span data-stu-id="3d583-268">This activity can either be scheduled for a specific time, or can be triggered manually, using the [Set-DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet with the parameter ```-NOW```.</span></span>

```
PS C:\> Set-DPMReplicaCreationMethod -ProtectionGroup $MPG -NOW
```
### <a name="changing-the-size-of-dpm-replica--recovery-point-volume"></a><span data-ttu-id="3d583-269">Zmiana rozmiaru repliki programu DPM i wolumin punktu odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="3d583-269">Changing the size of DPM Replica & recovery point volume</span></span>
<span data-ttu-id="3d583-270">Możesz również zmienić rozmiar woluminu repliki programu DPM i kopii w tle woluminu przy użyciu [DPMDatasourceDiskAllocation zestaw](https://technet.microsoft.com/library/hh881618.aspx) jak w poniższym przykładzie polecenie cmdlet: Get-DatasourceDiskAllocation - Datasource $DS Set-DatasourceDiskAllocation - Źródło danych $DS - ProtectionGroup $MPG-ręczne - ReplicaArea (2 gb) — ShadowCopyArea (2 gb)</span><span class="sxs-lookup"><span data-stu-id="3d583-270">You can also change the size of DPM Replica volume and Shadow Copy volume using [Set-DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) cmdlet as in the following example: Get-DatasourceDiskAllocation -Datasource $DS Set-DatasourceDiskAllocation -Datasource $DS -ProtectionGroup $MPG -manual -ReplicaArea (2gb) -ShadowCopyArea (2gb)</span></span>

### <a name="committing-the-changes-to-the-protection-group"></a><span data-ttu-id="3d583-271">Zatwierdzenie zmian do grupy ochrony</span><span class="sxs-lookup"><span data-stu-id="3d583-271">Committing the changes to the Protection Group</span></span>
<span data-ttu-id="3d583-272">Na koniec zmiany muszą być zatwierdzone przed programu DPM można wykonać kopię zapasową na nową konfigurację grupy ochrony.</span><span class="sxs-lookup"><span data-stu-id="3d583-272">Finally, the changes need to be committed before DPM can take the backup per the new Protection Group configuration.</span></span> <span data-ttu-id="3d583-273">Można to osiągnąć przy użyciu [DPMProtectionGroup zestaw](https://technet.microsoft.com/library/hh881758) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3d583-273">This can be achieved using the [Set-DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet.</span></span>

```
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```
## <a name="view-the-backup-points"></a><span data-ttu-id="3d583-274">Wyświetlanie punktów kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="3d583-274">View the backup points</span></span>
<span data-ttu-id="3d583-275">Można użyć [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) polecenia cmdlet, aby uzyskać listę wszystkich punktów odzyskiwania dla źródła danych.</span><span class="sxs-lookup"><span data-stu-id="3d583-275">You can use the [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) cmdlet to get a list of all recovery points for a datasource.</span></span> <span data-ttu-id="3d583-276">W tym przykładzie zostaną wykonane następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="3d583-276">In this example, we will:</span></span>

* <span data-ttu-id="3d583-277">Pobierz wszystkie PGA na serwerze DPM i przechowywane w tablicy```$PG```</span><span class="sxs-lookup"><span data-stu-id="3d583-277">fetch all the PGs on the DPM server and stored in an array ```$PG```</span></span>
* <span data-ttu-id="3d583-278">Pobierz odpowiadający źródeł danych```$PG[0]```</span><span class="sxs-lookup"><span data-stu-id="3d583-278">get the datasources corresponding to the ```$PG[0]```</span></span>
* <span data-ttu-id="3d583-279">Pobierz wszystkie punkty odzyskiwania dla źródła danych.</span><span class="sxs-lookup"><span data-stu-id="3d583-279">get all the recovery points for a datasource.</span></span>

```
PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online
```

## <a name="restore-data-protected-on-azure"></a><span data-ttu-id="3d583-280">Przywracanie danych chronionych na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="3d583-280">Restore data protected on Azure</span></span>
<span data-ttu-id="3d583-281">Przywracanie danych jest kombinacją ```RecoverableItem``` obiektu i ```RecoveryOption``` obiektu.</span><span class="sxs-lookup"><span data-stu-id="3d583-281">Restoring data is a combination of a ```RecoverableItem``` object and a ```RecoveryOption``` object.</span></span> <span data-ttu-id="3d583-282">W poprzedniej sekcji dotarliśmy listę punktów kopii zapasowej dla źródła danych.</span><span class="sxs-lookup"><span data-stu-id="3d583-282">In the previous section, we got a list of the backup points for a datasource.</span></span>

<span data-ttu-id="3d583-283">W poniższym przykładzie przedstawiony sposób przywracania maszyny wirtualnej funkcji Hyper-V z kopii zapasowej Azure dzięki połączeniu z elementem docelowym odzyskiwania punktów kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="3d583-283">In the example below, we demonstrate how to restore a Hyper-V virtual machine from Azure Backup by combining backup points with the target for recovery.</span></span> <span data-ttu-id="3d583-284">Ten przykład obejmuje:</span><span class="sxs-lookup"><span data-stu-id="3d583-284">This example includes:</span></span>

* <span data-ttu-id="3d583-285">Utworzenie przy użyciu opcji odzyskiwania [DPMRecoveryOption nowy](https://technet.microsoft.com/library/hh881592) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3d583-285">Creating a recovery option using the  [New-DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) cmdlet.</span></span>
* <span data-ttu-id="3d583-286">Tablica punktów kopii zapasowej przy użyciu pobierania ```Get-DPMRecoveryPoint``` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3d583-286">Fetching the array of backup points using the ```Get-DPMRecoveryPoint``` cmdlet.</span></span>
* <span data-ttu-id="3d583-287">Wybieranie punktu kopii zapasowej do przywrócenia z.</span><span class="sxs-lookup"><span data-stu-id="3d583-287">Choosing a backup point to restore from.</span></span>

```
PS C:\> $RecoveryOption = New-DPMRecoveryOption -HyperVDatasource -TargetServer "HVDCenter02" -RecoveryLocation AlternateHyperVServer -RecoveryType Recover -TargetLocation “C:\VMRecovery”

PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online

PS C:\> Restore-DPMRecoverableItem -RecoverableItem $RecoveryPoints[0] -RecoveryOption $RecoveryOption
```

<span data-ttu-id="3d583-288">Polecenia można z łatwością rozszerzyć dla dowolnego typu źródła danych.</span><span class="sxs-lookup"><span data-stu-id="3d583-288">The commands can easily be extended for any datasource type.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d583-289">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3d583-289">Next steps</span></span>
* <span data-ttu-id="3d583-290">Aby uzyskać więcej informacji na temat programu DPM w usłudze Kopia zapasowa Azure zobacz [wprowadzenie do kopii zapasowej programu DPM](backup-azure-dpm-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="3d583-290">For more information about DPM to Azure Backup see [Introduction to DPM Backup](backup-azure-dpm-introduction.md)</span></span>
