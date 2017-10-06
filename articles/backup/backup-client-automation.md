---
title: "tooback PowerShell aaaUse się tooAzure systemu Windows Server | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toodeploy i zarządzać nimi za pomocą programu PowerShell usługi Kopia zapasowa Azure"
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
ms.openlocfilehash: f13224f53abd6fbd132fee4347b0b99e8f5e2678
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-backup-tooazure-for-windows-serverwindows-client-using-powershell"></a><span data-ttu-id="9cf11-103">Wdrażanie i zarządzanie nimi tooAzure kopii zapasowej dla klienta systemu Windows i serwera systemu Windows przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="9cf11-103">Deploy and manage backup tooAzure for Windows Server/Windows Client using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9cf11-104">ARM</span><span class="sxs-lookup"><span data-stu-id="9cf11-104">ARM</span></span>](backup-client-automation.md)
> * [<span data-ttu-id="9cf11-105">Wdrożenie klasyczne</span><span class="sxs-lookup"><span data-stu-id="9cf11-105">Classic</span></span>](backup-client-automation-classic.md)
>
>

<span data-ttu-id="9cf11-106">W tym artykule opisano sposób toouse PowerShell Konfigurowanie usługi Kopia zapasowa Azure w systemie Windows Server lub klienta systemu Windows oraz zarządzania nimi kopii zapasowych i odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="9cf11-106">This article shows you how toouse PowerShell for setting up Azure Backup on Windows Server or a Windows client, and managing backup and recovery.</span></span>

## <a name="install-azure-powershell"></a><span data-ttu-id="9cf11-107">Instalowanie programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="9cf11-107">Install Azure PowerShell</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="9cf11-108">Ten artykuł dotyczy hello Azure Resource Manager (ARM) i hello poleceń cmdlet programu PowerShell kopii zapasowej Online MS, umożliwiające toouse magazynu usług odzyskiwania w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="9cf11-108">This article focuses on hello Azure Resource Manager (ARM) and hello MS Online Backup PowerShell cmdlets that enable you toouse a Recovery Services vault in a resource group.</span></span>

<span data-ttu-id="9cf11-109">Października 2015 Azure PowerShell 1.0 został wydany.</span><span class="sxs-lookup"><span data-stu-id="9cf11-109">In October 2015, Azure PowerShell 1.0 was released.</span></span> <span data-ttu-id="9cf11-110">Ta wersja zakończyło się pomyślnie wersji hello 0.9.8 i temat istotne zmiany, szczególnie w hello wzorzec nazewnictwa hello poleceń cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9cf11-110">This release succeeded hello 0.9.8 release and brought about some significant changes, especially in hello naming pattern of hello cmdlets.</span></span> <span data-ttu-id="9cf11-111">Wykonaj polecenia cmdlet 1.0 hello wzorzec nazewnictwa {czasownik}-AzureRm {rzeczownik}; natomiast nie dołączaj nazwy hello 0.9.8 **Rm** (na przykład, New-AzureRmResourceGroup zamiast New-AzureResourceGroup).</span><span class="sxs-lookup"><span data-stu-id="9cf11-111">1.0 cmdlets follow hello naming pattern {verb}-AzureRm{noun}; whereas, hello 0.9.8 names do not include **Rm** (for example, New-AzureRmResourceGroup instead of New-AzureResourceGroup).</span></span> <span data-ttu-id="9cf11-112">Podczas korzystania z programu Azure PowerShell 0.9.8, należy najpierw włączyć tryb Resource Manager hello, uruchamiając hello **Switch-AzureMode AzureResourceManager** polecenia.</span><span class="sxs-lookup"><span data-stu-id="9cf11-112">When using Azure PowerShell 0.9.8, you must first enable hello Resource Manager mode by running hello **Switch-AzureMode AzureResourceManager** command.</span></span> <span data-ttu-id="9cf11-113">To polecenie nie jest konieczne w wersji 1.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="9cf11-113">This command is not necessary in 1.0 or later.</span></span>

<span data-ttu-id="9cf11-114">Jeśli chcesz toouse skryptów przeznaczony dla środowiska hello 0.9.8, hello 1.0 lub nowszej środowiska, należy ostrożnie aktualizacji i testowanie skryptów hello w środowisku przedprodukcyjnym przed ich użyciem w środowisku produkcyjnym tooavoid nieoczekiwany wpływu.</span><span class="sxs-lookup"><span data-stu-id="9cf11-114">If you want toouse your scripts written for hello 0.9.8 environment, in hello 1.0 or later environment, you should carefully update and test hello scripts in a pre-production environment before using them in production tooavoid unexpected impact.</span></span>

<span data-ttu-id="9cf11-115">[Pobierz najnowszą wersję programu PowerShell hello](https://github.com/Azure/azure-powershell/releases) (minimalna wersja wymagana jest: 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="9cf11-115">[Download hello latest PowerShell release](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>

[!INCLUDE [arm-getting-setup-powershell](../../includes/arm-getting-setup-powershell.md)]

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="9cf11-116">Tworzenie magazynu usługi Recovery Services</span><span class="sxs-lookup"><span data-stu-id="9cf11-116">Create a recovery services vault</span></span>
<span data-ttu-id="9cf11-117">następujące kroki Hello przeprowadzi Cię przez tworzenie magazynu usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="9cf11-117">hello following steps lead you through creating a Recovery Services vault.</span></span> <span data-ttu-id="9cf11-118">Magazyn usług odzyskiwania są inne niż magazynu kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="9cf11-118">A Recovery Services vault is different than a Backup vault.</span></span>

1. <span data-ttu-id="9cf11-119">Jeśli kopia zapasowa Azure jest używana do powitania po raz pierwszy, należy użyć hello **AzureRMResourceProvider rejestru** polecenia cmdlet tooregister hello Azure odzyskiwania usługodawcy w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="9cf11-119">If you are using Azure Backup for hello first time, you must use hello **Register-AzureRMResourceProvider** cmdlet tooregister hello Azure Recovery Service provider with your subscription.</span></span>

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. <span data-ttu-id="9cf11-120">Witaj magazyn usług odzyskiwania jest zasobu ARM, więc należy tooplace go w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="9cf11-120">hello Recovery Services vault is an ARM resource, so you need tooplace it within a Resource Group.</span></span> <span data-ttu-id="9cf11-121">Użyj istniejącej grupy zasobów lub Utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="9cf11-121">You can use an existing resource group, or create a new one.</span></span> <span data-ttu-id="9cf11-122">Podczas tworzenia nowej grupy zasobów, określ hello nazwy i lokalizacji hello grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="9cf11-122">When creating a new resource group, specify hello name and location for hello resource group.</span></span>  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "WestUS"
    ```
3. <span data-ttu-id="9cf11-123">Użyj hello **AzureRmRecoveryServicesVault nowy** nowy magazyn hello toocreate polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9cf11-123">Use hello **New-AzureRmRecoveryServicesVault** cmdlet toocreate hello new vault.</span></span> <span data-ttu-id="9cf11-124">Pamiętaj, toospecify hello tę samą lokalizację dla magazynu hello, które było używane dla grupy zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="9cf11-124">Be sure toospecify hello same location for hello vault as was used for hello resource group.</span></span>

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "WestUS"
    ```
4. <span data-ttu-id="9cf11-125">Określ typ hello toouse nadmiarowość magazynu; można użyć [lokalnie nadmiarowego magazynu (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) lub [z magazynu geograficznie nadmiarowego magazynu (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span><span class="sxs-lookup"><span data-stu-id="9cf11-125">Specify hello type of storage redundancy toouse; you can use [Locally Redundant Storage (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) or [Geo Redundant Storage (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span></span> <span data-ttu-id="9cf11-126">Witaj poniższy przykład przedstawia się, że opcja - BackupStorageRedundancy hello testVault ustawiono tooGeoRedundant.</span><span class="sxs-lookup"><span data-stu-id="9cf11-126">hello following example shows hello -BackupStorageRedundancy option for testVault is set tooGeoRedundant.</span></span>

   > [!TIP]
   > <span data-ttu-id="9cf11-127">Wiele poleceń cmdlet narzędzia Kopia zapasowa Azure wymaga obiektu magazynu usług odzyskiwania hello jako danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="9cf11-127">Many Azure Backup cmdlets require hello Recovery Services vault object as an input.</span></span> <span data-ttu-id="9cf11-128">Z tego powodu jest wygodne toostore hello usług odzyskiwania kopii zapasowej magazynu obiekt w zmiennej.</span><span class="sxs-lookup"><span data-stu-id="9cf11-128">For this reason, it is convenient toostore hello Backup Recovery Services vault object in a variable.</span></span>
   >
   >

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testVault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

## <a name="view-hello-vaults-in-a-subscription"></a><span data-ttu-id="9cf11-129">Widok hello magazynów w ramach subskrypcji</span><span class="sxs-lookup"><span data-stu-id="9cf11-129">View hello vaults in a subscription</span></span>
<span data-ttu-id="9cf11-130">Użyj **Get-AzureRmRecoveryServicesVault** tooview hello listę wszystkich magazynów w hello bieżącej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="9cf11-130">Use **Get-AzureRmRecoveryServicesVault** tooview hello list of all vaults in hello current subscription.</span></span> <span data-ttu-id="9cf11-131">Możesz użyć tego polecenia toocheck, utworzono nowy magazyn lub toosee magazynów, jakie są dostępne w hello subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="9cf11-131">You can use this command toocheck that a new  vault was created, or toosee what vaults are available in hello subscription.</span></span>

<span data-ttu-id="9cf11-132">Uruchom polecenie hello **Get-AzureRmRecoveryServicesVault**, i wszystkich magazynów w subskrypcji hello są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="9cf11-132">Run hello command, **Get-AzureRmRecoveryServicesVault**, and all vaults in hello subscription are listed.</span></span>

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


## <a name="installing-hello-azure-backup-agent"></a><span data-ttu-id="9cf11-133">Instalowanie agenta usługi Kopia zapasowa Azure hello</span><span class="sxs-lookup"><span data-stu-id="9cf11-133">Installing hello Azure Backup agent</span></span>
<span data-ttu-id="9cf11-134">Przed zainstalowaniem agenta usługi Kopia zapasowa Azure hello należy toohave hello Instalatora, pobranych i znajdują się na powitania serwera systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="9cf11-134">Before you install hello Azure Backup agent, you need toohave hello installer downloaded and present on hello Windows Server.</span></span> <span data-ttu-id="9cf11-135">Możesz pobrać najnowszą wersję Instalatora hello hello ze hello [Microsoft Download Center](http://aka.ms/azurebackup_agent) lub z magazynu usług odzyskiwania hello strony pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="9cf11-135">You can get hello latest version of hello installer from hello [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from hello Recovery Services vault's Dashboard page.</span></span> <span data-ttu-id="9cf11-136">Zapisz Instalator hello tooan łatwo dostępnej lokalizacji, takich jak * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="9cf11-136">Save hello installer tooan easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="9cf11-137">Alternatywnie można użyć narzędzia pobierania hello tooget środowiska PowerShell:</span><span class="sxs-lookup"><span data-stu-id="9cf11-137">Alternatively, use PowerShell tooget hello downloader:</span></span>
 
 ```
 $MarsAURL = 'Http://Aka.Ms/Azurebackup_Agent'
 $WC = New-Object System.Net.WebClient
 $WC.DownloadFile($MarsAURL,'C:\downloads\MARSAgentInstaller.EXE')
 C:\Downloads\MARSAgentInstaller.EXE /q
 ```

<span data-ttu-id="9cf11-138">tooinstall hello agenta, uruchom następujące polecenie w konsoli programu PowerShell z podwyższonym poziomem uprawnień hello:</span><span class="sxs-lookup"><span data-stu-id="9cf11-138">tooinstall hello agent, run hello following command in an elevated PowerShell console:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="9cf11-139">Spowoduje to zainstalowanie agenta hello z wszystkich opcji domyślnych hello.</span><span class="sxs-lookup"><span data-stu-id="9cf11-139">This installs hello agent with all hello default options.</span></span> <span data-ttu-id="9cf11-140">Instalacja Hello zajmuje kilka minut w tle hello.</span><span class="sxs-lookup"><span data-stu-id="9cf11-140">hello installation takes a few minutes in hello background.</span></span> <span data-ttu-id="9cf11-141">Jeśli nie określisz hello */nu* opcji, a następnie hello **usługi Windows Update** na końcu hello hello toocheck instalacji dla wszystkich aktualizacji, zostanie otwarte okno.</span><span class="sxs-lookup"><span data-stu-id="9cf11-141">If you do not specify hello */nu* option then hello **Windows Update** window will open at hello end of hello installation toocheck for any updates.</span></span> <span data-ttu-id="9cf11-142">Po zainstalowaniu agenta hello wyświetli hello listy zainstalowanych programów.</span><span class="sxs-lookup"><span data-stu-id="9cf11-142">Once installed, hello agent will show in hello list of installed programs.</span></span>

<span data-ttu-id="9cf11-143">toosee hello listy zainstalowanych programów, należy przejść za**Panelu sterowania** > **programy** > **programy i funkcje**.</span><span class="sxs-lookup"><span data-stu-id="9cf11-143">toosee hello list of installed programs, go too**Control Panel** > **Programs** > **Programs and Features**.</span></span>

![Agent został zainstalowany](./media/backup-client-automation/installed-agent-listing.png)

### <a name="installation-options"></a><span data-ttu-id="9cf11-145">Opcje instalacji</span><span class="sxs-lookup"><span data-stu-id="9cf11-145">Installation options</span></span>
<span data-ttu-id="9cf11-146">toosee, który hello wszystkie opcje dostępne za pośrednictwem hello wiersza polecenia, użyj następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="9cf11-146">toosee all hello options available via hello command-line, use hello following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="9cf11-147">Witaj dostępne opcje to:</span><span class="sxs-lookup"><span data-stu-id="9cf11-147">hello available options include:</span></span>

| <span data-ttu-id="9cf11-148">Opcja</span><span class="sxs-lookup"><span data-stu-id="9cf11-148">Option</span></span> | <span data-ttu-id="9cf11-149">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="9cf11-149">Details</span></span> | <span data-ttu-id="9cf11-150">Domyślne</span><span class="sxs-lookup"><span data-stu-id="9cf11-150">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9cf11-151">/q</span><span class="sxs-lookup"><span data-stu-id="9cf11-151">/q</span></span> |<span data-ttu-id="9cf11-152">Instalację cichą</span><span class="sxs-lookup"><span data-stu-id="9cf11-152">Quiet installation</span></span> |- |
| <span data-ttu-id="9cf11-153">/ p: "Lokalizacja"</span><span class="sxs-lookup"><span data-stu-id="9cf11-153">/p:"location"</span></span> |<span data-ttu-id="9cf11-154">Ścieżka folderu instalacji toohello hello Azure Backup Agent.</span><span class="sxs-lookup"><span data-stu-id="9cf11-154">Path toohello installation folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="9cf11-155">C:\Program Files\Microsoft Azure Recovery usługi agenta</span><span class="sxs-lookup"><span data-stu-id="9cf11-155">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="9cf11-156">/ s: "Lokalizacja"</span><span class="sxs-lookup"><span data-stu-id="9cf11-156">/s:"location"</span></span> |<span data-ttu-id="9cf11-157">Ścieżka folderu pamięci podręcznej toohello hello Azure Backup Agent.</span><span class="sxs-lookup"><span data-stu-id="9cf11-157">Path toohello cache folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="9cf11-158">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="9cf11-158">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="9cf11-159">/m</span><span class="sxs-lookup"><span data-stu-id="9cf11-159">/m</span></span> |<span data-ttu-id="9cf11-160">TooMicrosoft opcjonalnych aktualizacji</span><span class="sxs-lookup"><span data-stu-id="9cf11-160">Opt-in tooMicrosoft Update</span></span> |- |
| <span data-ttu-id="9cf11-161">/nu</span><span class="sxs-lookup"><span data-stu-id="9cf11-161">/nu</span></span> |<span data-ttu-id="9cf11-162">Nie sprawdzaj aktualizacji po ukończeniu instalacji</span><span class="sxs-lookup"><span data-stu-id="9cf11-162">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="9cf11-163">/d</span><span class="sxs-lookup"><span data-stu-id="9cf11-163">/d</span></span> |<span data-ttu-id="9cf11-164">Odinstalowuje agenta usług odzyskiwania Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="9cf11-164">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="9cf11-165">/pH</span><span class="sxs-lookup"><span data-stu-id="9cf11-165">/ph</span></span> |<span data-ttu-id="9cf11-166">Adres hosta serwera proxy</span><span class="sxs-lookup"><span data-stu-id="9cf11-166">Proxy Host Address</span></span> |- |
| <span data-ttu-id="9cf11-167">/Po</span><span class="sxs-lookup"><span data-stu-id="9cf11-167">/po</span></span> |<span data-ttu-id="9cf11-168">Numer portu hosta serwera proxy</span><span class="sxs-lookup"><span data-stu-id="9cf11-168">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="9cf11-169">/Pu</span><span class="sxs-lookup"><span data-stu-id="9cf11-169">/pu</span></span> |<span data-ttu-id="9cf11-170">Nazwa użytkownika serwera proxy hosta</span><span class="sxs-lookup"><span data-stu-id="9cf11-170">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="9cf11-171">/PW</span><span class="sxs-lookup"><span data-stu-id="9cf11-171">/pw</span></span> |<span data-ttu-id="9cf11-172">Hasło serwera proxy</span><span class="sxs-lookup"><span data-stu-id="9cf11-172">Proxy Password</span></span> |- |

## <a name="registering-windows-server-or-windows-client-machine-tooa-recovery-services-vault"></a><span data-ttu-id="9cf11-173">Rejestracja systemu Windows Server lub klienta systemu Windows w maszynie tooa magazynu usług odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="9cf11-173">Registering Windows Server or Windows client machine tooa Recovery Services Vault</span></span>
<span data-ttu-id="9cf11-174">Po utworzeniu magazynu usług odzyskiwania hello, Pobierz najnowszą wersję agenta hello i poświadczenia magazynu hello i zapisz go w dogodnym miejscu, podobnie jak C:\Downloads.</span><span class="sxs-lookup"><span data-stu-id="9cf11-174">After you created hello Recovery Services vault, download hello latest agent and hello vault credentials and store it in a convenient location like C:\Downloads.</span></span>

```
PS C:\> $credspath = "C:\downloads"
PS C:\> $credsfilename = Get-AzureRmRecoveryServicesVaultSettingsFile -Backup -Vault $vault1 -Path  $credspath
```

<span data-ttu-id="9cf11-175">Uruchom na powitania serwera systemu Windows lub komputera klienckiego z systemem Windows hello [Start OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) polecenia cmdlet tooregister hello maszyny z magazynem hello.</span><span class="sxs-lookup"><span data-stu-id="9cf11-175">On hello Windows Server or Windows client machine, run hello [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet tooregister hello machine with hello vault.</span></span>
<span data-ttu-id="9cf11-176">To i inne polecenia cmdlet używane do tworzenia kopii zapasowych, są z modułu MSONLINE hello które hello Mars AgentInstaller dodany jako część procesu instalacji hello.</span><span class="sxs-lookup"><span data-stu-id="9cf11-176">This, and other cmdlets used for backup, are from hello MSONLINE module which hello Mars AgentInstaller added as part of hello installation process.</span></span> 

<span data-ttu-id="9cf11-177">Witaj Instalatora agenta nie aktualizuje hello $Env: PSModulePath zmiennej.</span><span class="sxs-lookup"><span data-stu-id="9cf11-177">hello Agent installer does not update hello $Env:PSModulePath variable.</span></span> <span data-ttu-id="9cf11-178">Oznacza to, że automatyczne ładowanie modułu nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="9cf11-178">This means module auto-load fails.</span></span> <span data-ttu-id="9cf11-179">tooresolve to można wykonać następujące hello:</span><span class="sxs-lookup"><span data-stu-id="9cf11-179">tooresolve this you can do hello following:</span></span>

```
PS C:\>  $Env:psmodulepath += ';C:\Program Files\Microsoft Azure Recovery Services Agent\bin\Modules
```

<span data-ttu-id="9cf11-180">Alternatywnie można ręcznie załadować moduł hello w skrypcie w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="9cf11-180">Alternatively, you can manually load hello module in your script as follows:</span></span>

```
PS C:\>  Import-Module  'C:\Program Files\Microsoft Azure Recovery Services Agent\bin\Modules\MSOnlineBackup'

```

<span data-ttu-id="9cf11-181">Po załadowaniu hello poleceń cmdlet z kopii zapasowej Online, zarejestruj się poświadczenia magazynu hello:</span><span class="sxs-lookup"><span data-stu-id="9cf11-181">Once you load hello Online Backup cmdlets, you register hello vault credentials:</span></span>


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
> <span data-ttu-id="9cf11-182">Nie należy używać pliku poświadczeń magazynu hello toospecify ścieżek względnych.</span><span class="sxs-lookup"><span data-stu-id="9cf11-182">Do not use relative paths toospecify hello vault credentials file.</span></span> <span data-ttu-id="9cf11-183">Należy podać ścieżkę bezwzględną jako polecenia cmdlet toohello wejściowego.</span><span class="sxs-lookup"><span data-stu-id="9cf11-183">You must provide an absolute path as an input toohello cmdlet.</span></span>
>
>

## <a name="networking-settings"></a><span data-ttu-id="9cf11-184">Ustawienia sieciowe</span><span class="sxs-lookup"><span data-stu-id="9cf11-184">Networking settings</span></span>
<span data-ttu-id="9cf11-185">Gdy łączność hello hello systemu Windows maszyny toohello jest internet za pośrednictwem serwera proxy, ustawienia serwera proxy hello można również podać o toohello agenta.</span><span class="sxs-lookup"><span data-stu-id="9cf11-185">When hello connectivity of hello Windows machine toohello internet is through a proxy server, hello proxy settings can also be provided toohello agent.</span></span> <span data-ttu-id="9cf11-186">W tym przykładzie nie żadnego serwera proxy, dlatego firma Microsoft są jawnie wyczyszczenie żadnych informacji dotyczących serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="9cf11-186">In this example, there is no proxy server, so we are explicitly clearing any proxy-related information.</span></span>

<span data-ttu-id="9cf11-187">Wykorzystanie przepustowości można również sterować za pomocą opcji hello ```work hour bandwidth``` i ```non-work hour bandwidth``` dla danego zestawu dni tygodnia hello.</span><span class="sxs-lookup"><span data-stu-id="9cf11-187">Bandwidth usage can also be controlled with hello options of ```work hour bandwidth``` and ```non-work hour bandwidth``` for a given set of days of hello week.</span></span>

<span data-ttu-id="9cf11-188">Ustawienie szczegóły serwera proxy i przepustowości hello jest wykonywane przy użyciu hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="9cf11-188">Setting hello proxy and bandwidth details is done using hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) cmdlet:</span></span>

```
PS C:\> Set-OBMachineSetting -NoProxy
Server properties updated successfully.

PS C:\> Set-OBMachineSetting -NoThrottle
Server properties updated successfully.
```

## <a name="encryption-settings"></a><span data-ttu-id="9cf11-189">Ustawienia szyfrowania</span><span class="sxs-lookup"><span data-stu-id="9cf11-189">Encryption settings</span></span>
<span data-ttu-id="9cf11-190">tooAzure wysyłane dane kopii zapasowej Hello kopii zapasowej jest zaszyfrowany tooprotect hello poufność danych hello.</span><span class="sxs-lookup"><span data-stu-id="9cf11-190">hello backup data sent tooAzure Backup is encrypted tooprotect hello confidentiality of hello data.</span></span> <span data-ttu-id="9cf11-191">hasło szyfrowania Hello jest hello "password" toodecrypt hello danych w czasie hello przywracania.</span><span class="sxs-lookup"><span data-stu-id="9cf11-191">hello encryption passphrase is hello "password" toodecrypt hello data at hello time of restore.</span></span>

```
PS C:\> ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force | Set-OBMachineSetting
PS C:\> $PassPhrase = ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force 
PS C:\> $PassCode   = 'AzureR0ckx'
PS C:\> Set-OBMachineSetting -EncryptionPassPhrase $PassPhrase
Server properties updated successfully
```

> [!IMPORTANT]
> <span data-ttu-id="9cf11-192">Zachowaj informacje hasło hello bezpieczne po ustawieniu.</span><span class="sxs-lookup"><span data-stu-id="9cf11-192">Keep hello passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="9cf11-193">Są nie jest możliwe toorestore danych z platformy Azure bez tego hasła.</span><span class="sxs-lookup"><span data-stu-id="9cf11-193">You are not be able toorestore data from Azure without this passphrase.</span></span>
>
>

## <a name="back-up-files-and-folders"></a><span data-ttu-id="9cf11-194">Tworzenie kopii zapasowych plików i folderów</span><span class="sxs-lookup"><span data-stu-id="9cf11-194">Back up files and folders</span></span>
<span data-ttu-id="9cf11-195">Wszystkie kopie zapasowe z serwerów z systemem Windows i klientów tooAzure kopii zapasowej zarządzane przez zasady.</span><span class="sxs-lookup"><span data-stu-id="9cf11-195">All backups from Windows Servers and clients tooAzure Backup are governed by a policy.</span></span> <span data-ttu-id="9cf11-196">zasady Hello składa się z trzech części:</span><span class="sxs-lookup"><span data-stu-id="9cf11-196">hello policy comprises three parts:</span></span>

1. <span data-ttu-id="9cf11-197">A **harmonogram tworzenia kopii zapasowych** , który określa podczas tworzenia kopii zapasowych należy toobe podjęte, a następnie synchronizowane z usługą hello.</span><span class="sxs-lookup"><span data-stu-id="9cf11-197">A **backup schedule** that specifies when backups need toobe taken and synchronized with hello service.</span></span>
2. <span data-ttu-id="9cf11-198">A **harmonogramu przechowywania** Określa, jak długo punkty odzyskiwania hello tooretain na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="9cf11-198">A **retention schedule** that specifies how long tooretain hello recovery points in Azure.</span></span>
3. <span data-ttu-id="9cf11-199">A **określania włączenia/wyłączenia pliku** które nakazują, co należy utworzyć kopię.</span><span class="sxs-lookup"><span data-stu-id="9cf11-199">A **file inclusion/exclusion specification** that dictates what should be backed up.</span></span>

<span data-ttu-id="9cf11-200">W tym dokumencie ponieważ będziemy w przypadku automatyzacji kopii zapasowej, przyjęto będzie założenie, że nic nie skonfigurowano.</span><span class="sxs-lookup"><span data-stu-id="9cf11-200">In this document, since we're automating backup, we'll assume nothing has been configured.</span></span> <span data-ttu-id="9cf11-201">Zaczniemy przez utworzenie nowych zasad tworzenia kopii zapasowej przy użyciu hello [OBPolicy nowy](https://technet.microsoft.com/library/hh770416.aspx) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9cf11-201">We begin by creating a new backup policy using hello [New-OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) cmdlet.</span></span>

```
PS C:\> $newpolicy = New-OBPolicy
```

<span data-ttu-id="9cf11-202">W tym hello czasu zasady jest pusta i innych poleceń cmdlet są potrzebne toodefine jakie elementy zostaną uwzględnione lub wykluczone, gdy kopie zapasowe zostaną uruchomione i gdy hello kopie zapasowe będą przechowywane.</span><span class="sxs-lookup"><span data-stu-id="9cf11-202">At this time hello policy is empty and other cmdlets are needed toodefine what items will be included or excluded, when backups will run, and where hello backups will be stored.</span></span>

### <a name="configuring-hello-backup-schedule"></a><span data-ttu-id="9cf11-203">Konfigurowanie hello harmonogram tworzenia kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="9cf11-203">Configuring hello backup schedule</span></span>
<span data-ttu-id="9cf11-204">Witaj najpierw hello 3 części zasad jest harmonogram tworzenia kopii zapasowych hello, który został utworzony za pomocą hello [OBSchedule nowy](https://technet.microsoft.com/library/hh770401) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9cf11-204">hello first of hello 3 parts of a policy is hello backup schedule, which is created using hello [New-OBSchedule](https://technet.microsoft.com/library/hh770401) cmdlet.</span></span> <span data-ttu-id="9cf11-205">harmonogram tworzenia kopii zapasowych Hello definiuje, podczas tworzenia kopii zapasowych należy toobe podjęte.</span><span class="sxs-lookup"><span data-stu-id="9cf11-205">hello backup schedule defines when backups need toobe taken.</span></span> <span data-ttu-id="9cf11-206">Podczas tworzenia harmonogramu należy toospecify 2 parametry wejściowe:</span><span class="sxs-lookup"><span data-stu-id="9cf11-206">When creating a schedule you need toospecify 2 input parameters:</span></span>

* <span data-ttu-id="9cf11-207">**Dni tygodnia hello** hello kopii zapasowej powinno być ono uruchomione.</span><span class="sxs-lookup"><span data-stu-id="9cf11-207">**Days of hello week** that hello backup should run.</span></span> <span data-ttu-id="9cf11-208">Można uruchomić zadanie tworzenia kopii zapasowej hello na tylko jeden dzień lub każdego dnia tygodnia hello lub dowolną kombinację między.</span><span class="sxs-lookup"><span data-stu-id="9cf11-208">You can run hello backup job on just one day, or every day of hello week, or any combination in between.</span></span>
* <span data-ttu-id="9cf11-209">**Pór dnia hello** uruchomienia hello kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="9cf11-209">**Times of hello day** when hello backup should run.</span></span> <span data-ttu-id="9cf11-210">Można zdefiniować się too3 różnych porach dnia hello, gdy zostanie wywołane hello kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="9cf11-210">You can define up too3 different times of hello day when hello backup will be triggered.</span></span>

<span data-ttu-id="9cf11-211">Na przykład można skonfigurować zasad tworzenia kopii zapasowej, wykonywany o 16: 00 w każdą sobotę i niedziela.</span><span class="sxs-lookup"><span data-stu-id="9cf11-211">For instance, you could configure a backup policy that runs at 4PM every Saturday and Sunday.</span></span>

```
PS C:\> $sched = New-OBSchedule -DaysofWeek Saturday, Sunday -TimesofDay 16:00
```

<span data-ttu-id="9cf11-212">harmonogram tworzenia kopii zapasowych Hello musi toobe skojarzonej z zasadami i można to osiągnąć przy użyciu hello [OBSchedule zestaw](https://technet.microsoft.com/library/hh770407) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9cf11-212">hello backup schedule needs toobe associated with a policy, and this can be achieved by using hello [Set-OBSchedule](https://technet.microsoft.com/library/hh770407) cmdlet.</span></span>

```
PS C:> Set-OBSchedule -Policy $newpolicy -Schedule $sched
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s) DsList : PolicyName : RetentionPolicy : State : New PolicyState : Valid
```
### <a name="configuring-a-retention-policy"></a><span data-ttu-id="9cf11-213">Konfigurowania zasad przechowywania</span><span class="sxs-lookup"><span data-stu-id="9cf11-213">Configuring a retention policy</span></span>
<span data-ttu-id="9cf11-214">zasady przechowywania Hello definiuje czas odzyskiwania, punkty utworzone na podstawie zadania tworzenia kopii zapasowej zostaną zachowane.</span><span class="sxs-lookup"><span data-stu-id="9cf11-214">hello retention policy defines how long recovery points created from backup jobs are retained.</span></span> <span data-ttu-id="9cf11-215">Podczas tworzenia nowych zasad przechowywania przy użyciu hello [OBRetentionPolicy nowy](https://technet.microsoft.com/library/hh770425) polecenia cmdlet, można określić hello liczbę dni, które hello punktów odzyskiwania należy toobe przechowywane w usłudze Kopia zapasowa Azure.</span><span class="sxs-lookup"><span data-stu-id="9cf11-215">When creating a new retention policy using hello [New-OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) cmdlet, you can specify hello number of days that hello backup recovery points need toobe retained with Azure Backup.</span></span> <span data-ttu-id="9cf11-216">w poniższym przykładzie Hello ustawia zasady przechowywania wynosi 7 dni.</span><span class="sxs-lookup"><span data-stu-id="9cf11-216">hello example below sets a retention policy of 7 days.</span></span>

```
PS C:\> $retentionpolicy = New-OBRetentionPolicy -RetentionDays 7
```

<span data-ttu-id="9cf11-217">Witaj zasady przechowywania muszą być skojarzone z zasadami głównego hello przy użyciu polecenia cmdlet hello [OBRetentionPolicy zestaw](https://technet.microsoft.com/library/hh770405):</span><span class="sxs-lookup"><span data-stu-id="9cf11-217">hello retention policy must be associated with hello main policy using hello cmdlet [Set-OBRetentionPolicy](https://technet.microsoft.com/library/hh770405):</span></span>

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
### <a name="including-and-excluding-files-toobe-backed-up"></a><span data-ttu-id="9cf11-218">Włączanie i wyłączanie toobe pliki kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="9cf11-218">Including and excluding files toobe backed up</span></span>
<span data-ttu-id="9cf11-219">```OBFileSpec``` Obiekt definiuje hello pliki toobe dołączone i wykluczone w kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="9cf11-219">An ```OBFileSpec``` object defines hello files toobe included and excluded in a backup.</span></span> <span data-ttu-id="9cf11-220">Jest to zestaw reguł, że zakres limit hello chronione pliki i foldery na komputerze.</span><span class="sxs-lookup"><span data-stu-id="9cf11-220">This is a set of rules that scope out hello protected files and folders on a machine.</span></span> <span data-ttu-id="9cf11-221">Może mieć wiele pliku reguł dołączania lub wykluczania zgodnie z wymaganiami i skojarzyć je z zasadami.</span><span class="sxs-lookup"><span data-stu-id="9cf11-221">You can have as many file inclusion or exclusion rules as required, and associate them with a policy.</span></span> <span data-ttu-id="9cf11-222">Tworząc nowy obiekt OBFileSpec, można:</span><span class="sxs-lookup"><span data-stu-id="9cf11-222">When creating a new OBFileSpec object, you can:</span></span>

* <span data-ttu-id="9cf11-223">Określ toobe pliki i foldery hello włączone</span><span class="sxs-lookup"><span data-stu-id="9cf11-223">Specify hello files and folders toobe included</span></span>
* <span data-ttu-id="9cf11-224">Określ toobe pliki i foldery hello wyłączone</span><span class="sxs-lookup"><span data-stu-id="9cf11-224">Specify hello files and folders toobe excluded</span></span>
* <span data-ttu-id="9cf11-225">Określ rekursywne tworzenie kopii zapasowych danych w folderze (lub) czy tylko hello pliki najwyższego poziomu w określonym folderze hello należy utworzyć kopię zapasową.</span><span class="sxs-lookup"><span data-stu-id="9cf11-225">Specify recursive backup of data in a folder (or) whether only hello top-level files in hello specified folder should be backed up.</span></span>

<span data-ttu-id="9cf11-226">ostatnie Hello odbywa się przy użyciu flagi - Nierekurencyjny hello w poleceniu hello OBFileSpec nowy.</span><span class="sxs-lookup"><span data-stu-id="9cf11-226">hello latter is achieved by using hello -NonRecursive flag in hello New-OBFileSpec command.</span></span>

<span data-ttu-id="9cf11-227">W poniższym przykładzie hello możemy utworzyć kopię zapasową woluminu, C: i D: i wykluczanie plików binarnych systemu operacyjnego hello w folderze systemu Windows hello i foldery tymczasowe.</span><span class="sxs-lookup"><span data-stu-id="9cf11-227">In hello example below, we'll back up volume C: and D: and exclude hello OS binaries in hello Windows folder and any temporary folders.</span></span> <span data-ttu-id="9cf11-228">toodo, utworzymy dwa specyfikacji pliku przy użyciu hello [OBFileSpec nowy](https://technet.microsoft.com/library/hh770408) polecenia cmdlet — jeden dla dołączania i jeden do wykluczenia.</span><span class="sxs-lookup"><span data-stu-id="9cf11-228">toodo so we'll create two file specifications using hello [New-OBFileSpec](https://technet.microsoft.com/library/hh770408) cmdlet - one for inclusion and one for exclusion.</span></span> <span data-ttu-id="9cf11-229">Po utworzeniu specyfikacji pliku hello są powiązane z zasadami hello przy użyciu hello [OBFileSpec Dodaj](https://technet.microsoft.com/library/hh770424) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9cf11-229">Once hello file specifications have been created, they're associated with hello policy using hello [Add-OBFileSpec](https://technet.microsoft.com/library/hh770424) cmdlet.</span></span>

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

### <a name="applying-hello-policy"></a><span data-ttu-id="9cf11-230">Zastosowanie zasad hello</span><span class="sxs-lookup"><span data-stu-id="9cf11-230">Applying hello policy</span></span>
<span data-ttu-id="9cf11-231">Teraz hello obiektu zasad została zakończona i ma skojarzone harmonogram tworzenia kopii zapasowych, zasad przechowywania i włączenia/wyłączenia lista plików.</span><span class="sxs-lookup"><span data-stu-id="9cf11-231">Now hello policy object is complete and has an associated backup schedule, retention policy, and an inclusion/exclusion list of files.</span></span> <span data-ttu-id="9cf11-232">Te zasady można teraz zatwierdzone dla toouse kopia zapasowa Azure.</span><span class="sxs-lookup"><span data-stu-id="9cf11-232">This policy can now be committed for Azure Backup toouse.</span></span> <span data-ttu-id="9cf11-233">Przed zastosowaniem hello nowo utworzone zasady upewnij się, że nie ma żadnych istniejących zasad tworzenia kopii zapasowej skojarzonego z serwerem hello przy użyciu hello [OBPolicy Usuń](https://technet.microsoft.com/library/hh770415) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9cf11-233">Before you apply hello newly created policy ensure that there are no existing backup policies associated with hello server by using hello [Remove-OBPolicy](https://technet.microsoft.com/library/hh770415) cmdlet.</span></span> <span data-ttu-id="9cf11-234">Usuwanie zasad hello wyświetli monit o potwierdzenie.</span><span class="sxs-lookup"><span data-stu-id="9cf11-234">Removing hello policy will prompt for confirmation.</span></span> <span data-ttu-id="9cf11-235">Potwierdzenie hello tooskip Użyj hello ```-Confirm:$false``` flagę hello polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9cf11-235">tooskip hello confirmation use hello ```-Confirm:$false``` flag with hello cmdlet.</span></span>

```
PS C:> Get-OBPolicy | Remove-OBPolicy
Microsoft Azure Backup Are you sure you want tooremove this backup policy? This will delete all hello backed up data. [Y] Yes [A] Yes tooAll [N] No [L] No tooAll [S] Suspend [?] Help (default is "Y"):
```

<span data-ttu-id="9cf11-236">Przekazywanie obiektu zasad hello jest wykonywane przy użyciu hello [OBPolicy zestaw](https://technet.microsoft.com/library/hh770421) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9cf11-236">Committing hello policy object is done using hello [Set-OBPolicy](https://technet.microsoft.com/library/hh770421) cmdlet.</span></span> <span data-ttu-id="9cf11-237">Spowoduje to również monituje o potwierdzenie.</span><span class="sxs-lookup"><span data-stu-id="9cf11-237">This will also ask for confirmation.</span></span> <span data-ttu-id="9cf11-238">Potwierdzenie hello tooskip Użyj hello ```-Confirm:$false``` flagę hello polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9cf11-238">tooskip hello confirmation use hello ```-Confirm:$false``` flag with hello cmdlet.</span></span>

```
PS C:> Set-OBPolicy -Policy $newpolicy
Microsoft Azure Backup Do you want toosave this backup policy ? [Y] Yes [A] Yes tooAll [N] No [L] No tooAll [S] Suspend [?] Help (default is "Y"):
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

<span data-ttu-id="9cf11-239">Możesz wyświetlić szczegóły hello hello istniejących zasad tworzenia kopii zapasowej przy użyciu hello [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9cf11-239">You can view hello details of hello existing backup policy using hello [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) cmdlet.</span></span> <span data-ttu-id="9cf11-240">Użytkownik może przejść za pomocą hello [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) polecenia cmdlet hello harmonogram tworzenia kopii zapasowych i hello [Get-OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) polecenia cmdlet dla zasad przechowywania hello</span><span class="sxs-lookup"><span data-stu-id="9cf11-240">You can drill-down further using hello [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) cmdlet for hello backup schedule and hello [Get-OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) cmdlet for hello retention policies</span></span>

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

### <a name="performing-an-ad-hoc-backup"></a><span data-ttu-id="9cf11-241">Wykonywanie kopii zapasowych ad hoc</span><span class="sxs-lookup"><span data-stu-id="9cf11-241">Performing an ad-hoc backup</span></span>
<span data-ttu-id="9cf11-242">Po ustawieniu zasad tworzenia kopii zapasowej hello kopii zapasowych zostanie przeprowadzona na powitania harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="9cf11-242">Once a backup policy has been set hello backups will occur per hello schedule.</span></span> <span data-ttu-id="9cf11-243">Wyzwolenie kopii zapasowych ad hoc jest także możliwe przy użyciu hello [Start OBBackup](https://technet.microsoft.com/library/hh770426) polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="9cf11-243">Triggering an ad-hoc backup is also possible using hello [Start-OBBackup](https://technet.microsoft.com/library/hh770426) cmdlet:</span></span>

```
PS C:> Get-OBPolicy | Start-OBBackup
Initializing
Taking snapshot of volumes...
Preparing storage...
Generating backup metadata information and preparing hello metadata VHD...
Data transfer is in progress. It might take longer since it is hello first backup and all data needs toobe transferred...
Data transfer completed and all backed up data is in hello cloud. Verifying data integrity...
Data transfer completed
In progress...
Job completed.
hello backup operation completed successfully.
```

## <a name="restore-data-from-azure-backup"></a><span data-ttu-id="9cf11-244">Przywróć dane z usługi Kopia zapasowa Azure</span><span class="sxs-lookup"><span data-stu-id="9cf11-244">Restore data from Azure Backup</span></span>
<span data-ttu-id="9cf11-245">W tej sekcji przedstawiono kroki hello do automatyzacji odzyskiwanie danych z kopii zapasowej Azure.</span><span class="sxs-lookup"><span data-stu-id="9cf11-245">This section will guide you through hello steps for automating recovery of data from Azure Backup.</span></span> <span data-ttu-id="9cf11-246">Spowoduje to obejmuje hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="9cf11-246">Doing so involves hello following steps:</span></span>

1. <span data-ttu-id="9cf11-247">Wybierz wolumin źródłowy hello</span><span class="sxs-lookup"><span data-stu-id="9cf11-247">Pick hello source volume</span></span>
2. <span data-ttu-id="9cf11-248">Wybierz opcję tworzenia kopii zapasowej toorestore punktu</span><span class="sxs-lookup"><span data-stu-id="9cf11-248">Choose a backup point toorestore</span></span>
3. <span data-ttu-id="9cf11-249">Wybierz element toorestore</span><span class="sxs-lookup"><span data-stu-id="9cf11-249">Choose an item toorestore</span></span>
4. <span data-ttu-id="9cf11-250">Proces przywracania hello wyzwalacza</span><span class="sxs-lookup"><span data-stu-id="9cf11-250">Trigger hello restore process</span></span>

### <a name="picking-hello-source-volume"></a><span data-ttu-id="9cf11-251">Wolumin źródła hello pobrania</span><span class="sxs-lookup"><span data-stu-id="9cf11-251">Picking hello source volume</span></span>
<span data-ttu-id="9cf11-252">W kolejności toorestore element z kopii zapasowej Azure najpierw tooidentify hello źródła elementu hello.</span><span class="sxs-lookup"><span data-stu-id="9cf11-252">In order toorestore an item from Azure Backup, you first need tooidentify hello source of hello item.</span></span> <span data-ttu-id="9cf11-253">Ponieważ firma Microsoft jest wykonywania poleceń hello w kontekście systemu Windows Server lub klienta systemu Windows hello, jest już zidentyfikowany hello maszyny.</span><span class="sxs-lookup"><span data-stu-id="9cf11-253">Since we're executing hello commands in hello context of a Windows Server or a Windows client, hello machine is already identified.</span></span> <span data-ttu-id="9cf11-254">następnym krokiem Hello w identyfikacji źródła hello jest tooidentify hello woluminu zawierającego go.</span><span class="sxs-lookup"><span data-stu-id="9cf11-254">hello next step in identifying hello source is tooidentify hello volume containing it.</span></span> <span data-ttu-id="9cf11-255">Listę woluminów lub źródła Trwa wykonywanie kopii zapasowej z tego komputera mogą być pobierane, wykonując hello [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9cf11-255">A list of volumes or sources being backed up from this machine can be retrieved by executing hello [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) cmdlet.</span></span> <span data-ttu-id="9cf11-256">To polecenie zwraca tablicę wszystkich źródeł hello kopii zapasowej z serwera/klienta.</span><span class="sxs-lookup"><span data-stu-id="9cf11-256">This command returns an array of all hello sources backed up from this server/client.</span></span>

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

### <a name="choosing-a-backup-point-from-which-toorestore"></a><span data-ttu-id="9cf11-257">Wybieranie punktu kopii zapasowej, z których toorestore</span><span class="sxs-lookup"><span data-stu-id="9cf11-257">Choosing a backup point from which toorestore</span></span>
<span data-ttu-id="9cf11-258">Pobieranie listy punktów kopii zapasowej, wykonując hello [Get OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) polecenie cmdlet z odpowiednimi parametrami.</span><span class="sxs-lookup"><span data-stu-id="9cf11-258">You retreive a list of backup points by executing hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet with appropriate parameters.</span></span> <span data-ttu-id="9cf11-259">W naszym przykładzie wybrano hello najnowszego punktu kopii zapasowej dla woluminu źródłowego hello *D:* i korzystać z niego toorecover określonego pliku.</span><span class="sxs-lookup"><span data-stu-id="9cf11-259">In our example, we’ll choose hello latest backup point for hello source volume *D:* and use it toorecover a specific file.</span></span>

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
<span data-ttu-id="9cf11-260">Obiekt Hello ```$rps``` jest tablicą punktów kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="9cf11-260">hello object ```$rps``` is an array of backup points.</span></span> <span data-ttu-id="9cf11-261">pierwszy element Hello jest hello najnowszy punkt i hello n-tego elementu jest hello starsze punkty.</span><span class="sxs-lookup"><span data-stu-id="9cf11-261">hello first element is hello latest point and hello Nth element is hello oldest point.</span></span> <span data-ttu-id="9cf11-262">używamy toochoose hello najnowszy punkt ```$rps[0]```.</span><span class="sxs-lookup"><span data-stu-id="9cf11-262">toochoose hello latest point, we will use ```$rps[0]```.</span></span>

### <a name="choosing-an-item-toorestore"></a><span data-ttu-id="9cf11-263">Wybieranie toorestore elementu</span><span class="sxs-lookup"><span data-stu-id="9cf11-263">Choosing an item toorestore</span></span>
<span data-ttu-id="9cf11-264">tooidentify hello plików lub folder toorestore rekursywnie Użyj hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9cf11-264">tooidentify hello exact file or folder toorestore, recursively use hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet.</span></span> <span data-ttu-id="9cf11-265">Hierarchia folderów hello ten sposób można przeglądać wyłącznie przy użyciu hello ```Get-OBRecoverableItem```.</span><span class="sxs-lookup"><span data-stu-id="9cf11-265">That way hello folder hierarchy can be browsed solely using hello ```Get-OBRecoverableItem```.</span></span>

<span data-ttu-id="9cf11-266">W tym przykładzie, jeśli chcemy pliku hello toorestore *finances.xls* firma Microsoft może odwoływać się przy użyciu tego obiektu hello ```$filesFolders[1]```.</span><span class="sxs-lookup"><span data-stu-id="9cf11-266">In this example, if we want toorestore hello file *finances.xls* we can reference that using hello object ```$filesFolders[1]```.</span></span>

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

<span data-ttu-id="9cf11-267">Możesz również wyszukać toorestore elementów przy użyciu hello ```Get-OBRecoverableItem``` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9cf11-267">You can also search for items toorestore using hello ```Get-OBRecoverableItem``` cmdlet.</span></span> <span data-ttu-id="9cf11-268">W naszym przykładzie toosearch dla *finances.xls* firma Microsoft można uzyskać dojścia do pliku hello, uruchamiając polecenie:</span><span class="sxs-lookup"><span data-stu-id="9cf11-268">In our example, toosearch for *finances.xls* we could get a handle on hello file by running this command:</span></span>

```
PS C:\> $item = Get-OBRecoverableItem -RecoveryPoint $rps[0] -Location "D:\MyData" -SearchString "finance*"
```

### <a name="triggering-hello-restore-process"></a><span data-ttu-id="9cf11-269">Wyzwolenie procesu przywracania hello</span><span class="sxs-lookup"><span data-stu-id="9cf11-269">Triggering hello restore process</span></span>
<span data-ttu-id="9cf11-270">proces przywracania hello tootrigger, najpierw musisz opcje odzyskiwania hello toospecify.</span><span class="sxs-lookup"><span data-stu-id="9cf11-270">tootrigger hello restore process, we first need toospecify hello recovery options.</span></span> <span data-ttu-id="9cf11-271">Można to zrobić za pomocą hello [OBRecoveryOption nowy](https://technet.microsoft.com/library/hh770417.aspx) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9cf11-271">This can be done by using hello [New-OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) cmdlet.</span></span> <span data-ttu-id="9cf11-272">Na przykład załóżmy, że czy zbyt chcemy pliki hello toorestore*C:\temp*. Umożliwia również założono, że chcemy tooskip pliki, które już istnieją w folderze docelowym hello *C:\temp*. toocreate takie opcję odzyskiwania, użyj hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="9cf11-272">For this example, let's assume that we want toorestore hello files too*C:\temp*. Let's also assume that we want tooskip files that already exist on hello destination folder *C:\temp*. toocreate such a recovery option, use hello following command:</span></span>

```
PS C:\> $recovery_option = New-OBRecoveryOption -DestinationPath "C:\temp" -OverwriteType Skip
```

<span data-ttu-id="9cf11-273">Teraz uruchomić proces przywracania hello, używając hello [Start OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) na powitania wybrane ```$item``` z danych wyjściowych hello hello ```Get-OBRecoverableItem``` polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="9cf11-273">Now trigger hello restore process by using hello [Start-OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) command on hello selected ```$item``` from hello output of hello ```Get-OBRecoverableItem``` cmdlet:</span></span>

```
PS C:\> Start-OBRecovery -RecoverableItem $item -RecoveryOption $recover_option
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Job completed.
hello recovery operation completed successfully.
```


## <a name="uninstalling-hello-azure-backup-agent"></a><span data-ttu-id="9cf11-274">Odinstalowanie agenta usługi Kopia zapasowa Azure hello</span><span class="sxs-lookup"><span data-stu-id="9cf11-274">Uninstalling hello Azure Backup agent</span></span>
<span data-ttu-id="9cf11-275">Odinstalowanie agenta usługi Kopia zapasowa Azure hello może odbywać się przy użyciu hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="9cf11-275">Uninstalling hello Azure Backup agent can be done by using hello following command:</span></span>

```
PS C:\> .\MARSAgentInstaller.exe /d /q
```

<span data-ttu-id="9cf11-276">Odinstalowywanie pliki binarne agenta hello z maszyny hello ma niektórych tooconsider konsekwencje:</span><span class="sxs-lookup"><span data-stu-id="9cf11-276">Uninstalling hello agent binaries from hello machine has some consequences tooconsider:</span></span>

* <span data-ttu-id="9cf11-277">Usuwa filtr plików hello z hello maszyny i śledzenie zmian jest zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="9cf11-277">It removes hello file-filter from hello machine, and tracking of changes is stopped.</span></span>
* <span data-ttu-id="9cf11-278">Wszystkie informacje o zasadach zostanie usunięty z maszyny hello, ale informacje o zasadach hello nadal toobe przechowywany w usłudze hello.</span><span class="sxs-lookup"><span data-stu-id="9cf11-278">All policy information is removed from hello machine, but hello policy information continues toobe stored in hello service.</span></span>
* <span data-ttu-id="9cf11-279">Wszystkie harmonogramy tworzenia kopii zapasowej są usuwane i są pobierane nie dalsze kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="9cf11-279">All backup schedules are removed, and no further backups are taken.</span></span>

<span data-ttu-id="9cf11-280">Jednak hello dane przechowywane w pozostaje Azure i są przechowywane zgodnie z ustawień zasad przechowywania hello przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9cf11-280">However, hello data stored in Azure remains and is retained as per hello retention policy setup by you.</span></span> <span data-ttu-id="9cf11-281">Starsze punkty automatycznie są przestarzałe.</span><span class="sxs-lookup"><span data-stu-id="9cf11-281">Older points are automatically aged out.</span></span>

## <a name="remote-management"></a><span data-ttu-id="9cf11-282">Zdalne zarządzanie</span><span class="sxs-lookup"><span data-stu-id="9cf11-282">Remote management</span></span>
<span data-ttu-id="9cf11-283">Całe Zarządzanie hello wokół hello agenta usługi Kopia zapasowa Azure, zasady i źródłami danych mogą to robić zdalnie za pomocą programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9cf11-283">All hello management around hello Azure Backup agent, policies, and data sources can be done remotely through PowerShell.</span></span> <span data-ttu-id="9cf11-284">Witaj maszyny, który będzie zarządzany zdalnie musi toobe poprawnie przygotowany.</span><span class="sxs-lookup"><span data-stu-id="9cf11-284">hello machine that will be managed remotely needs toobe prepared correctly.</span></span>

<span data-ttu-id="9cf11-285">Domyślnie program hello Usługa WinRM jest skonfigurowany do uruchamiania ręcznego.</span><span class="sxs-lookup"><span data-stu-id="9cf11-285">By default, hello WinRM service is configured for manual startup.</span></span> <span data-ttu-id="9cf11-286">musi być zbyt ustawionym typem uruchomienia Hello*automatyczne* i hello usługi powinny być uruchamiane.</span><span class="sxs-lookup"><span data-stu-id="9cf11-286">hello startup type must be set too*Automatic* and hello service should be started.</span></span> <span data-ttu-id="9cf11-287">tooverify, który hello Usługa WinRM jest uruchomiona, musi mieć wartość hello hello właściwość stanu *systemem*.</span><span class="sxs-lookup"><span data-stu-id="9cf11-287">tooverify that hello WinRM service is running, hello value of hello Status property should be *Running*.</span></span>

```
PS C:\> Get-Service WinRM

Status   Name               DisplayName
------   ----               -----------
Running  winrm              Windows Remote Management (WS-Manag...
```

<span data-ttu-id="9cf11-288">Programu PowerShell, należy skonfigurować dla niego komunikację zdalną.</span><span class="sxs-lookup"><span data-stu-id="9cf11-288">PowerShell should be configured for remoting.</span></span>

```
PS C:\> Enable-PSRemoting -force
WinRM is already set up tooreceive requests on this computer.
WinRM has been updated for remote management.
WinRM firewall exception enabled.

PS C:\> Set-ExecutionPolicy unrestricted -force
```

<span data-ttu-id="9cf11-289">maszyny Hello teraz można zarządzać zdalnie — począwszy od instalacji hello hello agenta.</span><span class="sxs-lookup"><span data-stu-id="9cf11-289">hello machine can now be managed remotely - starting from hello installation of hello agent.</span></span> <span data-ttu-id="9cf11-290">Na przykład hello następującego skryptu kopiuje hello maszyny zdalnej toohello agenta i instaluje je.</span><span class="sxs-lookup"><span data-stu-id="9cf11-290">For example, hello following script copies hello agent toohello remote machine and installs it.</span></span>

```
PS C:\> $dloc = "\\REMOTESERVER01\c$\Windows\Temp"
PS C:\> $agent = "\\REMOTESERVER01\c$\Windows\Temp\MARSAgentInstaller.exe"
PS C:\> $args = "/q"
PS C:\> Copy-Item "C:\Downloads\MARSAgentInstaller.exe" -Destination $dloc - force

PS C:\> $s = New-PSSession -ComputerName REMOTESERVER01
PS C:\> Invoke-Command -Session $s -Script { param($d, $a) Start-Process -FilePath $d $a -Wait } -ArgumentList $agent $args
```

## <a name="next-steps"></a><span data-ttu-id="9cf11-291">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9cf11-291">Next steps</span></span>
<span data-ttu-id="9cf11-292">Aby uzyskać więcej informacji o kopii zapasowej dla systemu Windows Server/klienta Azure, zobacz</span><span class="sxs-lookup"><span data-stu-id="9cf11-292">For more information about Azure Backup for Windows Server/Client see</span></span>

* [<span data-ttu-id="9cf11-293">Wprowadzenie tooAzure kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="9cf11-293">Introduction tooAzure Backup</span></span>](backup-introduction-to-azure-backup.md)
* [<span data-ttu-id="9cf11-294">Wykonaj kopię zapasową serwerów z systemem Windows</span><span class="sxs-lookup"><span data-stu-id="9cf11-294">Back up Windows Servers</span></span>](backup-configure-vault.md)
