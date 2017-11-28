---
title: "aaaAzure Backup - Użyj programu PowerShell tooback zapasowej obciążeń programu DPM | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toodeploy i zarządzanie nimi dla Data Protection Manager (DPM) przy użyciu programu PowerShell usługi Kopia zapasowa Azure"
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
ms.openlocfilehash: 27d2b4b3127b68c9da564697eb61dc3ccbc34b3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-backup-tooazure-for-data-protection-manager-dpm-servers-using-powershell"></a><span data-ttu-id="96f42-103">Wdrażanie i zarządzanie nimi tooAzure kopii zapasowej na serwerach Data Protection Manager (DPM) przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="96f42-103">Deploy and manage backup tooAzure for Data Protection Manager (DPM) servers using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="96f42-104">ARM</span><span class="sxs-lookup"><span data-stu-id="96f42-104">ARM</span></span>](backup-dpm-automation.md)
> * [<span data-ttu-id="96f42-105">Wdrożenie klasyczne</span><span class="sxs-lookup"><span data-stu-id="96f42-105">Classic</span></span>](backup-dpm-automation-classic.md)
>
>

<span data-ttu-id="96f42-106">W tym artykule opisano sposób toouse PowerShell toosetup Azure Backup na serwerze DPM i toomanage kopii zapasowej i odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="96f42-106">This article shows you how toouse PowerShell toosetup Azure Backup on a DPM server, and toomanage backup and recovery.</span></span>

## <a name="setting-up-hello-powershell-environment"></a><span data-ttu-id="96f42-107">Konfigurowanie środowiska PowerShell hello</span><span class="sxs-lookup"><span data-stu-id="96f42-107">Setting up hello PowerShell environment</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="96f42-108">Przed użyciem programu PowerShell toomanage tworzenia kopii zapasowych z tooAzure programu Data Protection Manager, należy toohave hello prawo środowiska PowerShell.</span><span class="sxs-lookup"><span data-stu-id="96f42-108">Before you can use PowerShell toomanage backups from Data Protection Manager tooAzure, you need toohave hello right environment in PowerShell.</span></span> <span data-ttu-id="96f42-109">Na początku hello hello sesji programu PowerShell upewnij się, uruchom hello następujące polecenia tooimport hello prawo modułów i pozwala toocorrectly poleceń cmdlet DPM powitania dla odwołania:</span><span class="sxs-lookup"><span data-stu-id="96f42-109">At hello start of hello PowerShell session, ensure that you run hello following command tooimport hello right modules and allow you toocorrectly reference hello DPM cmdlets:</span></span>

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

## <a name="setup-and-registration"></a><span data-ttu-id="96f42-110">Instalację i rejestrację</span><span class="sxs-lookup"><span data-stu-id="96f42-110">Setup and Registration</span></span>
<span data-ttu-id="96f42-111">toobegin:</span><span class="sxs-lookup"><span data-stu-id="96f42-111">toobegin:</span></span>

1. <span data-ttu-id="96f42-112">[Pobierz najnowsze PowerShell](https://github.com/Azure/azure-powershell/releases) (minimalna wersja wymagana jest: 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="96f42-112">[Download latest PowerShell](https://github.com/Azure/azure-powershell/releases) (minimum version required is: 1.0.0)</span></span>
2. <span data-ttu-id="96f42-113">Włącz polecenia cmdlet usługi Kopia zapasowa Azure hello przełączając zbyt*AzureResourceManager* trybie przy użyciu hello **Switch-AzureMode** apletu polecenia:</span><span class="sxs-lookup"><span data-stu-id="96f42-113">Enable hello Azure Backup commandlets by switching too*AzureResourceManager* mode by using hello **Switch-AzureMode** commandlet:</span></span>

```
PS C:\> Switch-AzureMode AzureResourceManager
```

<span data-ttu-id="96f42-114">Witaj następujące ustawienia i zadania rejestracji można zautomatyzować przy użyciu programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="96f42-114">hello following setup and registration tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="96f42-115">Tworzenie magazynu Usług odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="96f42-115">Create a Recovery Services vault</span></span>
* <span data-ttu-id="96f42-116">Instalowanie agenta usługi Kopia zapasowa Azure hello</span><span class="sxs-lookup"><span data-stu-id="96f42-116">Installing hello Azure Backup agent</span></span>
* <span data-ttu-id="96f42-117">Rejestrowanie w hello usługi Kopia zapasowa Azure</span><span class="sxs-lookup"><span data-stu-id="96f42-117">Registering with hello Azure Backup service</span></span>
* <span data-ttu-id="96f42-118">Ustawienia sieciowe</span><span class="sxs-lookup"><span data-stu-id="96f42-118">Networking settings</span></span>
* <span data-ttu-id="96f42-119">Ustawienia szyfrowania</span><span class="sxs-lookup"><span data-stu-id="96f42-119">Encryption settings</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="96f42-120">Tworzenie magazynu usługi Recovery Services</span><span class="sxs-lookup"><span data-stu-id="96f42-120">Create a recovery services vault</span></span>
<span data-ttu-id="96f42-121">następujące kroki Hello przeprowadzi Cię przez tworzenie magazynu usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="96f42-121">hello following steps lead you through creating a Recovery Services vault.</span></span> <span data-ttu-id="96f42-122">Magazyn usług odzyskiwania są inne niż magazynu kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="96f42-122">A Recovery Services vault is different than a Backup vault.</span></span>

1. <span data-ttu-id="96f42-123">Jeśli kopia zapasowa Azure jest używana do powitania po raz pierwszy, należy użyć hello **AzureRMResourceProvider rejestru** polecenia cmdlet tooregister hello Azure odzyskiwania usługodawcy w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="96f42-123">If you are using Azure Backup for hello first time, you must use hello **Register-AzureRMResourceProvider** cmdlet tooregister hello Azure Recovery Service provider with your subscription.</span></span>

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. <span data-ttu-id="96f42-124">Witaj magazyn usług odzyskiwania jest zasobu ARM, więc należy tooplace go w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="96f42-124">hello Recovery Services vault is an ARM resource, so you need tooplace it within a Resource Group.</span></span> <span data-ttu-id="96f42-125">Użyj istniejącej grupy zasobów lub Utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="96f42-125">You can use an existing resource group, or create a new one.</span></span> <span data-ttu-id="96f42-126">Podczas tworzenia nowej grupy zasobów, określ hello nazwy i lokalizacji hello grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="96f42-126">When creating a new resource group, specify hello name and location for hello resource group.</span></span>  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "West US"
    ```
3. <span data-ttu-id="96f42-127">Użyj hello **AzureRmRecoveryServicesVault nowy** toocreate polecenia cmdlet nowy magazyn.</span><span class="sxs-lookup"><span data-stu-id="96f42-127">Use hello **New-AzureRmRecoveryServicesVault** cmdlet toocreate a new vault.</span></span> <span data-ttu-id="96f42-128">Pamiętaj, toospecify hello tę samą lokalizację dla magazynu hello, które było używane dla grupy zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="96f42-128">Be sure toospecify hello same location for hello vault as was used for hello resource group.</span></span>

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "West US"
    ```
4. <span data-ttu-id="96f42-129">Określ typ hello toouse nadmiarowość magazynu; można użyć [lokalnie nadmiarowego magazynu (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) lub [z magazynu geograficznie nadmiarowego magazynu (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span><span class="sxs-lookup"><span data-stu-id="96f42-129">Specify hello type of storage redundancy toouse; you can use [Locally Redundant Storage (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) or [Geo Redundant Storage (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span></span> <span data-ttu-id="96f42-130">Witaj poniższy przykład przedstawia się, że opcja - BackupStorageRedundancy hello testVault ustawiono tooGeoRedundant.</span><span class="sxs-lookup"><span data-stu-id="96f42-130">hello following example shows hello -BackupStorageRedundancy option for testVault is set tooGeoRedundant.</span></span>

   > [!TIP]
   > <span data-ttu-id="96f42-131">Wiele poleceń cmdlet narzędzia Kopia zapasowa Azure wymaga obiektu magazynu usług odzyskiwania hello jako danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="96f42-131">Many Azure Backup cmdlets require hello Recovery Services vault object as an input.</span></span> <span data-ttu-id="96f42-132">Z tego powodu jest wygodne toostore hello usług odzyskiwania kopii zapasowej magazynu obiekt w zmiennej.</span><span class="sxs-lookup"><span data-stu-id="96f42-132">For this reason, it is convenient toostore hello Backup Recovery Services vault object in a variable.</span></span>
   >
   >

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testVault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

## <a name="view-hello-vaults-in-a-subscription"></a><span data-ttu-id="96f42-133">Widok hello magazynów w ramach subskrypcji</span><span class="sxs-lookup"><span data-stu-id="96f42-133">View hello vaults in a subscription</span></span>
<span data-ttu-id="96f42-134">Użyj **Get-AzureRmRecoveryServicesVault** tooview hello listę wszystkich magazynów w hello bieżącej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="96f42-134">Use **Get-AzureRmRecoveryServicesVault** tooview hello list of all vaults in hello current subscription.</span></span> <span data-ttu-id="96f42-135">Możesz użyć tego polecenia toocheck, utworzono nowy magazyn lub toosee magazynów, jakie są dostępne w hello subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="96f42-135">You can use this command toocheck that a new  vault was created, or toosee what vaults are available in hello subscription.</span></span>

<span data-ttu-id="96f42-136">Uruchom polecenie hello, Get-AzureRmRecoveryServicesVault i wszystkich magazynów w subskrypcji hello są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="96f42-136">Run hello command, Get-AzureRmRecoveryServicesVault, and all vaults in hello subscription are listed.</span></span>

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


## <a name="installing-hello-azure-backup-agent-on-a-dpm-server"></a><span data-ttu-id="96f42-137">Instalowanie agenta usługi Kopia zapasowa Azure hello na serwerze programu DPM</span><span class="sxs-lookup"><span data-stu-id="96f42-137">Installing hello Azure Backup agent on a DPM Server</span></span>
<span data-ttu-id="96f42-138">Przed zainstalowaniem agenta usługi Kopia zapasowa Azure hello należy toohave hello Instalatora, pobranych i znajdują się na powitania serwera systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="96f42-138">Before you install hello Azure Backup agent, you need toohave hello installer downloaded and present on hello Windows Server.</span></span> <span data-ttu-id="96f42-139">Możesz pobrać najnowszą wersję Instalatora hello hello ze hello [Microsoft Download Center](http://aka.ms/azurebackup_agent) lub z magazynu usług odzyskiwania hello strony pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="96f42-139">You can get hello latest version of hello installer from hello [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from hello Recovery Services vault's Dashboard page.</span></span> <span data-ttu-id="96f42-140">Zapisz Instalator hello tooan łatwo dostępnej lokalizacji, takich jak * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="96f42-140">Save hello installer tooan easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="96f42-141">tooinstall hello agenta, uruchom następujące polecenie w konsoli programu PowerShell z podwyższonym poziomem uprawnień hello **na serwerze DPM hello**:</span><span class="sxs-lookup"><span data-stu-id="96f42-141">tooinstall hello agent, run hello following command in an elevated PowerShell console **on hello DPM server**:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="96f42-142">Spowoduje to zainstalowanie agenta hello z wszystkich opcji domyślnych hello.</span><span class="sxs-lookup"><span data-stu-id="96f42-142">This installs hello agent with all hello default options.</span></span> <span data-ttu-id="96f42-143">Instalacja Hello zajmuje kilka minut w tle hello.</span><span class="sxs-lookup"><span data-stu-id="96f42-143">hello installation takes a few minutes in hello background.</span></span> <span data-ttu-id="96f42-144">Jeśli nie określisz hello */nu* hello opcja **usługi Windows Update** na końcu hello hello toocheck instalacji dla wszystkich aktualizacji, zostanie otwarte okno.</span><span class="sxs-lookup"><span data-stu-id="96f42-144">If you do not specify hello */nu* option hello **Windows Update** window opens at hello end of hello installation toocheck for any updates.</span></span>

<span data-ttu-id="96f42-145">Hello agent zostaną wyświetlone w hello listy zainstalowanych programów.</span><span class="sxs-lookup"><span data-stu-id="96f42-145">hello agent shows up in hello list of installed programs.</span></span> <span data-ttu-id="96f42-146">toosee hello listy zainstalowanych programów, należy przejść za**Panelu sterowania** > **programy** > **programy i funkcje**.</span><span class="sxs-lookup"><span data-stu-id="96f42-146">toosee hello list of installed programs, go too**Control Panel** > **Programs** > **Programs and Features**.</span></span>

![Agent został zainstalowany](./media/backup-dpm-automation/installed-agent-listing.png)

### <a name="installation-options"></a><span data-ttu-id="96f42-148">Opcje instalacji</span><span class="sxs-lookup"><span data-stu-id="96f42-148">Installation options</span></span>
<span data-ttu-id="96f42-149">toosee wszystkie opcje hello dostępne za pośrednictwem commandline hello, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="96f42-149">toosee all hello options available via hello commandline, use hello following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="96f42-150">Witaj dostępne opcje to:</span><span class="sxs-lookup"><span data-stu-id="96f42-150">hello available options include:</span></span>

| <span data-ttu-id="96f42-151">Opcja</span><span class="sxs-lookup"><span data-stu-id="96f42-151">Option</span></span> | <span data-ttu-id="96f42-152">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="96f42-152">Details</span></span> | <span data-ttu-id="96f42-153">Domyślne</span><span class="sxs-lookup"><span data-stu-id="96f42-153">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="96f42-154">/q</span><span class="sxs-lookup"><span data-stu-id="96f42-154">/q</span></span> |<span data-ttu-id="96f42-155">Instalację cichą</span><span class="sxs-lookup"><span data-stu-id="96f42-155">Quiet installation</span></span> |- |
| <span data-ttu-id="96f42-156">/ p: "Lokalizacja"</span><span class="sxs-lookup"><span data-stu-id="96f42-156">/p:"location"</span></span> |<span data-ttu-id="96f42-157">Ścieżka folderu instalacji toohello hello Azure Backup Agent.</span><span class="sxs-lookup"><span data-stu-id="96f42-157">Path toohello installation folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="96f42-158">C:\Program Files\Microsoft Azure Recovery usługi agenta</span><span class="sxs-lookup"><span data-stu-id="96f42-158">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="96f42-159">/ s: "Lokalizacja"</span><span class="sxs-lookup"><span data-stu-id="96f42-159">/s:"location"</span></span> |<span data-ttu-id="96f42-160">Ścieżka folderu pamięci podręcznej toohello hello Azure Backup Agent.</span><span class="sxs-lookup"><span data-stu-id="96f42-160">Path toohello cache folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="96f42-161">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="96f42-161">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="96f42-162">/m</span><span class="sxs-lookup"><span data-stu-id="96f42-162">/m</span></span> |<span data-ttu-id="96f42-163">TooMicrosoft opcjonalnych aktualizacji</span><span class="sxs-lookup"><span data-stu-id="96f42-163">Opt-in tooMicrosoft Update</span></span> |- |
| <span data-ttu-id="96f42-164">/nu</span><span class="sxs-lookup"><span data-stu-id="96f42-164">/nu</span></span> |<span data-ttu-id="96f42-165">Nie sprawdzaj aktualizacji po ukończeniu instalacji</span><span class="sxs-lookup"><span data-stu-id="96f42-165">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="96f42-166">/d</span><span class="sxs-lookup"><span data-stu-id="96f42-166">/d</span></span> |<span data-ttu-id="96f42-167">Odinstalowuje agenta usług odzyskiwania Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="96f42-167">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="96f42-168">/pH</span><span class="sxs-lookup"><span data-stu-id="96f42-168">/ph</span></span> |<span data-ttu-id="96f42-169">Adres hosta serwera proxy</span><span class="sxs-lookup"><span data-stu-id="96f42-169">Proxy Host Address</span></span> |- |
| <span data-ttu-id="96f42-170">/Po</span><span class="sxs-lookup"><span data-stu-id="96f42-170">/po</span></span> |<span data-ttu-id="96f42-171">Numer portu hosta serwera proxy</span><span class="sxs-lookup"><span data-stu-id="96f42-171">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="96f42-172">/Pu</span><span class="sxs-lookup"><span data-stu-id="96f42-172">/pu</span></span> |<span data-ttu-id="96f42-173">Nazwa użytkownika serwera proxy hosta</span><span class="sxs-lookup"><span data-stu-id="96f42-173">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="96f42-174">/PW</span><span class="sxs-lookup"><span data-stu-id="96f42-174">/pw</span></span> |<span data-ttu-id="96f42-175">Hasło serwera proxy</span><span class="sxs-lookup"><span data-stu-id="96f42-175">Proxy Password</span></span> |- |

## <a name="registering-dpm-tooa-recovery-services-vault"></a><span data-ttu-id="96f42-176">Rejestrowanie programu DPM tooa magazynu usług odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="96f42-176">Registering DPM tooa Recovery Services Vault</span></span>
<span data-ttu-id="96f42-177">Po utworzeniu magazynu usług odzyskiwania hello, Pobierz najnowszą wersję agenta hello i poświadczenia magazynu hello i zapisz go w dogodnym miejscu, podobnie jak C:\Downloads.</span><span class="sxs-lookup"><span data-stu-id="96f42-177">After you created hello Recovery Services vault, download hello latest agent and hello vault credentials and store it in a convenient location like C:\Downloads.</span></span>

```
PS C:\> $credspath = "C:\downloads"
PS C:\> $credsfilename = Get-AzureRmRecoveryServicesVaultSettingsFile -Backup -Vault $vault1 -Path  $credspath
PS C:\> $credsfilename
C:\downloads\testvault\_Sun Apr 10 2016.VaultCredentials
```

<span data-ttu-id="96f42-178">Na powitania serwera DPM, uruchom hello [Start OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) polecenia cmdlet tooregister hello maszyny z magazynem hello.</span><span class="sxs-lookup"><span data-stu-id="96f42-178">On hello DPM server, run hello [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet tooregister hello machine with hello vault.</span></span>

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-OBRegistration-VaultCredentials $cred -Confirm:$false
CertThumbprint      :7a2ef2caa2e74b6ed1222a5e89288ddad438df2
SubscriptionID      : ef4ab577-c2c0-43e4-af80-af49f485f3d1
ServiceResourceName: testvault
Region              :West US
Machine registration succeeded.
```

### <a name="initial-configuration-settings"></a><span data-ttu-id="96f42-179">Ustawienia konfiguracji początkowej</span><span class="sxs-lookup"><span data-stu-id="96f42-179">Initial configuration settings</span></span>
<span data-ttu-id="96f42-180">Po hello serwer DPM został zarejestrowany za pomocą hello magazyn usług odzyskiwania, rozpoczyna się domyślnych ustawień subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="96f42-180">Once hello DPM Server is registered with hello Recovery Services vault, it starts with default subscription settings.</span></span> <span data-ttu-id="96f42-181">Te ustawienia subskrypcji obejmują sieci, szyfrowania i hello obszaru przemieszczania.</span><span class="sxs-lookup"><span data-stu-id="96f42-181">These subscription settings include Networking, Encryption and hello Staging area.</span></span> <span data-ttu-id="96f42-182">ustawienia subskrypcji toochange należy toofirst uzyskać dojścia do na powitania istniejące ustawienia (ustawienie domyślne) przy użyciu hello [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="96f42-182">toochange subscription settings you need toofirst get a handle on hello existing (default) settings using hello [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet:</span></span>

```
$setting = Get-DPMCloudSubscriptionSetting -DPMServerName "TestingServer"
```

<span data-ttu-id="96f42-183">Wszystkie modyfikacje są wykonane toothis lokalnego środowiska PowerShell obiektu ```$setting``` , a następnie obiektowego hello jest tooDPM zatwierdzone i kopia zapasowa Azure toosave je przy użyciu hello [DPMCloudSubscriptionSetting zestaw](https://technet.microsoft.com/library/jj612791) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="96f42-183">All modifications are made toothis local PowerShell object ```$setting```  and then hello full object is committed tooDPM and Azure Backup toosave them using hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="96f42-184">Należy toouse hello ```–Commit``` tooensure flagę, która hello zmiany są zachowywane.</span><span class="sxs-lookup"><span data-stu-id="96f42-184">You need toouse hello ```–Commit``` flag tooensure that hello changes are persisted.</span></span> <span data-ttu-id="96f42-185">Witaj ustawienia nie będą stosowane i używane przez usługi Kopia zapasowa Azure, chyba że zostało zatwierdzone.</span><span class="sxs-lookup"><span data-stu-id="96f42-185">hello settings will not be applied and used by Azure Backup unless committed.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="networking"></a><span data-ttu-id="96f42-186">Sieć</span><span class="sxs-lookup"><span data-stu-id="96f42-186">Networking</span></span>
<span data-ttu-id="96f42-187">W przypadku łączności hello hello DPM maszyny toohello usługi Azure Backup na powitania internet za pośrednictwem serwera proxy, ustawienia serwera proxy hello należy podać dla pomyślnie utworzone kopie zapasowe.</span><span class="sxs-lookup"><span data-stu-id="96f42-187">If hello connectivity of hello DPM machine toohello Azure Backup service on hello internet is through a proxy server, then hello proxy server settings should be provided for successful backups.</span></span> <span data-ttu-id="96f42-188">Odbywa się przy użyciu hello ```-ProxyServer```i ```-ProxyPort```, ```-ProxyUsername``` i hello ```ProxyPassword``` parametrów z hello [DPMCloudSubscriptionSetting zestaw](https://technet.microsoft.com/library/jj612791) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="96f42-188">This is done by using hello ```-ProxyServer```and ```-ProxyPort```, ```-ProxyUsername``` and hello ```ProxyPassword``` parameters with hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="96f42-189">W tym przykładzie nie żadnego serwera proxy, dlatego firma Microsoft są jawnie wyczyszczenie żadnych informacji dotyczących serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="96f42-189">In this example, there is no proxy server so we are explicitly clearing any proxy-related information.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoProxy
```

<span data-ttu-id="96f42-190">Wykorzystanie przepustowości można również sterować za pomocą opcji ```-WorkHourBandwidth``` i ```-NonWorkHourBandwidth``` dla danego zestawu dni tygodnia hello.</span><span class="sxs-lookup"><span data-stu-id="96f42-190">Bandwidth usage can also be controlled with options of ```-WorkHourBandwidth``` and ```-NonWorkHourBandwidth``` for a given set of days of hello week.</span></span> <span data-ttu-id="96f42-191">W tym przykładzie firma Microsoft nie ustawienia dowolnej ograniczania.</span><span class="sxs-lookup"><span data-stu-id="96f42-191">In this example, we are not setting any throttling.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoThrottle
```

## <a name="configuring-hello-staging-area"></a><span data-ttu-id="96f42-192">Konfigurowanie hello obszaru przemieszczania</span><span class="sxs-lookup"><span data-stu-id="96f42-192">Configuring hello staging Area</span></span>
<span data-ttu-id="96f42-193">agent usługi Kopia zapasowa Azure Hello działającej na serwerze DPM hello wymaga tymczasowego magazynu dla danych przywróconych z chmury hello (lokalny obszar przemieszczania).</span><span class="sxs-lookup"><span data-stu-id="96f42-193">hello Azure Backup agent running on hello DPM server needs temporary storage for data restored from hello cloud (local staging area).</span></span> <span data-ttu-id="96f42-194">Konfigurowanie przy użyciu hello obszaru przemieszczania hello [DPMCloudSubscriptionSetting zestaw](https://technet.microsoft.com/library/jj612791) polecenia cmdlet i hello ```-StagingAreaPath``` parametru.</span><span class="sxs-lookup"><span data-stu-id="96f42-194">Configure hello staging area using hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet and hello ```-StagingAreaPath``` parameter.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -StagingAreaPath "C:\StagingArea"
```

<span data-ttu-id="96f42-195">W powyższym przykładzie hello, obszaru przemieszczania hello zostanie ustawiona zbyt*C:\StagingArea* w obiekcie środowiska PowerShell hello ```$setting```.</span><span class="sxs-lookup"><span data-stu-id="96f42-195">In hello example above, hello staging area will be set too*C:\StagingArea* in hello PowerShell object ```$setting```.</span></span> <span data-ttu-id="96f42-196">Upewnij się, że hello określony folder już istnieje, w przeciwnym razie hello końcowego zatwierdzania ustawienia subskrypcji hello zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="96f42-196">Ensure that hello specified folder already exists, or else hello final commit of hello subscription settings will fail.</span></span>

### <a name="encryption-settings"></a><span data-ttu-id="96f42-197">Ustawienia szyfrowania</span><span class="sxs-lookup"><span data-stu-id="96f42-197">Encryption settings</span></span>
<span data-ttu-id="96f42-198">tooAzure wysyłane dane kopii zapasowej Hello kopii zapasowej jest zaszyfrowany tooprotect hello poufność danych hello.</span><span class="sxs-lookup"><span data-stu-id="96f42-198">hello backup data sent tooAzure Backup is encrypted tooprotect hello confidentiality of hello data.</span></span> <span data-ttu-id="96f42-199">hasło szyfrowania Hello jest hello "password" toodecrypt hello danych w czasie hello przywracania.</span><span class="sxs-lookup"><span data-stu-id="96f42-199">hello encryption passphrase is hello "password" toodecrypt hello data at hello time of restore.</span></span> <span data-ttu-id="96f42-200">Jest to bezpieczne informacje ważne tookeep i secure po ustawieniu.</span><span class="sxs-lookup"><span data-stu-id="96f42-200">It is important tookeep this information safe and secure once it is set.</span></span>

<span data-ttu-id="96f42-201">W poniższym przykładzie hello, pierwsze polecenie hello konwertuje ciąg hello ```passphrase123456789``` tooa bezpieczny ciąg i przypisuje hello bezpieczny ciąg toohello zmiennej o nazwie ```$Passphrase```.</span><span class="sxs-lookup"><span data-stu-id="96f42-201">In hello example below, hello first command converts hello string ```passphrase123456789``` tooa secure string and assigns hello secure string toohello variable named ```$Passphrase```.</span></span> <span data-ttu-id="96f42-202">drugie polecenie Hello ustawia bezpieczny ciąg hello w ```$Passphrase``` jako hello hasła do szyfrowania kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="96f42-202">hello second command sets hello secure string in ```$Passphrase``` as hello password for encrypting backups.</span></span>

```
PS C:\> $Passphrase = ConvertTo-SecureString -string "passphrase123456789" -AsPlainText -Force

PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -EncryptionPassphrase $Passphrase
```

> [!IMPORTANT]
> <span data-ttu-id="96f42-203">Zachowaj informacje hasło hello bezpieczne po ustawieniu.</span><span class="sxs-lookup"><span data-stu-id="96f42-203">Keep hello passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="96f42-204">Nie będzie możliwe toorestore danych z platformy Azure bez tego hasła.</span><span class="sxs-lookup"><span data-stu-id="96f42-204">You will not be able toorestore data from Azure without this passphrase.</span></span>
>
>

<span data-ttu-id="96f42-205">W tym momencie powinien wprowadzone wszystkie hello wymagane zmiany toohello ```$setting``` obiektu.</span><span class="sxs-lookup"><span data-stu-id="96f42-205">At this point, you should have made all hello required changes toohello ```$setting``` object.</span></span> <span data-ttu-id="96f42-206">Należy pamiętać, toocommit hello zmiany.</span><span class="sxs-lookup"><span data-stu-id="96f42-206">Remember toocommit hello changes.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="protect-data-tooazure-backup"></a><span data-ttu-id="96f42-207">Ochrona danych tooAzure kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="96f42-207">Protect data tooAzure Backup</span></span>
<span data-ttu-id="96f42-208">W tej sekcji możesz dodać tooDPM serwera produkcyjnego i chronić magazynu programu DPM toolocal danych hello, a następnie tooAzure kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="96f42-208">In this section, you will add a production server tooDPM and then protect hello data toolocal DPM storage and then tooAzure Backup.</span></span> <span data-ttu-id="96f42-209">W przykładach hello przedstawiony zostanie sposób tooback zapasowe plików i folderów.</span><span class="sxs-lookup"><span data-stu-id="96f42-209">In hello examples, we will demonstrate how tooback up files and folders.</span></span> <span data-ttu-id="96f42-210">Witaj logiki można łatwo można toobackup rozszerzonej z dowolnego źródła danych obsługiwane przez program DPM.</span><span class="sxs-lookup"><span data-stu-id="96f42-210">hello logic can easily be extended toobackup any DPM-supported data source.</span></span> <span data-ttu-id="96f42-211">Kopii zapasowych programu DPM są regulowane przez ochronę grupy (PG) z czterech części:</span><span class="sxs-lookup"><span data-stu-id="96f42-211">All your DPM backups are governed by a Protection Group (PG) with four parts:</span></span>

1. <span data-ttu-id="96f42-212">**Członków grupy** znajduje się lista wszystkich hello obiekty chronione (nazywane również *źródeł danych* w programie DPM), które mają tooprotect w hello tej samej grupy ochrony.</span><span class="sxs-lookup"><span data-stu-id="96f42-212">**Group members** is a list of all hello protectable objects (also known as *Datasources* in DPM) that you want tooprotect in hello same protection group.</span></span> <span data-ttu-id="96f42-213">Na przykład można tooprotect produkcji maszyny wirtualne w jednej grupy ochrony i baz danych programu SQL Server w innej grupy ochrony jako mogą mieć różne wymagania kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="96f42-213">For example, you may want tooprotect production VMs in one protection group and SQL Server databases in another protection group as they may have different backup requirements.</span></span> <span data-ttu-id="96f42-214">Przed utworzeniem kopii zapasowej żadnego źródła danych na serwerze produkcyjnym należy toomake hello się, że Agent programu DPM jest zainstalowany na serwerze hello i jest zarządzany przez program DPM.</span><span class="sxs-lookup"><span data-stu-id="96f42-214">Before you can back up any datasource on a production server you need toomake sure hello DPM Agent is installed on hello server and is managed by DPM.</span></span> <span data-ttu-id="96f42-215">Wykonaj procedurę hello [instalowanie hello agenta DPM](https://technet.microsoft.com/library/bb870935.aspx) i połączenie go toohello odpowiednie serwera DPM.</span><span class="sxs-lookup"><span data-stu-id="96f42-215">Follow hello steps for [installing hello DPM Agent](https://technet.microsoft.com/library/bb870935.aspx) and linking it toohello appropriate DPM Server.</span></span>
2. <span data-ttu-id="96f42-216">**Metoda ochrony danych** określa hello docelowej lokalizacji kopii zapasowych — taśma, dysk i chmura.</span><span class="sxs-lookup"><span data-stu-id="96f42-216">**Data protection method** specifies hello target backup locations - tape, disk, and cloud.</span></span> <span data-ttu-id="96f42-217">W naszym przykładzie będzie chronić danych toohello lokalny dysk i toohello w chmurze.</span><span class="sxs-lookup"><span data-stu-id="96f42-217">In our example we will protect data toohello local disk and toohello cloud.</span></span>
3. <span data-ttu-id="96f42-218">A **harmonogram tworzenia kopii zapasowych** , który określa podczas tworzenia kopii zapasowych należy toobe podjęte i jak często hello dane mają być synchronizowane między hello serwera programu DPM i serwerze produkcyjnym hello.</span><span class="sxs-lookup"><span data-stu-id="96f42-218">A **backup schedule** that specifies when backups need toobe taken and how often hello data should be synchronized between hello DPM Server and hello production server.</span></span>
4. <span data-ttu-id="96f42-219">A **harmonogramu przechowywania** Określa, jak długo punkty odzyskiwania hello tooretain na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="96f42-219">A **retention schedule** that specifies how long tooretain hello recovery points in Azure.</span></span>

### <a name="creating-a-protection-group"></a><span data-ttu-id="96f42-220">Utworzenie grupy ochrony</span><span class="sxs-lookup"><span data-stu-id="96f42-220">Creating a protection group</span></span>
<span data-ttu-id="96f42-221">Rozpocznij od utworzenia nowej grupy ochrony za pomocą hello [DPMProtectionGroup nowy](https://technet.microsoft.com/library/hh881722) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="96f42-221">Start by creating a new Protection Group using hello [New-DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) cmdlet.</span></span>

```
PS C:\> $PG = New-DPMProtectionGroup -DPMServerName " TestingServer " -Name "ProtectGroup01"
```

<span data-ttu-id="96f42-222">Witaj powyżej polecenie cmdlet spowoduje utworzenie grupy ochrony o nazwie *ProtectGroup01*.</span><span class="sxs-lookup"><span data-stu-id="96f42-222">hello above cmdlet will create a Protection Group named *ProtectGroup01*.</span></span> <span data-ttu-id="96f42-223">Istniejącej grupy ochrony można także modyfikować nowszych kopii zapasowej tooadd toohello chmury Azure.</span><span class="sxs-lookup"><span data-stu-id="96f42-223">An existing protection group can also be modified later tooadd backup toohello Azure cloud.</span></span> <span data-ttu-id="96f42-224">Jednak toomake zmiany toohello grupy ochrony — nowy lub istniejący - potrzebujemy tooget dojścia na *modyfikowalnymi* obiektu przy użyciu hello [Get DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="96f42-224">However, toomake any changes toohello Protection Group - new or existing - we need tooget a handle on a *modifiable* object using hello [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) cmdlet.</span></span>

```
PS C:\> $MPG = Get-ModifiableProtectionGroup $PG
```

### <a name="adding-group-members-toohello-protection-group"></a><span data-ttu-id="96f42-225">Dodawanie grupy toohello członków grupy ochrony</span><span class="sxs-lookup"><span data-stu-id="96f42-225">Adding group members toohello Protection Group</span></span>
<span data-ttu-id="96f42-226">Każdy Agent programu DPM wie hello listy źródeł danych na powitania serwera, który jest zainstalowany na.</span><span class="sxs-lookup"><span data-stu-id="96f42-226">Each DPM Agent knows hello list of datasources on hello server that it is installed on.</span></span> <span data-ttu-id="96f42-227">tooadd toohello datasource grupy ochrony, hello toofirst potrzeb agenta DPM wysyła listę hello źródeł danych toohello zapasowego serwera programu DPM.</span><span class="sxs-lookup"><span data-stu-id="96f42-227">tooadd a datasource toohello Protection Group, hello DPM Agent needs toofirst send a list of hello datasources back toohello DPM server.</span></span> <span data-ttu-id="96f42-228">Jeden lub więcej źródeł danych są, a następnie wybrać i dodać toohello grupy ochrony.</span><span class="sxs-lookup"><span data-stu-id="96f42-228">One or more datasources are then selected and added toohello Protection Group.</span></span> <span data-ttu-id="96f42-229">Hello PowerShell kroki potrzebne tooachieve są to:</span><span class="sxs-lookup"><span data-stu-id="96f42-229">hello PowerShell steps needed tooachieve this are:</span></span>

1. <span data-ttu-id="96f42-230">Pobierz listę wszystkich serwerów zarządzanych przez program DPM za pomocą hello agenta programu DPM.</span><span class="sxs-lookup"><span data-stu-id="96f42-230">Fetch a list of all servers managed by DPM through hello DPM Agent.</span></span>
2. <span data-ttu-id="96f42-231">Wybierz określonego serwera.</span><span class="sxs-lookup"><span data-stu-id="96f42-231">Choose a specific server.</span></span>
3. <span data-ttu-id="96f42-232">Pobranie listy wszystkich źródeł danych na powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="96f42-232">Fetch a list of all datasources on hello server.</span></span>
4. <span data-ttu-id="96f42-233">Wybierz co najmniej jednego źródła danych, a następnie dodać toohello grupy ochrony</span><span class="sxs-lookup"><span data-stu-id="96f42-233">Choose one or more datasources and add them toohello Protection Group</span></span>

<span data-ttu-id="96f42-234">Hello listy serwerów, na które hello agenta programu DPM jest zainstalowany i jest zarządzany przez powitania serwera programu DPM są uzyskiwane z hello [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="96f42-234">hello list of servers on which hello DPM Agent is installed and is being managed by hello DPM Server is acquired with hello [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet.</span></span> <span data-ttu-id="96f42-235">W tym przykładzie firma Microsoft będzie filtrowania i skonfigurować tylko PS o nazwie *productionserver01* do utworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="96f42-235">In this example we will filter and only configure PS with name *productionserver01* for backup.</span></span>

```
PS C:\> $server = Get-ProductionServer -DPMServerName "TestingServer" | where {($_.servername) –contains “productionserver01”
```

<span data-ttu-id="96f42-236">Teraz pobrać hello listy źródeł danych na ```$server``` przy użyciu hello [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="96f42-236">Now fetch hello list of datasources on ```$server``` using hello [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet.</span></span> <span data-ttu-id="96f42-237">W tym przykładzie mamy filtrowania dla woluminu hello * D:\* chcemy tooconfigure do utworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="96f42-237">In this example we are filtering for hello volume *D:\* that we want tooconfigure for backup.</span></span> <span data-ttu-id="96f42-238">To źródło danych jest następnie dodawana toohello grupy ochrony za pomocą hello [DPMChildDatasource Dodaj](https://technet.microsoft.com/library/hh881732) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="96f42-238">This datasource is then added toohello Protection Group using hello [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet.</span></span> <span data-ttu-id="96f42-239">Pamiętaj toouse hello *modyfikowalnymi* obiektu grupy ochrony ```$MPG``` toomake hello dodatków.</span><span class="sxs-lookup"><span data-stu-id="96f42-239">Remember toouse hello *modifiable* protection group object ```$MPG``` toomake hello additions.</span></span>

```
PS C:\> $DS = Get-Datasource -ProductionServer $server -Inquire | where { $_.Name -contains “D:\” }

PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS
```

<span data-ttu-id="96f42-240">Powtórz ten krok liczbę razy, aż zostaną dodane wszystkie hello wybrane grupy ochrony toohello źródeł danych.</span><span class="sxs-lookup"><span data-stu-id="96f42-240">Repeat this step as many times as required, until you have added all hello chosen datasources toohello protection group.</span></span> <span data-ttu-id="96f42-241">Można również uruchomić tylko jedno źródło danych i hello pełny przepływ pracy tworzenia hello grupy ochrony i w późniejszym czasie dodać więcej źródeł danych toohello grupy ochrony.</span><span class="sxs-lookup"><span data-stu-id="96f42-241">You can also start with just one datasource, and complete hello workflow for creating hello Protection Group, and at a later point add more datasources toohello Protection Group.</span></span>

### <a name="selecting-hello-data-protection-method"></a><span data-ttu-id="96f42-242">Wybieranie metody ochrony danych hello</span><span class="sxs-lookup"><span data-stu-id="96f42-242">Selecting hello data protection method</span></span>
<span data-ttu-id="96f42-243">Po dodaniu źródła danych hello toohello grupy ochrony, hello następnym krokiem jest metoda ochrony hello toospecify przy użyciu hello [DPMProtectionType zestaw](https://technet.microsoft.com/library/hh881725) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="96f42-243">Once hello datasources have been added toohello Protection Group, hello next step is toospecify hello protection method using hello [Set-DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet.</span></span> <span data-ttu-id="96f42-244">W tym przykładzie hello grupy ochrony jest ustawiony na potrzeby dysku lokalnego, a kopia zapasowa w chmurze.</span><span class="sxs-lookup"><span data-stu-id="96f42-244">In this example, hello Protection Group is setup for local disk and cloud backup.</span></span> <span data-ttu-id="96f42-245">Należy również toospecify hello datasource, które mają toocloud tooprotect przy użyciu hello [DPMChildDatasource Dodaj](https://technet.microsoft.com/library/hh881732.aspx) polecenia cmdlet flagą - Online.</span><span class="sxs-lookup"><span data-stu-id="96f42-245">You also need toospecify hello datasource that you want tooprotect toocloud using hello [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet with -Online flag.</span></span>

```
PS C:\> Set-DPMProtectionType -ProtectionGroup $MPG -ShortTerm Disk –LongTerm Online
PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS –Online
```

### <a name="setting-hello-retention-range"></a><span data-ttu-id="96f42-246">Ustawianie zakresu przechowywania hello</span><span class="sxs-lookup"><span data-stu-id="96f42-246">Setting hello retention range</span></span>
<span data-ttu-id="96f42-247">Ustawienia przechowywania hello hello punktów kopii zapasowej za pomocą hello [DPMPolicyObjective zestaw](https://technet.microsoft.com/library/hh881762) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="96f42-247">Set hello retention for hello backup points using hello [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span> <span data-ttu-id="96f42-248">Gdy może wydawać się przechowywania hello nieparzysta tooset przed zdefiniowaniem hello harmonogram tworzenia kopii zapasowych, przy użyciu hello ```Set-DPMPolicyObjective``` polecenie cmdlet automatycznie ustawia domyślny harmonogram tworzenia kopii zapasowej, który może być modyfikowany.</span><span class="sxs-lookup"><span data-stu-id="96f42-248">While it might seem odd tooset hello retention before hello backup schedule has been defined, using hello ```Set-DPMPolicyObjective``` cmdlet automatically sets a default backup schedule that can then be modified.</span></span> <span data-ttu-id="96f42-249">Jest zawsze harmonogram tworzenia kopii zapasowych hello możliwe tooset najpierw i hello zasady przechowywania po.</span><span class="sxs-lookup"><span data-stu-id="96f42-249">It is always possible tooset hello backup schedule first and hello retention policy after.</span></span>

<span data-ttu-id="96f42-250">W poniższym przykładzie hello polecenia cmdlet hello ustawia hello parametry przechowywania kopii zapasowych na dysku.</span><span class="sxs-lookup"><span data-stu-id="96f42-250">In hello example below, hello cmdlet sets hello retention parameters for disk backups.</span></span> <span data-ttu-id="96f42-251">To zachowują kopie zapasowe 10 dni i synchronizowanie danych co 6 godzin między serwerem produkcyjnym hello i hello programu DPM.</span><span class="sxs-lookup"><span data-stu-id="96f42-251">This will retain backups for 10 days, and sync data every 6 hours between hello production server and hello DPM server.</span></span> <span data-ttu-id="96f42-252">Witaj ```SynchronizationFrequencyMinutes``` nie definiuje, jak często punktu kopii zapasowej jest tworzony, ale jak często dane są skopiowanych toohello serwera DPM.</span><span class="sxs-lookup"><span data-stu-id="96f42-252">hello ```SynchronizationFrequencyMinutes``` doesn't define how often a backup point is created, but how often data is copied toohello DPM server.</span></span>  <span data-ttu-id="96f42-253">To ustawienie uniemożliwia tworzenie kopii zapasowych za duży.</span><span class="sxs-lookup"><span data-stu-id="96f42-253">This setting prevents backups from becoming too large.</span></span>

```
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -RetentionRangeInDays 10 -SynchronizationFrequencyMinutes 360
```

<span data-ttu-id="96f42-254">Kopii zapasowych będzie tooAzure (Program DPM stosowany jest wspólny termin toothem kopii zapasowych Online) można skonfigurować dla zakresów przechowywania hello [długoterminowych przechowywania użyciu schematu dziadek-ojciec-syn. (GFS)](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="96f42-254">For backups going tooAzure (DPM refers toothem as Online backups) hello retention ranges can be configured for [long term retention using a Grandfather-Father-Son scheme (GFS)](backup-azure-backup-cloud-as-tape.md).</span></span> <span data-ttu-id="96f42-255">Oznacza to można zdefiniować zasady przechowywania Scalonej obejmujące codziennie, co tydzień, miesięcznych i rocznych zasady przechowywania.</span><span class="sxs-lookup"><span data-stu-id="96f42-255">That is, you can define a combined retention policy involving daily, weekly, monthly and yearly retention policies.</span></span> <span data-ttu-id="96f42-256">W tym przykładzie firma Microsoft utworzenia tablicy reprezentujący schemat przechowywania złożonych hello chcemy, a następnie skonfiguruj zakres przechowywania hello za pomocą hello [DPMPolicyObjective zestaw](https://technet.microsoft.com/library/hh881762) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="96f42-256">In this example, we create an array representing hello complex retention scheme that we want, and then configure hello retention range using hello [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span>

```
PS C:\> $RRlist = @()
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 180, Days)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 104, Weeks)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 60, Month)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 10, Years)
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -OnlineRetentionRangeList $RRlist
```

### <a name="set-hello-backup-schedule"></a><span data-ttu-id="96f42-257">Harmonogram tworzenia kopii zapasowych hello zestawu</span><span class="sxs-lookup"><span data-stu-id="96f42-257">Set hello backup schedule</span></span>
<span data-ttu-id="96f42-258">Program DPM ustawia automatycznie domyślny harmonogram tworzenia kopii zapasowej, jeśli Określ cel ochrony hello przy użyciu hello ```Set-DPMPolicyObjective``` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="96f42-258">DPM sets a default backup schedule automatically if you specify hello protection objective using hello ```Set-DPMPolicyObjective``` cmdlet.</span></span> <span data-ttu-id="96f42-259">toochange hello domyślne harmonogramy, użyj hello [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) polecenia cmdlet następuje hello [DPMPolicySchedule zestaw](https://technet.microsoft.com/library/hh881723) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="96f42-259">toochange hello default schedules, use hello [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet followed by hello [Set-DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) cmdlet.</span></span>

```
PS C:\> $onlineSch = Get-DPMPolicySchedule -ProtectionGroup $mpg -LongTerm Online
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[0] -TimesOfDay 02:00
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[1] -TimesOfDay 02:00 -DaysOfWeek Sa,Su –Interval 1
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[2] -TimesOfDay 02:00 -RelativeIntervals First,Third –DaysOfWeek Sa
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[3] -TimesOfDay 02:00 -DaysOfMonth 2,5,8,9 -Months Jan,Jul
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```

<span data-ttu-id="96f42-260">W hello powyżej przykład ```$onlineSch``` jest tablicy z czterech elementów, które zawierają hello istniejący harmonogram ochrony w trybie online dla hello grupy ochrony w schemacie GFS hello:</span><span class="sxs-lookup"><span data-stu-id="96f42-260">In hello above example, ```$onlineSch``` is an array with four elements that contains hello existing online protection schedule for hello Protection Group in hello GFS scheme:</span></span>

1. <span data-ttu-id="96f42-261">```$onlineSch[0]```zawiera harmonogramu dziennego hello</span><span class="sxs-lookup"><span data-stu-id="96f42-261">```$onlineSch[0]``` contains hello daily schedule</span></span>
2. <span data-ttu-id="96f42-262">```$onlineSch[1]```zawiera hello harmonogramu tygodniowego</span><span class="sxs-lookup"><span data-stu-id="96f42-262">```$onlineSch[1]``` contains hello weekly schedule</span></span>
3. <span data-ttu-id="96f42-263">```$onlineSch[2]```zawiera hello harmonogramu miesięcznego</span><span class="sxs-lookup"><span data-stu-id="96f42-263">```$onlineSch[2]``` contains hello monthly schedule</span></span>
4. <span data-ttu-id="96f42-264">```$onlineSch[3]```zawiera hello corocznych harmonogramu</span><span class="sxs-lookup"><span data-stu-id="96f42-264">```$onlineSch[3]``` contains hello yearly schedule</span></span>

<span data-ttu-id="96f42-265">Więc jeśli potrzebujesz harmonogramu tygodniowego hello toomodify należy toorefer toohello ```$onlineSch[1]```.</span><span class="sxs-lookup"><span data-stu-id="96f42-265">So if you need toomodify hello weekly schedule, you need toorefer toohello ```$onlineSch[1]```.</span></span>

### <a name="initial-backup"></a><span data-ttu-id="96f42-266">Początkowa kopia zapasowa</span><span class="sxs-lookup"><span data-stu-id="96f42-266">Initial backup</span></span>
<span data-ttu-id="96f42-267">Podczas tworzenia kopii zapasowej źródła danych powitania po raz pierwszy, program DPM musi tworzy repliki początkowej który tworzy pełną kopię hello toobe źródeł danych chronionych na woluminie repliki programu DPM.</span><span class="sxs-lookup"><span data-stu-id="96f42-267">When backing up a datasource for hello first time, DPM needs creates initial replica that creates a full copy of hello datasource toobe protected on DPM replica volume.</span></span> <span data-ttu-id="96f42-268">To działanie albo mogą być planowane na określoną godzinę lub mogą być wyzwalane ręcznie, używając hello [DPMReplicaCreationMethod zestaw](https://technet.microsoft.com/library/hh881715) polecenia cmdlet z parametrem hello ```-NOW```.</span><span class="sxs-lookup"><span data-stu-id="96f42-268">This activity can either be scheduled for a specific time, or can be triggered manually, using hello [Set-DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet with hello parameter ```-NOW```.</span></span>

```
PS C:\> Set-DPMReplicaCreationMethod -ProtectionGroup $MPG -NOW
```
### <a name="changing-hello-size-of-dpm-replica--recovery-point-volume"></a><span data-ttu-id="96f42-269">Zmiana rozmiaru hello repliki programu DPM i wolumin punktu odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="96f42-269">Changing hello size of DPM Replica & recovery point volume</span></span>
<span data-ttu-id="96f42-270">Możesz również zmienić rozmiar hello woluminu repliki programu DPM i kopii w tle woluminu przy użyciu [DPMDatasourceDiskAllocation zestaw](https://technet.microsoft.com/library/hh881618.aspx) polecenia cmdlet, tak jak hello poniższy przykład: Get-DatasourceDiskAllocation - Datasource $DS Set-DatasourceDiskAllocation - Datasource $DS - ProtectionGroup $MPG-ręczne - ReplicaArea (2 gb) — ShadowCopyArea (2 gb)</span><span class="sxs-lookup"><span data-stu-id="96f42-270">You can also change hello size of DPM Replica volume and Shadow Copy volume using [Set-DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) cmdlet as in hello following example: Get-DatasourceDiskAllocation -Datasource $DS Set-DatasourceDiskAllocation -Datasource $DS -ProtectionGroup $MPG -manual -ReplicaArea (2gb) -ShadowCopyArea (2gb)</span></span>

### <a name="committing-hello-changes-toohello-protection-group"></a><span data-ttu-id="96f42-271">Przekazywanie hello toohello zmiany grupy ochrony</span><span class="sxs-lookup"><span data-stu-id="96f42-271">Committing hello changes toohello Protection Group</span></span>
<span data-ttu-id="96f42-272">Na koniec hello zmiany muszą toobe zatwierdzona przed programu DPM można wykonać kopię zapasową hello na powitania nowej konfiguracji grupy ochrony.</span><span class="sxs-lookup"><span data-stu-id="96f42-272">Finally, hello changes need toobe committed before DPM can take hello backup per hello new Protection Group configuration.</span></span> <span data-ttu-id="96f42-273">Można to osiągnąć przy użyciu hello [DPMProtectionGroup zestaw](https://technet.microsoft.com/library/hh881758) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="96f42-273">This can be achieved using hello [Set-DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet.</span></span>

```
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```
## <a name="view-hello-backup-points"></a><span data-ttu-id="96f42-274">Wyświetlanie hello punktów kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="96f42-274">View hello backup points</span></span>
<span data-ttu-id="96f42-275">Można użyć hello [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) tooget polecenia cmdlet listę wszystkich punktów odzyskiwania dla źródła danych.</span><span class="sxs-lookup"><span data-stu-id="96f42-275">You can use hello [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) cmdlet tooget a list of all recovery points for a datasource.</span></span> <span data-ttu-id="96f42-276">W tym przykładzie zostaną wykonane następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="96f42-276">In this example, we will:</span></span>

* <span data-ttu-id="96f42-277">Pobieranie wszystkich hello PGA na serwerze DPM hello i przechowywane w tablicy```$PG```</span><span class="sxs-lookup"><span data-stu-id="96f42-277">fetch all hello PGs on hello DPM server and stored in an array ```$PG```</span></span>
* <span data-ttu-id="96f42-278">Pobierz toohello odpowiedniego hello źródeł danych```$PG[0]```</span><span class="sxs-lookup"><span data-stu-id="96f42-278">get hello datasources corresponding toohello ```$PG[0]```</span></span>
* <span data-ttu-id="96f42-279">Pobierz wszystkie hello punkty odzyskiwania dla źródła danych.</span><span class="sxs-lookup"><span data-stu-id="96f42-279">get all hello recovery points for a datasource.</span></span>

```
PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online
```

## <a name="restore-data-protected-on-azure"></a><span data-ttu-id="96f42-280">Przywracanie danych chronionych na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="96f42-280">Restore data protected on Azure</span></span>
<span data-ttu-id="96f42-281">Przywracanie danych jest kombinacją ```RecoverableItem``` obiektu i ```RecoveryOption``` obiektu.</span><span class="sxs-lookup"><span data-stu-id="96f42-281">Restoring data is a combination of a ```RecoverableItem``` object and a ```RecoveryOption``` object.</span></span> <span data-ttu-id="96f42-282">W poprzedniej sekcji hello dotarliśmy listę hello punktów kopii zapasowej dla źródła danych.</span><span class="sxs-lookup"><span data-stu-id="96f42-282">In hello previous section, we got a list of hello backup points for a datasource.</span></span>

<span data-ttu-id="96f42-283">W poniższym przykładzie hello przedstawiony sposób toorestore funkcji Hyper-V maszyny wirtualnej z kopii zapasowej Azure za pomocą punktów kopii zapasowej łączenie z hello docelowe dla odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="96f42-283">In hello example below, we demonstrate how toorestore a Hyper-V virtual machine from Azure Backup by combining backup points with hello target for recovery.</span></span> <span data-ttu-id="96f42-284">Ten przykład obejmuje:</span><span class="sxs-lookup"><span data-stu-id="96f42-284">This example includes:</span></span>

* <span data-ttu-id="96f42-285">Tworzenie opcję odzyskiwania przy użyciu hello [DPMRecoveryOption nowy](https://technet.microsoft.com/library/hh881592) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="96f42-285">Creating a recovery option using hello  [New-DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) cmdlet.</span></span>
* <span data-ttu-id="96f42-286">Pobrano tablicy hello punktów kopii zapasowej za pomocą hello ```Get-DPMRecoveryPoint``` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="96f42-286">Fetching hello array of backup points using hello ```Get-DPMRecoveryPoint``` cmdlet.</span></span>
* <span data-ttu-id="96f42-287">Po wybraniu opcji tworzenia kopii zapasowej toorestore punktu z.</span><span class="sxs-lookup"><span data-stu-id="96f42-287">Choosing a backup point toorestore from.</span></span>

```
PS C:\> $RecoveryOption = New-DPMRecoveryOption -HyperVDatasource -TargetServer "HVDCenter02" -RecoveryLocation AlternateHyperVServer -RecoveryType Recover -TargetLocation “C:\VMRecovery”

PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online

PS C:\> Restore-DPMRecoverableItem -RecoverableItem $RecoveryPoints[0] -RecoveryOption $RecoveryOption
```

<span data-ttu-id="96f42-288">polecenia Hello można z łatwością rozszerzyć dla dowolnego typu źródła danych.</span><span class="sxs-lookup"><span data-stu-id="96f42-288">hello commands can easily be extended for any datasource type.</span></span>

## <a name="next-steps"></a><span data-ttu-id="96f42-289">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="96f42-289">Next steps</span></span>
* <span data-ttu-id="96f42-290">Aby uzyskać więcej informacji na temat programu DPM Zobacz tooAzure kopii zapasowej [tooDPM wprowadzenie kopii zapasowej](backup-azure-dpm-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="96f42-290">For more information about DPM tooAzure Backup see [Introduction tooDPM Backup](backup-azure-dpm-introduction.md)</span></span>
