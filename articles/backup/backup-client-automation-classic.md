---
title: kopie zapasowe systemu Windows Server toomanage PowerShell aaaUse na platformie Azure | Dokumentacja firmy Microsoft
description: "Wdrażanie i zarządzanie kopiami zapasowymi systemu Windows Server przy użyciu programu PowerShell."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: e7e269e2-1f11-41a9-957b-a2155de6a1e0
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: saurse;markgal;nkolli;trinadhk
ms.openlocfilehash: 72292e510b0f059102440bd49a195be4ef700a6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-backup-tooazure-for-windows-serverwindows-client-using-powershell"></a><span data-ttu-id="89185-103">Wdrażanie i zarządzanie nimi tooAzure kopii zapasowej dla klienta systemu Windows i serwera systemu Windows przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="89185-103">Deploy and manage backup tooAzure for Windows Server/Windows Client using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="89185-104">ARM</span><span class="sxs-lookup"><span data-stu-id="89185-104">ARM</span></span>](backup-client-automation.md)
> * [<span data-ttu-id="89185-105">Wdrożenie klasyczne</span><span class="sxs-lookup"><span data-stu-id="89185-105">Classic</span></span>](backup-client-automation-classic.md)
>
>

<span data-ttu-id="89185-106">W tym artykule opisano, jak magazynu kopii zapasowej na toouse tooback programu PowerShell systemu Windows Server lub tooa danych stacji roboczej systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="89185-106">This article explains how toouse PowerShell tooback up Windows Server or Windows workstation data tooa backup vault.</span></span> <span data-ttu-id="89185-107">Firma Microsoft zaleca używanie Magazyny usług odzyskiwania dla wszystkich nowych wdrożeń.</span><span class="sxs-lookup"><span data-stu-id="89185-107">Microsoft recommends using Recovery Services vaults for all new deployments.</span></span> <span data-ttu-id="89185-108">Jeśli dla nowych użytkowników kopia zapasowa Azure i nie został utworzony magazyn kopii zapasowych w ramach subskrypcji, użyj hello artykułu, [wdrażania i zarządzania nimi przy użyciu programu PowerShell tooAzure danych programu Data Protection Manager](backup-client-automation.md) , dane są przechowywane w magazynie usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="89185-108">If you are a new Azure Backup user and have not created a backup vault in your subscription, use hello article, [Deploy and manage Data Protection Manager data tooAzure using PowerShell](backup-client-automation.md) so you store your data in a Recovery Services vault.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="89185-109">Teraz można uaktualnić Twoje Magazyny usług tooRecovery magazynów kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="89185-109">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="89185-110">Aby uzyskać więcej informacji, zobacz artykuł hello [uaktualnienia tooa magazynu kopii zapasowej, Magazyn usług odzyskiwania i](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="89185-110">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="89185-111">Firma Microsoft zachęca tooupgrade Magazyny usług tooRecovery magazyny kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="89185-111">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="89185-112">Po 15 października 2017 nie można użyć magazyny kopii zapasowych toocreate środowiska PowerShell.</span><span class="sxs-lookup"><span data-stu-id="89185-112">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="89185-113">**Do 1 listopada 2017 r.**:</span><span class="sxs-lookup"><span data-stu-id="89185-113">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="89185-114">Wszystkie pozostałe magazyny kopii zapasowych zostanie automatycznie uaktualniony tooRecovery Magazyny usług.</span><span class="sxs-lookup"><span data-stu-id="89185-114">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="89185-115">Użytkownik nie będzie możliwe tooaccess danych kopii zapasowych w portalu klasycznym hello.</span><span class="sxs-lookup"><span data-stu-id="89185-115">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="89185-116">Zamiast tego użyj hello Azure tooaccess portalu tej kopii zapasowej w Magazyny usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="89185-116">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

## <a name="install-azure-powershell"></a><span data-ttu-id="89185-117">Instalowanie programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="89185-117">Install Azure PowerShell</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="89185-118">Października 2015 Azure PowerShell 1.0 został wydany.</span><span class="sxs-lookup"><span data-stu-id="89185-118">In October 2015, Azure PowerShell 1.0 was released.</span></span> <span data-ttu-id="89185-119">Ta wersja zakończyło się pomyślnie wersji hello 0.9.8 i temat istotne zmiany, szczególnie w hello wzorzec nazewnictwa hello poleceń cmdlet.</span><span class="sxs-lookup"><span data-stu-id="89185-119">This release succeeded hello 0.9.8 release and brought about some significant changes, especially in hello naming pattern of hello cmdlets.</span></span> <span data-ttu-id="89185-120">Wykonaj polecenia cmdlet 1.0 hello wzorzec nazewnictwa {czasownik}-AzureRm {rzeczownik}; natomiast nie dołączaj nazwy hello 0.9.8 **Rm** (na przykład, New-AzureRmResourceGroup zamiast New-AzureResourceGroup).</span><span class="sxs-lookup"><span data-stu-id="89185-120">1.0 cmdlets follow hello naming pattern {verb}-AzureRm{noun}; whereas, hello 0.9.8 names do not include **Rm** (for example, New-AzureRmResourceGroup instead of New-AzureResourceGroup).</span></span> <span data-ttu-id="89185-121">Podczas korzystania z programu Azure PowerShell 0.9.8, należy najpierw włączyć tryb Resource Manager hello, uruchamiając hello **Switch-AzureMode AzureResourceManager** polecenia.</span><span class="sxs-lookup"><span data-stu-id="89185-121">When using Azure PowerShell 0.9.8, you must first enable hello Resource Manager mode by running hello **Switch-AzureMode AzureResourceManager** command.</span></span> <span data-ttu-id="89185-122">To polecenie nie jest konieczne w wersji 1.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="89185-122">This command is not necessary in 1.0 or later.</span></span>

<span data-ttu-id="89185-123">Jeśli chcesz toouse skryptów przeznaczony dla środowiska hello 0.9.8, hello 1.0 lub nowszej środowiska, należy dokładnie przetestować skrypty hello w środowisku przedprodukcyjnym przed ich użyciem w środowisku produkcyjnym tooavoid nieoczekiwany wpływu.</span><span class="sxs-lookup"><span data-stu-id="89185-123">If you want toouse your scripts written for hello 0.9.8 environment, in hello 1.0 or later environment, you should carefully test hello scripts in a pre-production environment before using them in production tooavoid unexpected impact.</span></span>

<span data-ttu-id="89185-124">[Pobierz najnowszą wersję programu PowerShell hello](https://github.com/Azure/azure-powershell/releases) (minimalna wersja wymagana jest: 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="89185-124">[Download hello latest PowerShell release](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>

[!INCLUDE [arm-getting-setup-powershell](../../includes/arm-getting-setup-powershell.md)]

## <a name="create-a-backup-vault"></a><span data-ttu-id="89185-125">Tworzenie magazynu kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="89185-125">Create a backup vault</span></span>
> [!WARNING]
> <span data-ttu-id="89185-126">W przypadku klientów przy kopia zapasowa Azure powitania po raz pierwszy należy tooregister hello kopia zapasowa Azure dostawcy toobe używane w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="89185-126">For customers using Azure Backup for hello first time, you need tooregister hello Azure Backup provider toobe used with your subscription.</span></span> <span data-ttu-id="89185-127">Można to zrobić, uruchamiając następujące polecenie hello: Register-AzureProvider - ProviderNamespace "Microsoft.Backup"</span><span class="sxs-lookup"><span data-stu-id="89185-127">This can be done by running hello following command: Register-AzureProvider -ProviderNamespace "Microsoft.Backup"</span></span>
>
>

<span data-ttu-id="89185-128">Można utworzyć nowy magazyn kopii zapasowych za pomocą hello **AzureRMBackupVault nowy** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="89185-128">You can create a new backup vault using hello **New-AzureRMBackupVault** cmdlet.</span></span> <span data-ttu-id="89185-129">Hello magazynu kopii zapasowych jest zasobem ARM, więc należy tooplace go w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="89185-129">hello backup vault is an ARM resource, so you need tooplace it within a Resource Group.</span></span> <span data-ttu-id="89185-130">W konsoli programu Azure PowerShell z podwyższonym poziomem uprawnień uruchom następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="89185-130">In an elevated Azure PowerShell console, run hello following commands:</span></span>

```
PS C:\> New-AzureResourceGroup –Name “test-rg” -Region “West US”
PS C:\> $backupvault = New-AzureRMBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GeoRedundant
```

<span data-ttu-id="89185-131">Użyj hello **Get AzureRMBackupVault** magazyny kopii zapasowych hello toolist polecenia cmdlet w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="89185-131">Use hello **Get-AzureRMBackupVault** cmdlet toolist hello backup vaults in a subscription.</span></span>

## <a name="installing-hello-azure-backup-agent"></a><span data-ttu-id="89185-132">Instalowanie agenta usługi Kopia zapasowa Azure hello</span><span class="sxs-lookup"><span data-stu-id="89185-132">Installing hello Azure Backup agent</span></span>
<span data-ttu-id="89185-133">Przed zainstalowaniem agenta usługi Kopia zapasowa Azure hello należy toohave hello Instalatora, pobranych i znajdują się na powitania serwera systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="89185-133">Before you install hello Azure Backup agent, you need toohave hello installer downloaded and present on hello Windows Server.</span></span> <span data-ttu-id="89185-134">Możesz pobrać najnowszą wersję Instalatora hello hello ze hello [Microsoft Download Center](http://aka.ms/azurebackup_agent) lub ze strony pulpitu nawigacyjnego hello magazynu kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="89185-134">You can get hello latest version of hello installer from hello [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from hello backup vault's Dashboard page.</span></span> <span data-ttu-id="89185-135">Zapisz Instalator hello tooan łatwo dostępnej lokalizacji, takich jak * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="89185-135">Save hello installer tooan easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="89185-136">tooinstall hello agenta, uruchom następujące polecenie w konsoli programu PowerShell z podwyższonym poziomem uprawnień hello:</span><span class="sxs-lookup"><span data-stu-id="89185-136">tooinstall hello agent, run hello following command in an elevated PowerShell console:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="89185-137">Spowoduje to zainstalowanie agenta hello z wszystkich opcji domyślnych hello.</span><span class="sxs-lookup"><span data-stu-id="89185-137">This installs hello agent with all hello default options.</span></span> <span data-ttu-id="89185-138">Instalacja Hello zajmuje kilka minut w tle hello.</span><span class="sxs-lookup"><span data-stu-id="89185-138">hello installation takes a few minutes in hello background.</span></span> <span data-ttu-id="89185-139">Jeśli nie określisz hello */nu* opcji, a następnie hello **usługi Windows Update** na końcu hello hello toocheck instalacji dla wszystkich aktualizacji, zostanie otwarte okno.</span><span class="sxs-lookup"><span data-stu-id="89185-139">If you do not specify hello */nu* option then hello **Windows Update** window will open at hello end of hello installation toocheck for any updates.</span></span> <span data-ttu-id="89185-140">Po zainstalowaniu agenta hello wyświetli hello listy zainstalowanych programów.</span><span class="sxs-lookup"><span data-stu-id="89185-140">Once installed, hello agent will show in hello list of installed programs.</span></span>

<span data-ttu-id="89185-141">toosee hello listy zainstalowanych programów, należy przejść za**Panelu sterowania** > **programy** > **programy i funkcje**.</span><span class="sxs-lookup"><span data-stu-id="89185-141">toosee hello list of installed programs, go too**Control Panel** > **Programs** > **Programs and Features**.</span></span>

![Agent został zainstalowany](./media/backup-client-automation/installed-agent-listing.png)

### <a name="installation-options"></a><span data-ttu-id="89185-143">Opcje instalacji</span><span class="sxs-lookup"><span data-stu-id="89185-143">Installation options</span></span>
<span data-ttu-id="89185-144">toosee, który hello wszystkie opcje dostępne za pośrednictwem hello wiersza polecenia, użyj następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="89185-144">toosee all hello options available via hello command-line, use hello following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="89185-145">Witaj dostępne opcje to:</span><span class="sxs-lookup"><span data-stu-id="89185-145">hello available options include:</span></span>

| <span data-ttu-id="89185-146">Opcja</span><span class="sxs-lookup"><span data-stu-id="89185-146">Option</span></span> | <span data-ttu-id="89185-147">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="89185-147">Details</span></span> | <span data-ttu-id="89185-148">Domyślne</span><span class="sxs-lookup"><span data-stu-id="89185-148">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="89185-149">/q</span><span class="sxs-lookup"><span data-stu-id="89185-149">/q</span></span> |<span data-ttu-id="89185-150">Instalację cichą</span><span class="sxs-lookup"><span data-stu-id="89185-150">Quiet installation</span></span> |- |
| <span data-ttu-id="89185-151">/ p: "Lokalizacja"</span><span class="sxs-lookup"><span data-stu-id="89185-151">/p:"location"</span></span> |<span data-ttu-id="89185-152">Ścieżka folderu instalacji toohello hello Azure Backup Agent.</span><span class="sxs-lookup"><span data-stu-id="89185-152">Path toohello installation folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="89185-153">C:\Program Files\Microsoft Azure Recovery usługi agenta</span><span class="sxs-lookup"><span data-stu-id="89185-153">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="89185-154">/ s: "Lokalizacja"</span><span class="sxs-lookup"><span data-stu-id="89185-154">/s:"location"</span></span> |<span data-ttu-id="89185-155">Ścieżka folderu pamięci podręcznej toohello hello Azure Backup Agent.</span><span class="sxs-lookup"><span data-stu-id="89185-155">Path toohello cache folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="89185-156">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="89185-156">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="89185-157">/m</span><span class="sxs-lookup"><span data-stu-id="89185-157">/m</span></span> |<span data-ttu-id="89185-158">TooMicrosoft opcjonalnych aktualizacji</span><span class="sxs-lookup"><span data-stu-id="89185-158">Opt-in tooMicrosoft Update</span></span> |- |
| <span data-ttu-id="89185-159">/nu</span><span class="sxs-lookup"><span data-stu-id="89185-159">/nu</span></span> |<span data-ttu-id="89185-160">Nie sprawdzaj aktualizacji po ukończeniu instalacji</span><span class="sxs-lookup"><span data-stu-id="89185-160">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="89185-161">/d</span><span class="sxs-lookup"><span data-stu-id="89185-161">/d</span></span> |<span data-ttu-id="89185-162">Odinstalowuje agenta usług odzyskiwania Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="89185-162">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="89185-163">/pH</span><span class="sxs-lookup"><span data-stu-id="89185-163">/ph</span></span> |<span data-ttu-id="89185-164">Adres hosta serwera proxy</span><span class="sxs-lookup"><span data-stu-id="89185-164">Proxy Host Address</span></span> |- |
| <span data-ttu-id="89185-165">/Po</span><span class="sxs-lookup"><span data-stu-id="89185-165">/po</span></span> |<span data-ttu-id="89185-166">Numer portu hosta serwera proxy</span><span class="sxs-lookup"><span data-stu-id="89185-166">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="89185-167">/Pu</span><span class="sxs-lookup"><span data-stu-id="89185-167">/pu</span></span> |<span data-ttu-id="89185-168">Nazwa użytkownika serwera proxy hosta</span><span class="sxs-lookup"><span data-stu-id="89185-168">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="89185-169">/PW</span><span class="sxs-lookup"><span data-stu-id="89185-169">/pw</span></span> |<span data-ttu-id="89185-170">Hasło serwera proxy</span><span class="sxs-lookup"><span data-stu-id="89185-170">Proxy Password</span></span> |- |

## <a name="registering-with-hello-azure-backup-service"></a><span data-ttu-id="89185-171">Rejestrowanie w hello usługi Kopia zapasowa Azure</span><span class="sxs-lookup"><span data-stu-id="89185-171">Registering with hello Azure Backup service</span></span>
<span data-ttu-id="89185-172">Przed zarejestrowaniem z hello usługi Kopia zapasowa Azure, należy tooensure tego hello [wymagania wstępne](backup-configure-vault.md) są spełnione.</span><span class="sxs-lookup"><span data-stu-id="89185-172">Before you can register with hello Azure Backup service, you need tooensure that hello [prerequisites](backup-configure-vault.md) are met.</span></span> <span data-ttu-id="89185-173">Należy:</span><span class="sxs-lookup"><span data-stu-id="89185-173">You must:</span></span>

* <span data-ttu-id="89185-174">Masz ważną subskrypcję platformy Azure</span><span class="sxs-lookup"><span data-stu-id="89185-174">Have a valid Azure subscription</span></span>
* <span data-ttu-id="89185-175">Masz magazyn kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="89185-175">Have a backup vault</span></span>

<span data-ttu-id="89185-176">poświadczenia magazynu hello toodownload Uruchom hello **Get-AzureRMBackupVaultCredentials** polecenia cmdlet w konsoli programu PowerShell systemu Azure i zapisać go w dogodnym miejscu, takich jak * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="89185-176">toodownload hello vault credentials, run hello **Get-AzureRMBackupVaultCredentials** cmdlet in an Azure PowerShell console and store it in a convenient location like *C:\Downloads\*.</span></span>

```
PS C:\> $credspath = "C:\"
PS C:\> $credsfilename = Get-AzureRMBackupVaultCredentials -Vault $backupvault -TargetLocation $credspath
PS C:\> $credsfilename
f5303a0b-fae4-4cdb-b44d-0e4c032dde26_backuprg_backuprn_2015-08-11--06-22-35.VaultCredentials
```

<span data-ttu-id="89185-177">Rejestracji hello maszyny z magazynem hello jest wykonywane przy użyciu hello [Start OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="89185-177">Registering hello machine with hello vault is done using hello [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet:</span></span>

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-OBRegistration -VaultCredentials $cred -Confirm:$false

CertThumbprint      : 7a2ef2caa2e74b6ed1222a5e89288ddad438df2
SubscriptionID      : ef4ab577-c2c0-43e4-af80-af49f485f3d1
ServiceResourceName : test-vault
Region              : West US

Machine registration succeeded.
```

> [!IMPORTANT]
> <span data-ttu-id="89185-178">Nie należy używać pliku poświadczeń magazynu hello toospecify ścieżek względnych.</span><span class="sxs-lookup"><span data-stu-id="89185-178">Do not use relative paths toospecify hello vault credentials file.</span></span> <span data-ttu-id="89185-179">Należy podać ścieżkę bezwzględną jako polecenia cmdlet toohello wejściowego.</span><span class="sxs-lookup"><span data-stu-id="89185-179">You must provide an absolute path as an input toohello cmdlet.</span></span>
>
>

## <a name="networking-settings"></a><span data-ttu-id="89185-180">Ustawienia sieciowe</span><span class="sxs-lookup"><span data-stu-id="89185-180">Networking settings</span></span>
<span data-ttu-id="89185-181">Gdy łączność hello hello systemu Windows maszyny toohello jest internet za pośrednictwem serwera proxy, ustawienia serwera proxy hello można również podać o toohello agenta.</span><span class="sxs-lookup"><span data-stu-id="89185-181">When hello connectivity of hello Windows machine toohello internet is through a proxy server, hello proxy settings can also be provided toohello agent.</span></span> <span data-ttu-id="89185-182">W tym przykładzie nie żadnego serwera proxy, dlatego firma Microsoft są jawnie wyczyszczenie żadnych informacji dotyczących serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="89185-182">In this example, there is no proxy server, so we are explicitly clearing any proxy-related information.</span></span>

<span data-ttu-id="89185-183">Wykorzystanie przepustowości można również sterować za pomocą opcji hello ```work hour bandwidth``` i ```non-work hour bandwidth``` dla danego zestawu dni tygodnia hello.</span><span class="sxs-lookup"><span data-stu-id="89185-183">Bandwidth usage can also be controlled with hello options of ```work hour bandwidth``` and ```non-work hour bandwidth``` for a given set of days of hello week.</span></span>

<span data-ttu-id="89185-184">Ustawienie szczegóły serwera proxy i przepustowości hello jest wykonywane przy użyciu hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="89185-184">Setting hello proxy and bandwidth details is done using hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) cmdlet:</span></span>

```
PS C:\> Set-OBMachineSetting -NoProxy
Server properties updated successfully.

PS C:\> Set-OBMachineSetting -NoThrottle
Server properties updated successfully.
```

## <a name="encryption-settings"></a><span data-ttu-id="89185-185">Ustawienia szyfrowania</span><span class="sxs-lookup"><span data-stu-id="89185-185">Encryption settings</span></span>
<span data-ttu-id="89185-186">tooAzure wysyłane dane kopii zapasowej Hello kopii zapasowej jest zaszyfrowany tooprotect hello poufność danych hello.</span><span class="sxs-lookup"><span data-stu-id="89185-186">hello backup data sent tooAzure Backup is encrypted tooprotect hello confidentiality of hello data.</span></span> <span data-ttu-id="89185-187">hasło szyfrowania Hello jest hello "password" toodecrypt hello danych w czasie hello przywracania.</span><span class="sxs-lookup"><span data-stu-id="89185-187">hello encryption passphrase is hello "password" toodecrypt hello data at hello time of restore.</span></span>

```
PS C:\> ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force | Set-OBMachineSetting
Server properties updated successfully
```

> [!IMPORTANT]
> <span data-ttu-id="89185-188">Zachowaj informacje hasło hello bezpieczne po ustawieniu.</span><span class="sxs-lookup"><span data-stu-id="89185-188">Keep hello passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="89185-189">Nie będzie możliwe toorestore danych z platformy Azure bez tego hasła.</span><span class="sxs-lookup"><span data-stu-id="89185-189">You will not be able toorestore data from Azure without this passphrase.</span></span>
>
>

## <a name="back-up-files-and-folders"></a><span data-ttu-id="89185-190">Tworzenie kopii zapasowych plików i folderów</span><span class="sxs-lookup"><span data-stu-id="89185-190">Back up files and folders</span></span>
<span data-ttu-id="89185-191">Kopie zapasowe z serwerów z systemem Windows i klientów tooAzure kopii zapasowej zarządzane przez zasady.</span><span class="sxs-lookup"><span data-stu-id="89185-191">All your backups from Windows Servers and clients tooAzure Backup are governed by a policy.</span></span> <span data-ttu-id="89185-192">zasady Hello składa się z trzech części:</span><span class="sxs-lookup"><span data-stu-id="89185-192">hello policy comprises three parts:</span></span>

1. <span data-ttu-id="89185-193">A **harmonogram tworzenia kopii zapasowych** , który określa podczas tworzenia kopii zapasowych należy toobe podjęte, a następnie synchronizowane z usługą hello.</span><span class="sxs-lookup"><span data-stu-id="89185-193">A **backup schedule** that specifies when backups need toobe taken and synchronized with hello service.</span></span>
2. <span data-ttu-id="89185-194">A **harmonogramu przechowywania** Określa, jak długo punkty odzyskiwania hello tooretain na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="89185-194">A **retention schedule** that specifies how long tooretain hello recovery points in Azure.</span></span>
3. <span data-ttu-id="89185-195">A **określania włączenia/wyłączenia pliku** które nakazują, co należy utworzyć kopię.</span><span class="sxs-lookup"><span data-stu-id="89185-195">A **file inclusion/exclusion specification** that dictates what should be backed up.</span></span>

<span data-ttu-id="89185-196">W tym dokumencie ponieważ będziemy w przypadku automatyzacji kopii zapasowej, przyjęto będzie założenie, że nic nie skonfigurowano.</span><span class="sxs-lookup"><span data-stu-id="89185-196">In this document, since we're automating backup, we'll assume nothing has been configured.</span></span> <span data-ttu-id="89185-197">Zaczniemy przez utworzenie nowych zasad tworzenia kopii zapasowej przy użyciu hello [OBPolicy nowy](https://technet.microsoft.com/library/hh770416.aspx) polecenia cmdlet i przy jego użyciu.</span><span class="sxs-lookup"><span data-stu-id="89185-197">We begin by creating a new backup policy using hello [New-OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) cmdlet and using it.</span></span>

```
PS C:\> $newpolicy = New-OBPolicy
```

<span data-ttu-id="89185-198">W tym hello czasu zasady jest pusta i innych poleceń cmdlet są potrzebne toodefine jakie elementy zostaną uwzględnione lub wykluczone, gdy kopie zapasowe zostaną uruchomione i gdy hello kopie zapasowe będą przechowywane.</span><span class="sxs-lookup"><span data-stu-id="89185-198">At this time hello policy is empty and other cmdlets are needed toodefine what items will be included or excluded, when backups will run, and where hello backups will be stored.</span></span>

### <a name="configuring-hello-backup-schedule"></a><span data-ttu-id="89185-199">Konfigurowanie hello harmonogram tworzenia kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="89185-199">Configuring hello backup schedule</span></span>
<span data-ttu-id="89185-200">Witaj najpierw hello 3 części zasad jest harmonogram tworzenia kopii zapasowych hello, który został utworzony za pomocą hello [OBSchedule nowy](https://technet.microsoft.com/library/hh770401) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="89185-200">hello first of hello 3 parts of a policy is hello backup schedule, which is created using hello [New-OBSchedule](https://technet.microsoft.com/library/hh770401) cmdlet.</span></span> <span data-ttu-id="89185-201">harmonogram tworzenia kopii zapasowych Hello definiuje, podczas tworzenia kopii zapasowych należy toobe podjęte.</span><span class="sxs-lookup"><span data-stu-id="89185-201">hello backup schedule defines when backups need toobe taken.</span></span> <span data-ttu-id="89185-202">Podczas tworzenia harmonogramu należy toospecify 2 parametry wejściowe:</span><span class="sxs-lookup"><span data-stu-id="89185-202">When creating a schedule you need toospecify 2 input parameters:</span></span>

* <span data-ttu-id="89185-203">**Dni tygodnia hello** hello kopii zapasowej powinno być ono uruchomione.</span><span class="sxs-lookup"><span data-stu-id="89185-203">**Days of hello week** that hello backup should run.</span></span> <span data-ttu-id="89185-204">Można uruchomić zadanie tworzenia kopii zapasowej hello na tylko jeden dzień lub każdego dnia tygodnia hello lub dowolną kombinację między.</span><span class="sxs-lookup"><span data-stu-id="89185-204">You can run hello backup job on just one day, or every day of hello week, or any combination in between.</span></span>
* <span data-ttu-id="89185-205">**Pór dnia hello** uruchomienia hello kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="89185-205">**Times of hello day** when hello backup should run.</span></span> <span data-ttu-id="89185-206">Można zdefiniować się too3 różnych porach dnia hello, gdy zostanie wywołane hello kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="89185-206">You can define up too3 different times of hello day when hello backup will be triggered.</span></span>

<span data-ttu-id="89185-207">Na przykład można skonfigurować zasad tworzenia kopii zapasowej, wykonywany o 16: 00 w każdą sobotę i niedziela.</span><span class="sxs-lookup"><span data-stu-id="89185-207">For instance, you could configure a backup policy that runs at 4PM every Saturday and Sunday.</span></span>

```
PS C:\> $sched = New-OBSchedule -DaysofWeek Saturday, Sunday -TimesofDay 16:00
```

<span data-ttu-id="89185-208">harmonogram tworzenia kopii zapasowych Hello musi toobe skojarzonej z zasadami i można to osiągnąć przy użyciu hello [OBSchedule zestaw](https://technet.microsoft.com/library/hh770407) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="89185-208">hello backup schedule needs toobe associated with a policy, and this can be achieved by using hello [Set-OBSchedule](https://technet.microsoft.com/library/hh770407) cmdlet.</span></span>

```
PS C:> Set-OBSchedule -Policy $newpolicy -Schedule $sched
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s) DsList : PolicyName : RetentionPolicy : State : New PolicyState : Valid
```
### <a name="configuring-a-retention-policy"></a><span data-ttu-id="89185-209">Konfigurowania zasad przechowywania</span><span class="sxs-lookup"><span data-stu-id="89185-209">Configuring a retention policy</span></span>
<span data-ttu-id="89185-210">zasady przechowywania Hello definiuje czas odzyskiwania, punkty utworzone na podstawie zadania tworzenia kopii zapasowej zostaną zachowane.</span><span class="sxs-lookup"><span data-stu-id="89185-210">hello retention policy defines how long recovery points created from backup jobs are retained.</span></span> <span data-ttu-id="89185-211">Podczas tworzenia nowych zasad przechowywania przy użyciu hello [OBRetentionPolicy nowy](https://technet.microsoft.com/library/hh770425) polecenia cmdlet, można określić hello liczbę dni, które hello punktów odzyskiwania należy toobe przechowywane w usłudze Kopia zapasowa Azure.</span><span class="sxs-lookup"><span data-stu-id="89185-211">When creating a new retention policy using hello [New-OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) cmdlet, you can specify hello number of days that hello backup recovery points need toobe retained with Azure Backup.</span></span> <span data-ttu-id="89185-212">w poniższym przykładzie Hello ustawia zasady przechowywania wynosi 7 dni.</span><span class="sxs-lookup"><span data-stu-id="89185-212">hello example below sets a retention policy of 7 days.</span></span>

```
PS C:\> $retentionpolicy = New-OBRetentionPolicy -RetentionDays 7
```

<span data-ttu-id="89185-213">Witaj zasady przechowywania muszą być skojarzone z zasadami głównego hello przy użyciu polecenia cmdlet hello [OBRetentionPolicy zestaw](https://technet.microsoft.com/library/hh770405):</span><span class="sxs-lookup"><span data-stu-id="89185-213">hello retention policy must be associated with hello main policy using hello cmdlet [Set-OBRetentionPolicy](https://technet.microsoft.com/library/hh770405):</span></span>

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
### <a name="including-and-excluding-files-toobe-backed-up"></a><span data-ttu-id="89185-214">Włączanie i wyłączanie toobe pliki kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="89185-214">Including and excluding files toobe backed up</span></span>
<span data-ttu-id="89185-215">```OBFileSpec``` Obiekt definiuje hello pliki toobe dołączone i wykluczone w kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="89185-215">An ```OBFileSpec``` object defines hello files toobe included and excluded in a backup.</span></span> <span data-ttu-id="89185-216">Jest to zestaw reguł, że zakres limit hello chronione pliki i foldery na komputerze.</span><span class="sxs-lookup"><span data-stu-id="89185-216">This is a set of rules that scope out hello protected files and folders on a machine.</span></span> <span data-ttu-id="89185-217">Może mieć wiele pliku reguł dołączania lub wykluczania zgodnie z wymaganiami i skojarzyć je z zasadami.</span><span class="sxs-lookup"><span data-stu-id="89185-217">You can have as many file inclusion or exclusion rules as required, and associate them with a policy.</span></span> <span data-ttu-id="89185-218">Tworząc nowy obiekt OBFileSpec, można:</span><span class="sxs-lookup"><span data-stu-id="89185-218">When creating a new OBFileSpec object, you can:</span></span>

* <span data-ttu-id="89185-219">Określ toobe pliki i foldery hello włączone</span><span class="sxs-lookup"><span data-stu-id="89185-219">Specify hello files and folders toobe included</span></span>
* <span data-ttu-id="89185-220">Określ toobe pliki i foldery hello wyłączone</span><span class="sxs-lookup"><span data-stu-id="89185-220">Specify hello files and folders toobe excluded</span></span>
* <span data-ttu-id="89185-221">Określ rekursywne tworzenie kopii zapasowych danych w folderze (lub) czy tylko hello pliki najwyższego poziomu w określonym folderze hello należy utworzyć kopię zapasową.</span><span class="sxs-lookup"><span data-stu-id="89185-221">Specify recursive backup of data in a folder (or) whether only hello top-level files in hello specified folder should be backed up.</span></span>

<span data-ttu-id="89185-222">ostatnie Hello odbywa się przy użyciu flagi - Nierekurencyjny hello w poleceniu hello OBFileSpec nowy.</span><span class="sxs-lookup"><span data-stu-id="89185-222">hello latter is achieved by using hello -NonRecursive flag in hello New-OBFileSpec command.</span></span>

<span data-ttu-id="89185-223">W poniższym przykładzie hello możemy utworzyć kopię zapasową woluminu, C: i D: i wykluczanie plików binarnych systemu operacyjnego hello w folderze systemu Windows hello i foldery tymczasowe.</span><span class="sxs-lookup"><span data-stu-id="89185-223">In hello example below, we'll back up volume C: and D: and exclude hello OS binaries in hello Windows folder and any temporary folders.</span></span> <span data-ttu-id="89185-224">toodo, utworzymy dwa specyfikacji pliku przy użyciu hello [OBFileSpec nowy](https://technet.microsoft.com/library/hh770408) polecenia cmdlet — jeden dla dołączania i jeden do wykluczenia.</span><span class="sxs-lookup"><span data-stu-id="89185-224">toodo so we'll create two file specifications using hello [New-OBFileSpec](https://technet.microsoft.com/library/hh770408) cmdlet - one for inclusion and one for exclusion.</span></span> <span data-ttu-id="89185-225">Po utworzeniu specyfikacji pliku hello są powiązane z zasadami hello przy użyciu hello [OBFileSpec Dodaj](https://technet.microsoft.com/library/hh770424) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="89185-225">Once hello file specifications have been created, they're associated with hello policy using hello [Add-OBFileSpec](https://technet.microsoft.com/library/hh770424) cmdlet.</span></span>

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

### <a name="applying-hello-policy"></a><span data-ttu-id="89185-226">Zastosowanie zasad hello</span><span class="sxs-lookup"><span data-stu-id="89185-226">Applying hello policy</span></span>
<span data-ttu-id="89185-227">Teraz hello obiektu zasad została zakończona i ma skojarzone harmonogram tworzenia kopii zapasowych, zasad przechowywania i włączenia/wyłączenia lista plików.</span><span class="sxs-lookup"><span data-stu-id="89185-227">Now hello policy object is complete and has an associated backup schedule, retention policy, and an inclusion/exclusion list of files.</span></span> <span data-ttu-id="89185-228">Te zasady można teraz zatwierdzone dla toouse kopia zapasowa Azure.</span><span class="sxs-lookup"><span data-stu-id="89185-228">This policy can now be committed for Azure Backup toouse.</span></span> <span data-ttu-id="89185-229">Przed zastosowaniem hello nowo utworzone zasady upewnij się, że nie ma żadnych istniejących zasad tworzenia kopii zapasowej skojarzonego z serwerem hello przy użyciu hello [OBPolicy Usuń](https://technet.microsoft.com/library/hh770415) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="89185-229">Before you apply hello newly created policy ensure that there are no existing backup policies associated with hello server by using hello [Remove-OBPolicy](https://technet.microsoft.com/library/hh770415) cmdlet.</span></span> <span data-ttu-id="89185-230">Usuwanie zasad hello wyświetli monit o potwierdzenie.</span><span class="sxs-lookup"><span data-stu-id="89185-230">Removing hello policy will prompt for confirmation.</span></span> <span data-ttu-id="89185-231">Potwierdzenie hello tooskip Użyj hello ```-Confirm:$false``` flagę hello polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="89185-231">tooskip hello confirmation use hello ```-Confirm:$false``` flag with hello cmdlet.</span></span>

```
PS C:> Get-OBPolicy | Remove-OBPolicy
Microsoft Azure Backup Are you sure you want tooremove this backup policy? This will delete all hello backed up data. [Y] Yes [A] Yes tooAll [N] No [L] No tooAll [S] Suspend [?] Help (default is "Y"):
```

<span data-ttu-id="89185-232">Przekazywanie obiektu zasad hello jest wykonywane przy użyciu hello [OBPolicy zestaw](https://technet.microsoft.com/library/hh770421) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="89185-232">Committing hello policy object is done using hello [Set-OBPolicy](https://technet.microsoft.com/library/hh770421) cmdlet.</span></span> <span data-ttu-id="89185-233">Spowoduje to również monituje o potwierdzenie.</span><span class="sxs-lookup"><span data-stu-id="89185-233">This will also ask for confirmation.</span></span> <span data-ttu-id="89185-234">Potwierdzenie hello tooskip Użyj hello ```-Confirm:$false``` flagę hello polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="89185-234">tooskip hello confirmation use hello ```-Confirm:$false``` flag with hello cmdlet.</span></span>

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

<span data-ttu-id="89185-235">Możesz wyświetlić szczegóły hello hello istniejących zasad tworzenia kopii zapasowej przy użyciu hello [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="89185-235">You can view hello details of hello existing backup policy using hello [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) cmdlet.</span></span> <span data-ttu-id="89185-236">Użytkownik może przejść za pomocą hello [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) polecenia cmdlet hello harmonogram tworzenia kopii zapasowych i hello [Get-OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) polecenia cmdlet dla zasad przechowywania hello</span><span class="sxs-lookup"><span data-stu-id="89185-236">You can drill-down further using hello [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) cmdlet for hello backup schedule and hello [Get-OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) cmdlet for hello retention policies</span></span>

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

### <a name="performing-an-ad-hoc-backup"></a><span data-ttu-id="89185-237">Wykonywanie kopii zapasowych ad hoc</span><span class="sxs-lookup"><span data-stu-id="89185-237">Performing an ad-hoc backup</span></span>
<span data-ttu-id="89185-238">Po ustawieniu zasad tworzenia kopii zapasowej hello kopii zapasowych zostanie przeprowadzona na powitania harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="89185-238">Once a backup policy has been set hello backups will occur per hello schedule.</span></span> <span data-ttu-id="89185-239">Wyzwolenie kopii zapasowych ad hoc jest także możliwe przy użyciu hello [Start OBBackup](https://technet.microsoft.com/library/hh770426) polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="89185-239">Triggering an ad-hoc backup is also possible using hello [Start-OBBackup](https://technet.microsoft.com/library/hh770426) cmdlet:</span></span>

```
PS C:> Get-OBPolicy | Start-OBBackup
Taking snapshot of volumes...
Preparing storage...
Estimating size of backup items...
Estimating size of backup items...
Transferring data...
Verifying backup...
Job completed.
hello backup operation completed successfully.
```

## <a name="restore-data-from-azure-backup"></a><span data-ttu-id="89185-240">Przywróć dane z usługi Kopia zapasowa Azure</span><span class="sxs-lookup"><span data-stu-id="89185-240">Restore data from Azure Backup</span></span>
<span data-ttu-id="89185-241">W tej sekcji przedstawiono kroki hello do automatyzacji odzyskiwanie danych z kopii zapasowej Azure.</span><span class="sxs-lookup"><span data-stu-id="89185-241">This section will guide you through hello steps for automating recovery of data from Azure Backup.</span></span> <span data-ttu-id="89185-242">Spowoduje to obejmuje hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="89185-242">Doing so involves hello following steps:</span></span>

1. <span data-ttu-id="89185-243">Wybierz wolumin źródłowy hello</span><span class="sxs-lookup"><span data-stu-id="89185-243">Pick hello source volume</span></span>
2. <span data-ttu-id="89185-244">Wybierz opcję tworzenia kopii zapasowej toorestore punktu</span><span class="sxs-lookup"><span data-stu-id="89185-244">Choose a backup point toorestore</span></span>
3. <span data-ttu-id="89185-245">Wybierz element toorestore</span><span class="sxs-lookup"><span data-stu-id="89185-245">Choose an item toorestore</span></span>
4. <span data-ttu-id="89185-246">Proces przywracania hello wyzwalacza</span><span class="sxs-lookup"><span data-stu-id="89185-246">Trigger hello restore process</span></span>

### <a name="picking-hello-source-volume"></a><span data-ttu-id="89185-247">Wolumin źródła hello pobrania</span><span class="sxs-lookup"><span data-stu-id="89185-247">Picking hello source volume</span></span>
<span data-ttu-id="89185-248">W kolejności toorestore element z kopii zapasowej Azure najpierw tooidentify hello źródła elementu hello.</span><span class="sxs-lookup"><span data-stu-id="89185-248">In order toorestore an item from Azure Backup, you first need tooidentify hello source of hello item.</span></span> <span data-ttu-id="89185-249">Ponieważ firma Microsoft jest wykonywania poleceń hello w kontekście systemu Windows Server lub klienta systemu Windows hello, jest już zidentyfikowany hello maszyny.</span><span class="sxs-lookup"><span data-stu-id="89185-249">Since we're executing hello commands in hello context of a Windows Server or a Windows client, hello machine is already identified.</span></span> <span data-ttu-id="89185-250">następnym krokiem Hello w identyfikacji źródła hello jest tooidentify hello woluminu zawierającego go.</span><span class="sxs-lookup"><span data-stu-id="89185-250">hello next step in identifying hello source is tooidentify hello volume containing it.</span></span> <span data-ttu-id="89185-251">Listę woluminów lub źródła Trwa wykonywanie kopii zapasowej z tego komputera mogą być pobierane, wykonując hello [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="89185-251">A list of volumes or sources being backed up from this machine can be retrieved by executing hello [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) cmdlet.</span></span> <span data-ttu-id="89185-252">To polecenie zwraca tablicę wszystkich źródeł hello kopii zapasowej z serwera/klienta.</span><span class="sxs-lookup"><span data-stu-id="89185-252">This command returns an array of all hello sources backed up from this server/client.</span></span>

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

### <a name="choosing-a-backup-point-toorestore"></a><span data-ttu-id="89185-253">Wybieranie kopii zapasowej toorestore punktu</span><span class="sxs-lookup"><span data-stu-id="89185-253">Choosing a backup point toorestore</span></span>
<span data-ttu-id="89185-254">Witaj listy punktów kopii zapasowej mogą zostać pobrane przez wykonywania hello [Get OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) polecenie cmdlet z odpowiednimi parametrami.</span><span class="sxs-lookup"><span data-stu-id="89185-254">hello list of backup points can be retrieved by executing hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet with appropriate parameters.</span></span> <span data-ttu-id="89185-255">W naszym przykładzie wybrano hello najnowszego punktu kopii zapasowej dla woluminu źródłowego hello *D:* i korzystać z niego toorecover określonego pliku.</span><span class="sxs-lookup"><span data-stu-id="89185-255">In our example, we’ll choose hello latest backup point for hello source volume *D:* and use it toorecover a specific file.</span></span>

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
<span data-ttu-id="89185-256">Obiekt Hello ```$rps``` jest tablicą punktów kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="89185-256">hello object ```$rps``` is an array of backup points.</span></span> <span data-ttu-id="89185-257">pierwszy element Hello jest hello najnowszy punkt i hello n-tego elementu jest hello starsze punkty.</span><span class="sxs-lookup"><span data-stu-id="89185-257">hello first element is hello latest point and hello Nth element is hello oldest point.</span></span> <span data-ttu-id="89185-258">używamy toochoose hello najnowszy punkt ```$rps[0]```.</span><span class="sxs-lookup"><span data-stu-id="89185-258">toochoose hello latest point, we will use ```$rps[0]```.</span></span>

### <a name="choosing-an-item-toorestore"></a><span data-ttu-id="89185-259">Wybieranie toorestore elementu</span><span class="sxs-lookup"><span data-stu-id="89185-259">Choosing an item toorestore</span></span>
<span data-ttu-id="89185-260">tooidentify hello plików lub folder toorestore rekursywnie Użyj hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="89185-260">tooidentify hello exact file or folder toorestore, recursively use hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet.</span></span> <span data-ttu-id="89185-261">Hierarchia folderów hello ten sposób można przeglądać wyłącznie przy użyciu hello ```Get-OBRecoverableItem```.</span><span class="sxs-lookup"><span data-stu-id="89185-261">That way hello folder hierarchy can be browsed solely using hello ```Get-OBRecoverableItem```.</span></span>

<span data-ttu-id="89185-262">W tym przykładzie, jeśli chcemy pliku hello toorestore *finances.xls* firma Microsoft może odwoływać się przy użyciu tego obiektu hello ```$filesFolders[1]```.</span><span class="sxs-lookup"><span data-stu-id="89185-262">In this example, if we want toorestore hello file *finances.xls* we can reference that using hello object ```$filesFolders[1]```.</span></span>

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

<span data-ttu-id="89185-263">Możesz również wyszukać toorestore elementów przy użyciu hello ```Get-OBRecoverableItem``` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="89185-263">You can also search for items toorestore using hello ```Get-OBRecoverableItem``` cmdlet.</span></span> <span data-ttu-id="89185-264">W naszym przykładzie toosearch dla *finances.xls* firma Microsoft można uzyskać dojścia do pliku hello, uruchamiając polecenie:</span><span class="sxs-lookup"><span data-stu-id="89185-264">In our example, toosearch for *finances.xls* we could get a handle on hello file by running this command:</span></span>

```
PS C:\> $item = Get-OBRecoverableItem -RecoveryPoint $rps[0] -Location "D:\MyData" -SearchString "finance*"
```

### <a name="triggering-hello-restore-process"></a><span data-ttu-id="89185-265">Wyzwolenie procesu przywracania hello</span><span class="sxs-lookup"><span data-stu-id="89185-265">Triggering hello restore process</span></span>
<span data-ttu-id="89185-266">proces przywracania hello tootrigger, najpierw musisz opcje odzyskiwania hello toospecify.</span><span class="sxs-lookup"><span data-stu-id="89185-266">tootrigger hello restore process, we first need toospecify hello recovery options.</span></span> <span data-ttu-id="89185-267">Można to zrobić za pomocą hello [OBRecoveryOption nowy](https://technet.microsoft.com/library/hh770417.aspx) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="89185-267">This can be done by using hello [New-OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) cmdlet.</span></span> <span data-ttu-id="89185-268">Na przykład załóżmy, że czy zbyt chcemy pliki hello toorestore*C:\temp*. Umożliwia również założono, że chcemy tooskip pliki, które już istnieją w folderze docelowym hello *C:\temp*. toocreate takie opcję odzyskiwania, użyj hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="89185-268">For this example, let's assume that we want toorestore hello files too*C:\temp*. Let's also assume that we want tooskip files that already exist on hello destination folder *C:\temp*. toocreate such a recovery option, use hello following command:</span></span>

```
PS C:\> $recovery_option = New-OBRecoveryOption -DestinationPath "C:\temp" -OverwriteType Skip
```

<span data-ttu-id="89185-269">Teraz wyzwalanie przywracania przy użyciu hello [Start OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) na powitania wybrane ```$item``` z danych wyjściowych hello hello ```Get-OBRecoverableItem``` polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="89185-269">Now trigger restore by using hello [Start-OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) command on hello selected ```$item``` from hello output of hello ```Get-OBRecoverableItem``` cmdlet:</span></span>

```
PS C:\> Start-OBRecovery -RecoverableItem $item -RecoveryOption $recover_option
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Job completed.
hello recovery operation completed successfully.
```


## <a name="uninstalling-hello-azure-backup-agent"></a><span data-ttu-id="89185-270">Odinstalowanie agenta usługi Kopia zapasowa Azure hello</span><span class="sxs-lookup"><span data-stu-id="89185-270">Uninstalling hello Azure Backup agent</span></span>
<span data-ttu-id="89185-271">Odinstalowanie agenta usługi Kopia zapasowa Azure hello może odbywać się przy użyciu hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="89185-271">Uninstalling hello Azure Backup agent can be done by using hello following command:</span></span>

```
PS C:\> .\MARSAgentInstaller.exe /d /q
```

<span data-ttu-id="89185-272">Odinstalowywanie pliki binarne agenta hello z maszyny hello ma niektórych tooconsider konsekwencje:</span><span class="sxs-lookup"><span data-stu-id="89185-272">Uninstalling hello agent binaries from hello machine has some consequences tooconsider:</span></span>

* <span data-ttu-id="89185-273">Usuwa filtr plików hello z hello maszyny i śledzenie zmian jest zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="89185-273">It removes hello file-filter from hello machine, and tracking of changes is stopped.</span></span>
* <span data-ttu-id="89185-274">Wszystkie informacje o zasadach zostanie usunięty z maszyny hello, ale informacje o zasadach hello nadal toobe przechowywany w usłudze hello.</span><span class="sxs-lookup"><span data-stu-id="89185-274">All policy information is removed from hello machine, but hello policy information continues toobe stored in hello service.</span></span>
* <span data-ttu-id="89185-275">Wszystkie harmonogramy tworzenia kopii zapasowej są usuwane i są pobierane nie dalsze kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="89185-275">All backup schedules are removed, and no further backups are taken.</span></span>

<span data-ttu-id="89185-276">Jednak hello dane przechowywane w pozostaje Azure i są przechowywane zgodnie z ustawień zasad przechowywania hello przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="89185-276">However, hello data stored in Azure remains and is retained as per hello retention policy setup by you.</span></span> <span data-ttu-id="89185-277">Starsze punkty automatycznie są przestarzałe.</span><span class="sxs-lookup"><span data-stu-id="89185-277">Older points are automatically aged out.</span></span>

## <a name="remote-management"></a><span data-ttu-id="89185-278">Zdalne zarządzanie</span><span class="sxs-lookup"><span data-stu-id="89185-278">Remote management</span></span>
<span data-ttu-id="89185-279">Całe Zarządzanie hello wokół hello agenta usługi Kopia zapasowa Azure, zasady i źródłami danych mogą to robić zdalnie za pomocą programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="89185-279">All hello management around hello Azure Backup agent, policies, and data sources can be done remotely through PowerShell.</span></span> <span data-ttu-id="89185-280">Witaj maszyny, który będzie zarządzany zdalnie musi toobe poprawnie przygotowany.</span><span class="sxs-lookup"><span data-stu-id="89185-280">hello machine that will be managed remotely needs toobe prepared correctly.</span></span>

<span data-ttu-id="89185-281">Domyślnie program hello Usługa WinRM jest skonfigurowany do uruchamiania ręcznego.</span><span class="sxs-lookup"><span data-stu-id="89185-281">By default, hello WinRM service is configured for manual startup.</span></span> <span data-ttu-id="89185-282">musi być zbyt ustawionym typem uruchomienia Hello*automatyczne* i hello usługi powinny być uruchamiane.</span><span class="sxs-lookup"><span data-stu-id="89185-282">hello startup type must be set too*Automatic* and hello service should be started.</span></span> <span data-ttu-id="89185-283">tooverify, który hello Usługa WinRM jest uruchomiona, musi mieć wartość hello hello właściwość stanu *systemem*.</span><span class="sxs-lookup"><span data-stu-id="89185-283">tooverify that hello WinRM service is running, hello value of hello Status property should be *Running*.</span></span>

```
PS C:\> Get-Service WinRM

Status   Name               DisplayName
------   ----               -----------
Running  winrm              Windows Remote Management (WS-Manag...
```

<span data-ttu-id="89185-284">Programu PowerShell, należy skonfigurować dla niego komunikację zdalną.</span><span class="sxs-lookup"><span data-stu-id="89185-284">PowerShell should be configured for remoting.</span></span>

```
PS C:\> Enable-PSRemoting -force
WinRM is already set up tooreceive requests on this computer.
WinRM has been updated for remote management.
WinRM firewall exception enabled.

PS C:\> Set-ExecutionPolicy unrestricted -force
```

<span data-ttu-id="89185-285">maszyny Hello teraz można zarządzać zdalnie — począwszy od instalacji hello hello agenta.</span><span class="sxs-lookup"><span data-stu-id="89185-285">hello machine can now be managed remotely - starting from hello installation of hello agent.</span></span> <span data-ttu-id="89185-286">Na przykład hello następującego skryptu kopiuje hello maszyny zdalnej toohello agenta i instaluje je.</span><span class="sxs-lookup"><span data-stu-id="89185-286">For example, hello following script copies hello agent toohello remote machine and installs it.</span></span>

```
PS C:\> $dloc = "\\REMOTESERVER01\c$\Windows\Temp"
PS C:\> $agent = "\\REMOTESERVER01\c$\Windows\Temp\MARSAgentInstaller.exe"
PS C:\> $args = "/q"
PS C:\> Copy-Item "C:\Downloads\MARSAgentInstaller.exe" -Destination $dloc - force

PS C:\> $s = New-PSSession -ComputerName REMOTESERVER01
PS C:\> Invoke-Command -Session $s -Script { param($d, $a) Start-Process -FilePath $d $a -Wait } -ArgumentList $agent $args
```

## <a name="next-steps"></a><span data-ttu-id="89185-287">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="89185-287">Next steps</span></span>
<span data-ttu-id="89185-288">Aby uzyskać więcej informacji o kopii zapasowej dla systemu Windows Server/klienta Azure, zobacz</span><span class="sxs-lookup"><span data-stu-id="89185-288">For more information about Azure Backup for Windows Server/Client see</span></span>

* [<span data-ttu-id="89185-289">Wprowadzenie tooAzure kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="89185-289">Introduction tooAzure Backup</span></span>](backup-introduction-to-azure-backup.md)
* [<span data-ttu-id="89185-290">Wykonaj kopię zapasową serwerów z systemem Windows</span><span class="sxs-lookup"><span data-stu-id="89185-290">Back up Windows Servers</span></span>](backup-configure-vault.md)
