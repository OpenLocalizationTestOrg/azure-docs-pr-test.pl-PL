---
title: "Utwórz kopię zapasową serwera systemu Windows Azure przy użyciu programu PowerShell | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie wdrażania i zarządzania nimi przy użyciu programu PowerShell usługi Kopia zapasowa Azure"
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 65218095-2996-44d9-917b-8c84fc9ac415
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: saurse;markgal;jimpark;nkolli;trinadhk
ms.openlocfilehash: d3f165c749af0553c4918b33b0d24cc1e21af2a9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-and-manage-backup-to-azure-for-windows-serverwindows-client-using-powershell"></a><span data-ttu-id="e3600-103">Wdrażanie kopii zapasowych systemu Windows Server/Windows Client na platformie Azure i zarządzanie nimi przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="e3600-103">Deploy and manage backup to Azure for Windows Server/Windows Client using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e3600-104">ARM</span><span class="sxs-lookup"><span data-stu-id="e3600-104">ARM</span></span>](backup-client-automation.md)
> * [<span data-ttu-id="e3600-105">Wdrożenie klasyczne</span><span class="sxs-lookup"><span data-stu-id="e3600-105">Classic</span></span>](backup-client-automation-classic.md)
>
>

<span data-ttu-id="e3600-106">W tym artykule przedstawiono sposób konfigurowania usługi Kopia zapasowa Azure w systemie Windows Server lub klienta systemu Windows oraz zarządzania nimi kopii zapasowych i odzyskiwania przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e3600-106">This article shows you how to use PowerShell for setting up Azure Backup on Windows Server or a Windows client, and managing backup and recovery.</span></span>

## <a name="install-azure-powershell"></a><span data-ttu-id="e3600-107">Instalowanie programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e3600-107">Install Azure PowerShell</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="e3600-108">Ten artykuł dotyczy usługi Azure Resource Manager (ARM) i poleceń cmdlet programu środowiska PowerShell kopii zapasowej Online MS umożliwiają korzystanie z magazynu usług odzyskiwania w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="e3600-108">This article focuses on the Azure Resource Manager (ARM) and the MS Online Backup PowerShell cmdlets that enable you to use a Recovery Services vault in a resource group.</span></span>

<span data-ttu-id="e3600-109">Października 2015 Azure PowerShell 1.0 został wydany.</span><span class="sxs-lookup"><span data-stu-id="e3600-109">In October 2015, Azure PowerShell 1.0 was released.</span></span> <span data-ttu-id="e3600-110">Tej wersji 0.9.8 powiodło się. Zwolnij i temat istotne zmiany, szczególnie w wzorzec nazewnictwa poleceń cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e3600-110">This release succeeded the 0.9.8 release and brought about some significant changes, especially in the naming pattern of the cmdlets.</span></span> <span data-ttu-id="e3600-111">Polecenia cmdlet 1.0 mają wzorzec nazewnictwa {czasownik}-AzureRm{rzeczownik}; natomiast nazwy 0.9.8 nie zawierają elementu **Rm** (np. New-AzureRmResourceGroup zamiast New-AzureResourceGroup).</span><span class="sxs-lookup"><span data-stu-id="e3600-111">1.0 cmdlets follow the naming pattern {verb}-AzureRm{noun}; whereas, the 0.9.8 names do not include **Rm** (for example, New-AzureRmResourceGroup instead of New-AzureResourceGroup).</span></span> <span data-ttu-id="e3600-112">W przypadku korzystania z programu Azure PowerShell 0.9.8 trzeba najpierw włączyć tryb usługi Resource Manager przez uruchomienie polecenia **Switch-AzureMode AzureResourceManager**.</span><span class="sxs-lookup"><span data-stu-id="e3600-112">When using Azure PowerShell 0.9.8, you must first enable the Resource Manager mode by running the **Switch-AzureMode AzureResourceManager** command.</span></span> <span data-ttu-id="e3600-113">To polecenie nie jest konieczne w wersji 1.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="e3600-113">This command is not necessary in 1.0 or later.</span></span>

<span data-ttu-id="e3600-114">Jeśli chcesz używać skryptów przeznaczony dla 0.9.8 środowisko, w środowisku w wersji 1.0 lub nowszej, należy ostrożnie aktualizacji i przetestować skrypty w środowisku przedprodukcyjnym przed ich użyciem w środowisku produkcyjnym, aby uniknąć nieoczekiwanego wpływu.</span><span class="sxs-lookup"><span data-stu-id="e3600-114">If you want to use your scripts written for the 0.9.8 environment, in the 1.0 or later environment, you should carefully update and test the scripts in a pre-production environment before using them in production to avoid unexpected impact.</span></span>

<span data-ttu-id="e3600-115">[Pobierz najnowszą wersję programu PowerShell](https://github.com/Azure/azure-powershell/releases) (minimalna wersja wymagana jest: 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="e3600-115">[Download the latest PowerShell release](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>

[!INCLUDE [arm-getting-setup-powershell](../../includes/arm-getting-setup-powershell.md)]

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="e3600-116">Tworzenie magazynu usługi Recovery Services</span><span class="sxs-lookup"><span data-stu-id="e3600-116">Create a recovery services vault</span></span>
<span data-ttu-id="e3600-117">Poniższe kroki prowadzi przez proces tworzenia magazynu usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="e3600-117">The following steps lead you through creating a Recovery Services vault.</span></span> <span data-ttu-id="e3600-118">Magazyn usług odzyskiwania są inne niż magazynu kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="e3600-118">A Recovery Services vault is different than a Backup vault.</span></span>

1. <span data-ttu-id="e3600-119">Jeśli korzystasz z usługi Kopia zapasowa Azure po raz pierwszy, należy użyć **AzureRMResourceProvider rejestru** polecenia cmdlet, aby zarejestrować dostawcę usług odzyskiwania Azure w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="e3600-119">If you are using Azure Backup for the first time, you must use the **Register-AzureRMResourceProvider** cmdlet to register the Azure Recovery Service provider with your subscription.</span></span>

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. <span data-ttu-id="e3600-120">Magazyn usług odzyskiwania jest zasobem ARM, więc należy umieścić w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="e3600-120">The Recovery Services vault is an ARM resource, so you need to place it within a Resource Group.</span></span> <span data-ttu-id="e3600-121">Użyj istniejącej grupy zasobów lub Utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="e3600-121">You can use an existing resource group, or create a new one.</span></span> <span data-ttu-id="e3600-122">Podczas tworzenia nowej grupy zasobów, określ nazwę i lokalizację dla grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="e3600-122">When creating a new resource group, specify the name and location for the resource group.</span></span>  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "WestUS"
    ```
3. <span data-ttu-id="e3600-123">Użyj **AzureRmRecoveryServicesVault nowy** , aby utworzyć nowy magazyn.</span><span class="sxs-lookup"><span data-stu-id="e3600-123">Use the **New-AzureRmRecoveryServicesVault** cmdlet to create the new vault.</span></span> <span data-ttu-id="e3600-124">Należy określić tę samą lokalizację dla magazynu, które było używane dla grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="e3600-124">Be sure to specify the same location for the vault as was used for the resource group.</span></span>

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "WestUS"
    ```
4. <span data-ttu-id="e3600-125">Określ typ nadmiarowość magazynu mają być używane; można użyć [lokalnie nadmiarowego magazynu (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) lub [z magazynu geograficznie nadmiarowego magazynu (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span><span class="sxs-lookup"><span data-stu-id="e3600-125">Specify the type of storage redundancy to use; you can use [Locally Redundant Storage (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) or [Geo Redundant Storage (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span></span> <span data-ttu-id="e3600-126">W poniższym przykładzie przedstawiono, że opcja - BackupStorageRedundancy testVault jest ustawiona na GeoRedundant.</span><span class="sxs-lookup"><span data-stu-id="e3600-126">The following example shows the -BackupStorageRedundancy option for testVault is set to GeoRedundant.</span></span>

   > [!TIP]
   > <span data-ttu-id="e3600-127">Wiele poleceń cmdlet narzędzia Kopia zapasowa Azure wymaga obiektu magazynu usług odzyskiwania jako danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="e3600-127">Many Azure Backup cmdlets require the Recovery Services vault object as an input.</span></span> <span data-ttu-id="e3600-128">Z tego powodu jest wygodne do przechowywania obiektów magazynu usług odzyskiwania kopii zapasowej w zmiennej.</span><span class="sxs-lookup"><span data-stu-id="e3600-128">For this reason, it is convenient to store the Backup Recovery Services vault object in a variable.</span></span>
   >
   >

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testVault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

## <a name="view-the-vaults-in-a-subscription"></a><span data-ttu-id="e3600-129">Wyświetlanie magazynów w ramach subskrypcji</span><span class="sxs-lookup"><span data-stu-id="e3600-129">View the vaults in a subscription</span></span>
<span data-ttu-id="e3600-130">Użyj **Get AzureRmRecoveryServicesVault** Aby wyświetlić listę wszystkich magazynów w bieżącej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="e3600-130">Use **Get-AzureRmRecoveryServicesVault** to view the list of all vaults in the current subscription.</span></span> <span data-ttu-id="e3600-131">Można użyć tego polecenia, aby sprawdzić, czy został utworzony nowy magazyn lub aby zobaczyć, jakie magazyny są dostępne w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="e3600-131">You can use this command to check that a new  vault was created, or to see what vaults are available in the subscription.</span></span>

<span data-ttu-id="e3600-132">Uruchom polecenie **Get-AzureRmRecoveryServicesVault**, i są wyświetlane wszystkie magazyny do subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="e3600-132">Run the command, **Get-AzureRmRecoveryServicesVault**, and all vaults in the subscription are listed.</span></span>

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


## <a name="installing-the-azure-backup-agent"></a><span data-ttu-id="e3600-133">Instalowanie agenta usługi Kopia zapasowa Azure</span><span class="sxs-lookup"><span data-stu-id="e3600-133">Installing the Azure Backup agent</span></span>
<span data-ttu-id="e3600-134">Przed zainstalowaniem agenta usługi Kopia zapasowa Azure, musisz mieć Instalator pobrane i są obecne w systemie Windows Server.</span><span class="sxs-lookup"><span data-stu-id="e3600-134">Before you install the Azure Backup agent, you need to have the installer downloaded and present on the Windows Server.</span></span> <span data-ttu-id="e3600-135">Możesz pobrać najnowszą wersję Instalatora z [Microsoft Download Center](http://aka.ms/azurebackup_agent) lub ze strony pulpitu nawigacyjnego magazynu usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="e3600-135">You can get the latest version of the installer from the [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from the Recovery Services vault's Dashboard page.</span></span> <span data-ttu-id="e3600-136">Zapisanie Instalatora, aby łatwo dostępnej lokalizacji, takich jak * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="e3600-136">Save the installer to an easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="e3600-137">Można również użyć programu PowerShell, aby uzyskać narzędzia do pobierania:</span><span class="sxs-lookup"><span data-stu-id="e3600-137">Alternatively, use PowerShell to get the downloader:</span></span>
 
 ```
 $MarsAURL = 'Http://Aka.Ms/Azurebackup_Agent'
 $WC = New-Object System.Net.WebClient
 $WC.DownloadFile($MarsAURL,'C:\downloads\MARSAgentInstaller.EXE')
 C:\Downloads\MARSAgentInstaller.EXE /q
 ```

<span data-ttu-id="e3600-138">Aby zainstalować agenta, uruchom następujące polecenie w konsoli programu PowerShell z podwyższonym poziomem uprawnień:</span><span class="sxs-lookup"><span data-stu-id="e3600-138">To install the agent, run the following command in an elevated PowerShell console:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="e3600-139">Spowoduje to zainstalowanie agenta przy użyciu opcji domyślnej.</span><span class="sxs-lookup"><span data-stu-id="e3600-139">This installs the agent with all the default options.</span></span> <span data-ttu-id="e3600-140">Instalacja trwa kilka minut w tle.</span><span class="sxs-lookup"><span data-stu-id="e3600-140">The installation takes a few minutes in the background.</span></span> <span data-ttu-id="e3600-141">Jeśli nie określisz */nu* opcji, a następnie **usługi Windows Update** zostanie otwarte okno po zakończeniu instalacji sprawdź, czy wszystkie aktualizacje.</span><span class="sxs-lookup"><span data-stu-id="e3600-141">If you do not specify the */nu* option then the **Windows Update** window will open at the end of the installation to check for any updates.</span></span> <span data-ttu-id="e3600-142">Po zainstalowaniu agenta zostaną wyświetlone na liście zainstalowanych programów.</span><span class="sxs-lookup"><span data-stu-id="e3600-142">Once installed, the agent will show in the list of installed programs.</span></span>

<span data-ttu-id="e3600-143">Aby wyświetlić listę zainstalowanych programów, przejdź do **Panelu sterowania** > **programy** > **programy i funkcje**.</span><span class="sxs-lookup"><span data-stu-id="e3600-143">To see the list of installed programs, go to **Control Panel** > **Programs** > **Programs and Features**.</span></span>

![Agent został zainstalowany](./media/backup-client-automation/installed-agent-listing.png)

### <a name="installation-options"></a><span data-ttu-id="e3600-145">Opcje instalacji</span><span class="sxs-lookup"><span data-stu-id="e3600-145">Installation options</span></span>
<span data-ttu-id="e3600-146">Aby wyświetlić wszystkie opcje dostępne za pomocą wiersza polecenia, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="e3600-146">To see all the options available via the command-line, use the following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="e3600-147">Dostępne opcje to:</span><span class="sxs-lookup"><span data-stu-id="e3600-147">The available options include:</span></span>

| <span data-ttu-id="e3600-148">Opcja</span><span class="sxs-lookup"><span data-stu-id="e3600-148">Option</span></span> | <span data-ttu-id="e3600-149">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="e3600-149">Details</span></span> | <span data-ttu-id="e3600-150">Domyślne</span><span class="sxs-lookup"><span data-stu-id="e3600-150">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e3600-151">/q</span><span class="sxs-lookup"><span data-stu-id="e3600-151">/q</span></span> |<span data-ttu-id="e3600-152">Instalację cichą</span><span class="sxs-lookup"><span data-stu-id="e3600-152">Quiet installation</span></span> |- |
| <span data-ttu-id="e3600-153">/ p: "Lokalizacja"</span><span class="sxs-lookup"><span data-stu-id="e3600-153">/p:"location"</span></span> |<span data-ttu-id="e3600-154">Ścieżka do folderu instalacji agenta usługi Kopia zapasowa Azure.</span><span class="sxs-lookup"><span data-stu-id="e3600-154">Path to the installation folder for the Azure Backup agent.</span></span> |<span data-ttu-id="e3600-155">C:\Program Files\Microsoft Azure Recovery usługi agenta</span><span class="sxs-lookup"><span data-stu-id="e3600-155">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="e3600-156">/ s: "Lokalizacja"</span><span class="sxs-lookup"><span data-stu-id="e3600-156">/s:"location"</span></span> |<span data-ttu-id="e3600-157">Ścieżka do folderu pamięci podręcznej agenta usługi Kopia zapasowa Azure.</span><span class="sxs-lookup"><span data-stu-id="e3600-157">Path to the cache folder for the Azure Backup agent.</span></span> |<span data-ttu-id="e3600-158">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="e3600-158">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="e3600-159">/m</span><span class="sxs-lookup"><span data-stu-id="e3600-159">/m</span></span> |<span data-ttu-id="e3600-160">Zezwól na usługi Microsoft Update</span><span class="sxs-lookup"><span data-stu-id="e3600-160">Opt-in to Microsoft Update</span></span> |- |
| <span data-ttu-id="e3600-161">/nu</span><span class="sxs-lookup"><span data-stu-id="e3600-161">/nu</span></span> |<span data-ttu-id="e3600-162">Nie sprawdzaj aktualizacji po ukończeniu instalacji</span><span class="sxs-lookup"><span data-stu-id="e3600-162">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="e3600-163">/d</span><span class="sxs-lookup"><span data-stu-id="e3600-163">/d</span></span> |<span data-ttu-id="e3600-164">Odinstalowuje agenta usług odzyskiwania Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="e3600-164">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="e3600-165">/pH</span><span class="sxs-lookup"><span data-stu-id="e3600-165">/ph</span></span> |<span data-ttu-id="e3600-166">Adres hosta serwera proxy</span><span class="sxs-lookup"><span data-stu-id="e3600-166">Proxy Host Address</span></span> |- |
| <span data-ttu-id="e3600-167">/Po</span><span class="sxs-lookup"><span data-stu-id="e3600-167">/po</span></span> |<span data-ttu-id="e3600-168">Numer portu hosta serwera proxy</span><span class="sxs-lookup"><span data-stu-id="e3600-168">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="e3600-169">/Pu</span><span class="sxs-lookup"><span data-stu-id="e3600-169">/pu</span></span> |<span data-ttu-id="e3600-170">Nazwa użytkownika serwera proxy hosta</span><span class="sxs-lookup"><span data-stu-id="e3600-170">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="e3600-171">/PW</span><span class="sxs-lookup"><span data-stu-id="e3600-171">/pw</span></span> |<span data-ttu-id="e3600-172">Hasło serwera proxy</span><span class="sxs-lookup"><span data-stu-id="e3600-172">Proxy Password</span></span> |- |

## <a name="registering-windows-server-or-windows-client-machine-to-a-recovery-services-vault"></a><span data-ttu-id="e3600-173">Rejestracja systemu Windows Server lub komputer kliencki z systemem Windows w magazynie usług odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="e3600-173">Registering Windows Server or Windows client machine to a Recovery Services Vault</span></span>
<span data-ttu-id="e3600-174">Po utworzeniu magazynu usług odzyskiwania, Pobierz najnowszą wersję agenta i poświadczenia magazynu i zapisz go w dogodnym miejscu, podobnie jak C:\Downloads.</span><span class="sxs-lookup"><span data-stu-id="e3600-174">After you created the Recovery Services vault, download the latest agent and the vault credentials and store it in a convenient location like C:\Downloads.</span></span>

```
PS C:\> $credspath = "C:\downloads"
PS C:\> $credsfilename = Get-AzureRmRecoveryServicesVaultSettingsFile -Backup -Vault $vault1 -Path  $credspath
```

<span data-ttu-id="e3600-175">Na serwerze systemu Windows lub komputera klienckiego z systemem Windows, uruchom [Start OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) polecenia cmdlet, aby zarejestrować komputer w magazynie.</span><span class="sxs-lookup"><span data-stu-id="e3600-175">On the Windows Server or Windows client machine, run the [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet to register the machine with the vault.</span></span>
<span data-ttu-id="e3600-176">To i inne polecenia cmdlet używane do tworzenia kopii zapasowych, są w module MSONLINE, który Mars AgentInstaller dodany jako część procesu instalacji.</span><span class="sxs-lookup"><span data-stu-id="e3600-176">This, and other cmdlets used for backup, are from the MSONLINE module which the Mars AgentInstaller added as part of the installation process.</span></span> 

<span data-ttu-id="e3600-177">Instalator agenta nie aktualizuje $Env: PSModulePath zmiennej.</span><span class="sxs-lookup"><span data-stu-id="e3600-177">The Agent installer does not update the $Env:PSModulePath variable.</span></span> <span data-ttu-id="e3600-178">Oznacza to, że automatyczne ładowanie modułu nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="e3600-178">This means module auto-load fails.</span></span> <span data-ttu-id="e3600-179">Aby rozwiązać ten problem można wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="e3600-179">To resolve this you can do the following:</span></span>

```
PS C:\>  $Env:psmodulepath += ';C:\Program Files\Microsoft Azure Recovery Services Agent\bin\Modules
```

<span data-ttu-id="e3600-180">Alternatywnie można ręcznie załadować moduł skryptu w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="e3600-180">Alternatively, you can manually load the module in your script as follows:</span></span>

```
PS C:\>  Import-Module  'C:\Program Files\Microsoft Azure Recovery Services Agent\bin\Modules\MSOnlineBackup'

```

<span data-ttu-id="e3600-181">Po załadowaniu poleceń cmdlet programu kopii zapasowej Online, zarejestruj się poświadczenia magazynu:</span><span class="sxs-lookup"><span data-stu-id="e3600-181">Once you load the Online Backup cmdlets, you register the vault credentials:</span></span>


```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-OBRegistration-VaultCredentials $cred -Confirm:$false
CertThumbprint      :7a2ef2caa2e74b6ed1222a5e89288ddad438df2
SubscriptionID      : ef4ab577-c2c0-43e4-af80-af49f485f3d1
ServiceResourceName: testvault
Region              :WestUS
Machine registration succeeded.
```

> [!IMPORTANT]
> <span data-ttu-id="e3600-182">Aby określić plik poświadczeń magazynu nie należy używać ścieżek względnych.</span><span class="sxs-lookup"><span data-stu-id="e3600-182">Do not use relative paths to specify the vault credentials file.</span></span> <span data-ttu-id="e3600-183">Należy podać ścieżkę bezwzględną jako dane wejściowe polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e3600-183">You must provide an absolute path as an input to the cmdlet.</span></span>
>
>

## <a name="networking-settings"></a><span data-ttu-id="e3600-184">Ustawienia sieciowe</span><span class="sxs-lookup"><span data-stu-id="e3600-184">Networking settings</span></span>
<span data-ttu-id="e3600-185">W przypadku połączenia komputera z systemem Windows do Internetu za pośrednictwem serwera proxy, ustawienia serwera proxy można również podać agenta.</span><span class="sxs-lookup"><span data-stu-id="e3600-185">When the connectivity of the Windows machine to the internet is through a proxy server, the proxy settings can also be provided to the agent.</span></span> <span data-ttu-id="e3600-186">W tym przykładzie nie żadnego serwera proxy, dlatego firma Microsoft są jawnie wyczyszczenie żadnych informacji dotyczących serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="e3600-186">In this example, there is no proxy server, so we are explicitly clearing any proxy-related information.</span></span>

<span data-ttu-id="e3600-187">Przepustowości można również sterować za pomocą opcji ```work hour bandwidth``` i ```non-work hour bandwidth``` dla danego zestawu dni tygodnia.</span><span class="sxs-lookup"><span data-stu-id="e3600-187">Bandwidth usage can also be controlled with the options of ```work hour bandwidth``` and ```non-work hour bandwidth``` for a given set of days of the week.</span></span>

<span data-ttu-id="e3600-188">Ustawienie szczegóły serwera proxy i przepustowości jest wykonywane przy użyciu [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="e3600-188">Setting the proxy and bandwidth details is done using the [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) cmdlet:</span></span>

```
PS C:\> Set-OBMachineSetting -NoProxy
Server properties updated successfully.

PS C:\> Set-OBMachineSetting -NoThrottle
Server properties updated successfully.
```

## <a name="encryption-settings"></a><span data-ttu-id="e3600-189">Ustawienia szyfrowania</span><span class="sxs-lookup"><span data-stu-id="e3600-189">Encryption settings</span></span>
<span data-ttu-id="e3600-190">Dane kopii zapasowej wysyłane do usługi Kopia zapasowa Azure są szyfrowane w chronieniu poufności danych.</span><span class="sxs-lookup"><span data-stu-id="e3600-190">The backup data sent to Azure Backup is encrypted to protect the confidentiality of the data.</span></span> <span data-ttu-id="e3600-191">Hasło szyfrowania jest "password" do odszyfrowania danych w czasie przywracania.</span><span class="sxs-lookup"><span data-stu-id="e3600-191">The encryption passphrase is the "password" to decrypt the data at the time of restore.</span></span>

```
PS C:\> ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force | Set-OBMachineSetting
PS C:\> $PassPhrase = ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force 
PS C:\> $PassCode   = 'AzureR0ckx'
PS C:\> Set-OBMachineSetting -EncryptionPassPhrase $PassPhrase
Server properties updated successfully
```

> [!IMPORTANT]
> <span data-ttu-id="e3600-192">Zachowaj informacje hasło bezpieczne po ustawieniu.</span><span class="sxs-lookup"><span data-stu-id="e3600-192">Keep the passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="e3600-193">Nie są można przywrócić dane z usługi Azure bez tego hasła.</span><span class="sxs-lookup"><span data-stu-id="e3600-193">You are not be able to restore data from Azure without this passphrase.</span></span>
>
>

## <a name="back-up-files-and-folders"></a><span data-ttu-id="e3600-194">Tworzenie kopii zapasowych plików i folderów</span><span class="sxs-lookup"><span data-stu-id="e3600-194">Back up files and folders</span></span>
<span data-ttu-id="e3600-195">Wszystkie kopie zapasowe i serwery z systemem Windows Azure Backup zarządzane przez zasady.</span><span class="sxs-lookup"><span data-stu-id="e3600-195">All backups from Windows Servers and clients to Azure Backup are governed by a policy.</span></span> <span data-ttu-id="e3600-196">Zasady składa się z trzech części:</span><span class="sxs-lookup"><span data-stu-id="e3600-196">The policy comprises three parts:</span></span>

1. <span data-ttu-id="e3600-197">A **harmonogram tworzenia kopii zapasowych** określający, gdy kopie zapasowe muszą być podjęte i zsynchronizowane z usługą.</span><span class="sxs-lookup"><span data-stu-id="e3600-197">A **backup schedule** that specifies when backups need to be taken and synchronized with the service.</span></span>
2. <span data-ttu-id="e3600-198">A **harmonogramu przechowywania** określająca czas przechowywania punktów odzyskiwania na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="e3600-198">A **retention schedule** that specifies how long to retain the recovery points in Azure.</span></span>
3. <span data-ttu-id="e3600-199">A **określania włączenia/wyłączenia pliku** które nakazują, co należy utworzyć kopię.</span><span class="sxs-lookup"><span data-stu-id="e3600-199">A **file inclusion/exclusion specification** that dictates what should be backed up.</span></span>

<span data-ttu-id="e3600-200">W tym dokumencie ponieważ będziemy w przypadku automatyzacji kopii zapasowej, przyjęto będzie założenie, że nic nie skonfigurowano.</span><span class="sxs-lookup"><span data-stu-id="e3600-200">In this document, since we're automating backup, we'll assume nothing has been configured.</span></span> <span data-ttu-id="e3600-201">Zaczniemy poprzez tworzenie na podstawie nowych zasad tworzenia kopii zapasowej [OBPolicy nowy](https://technet.microsoft.com/library/hh770416.aspx) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e3600-201">We begin by creating a new backup policy using the [New-OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) cmdlet.</span></span>

```
PS C:\> $newpolicy = New-OBPolicy
```

<span data-ttu-id="e3600-202">W tym momencie zasady jest pusta i innych poleceń cmdlet są wymagane do zdefiniowania, jakie elementy będą dołączone lub wykluczone, kiedy kopii zapasowych zostanie wykonane, a w przypadku, gdy kopie zapasowe będą przechowywane.</span><span class="sxs-lookup"><span data-stu-id="e3600-202">At this time the policy is empty and other cmdlets are needed to define what items will be included or excluded, when backups will run, and where the backups will be stored.</span></span>

### <a name="configuring-the-backup-schedule"></a><span data-ttu-id="e3600-203">Konfigurowanie harmonogramu tworzenia kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="e3600-203">Configuring the backup schedule</span></span>
<span data-ttu-id="e3600-204">Pierwsza z 3 części zasad jest harmonogram tworzenia kopii zapasowych, który jest tworzony przy użyciu [OBSchedule nowy](https://technet.microsoft.com/library/hh770401) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e3600-204">The first of the 3 parts of a policy is the backup schedule, which is created using the [New-OBSchedule](https://technet.microsoft.com/library/hh770401) cmdlet.</span></span> <span data-ttu-id="e3600-205">Harmonogram tworzenia kopii zapasowych definiuje, gdy kopie zapasowe należy podjąć.</span><span class="sxs-lookup"><span data-stu-id="e3600-205">The backup schedule defines when backups need to be taken.</span></span> <span data-ttu-id="e3600-206">Podczas tworzenia harmonogramu, musisz podać parametry wejściowe 2:</span><span class="sxs-lookup"><span data-stu-id="e3600-206">When creating a schedule you need to specify 2 input parameters:</span></span>

* <span data-ttu-id="e3600-207">**Dni tygodnia** uruchomienia tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="e3600-207">**Days of the week** that the backup should run.</span></span> <span data-ttu-id="e3600-208">Można uruchomić zadanie tworzenia kopii zapasowej na tylko jeden dzień lub każdego dnia, tygodnia lub dowolnej kombinacji między.</span><span class="sxs-lookup"><span data-stu-id="e3600-208">You can run the backup job on just one day, or every day of the week, or any combination in between.</span></span>
* <span data-ttu-id="e3600-209">**Porach dnia** uruchomienia tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="e3600-209">**Times of the day** when the backup should run.</span></span> <span data-ttu-id="e3600-210">Można określić maksymalnie 3 różnych porach dnia, gdy zostanie wywołane kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="e3600-210">You can define up to 3 different times of the day when the backup will be triggered.</span></span>

<span data-ttu-id="e3600-211">Na przykład można skonfigurować zasad tworzenia kopii zapasowej, wykonywany o 16: 00 w każdą sobotę i niedziela.</span><span class="sxs-lookup"><span data-stu-id="e3600-211">For instance, you could configure a backup policy that runs at 4PM every Saturday and Sunday.</span></span>

```
PS C:\> $sched = New-OBSchedule -DaysofWeek Saturday, Sunday -TimesofDay 16:00
```

<span data-ttu-id="e3600-212">Harmonogram tworzenia kopii zapasowych musi być skojarzone z zasadami i można to osiągnąć przy użyciu [OBSchedule zestaw](https://technet.microsoft.com/library/hh770407) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e3600-212">The backup schedule needs to be associated with a policy, and this can be achieved by using the [Set-OBSchedule](https://technet.microsoft.com/library/hh770407) cmdlet.</span></span>

```
PS C:> Set-OBSchedule -Policy $newpolicy -Schedule $sched
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s) DsList : PolicyName : RetentionPolicy : State : New PolicyState : Valid
```
### <a name="configuring-a-retention-policy"></a><span data-ttu-id="e3600-213">Konfigurowania zasad przechowywania</span><span class="sxs-lookup"><span data-stu-id="e3600-213">Configuring a retention policy</span></span>
<span data-ttu-id="e3600-214">Zasady przechowywania określają, jak długo są przechowywane punkty odzyskiwania utworzone na podstawie zadania tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="e3600-214">The retention policy defines how long recovery points created from backup jobs are retained.</span></span> <span data-ttu-id="e3600-215">Podczas tworzenia nowych zasad przechowywania, przy użyciu [OBRetentionPolicy nowy](https://technet.microsoft.com/library/hh770425) polecenia cmdlet, można określić liczbę dni, które muszą być przechowywane w usłudze Kopia zapasowa Azure punktów odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="e3600-215">When creating a new retention policy using the [New-OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) cmdlet, you can specify the number of days that the backup recovery points need to be retained with Azure Backup.</span></span> <span data-ttu-id="e3600-216">W poniższym przykładzie ustawia zasady przechowywania wynosi 7 dni.</span><span class="sxs-lookup"><span data-stu-id="e3600-216">The example below sets a retention policy of 7 days.</span></span>

```
PS C:\> $retentionpolicy = New-OBRetentionPolicy -RetentionDays 7
```

<span data-ttu-id="e3600-217">Zasady przechowywania muszą być skojarzone z zasadami głównego za pomocą polecenia cmdlet [OBRetentionPolicy zestaw](https://technet.microsoft.com/library/hh770405):</span><span class="sxs-lookup"><span data-stu-id="e3600-217">The retention policy must be associated with the main policy using the cmdlet [Set-OBRetentionPolicy](https://technet.microsoft.com/library/hh770405):</span></span>

```
PS C:\> Set-OBRetentionPolicy -Policy $newpolicy -RetentionPolicy $retentionpolicy

BackupSchedule  : 4:00 PM
                  Saturday, Sunday,
                  Every 1 week(s)
DsList          :
PolicyName      :
RetentionPolicy : Retention Days : 7

                  WeeklyLTRSchedule :
                  Weekly schedule is not set

                  MonthlyLTRSchedule :
                  Monthly schedule is not set

                  YearlyLTRSchedule :
                  Yearly schedule is not set

State           : New
PolicyState     : Valid
```
### <a name="including-and-excluding-files-to-be-backed-up"></a><span data-ttu-id="e3600-218">Włączanie i wyłączanie plików do wykonania kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="e3600-218">Including and excluding files to be backed up</span></span>
<span data-ttu-id="e3600-219">```OBFileSpec``` Obiekt definiuje pliki mają być uwzględnione i wykluczone w kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="e3600-219">An ```OBFileSpec``` object defines the files to be included and excluded in a backup.</span></span> <span data-ttu-id="e3600-220">Jest to zestaw reguł, które zakres chronionych plików i folderów na komputerze.</span><span class="sxs-lookup"><span data-stu-id="e3600-220">This is a set of rules that scope out the protected files and folders on a machine.</span></span> <span data-ttu-id="e3600-221">Może mieć wiele pliku reguł dołączania lub wykluczania zgodnie z wymaganiami i skojarzyć je z zasadami.</span><span class="sxs-lookup"><span data-stu-id="e3600-221">You can have as many file inclusion or exclusion rules as required, and associate them with a policy.</span></span> <span data-ttu-id="e3600-222">Tworząc nowy obiekt OBFileSpec, można:</span><span class="sxs-lookup"><span data-stu-id="e3600-222">When creating a new OBFileSpec object, you can:</span></span>

* <span data-ttu-id="e3600-223">Określ pliki i foldery do uwzględnienia</span><span class="sxs-lookup"><span data-stu-id="e3600-223">Specify the files and folders to be included</span></span>
* <span data-ttu-id="e3600-224">Określ pliki i foldery do wykluczenia</span><span class="sxs-lookup"><span data-stu-id="e3600-224">Specify the files and folders to be excluded</span></span>
* <span data-ttu-id="e3600-225">Określ rekursywne tworzenie kopii zapasowych danych w folderze (lub) czy tylko pliki najwyższego poziomu w określonym folderze należy utworzyć kopię zapasową.</span><span class="sxs-lookup"><span data-stu-id="e3600-225">Specify recursive backup of data in a folder (or) whether only the top-level files in the specified folder should be backed up.</span></span>

<span data-ttu-id="e3600-226">Rozwinięciu przy użyciu flagi - Nierekurencyjny polecenia New-OBFileSpec.</span><span class="sxs-lookup"><span data-stu-id="e3600-226">The latter is achieved by using the -NonRecursive flag in the New-OBFileSpec command.</span></span>

<span data-ttu-id="e3600-227">W poniższym przykładzie możemy utworzyć kopię zapasową woluminu, C: i D: i wykluczanie plików binarnych systemu operacyjnego w folderze systemu Windows i foldery tymczasowe.</span><span class="sxs-lookup"><span data-stu-id="e3600-227">In the example below, we'll back up volume C: and D: and exclude the OS binaries in the Windows folder and any temporary folders.</span></span> <span data-ttu-id="e3600-228">Aby to zrobić, utworzymy dwóch plików przy użyciu specyfikacji [OBFileSpec nowy](https://technet.microsoft.com/library/hh770408) polecenia cmdlet — jeden dla dołączania i jeden do wykluczenia.</span><span class="sxs-lookup"><span data-stu-id="e3600-228">To do so we'll create two file specifications using the [New-OBFileSpec](https://technet.microsoft.com/library/hh770408) cmdlet - one for inclusion and one for exclusion.</span></span> <span data-ttu-id="e3600-229">Po utworzeniu specyfikacji pliku są powiązane z zasad przy użyciu opcji [OBFileSpec Dodaj](https://technet.microsoft.com/library/hh770424) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e3600-229">Once the file specifications have been created, they're associated with the policy using the [Add-OBFileSpec](https://technet.microsoft.com/library/hh770424) cmdlet.</span></span>

```
PS C:\> $inclusions = New-OBFileSpec -FileSpec @("C:\", "D:\")

PS C:\> $exclusions = New-OBFileSpec -FileSpec @("C:\windows", "C:\temp") -Exclude

PS C:\> Add-OBFileSpec -Policy $newpolicy -FileSpec $inclusions

BackupSchedule  : 4:00 PM
                  Saturday, Sunday,
                  Every 1 week(s)
DsList          : {DataSource
                  DatasourceId:0
                  Name:C:\
                  FileSpec:FileSpec
                  FileSpec:C:\
                  IsExclude:False
                  IsRecursive:True

                  , DataSource
                  DatasourceId:0
                  Name:D:\
                  FileSpec:FileSpec
                  FileSpec:D:\
                  IsExclude:False
                  IsRecursive:True

                  }
PolicyName      :
RetentionPolicy : Retention Days : 7

                  WeeklyLTRSchedule :
                  Weekly schedule is not set

                  MonthlyLTRSchedule :
                  Monthly schedule is not set

                  YearlyLTRSchedule :
                  Yearly schedule is not set

State           : New
PolicyState     : Valid


PS C:\> Add-OBFileSpec -Policy $newpolicy -FileSpec $exclusions

BackupSchedule  : 4:00 PM
                  Saturday, Sunday,
                  Every 1 week(s)
DsList          : {DataSource
                  DatasourceId:0
                  Name:C:\
                  FileSpec:FileSpec
                  FileSpec:C:\
                  IsExclude:False
                  IsRecursive:True
                  ,FileSpec
                  FileSpec:C:\windows
                  IsExclude:True
                  IsRecursive:True
                  ,FileSpec
                  FileSpec:C:\temp
                  IsExclude:True
                  IsRecursive:True

                  , DataSource
                  DatasourceId:0
                  Name:D:\
                  FileSpec:FileSpec
                  FileSpec:D:\
                  IsExclude:False
                  IsRecursive:True

                  }
PolicyName      :
RetentionPolicy : Retention Days : 7

                  WeeklyLTRSchedule :
                  Weekly schedule is not set

                  MonthlyLTRSchedule :
                  Monthly schedule is not set

                  YearlyLTRSchedule :
                  Yearly schedule is not set

State           : New
PolicyState     : Valid
```

### <a name="applying-the-policy"></a><span data-ttu-id="e3600-230">Stosowanie zasad</span><span class="sxs-lookup"><span data-stu-id="e3600-230">Applying the policy</span></span>
<span data-ttu-id="e3600-231">Teraz ten obiekt zasad została zakończona i ma skojarzone harmonogram tworzenia kopii zapasowych, zasad przechowywania i włączenia/wyłączenia lista plików.</span><span class="sxs-lookup"><span data-stu-id="e3600-231">Now the policy object is complete and has an associated backup schedule, retention policy, and an inclusion/exclusion list of files.</span></span> <span data-ttu-id="e3600-232">Te zasady można teraz zatwierdzona dla usługi Kopia zapasowa Azure do użycia.</span><span class="sxs-lookup"><span data-stu-id="e3600-232">This policy can now be committed for Azure Backup to use.</span></span> <span data-ttu-id="e3600-233">Przed zastosowaniem zasad nowo utworzony upewnij się, że nie ma żadnych istniejących zasad tworzenia kopii zapasowej skojarzone z serwerem przy użyciu [OBPolicy Usuń](https://technet.microsoft.com/library/hh770415) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e3600-233">Before you apply the newly created policy ensure that there are no existing backup policies associated with the server by using the [Remove-OBPolicy](https://technet.microsoft.com/library/hh770415) cmdlet.</span></span> <span data-ttu-id="e3600-234">Usuwanie zasad wyświetli monit o potwierdzenie.</span><span class="sxs-lookup"><span data-stu-id="e3600-234">Removing the policy will prompt for confirmation.</span></span> <span data-ttu-id="e3600-235">Aby pominąć użycie potwierdzenia ```-Confirm:$false``` flagę za pomocą polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e3600-235">To skip the confirmation use the ```-Confirm:$false``` flag with the cmdlet.</span></span>

```
PS C:> Get-OBPolicy | Remove-OBPolicy
Microsoft Azure Backup Are you sure you want to remove this backup policy? This will delete all the backed up data. [Y] Yes [A] Yes to All [N] No [L] No to All [S] Suspend [?] Help (default is "Y"):
```

<span data-ttu-id="e3600-236">Zatwierdzania obiektu zasad jest wykonywane przy użyciu [OBPolicy zestaw](https://technet.microsoft.com/library/hh770421) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e3600-236">Committing the policy object is done using the [Set-OBPolicy](https://technet.microsoft.com/library/hh770421) cmdlet.</span></span> <span data-ttu-id="e3600-237">Spowoduje to również monituje o potwierdzenie.</span><span class="sxs-lookup"><span data-stu-id="e3600-237">This will also ask for confirmation.</span></span> <span data-ttu-id="e3600-238">Aby pominąć użycie potwierdzenia ```-Confirm:$false``` flagę za pomocą polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e3600-238">To skip the confirmation use the ```-Confirm:$false``` flag with the cmdlet.</span></span>

```
PS C:> Set-OBPolicy -Policy $newpolicy
Microsoft Azure Backup Do you want to save this backup policy ? [Y] Yes [A] Yes to All [N] No [L] No to All [S] Suspend [?] Help (default is "Y"):
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s)
DsList : {DataSource
         DatasourceId:4508156004108672185
         Name:C:\
         FileSpec:FileSpec
         FileSpec:C:\
         IsExclude:False
         IsRecursive:True,

         FileSpec
         FileSpec:C:\windows
         IsExclude:True
         IsRecursive:True,

         FileSpec
         FileSpec:C:\temp
         IsExclude:True
         IsRecursive:True,

         DataSource
         DatasourceId:4508156005178868542
         Name:D:\
         FileSpec:FileSpec
         FileSpec:D:\
         IsExclude:False
         IsRecursive:True
    }
PolicyName : c2eb6568-8a06-49f4-a20e-3019ae411bac
RetentionPolicy : Retention Days : 7
              WeeklyLTRSchedule :
              Weekly schedule is not set

              MonthlyLTRSchedule :
              Monthly schedule is not set

              YearlyLTRSchedule :
              Yearly schedule is not set
State : Existing PolicyState : Valid
```

<span data-ttu-id="e3600-239">Można wyświetlić szczegółowe informacje o istniejących zasad tworzenia kopii zapasowej przy użyciu [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e3600-239">You can view the details of the existing backup policy using the [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) cmdlet.</span></span> <span data-ttu-id="e3600-240">Użytkownik może przejść za pomocą [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) polecenia cmdlet dla harmonogramu tworzenia kopii zapasowych i [Get-OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) polecenia cmdlet dla zasad przechowywania</span><span class="sxs-lookup"><span data-stu-id="e3600-240">You can drill-down further using the [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) cmdlet for the backup schedule and the [Get-OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) cmdlet for the retention policies</span></span>

```
PS C:> Get-OBPolicy | Get-OBSchedule
SchedulePolicyName : 71944081-9950-4f7e-841d-32f0a0a1359a
ScheduleRunDays : {Saturday, Sunday}
ScheduleRunTimes : {16:00:00}
State : Existing

PS C:> Get-OBPolicy | Get-OBRetentionPolicy
RetentionDays : 7
RetentionPolicyName : ca3574ec-8331-46fd-a605-c01743a5265e
State : Existing

PS C:> Get-OBPolicy | Get-OBFileSpec
FileName : *
FilePath : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\
FileSpec : D:\
IsExclude : False
IsRecursive : True

FileName : *
FilePath : \?\Volume{cdd41007-a22f-11e2-be6c-806e6f6e6963}\
FileSpec : C:\
IsExclude : False
IsRecursive : True

FileName : *
FilePath : \?\Volume{cdd41007-a22f-11e2-be6c-806e6f6e6963}\windows
FileSpec : C:\windows
IsExclude : True
IsRecursive : True

FileName : *
FilePath : \?\Volume{cdd41007-a22f-11e2-be6c-806e6f6e6963}\temp
FileSpec : C:\temp
IsExclude : True
IsRecursive : True
```

### <a name="performing-an-ad-hoc-backup"></a><span data-ttu-id="e3600-241">Wykonywanie kopii zapasowych ad hoc</span><span class="sxs-lookup"><span data-stu-id="e3600-241">Performing an ad-hoc backup</span></span>
<span data-ttu-id="e3600-242">Po ustawieniu zasad tworzenia kopii zapasowej kopie zapasowe zostanie przeprowadzona na harmonogram.</span><span class="sxs-lookup"><span data-stu-id="e3600-242">Once a backup policy has been set the backups will occur per the schedule.</span></span> <span data-ttu-id="e3600-243">Wyzwolenie kopii zapasowych ad hoc jest także możliwe przy użyciu [Start OBBackup](https://technet.microsoft.com/library/hh770426) polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="e3600-243">Triggering an ad-hoc backup is also possible using the [Start-OBBackup](https://technet.microsoft.com/library/hh770426) cmdlet:</span></span>

```
PS C:> Get-OBPolicy | Start-OBBackup
Initializing
Taking snapshot of volumes...
Preparing storage...
Generating backup metadata information and preparing the metadata VHD...
Data transfer is in progress. It might take longer since it is the first backup and all data needs to be transferred...
Data transfer completed and all backed up data is in the cloud. Verifying data integrity...
Data transfer completed
In progress...
Job completed.
The backup operation completed successfully.
```

## <a name="restore-data-from-azure-backup"></a><span data-ttu-id="e3600-244">Przywróć dane z usługi Kopia zapasowa Azure</span><span class="sxs-lookup"><span data-stu-id="e3600-244">Restore data from Azure Backup</span></span>
<span data-ttu-id="e3600-245">Ta sekcja przeprowadzi Cię przez kolejne kroki do automatyzacji odzyskiwanie danych z kopii zapasowej Azure.</span><span class="sxs-lookup"><span data-stu-id="e3600-245">This section will guide you through the steps for automating recovery of data from Azure Backup.</span></span> <span data-ttu-id="e3600-246">Dzięki temu obejmuje następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="e3600-246">Doing so involves the following steps:</span></span>

1. <span data-ttu-id="e3600-247">Wybierz wolumin źródłowy</span><span class="sxs-lookup"><span data-stu-id="e3600-247">Pick the source volume</span></span>
2. <span data-ttu-id="e3600-248">Wybierz punktu kopii zapasowej do przywrócenia</span><span class="sxs-lookup"><span data-stu-id="e3600-248">Choose a backup point to restore</span></span>
3. <span data-ttu-id="e3600-249">Wybierz element, aby przywrócić</span><span class="sxs-lookup"><span data-stu-id="e3600-249">Choose an item to restore</span></span>
4. <span data-ttu-id="e3600-250">Wyzwalacz proces przywracania</span><span class="sxs-lookup"><span data-stu-id="e3600-250">Trigger the restore process</span></span>

### <a name="picking-the-source-volume"></a><span data-ttu-id="e3600-251">Pobrania woluminu źródłowego</span><span class="sxs-lookup"><span data-stu-id="e3600-251">Picking the source volume</span></span>
<span data-ttu-id="e3600-252">Aby przywrócić element z kopii zapasowej Azure, należy najpierw określić źródło elementu.</span><span class="sxs-lookup"><span data-stu-id="e3600-252">In order to restore an item from Azure Backup, you first need to identify the source of the item.</span></span> <span data-ttu-id="e3600-253">Ponieważ firma Microsoft w przypadku wykonywania polecenia w kontekście systemu Windows Server lub klienta systemu Windows, komputer jest już zidentyfikowany.</span><span class="sxs-lookup"><span data-stu-id="e3600-253">Since we're executing the commands in the context of a Windows Server or a Windows client, the machine is already identified.</span></span> <span data-ttu-id="e3600-254">Następnym krokiem w identyfikacji źródła jest zidentyfikować woluminu zawierającego go.</span><span class="sxs-lookup"><span data-stu-id="e3600-254">The next step in identifying the source is to identify the volume containing it.</span></span> <span data-ttu-id="e3600-255">Listę woluminów lub źródła Trwa wykonywanie kopii zapasowej z tego komputera mogą być pobierane, wykonując [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e3600-255">A list of volumes or sources being backed up from this machine can be retrieved by executing the [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) cmdlet.</span></span> <span data-ttu-id="e3600-256">To polecenie zwraca tablicę wszystkich źródeł kopii zapasowej z serwera/klienta.</span><span class="sxs-lookup"><span data-stu-id="e3600-256">This command returns an array of all the sources backed up from this server/client.</span></span>

```
PS C:> $source = Get-OBRecoverableSource
PS C:> $source
FriendlyName : C:\
RecoverySourceName : C:\
ServerName : myserver.microsoft.com

FriendlyName : D:\
RecoverySourceName : D:\
ServerName : myserver.microsoft.com
```

### <a name="choosing-a-backup-point-from-which-to-restore"></a><span data-ttu-id="e3600-257">Wybieranie punktu kopii zapasowej, z której można przywrócić</span><span class="sxs-lookup"><span data-stu-id="e3600-257">Choosing a backup point from which to restore</span></span>
<span data-ttu-id="e3600-258">Pobieranie listy punktów kopii zapasowej, wykonując [Get OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) polecenie cmdlet z odpowiednimi parametrami.</span><span class="sxs-lookup"><span data-stu-id="e3600-258">You retreive a list of backup points by executing the [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet with appropriate parameters.</span></span> <span data-ttu-id="e3600-259">W naszym przykładzie wybrano najnowszego punktu kopii zapasowej woluminu źródłowego *D:* i używać go do odzyskania określonego pliku.</span><span class="sxs-lookup"><span data-stu-id="e3600-259">In our example, we’ll choose the latest backup point for the source volume *D:* and use it to recover a specific file.</span></span>

```
PS C:> $rps = Get-OBRecoverableItem -Source $source[1]
IsDir : False
ItemNameFriendly : D:\
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\
LocalMountPoint : D:\
MountPointName : D:\
Name : D:\
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize :
ItemLastModifiedTime :

IsDir : False
ItemNameFriendly : D:\
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\
LocalMountPoint : D:\
MountPointName : D:\
Name : D:\
PointInTime : 17-Jun-15 6:31:31 AM
ServerName : myserver.microsoft.com
ItemSize :
ItemLastModifiedTime :
```
<span data-ttu-id="e3600-260">Obiekt ```$rps``` jest tablicą punktów kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="e3600-260">The object ```$rps``` is an array of backup points.</span></span> <span data-ttu-id="e3600-261">Pierwszy element jest najnowszy punkt i n-tego elementu jest starsze punkty.</span><span class="sxs-lookup"><span data-stu-id="e3600-261">The first element is the latest point and the Nth element is the oldest point.</span></span> <span data-ttu-id="e3600-262">Aby wybrać najnowszy punkt, będziemy używać ```$rps[0]```.</span><span class="sxs-lookup"><span data-stu-id="e3600-262">To choose the latest point, we will use ```$rps[0]```.</span></span>

### <a name="choosing-an-item-to-restore"></a><span data-ttu-id="e3600-263">Wybranie elementu do przywrócenia</span><span class="sxs-lookup"><span data-stu-id="e3600-263">Choosing an item to restore</span></span>
<span data-ttu-id="e3600-264">Aby zidentyfikować dokładną plik lub folder do przywrócenia, użyj rekursywnie [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e3600-264">To identify the exact file or folder to restore, recursively use the [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet.</span></span> <span data-ttu-id="e3600-265">W ten sposób hierarchię folderów można przeglądać wyłącznie przy użyciu ```Get-OBRecoverableItem```.</span><span class="sxs-lookup"><span data-stu-id="e3600-265">That way the folder hierarchy can be browsed solely using the ```Get-OBRecoverableItem```.</span></span>

<span data-ttu-id="e3600-266">W tym przykładzie, jeśli chcemy przywrócić plik *finances.xls* firma Microsoft może odwoływać się który przy użyciu obiektu ```$filesFolders[1]```.</span><span class="sxs-lookup"><span data-stu-id="e3600-266">In this example, if we want to restore the file *finances.xls* we can reference that using the object ```$filesFolders[1]```.</span></span>

```
PS C:> $filesFolders = Get-OBRecoverableItem $rps[0]
PS C:> $filesFolders
IsDir : True
ItemNameFriendly : D:\MyData\
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\MyData\
LocalMountPoint : D:\
MountPointName : D:\
Name : MyData
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize :
ItemLastModifiedTime : 15-Jun-15 8:49:29 AM

PS C:> $filesFolders = Get-OBRecoverableItem $filesFolders[0]
PS C:> $filesFolders
IsDir : False
ItemNameFriendly : D:\MyData\screenshot.oxps
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\MyData\screenshot.oxps
LocalMountPoint : D:\
MountPointName : D:\
Name : screenshot.oxps
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize : 228313
ItemLastModifiedTime : 21-Jun-14 6:45:09 AM

IsDir : False
ItemNameFriendly : D:\MyData\finances.xls
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\MyData\finances.xls
LocalMountPoint : D:\
MountPointName : D:\
Name : finances.xls
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize : 96256
ItemLastModifiedTime : 21-Jun-14 6:43:02 AM
```

<span data-ttu-id="e3600-267">Możesz również wyszukać elementy do przywrócenia przy użyciu ```Get-OBRecoverableItem``` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e3600-267">You can also search for items to restore using the ```Get-OBRecoverableItem``` cmdlet.</span></span> <span data-ttu-id="e3600-268">W naszym przykładzie, aby wyszukać *finances.xls* firma Microsoft można uzyskać dojścia do pliku, uruchamiając poniższe polecenie:</span><span class="sxs-lookup"><span data-stu-id="e3600-268">In our example, to search for *finances.xls* we could get a handle on the file by running this command:</span></span>

```
PS C:\> $item = Get-OBRecoverableItem -RecoveryPoint $rps[0] -Location "D:\MyData" -SearchString "finance*"
```

### <a name="triggering-the-restore-process"></a><span data-ttu-id="e3600-269">Wyzwolenie procesu przywracania</span><span class="sxs-lookup"><span data-stu-id="e3600-269">Triggering the restore process</span></span>
<span data-ttu-id="e3600-270">Aby wyzwolić procesu przywracania, najpierw musimy Określ opcje odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="e3600-270">To trigger the restore process, we first need to specify the recovery options.</span></span> <span data-ttu-id="e3600-271">Można to zrobić za pomocą [OBRecoveryOption nowy](https://technet.microsoft.com/library/hh770417.aspx) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e3600-271">This can be done by using the [New-OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) cmdlet.</span></span> <span data-ttu-id="e3600-272">Na przykład załóżmy, że chcemy przywrócić pliki *C:\temp*. Załóżmy również, że chcemy pominąć pliki, które już istnieją w folderze docelowym *C:\temp*. Aby utworzyć opcji odzyskiwania, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="e3600-272">For this example, let's assume that we want to restore the files to *C:\temp*. Let's also assume that we want to skip files that already exist on the destination folder *C:\temp*. To create such a recovery option, use the following command:</span></span>

```
PS C:\> $recovery_option = New-OBRecoveryOption -DestinationPath "C:\temp" -OverwriteType Skip
```

<span data-ttu-id="e3600-273">Teraz uruchomić proces przywracania, używając [Start OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) polecenia na wybranym ```$item``` z danych wyjściowych ```Get-OBRecoverableItem``` polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="e3600-273">Now trigger the restore process by using the [Start-OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) command on the selected ```$item``` from the output of the ```Get-OBRecoverableItem``` cmdlet:</span></span>

```
PS C:\> Start-OBRecovery -RecoverableItem $item -RecoveryOption $recover_option
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Job completed.
The recovery operation completed successfully.
```


## <a name="uninstalling-the-azure-backup-agent"></a><span data-ttu-id="e3600-274">Odinstalowanie agenta usługi Kopia zapasowa Azure</span><span class="sxs-lookup"><span data-stu-id="e3600-274">Uninstalling the Azure Backup agent</span></span>
<span data-ttu-id="e3600-275">Odinstalowanie agenta usługi Kopia zapasowa Azure może odbywać się przy użyciu następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="e3600-275">Uninstalling the Azure Backup agent can be done by using the following command:</span></span>

```
PS C:\> .\MARSAgentInstaller.exe /d /q
```

<span data-ttu-id="e3600-276">Odinstalowywanie pliki binarne agenta na komputerze ma niektórych konsekwencje wziąć pod uwagę:</span><span class="sxs-lookup"><span data-stu-id="e3600-276">Uninstalling the agent binaries from the machine has some consequences to consider:</span></span>

* <span data-ttu-id="e3600-277">Usuwa filtr plików z komputera, a zatrzymania śledzenia zmian.</span><span class="sxs-lookup"><span data-stu-id="e3600-277">It removes the file-filter from the machine, and tracking of changes is stopped.</span></span>
* <span data-ttu-id="e3600-278">Wszystkie informacje o zasadach jest usuwany z komputera, ale informacje o zasadach nadal mają być przechowywane w usłudze.</span><span class="sxs-lookup"><span data-stu-id="e3600-278">All policy information is removed from the machine, but the policy information continues to be stored in the service.</span></span>
* <span data-ttu-id="e3600-279">Wszystkie harmonogramy tworzenia kopii zapasowej są usuwane i są pobierane nie dalsze kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="e3600-279">All backup schedules are removed, and no further backups are taken.</span></span>

<span data-ttu-id="e3600-280">Jednak dane przechowywane w pozostaje Azure i są przechowywane zgodnie z ustawień zasad przechowywania przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e3600-280">However, the data stored in Azure remains and is retained as per the retention policy setup by you.</span></span> <span data-ttu-id="e3600-281">Starsze punkty automatycznie są przestarzałe.</span><span class="sxs-lookup"><span data-stu-id="e3600-281">Older points are automatically aged out.</span></span>

## <a name="remote-management"></a><span data-ttu-id="e3600-282">Zdalne zarządzanie</span><span class="sxs-lookup"><span data-stu-id="e3600-282">Remote management</span></span>
<span data-ttu-id="e3600-283">Całe Zarządzanie wokół agenta usługi Kopia zapasowa Azure, zasady i źródłami danych mogą to robić zdalnie za pomocą programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e3600-283">All the management around the Azure Backup agent, policies, and data sources can be done remotely through PowerShell.</span></span> <span data-ttu-id="e3600-284">Komputer, który będzie zarządzany zdalnie musi poprawnie przygotowany.</span><span class="sxs-lookup"><span data-stu-id="e3600-284">The machine that will be managed remotely needs to be prepared correctly.</span></span>

<span data-ttu-id="e3600-285">Domyślnie Usługa WinRM jest skonfigurowany do uruchamiania ręcznego.</span><span class="sxs-lookup"><span data-stu-id="e3600-285">By default, the WinRM service is configured for manual startup.</span></span> <span data-ttu-id="e3600-286">Typ uruchamiania musi mieć ustawioną *automatyczne* i można uruchomić usługi.</span><span class="sxs-lookup"><span data-stu-id="e3600-286">The startup type must be set to *Automatic* and the service should be started.</span></span> <span data-ttu-id="e3600-287">Aby sprawdzić, czy Usługa WinRM jest uruchomiona, wartość właściwości Stan powinien być *systemem*.</span><span class="sxs-lookup"><span data-stu-id="e3600-287">To verify that the WinRM service is running, the value of the Status property should be *Running*.</span></span>

```
PS C:\> Get-Service WinRM

Status   Name               DisplayName
------   ----               -----------
Running  winrm              Windows Remote Management (WS-Manag...
```

<span data-ttu-id="e3600-288">Programu PowerShell, należy skonfigurować dla niego komunikację zdalną.</span><span class="sxs-lookup"><span data-stu-id="e3600-288">PowerShell should be configured for remoting.</span></span>

```
PS C:\> Enable-PSRemoting -force
WinRM is already set up to receive requests on this computer.
WinRM has been updated for remote management.
WinRM firewall exception enabled.

PS C:\> Set-ExecutionPolicy unrestricted -force
```

<span data-ttu-id="e3600-289">Komputer teraz można zarządzać zdalnie — począwszy od instalacji agenta.</span><span class="sxs-lookup"><span data-stu-id="e3600-289">The machine can now be managed remotely - starting from the installation of the agent.</span></span> <span data-ttu-id="e3600-290">Na przykład poniższy skrypt kopiuje agenta z komputerem zdalnym i instaluje je.</span><span class="sxs-lookup"><span data-stu-id="e3600-290">For example, the following script copies the agent to the remote machine and installs it.</span></span>

```
PS C:\> $dloc = "\\REMOTESERVER01\c$\Windows\Temp"
PS C:\> $agent = "\\REMOTESERVER01\c$\Windows\Temp\MARSAgentInstaller.exe"
PS C:\> $args = "/q"
PS C:\> Copy-Item "C:\Downloads\MARSAgentInstaller.exe" -Destination $dloc - force

PS C:\> $s = New-PSSession -ComputerName REMOTESERVER01
PS C:\> Invoke-Command -Session $s -Script { param($d, $a) Start-Process -FilePath $d $a -Wait } -ArgumentList $agent $args
```

## <a name="next-steps"></a><span data-ttu-id="e3600-291">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e3600-291">Next steps</span></span>
<span data-ttu-id="e3600-292">Aby uzyskać więcej informacji o kopii zapasowej dla systemu Windows Server/klienta Azure, zobacz</span><span class="sxs-lookup"><span data-stu-id="e3600-292">For more information about Azure Backup for Windows Server/Client see</span></span>

* [<span data-ttu-id="e3600-293">Wprowadzenie do usługi Azure Backup</span><span class="sxs-lookup"><span data-stu-id="e3600-293">Introduction to Azure Backup</span></span>](backup-introduction-to-azure-backup.md)
* [<span data-ttu-id="e3600-294">Wykonaj kopię zapasową serwerów z systemem Windows</span><span class="sxs-lookup"><span data-stu-id="e3600-294">Back up Windows Servers</span></span>](backup-configure-vault.md)
