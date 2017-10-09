---
title: " Zarządzanie serwerem konfiguracji w usłudze Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób tooset i zarządzać serwerem konfiguracji."
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: 2852bcd25409121be46a1ebf135ebfcdce6e5de5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-configuration-server"></a><span data-ttu-id="0db5f-103">Zarządzanie serwerem konfiguracji</span><span class="sxs-lookup"><span data-stu-id="0db5f-103">Manage a Configuration Server</span></span>

<span data-ttu-id="0db5f-104">Serwer konfiguracji pełni funkcję koordynatora między hello usługi Site Recovery i infrastruktury lokalnej.</span><span class="sxs-lookup"><span data-stu-id="0db5f-104">Configuration Server acts as a coordinator between hello Site Recovery services and your on-premises infrastructure.</span></span> <span data-ttu-id="0db5f-105">W tym artykule opisano, jak można skonfigurować, konfigurowania i zarządzania powitania serwera konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="0db5f-105">This article describes how you can set up, configure, and manage hello Configuration Server.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0db5f-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="0db5f-106">Prerequisites</span></span>
<span data-ttu-id="0db5f-107">Witaj poniżej przedstawiono hello minimalne wymagania dotyczące sprzętu, oprogramowania i sieci tooset wymagana jest konfiguracja serwera konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="0db5f-107">hello following are hello minimum hardware, software, and network configuration required tooset up a Configuration Server.</span></span>

> [!NOTE]
> <span data-ttu-id="0db5f-108">[Planowanie pojemności](site-recovery-capacity-planner.md) jest tooensure ważnym krokiem wdrażania powitania serwera konfiguracji z konfiguracją tego pakiety wymagań obciążenia.</span><span class="sxs-lookup"><span data-stu-id="0db5f-108">[Capacity planning](site-recovery-capacity-planner.md) is an important step tooensure that you deploy hello Configuration Server with a configuration that suites your load requirements.</span></span> <span data-ttu-id="0db5f-109">Przeczytaj więcej na temat [zmiany rozmiaru wymagania dotyczące serwera konfiguracji](#sizing-requirements-for-a-configuration-server).</span><span class="sxs-lookup"><span data-stu-id="0db5f-109">Read more about [Sizing requirements for a Configuration Server](#sizing-requirements-for-a-configuration-server).</span></span>

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-hello-configuration-server-software"></a><span data-ttu-id="0db5f-110">Pobieranie powitania serwera konfiguracji oprogramowania</span><span class="sxs-lookup"><span data-stu-id="0db5f-110">Downloading hello Configuration Server software</span></span>
1. <span data-ttu-id="0db5f-111">Zaloguj się na toohello Azure tooyour portalu i przeglądania magazynu usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="0db5f-111">Log on toohello Azure portal and browse tooyour Recovery Services Vault.</span></span>
2. <span data-ttu-id="0db5f-112">Przeglądaj zbyt**infrastruktura usługi Site Recovery** > **serwery konfiguracji** (w przypadku VMware i maszyn fizycznych).</span><span class="sxs-lookup"><span data-stu-id="0db5f-112">Browse too**Site Recovery Infrastructure** > **Configuration Servers** (under For VMware & Physical Machines).</span></span>

  ![Dodaj stronę serwerów](./media/site-recovery-vmware-to-azure-manage-configuration-server/AddServers.png)
3. <span data-ttu-id="0db5f-114">Kliknij przycisk hello **+ serwery** przycisku.</span><span class="sxs-lookup"><span data-stu-id="0db5f-114">Click hello **+Servers** button.</span></span>
4. <span data-ttu-id="0db5f-115">Na powitania **Dodaj serwer** kliknij klucz rejestracji hello toodownload hello pobierania przycisku.</span><span class="sxs-lookup"><span data-stu-id="0db5f-115">On hello **Add Server** page, click hello Download button toodownload hello Registration key.</span></span> <span data-ttu-id="0db5f-116">Ten klucz jest potrzebne podczas tooregister instalacji serwera konfiguracji hello za pomocą usługi Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="0db5f-116">You need this key during hello Configuration Server installation tooregister it with Azure Site Recovery service.</span></span>
5. <span data-ttu-id="0db5f-117">Kliknij przycisk hello **hello pobierania Instalatora Microsoft Azure Site Recovery Unified** łącze toodownload hello najnowszą wersję powitania serwera konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="0db5f-117">Click hello **Download hello Microsoft Azure Site Recovery Unified Setup** link toodownload hello latest version of hello Configuration Server.</span></span>

  ![Strona pobierania](./media/site-recovery-vmware-to-azure-manage-configuration-server/downloadcs.png)

  > [!TIP]
  <span data-ttu-id="0db5f-119">Można pobrać najnowszą wersję powitania serwera konfiguracji bezpośrednio z [strony pobierania witryny Microsoft Download Center](http://aka.ms/unifiedsetup)</span><span class="sxs-lookup"><span data-stu-id="0db5f-119">Latest version of hello Configuration Server can be downloaded directly from [Microsoft Download Center download page](http://aka.ms/unifiedsetup)</span></span>

## <a name="installing-and-registering-a-configuration-server-from-gui"></a><span data-ttu-id="0db5f-120">Instalowanie i rejestrowanie konfiguracji serwer z graficznym interfejsem użytkownika</span><span class="sxs-lookup"><span data-stu-id="0db5f-120">Installing and Registering a Configuration Server from GUI</span></span>
[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

## <a name="installing-and-registering-a-configuration-server-using-command-line"></a><span data-ttu-id="0db5f-121">Instalowanie i rejestrowanie serwera konfiguracji przy użyciu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="0db5f-121">Installing and registering a Configuration Server using Command line</span></span>

  ```
  UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address toobe used for data transfer] [/CSIP <IP address of CS toobe registered with>] [/PassphraseFilePath <Passphrase file path>]
  ```

### <a name="sample-usage"></a><span data-ttu-id="0db5f-122">Przykładowe zastosowanie</span><span class="sxs-lookup"><span data-stu-id="0db5f-122">Sample usage</span></span>
  ```
  MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /xC:\Temp\Extracted
  cd C:\Temp\Extracted
  UNIFIEDSETUP.EXE /AcceptThirdpartyEULA /servermode "CS" /InstallLocation "D:\" /MySQLCredsFilePath "C:\Temp\MySQLCredentialsfile.txt" /VaultCredsFilePath "C:\Temp\MyVault.vaultcredentials" /EnvType "VMWare"
  ```


### <a name="configuration-server-installer-command-line-arguments"></a><span data-ttu-id="0db5f-123">Serwer konfiguracji Instalator argumenty wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="0db5f-123">Configuration Server installer command-line arguments.</span></span>
[!INCLUDE [site-recovery-unified-setup-parameters](../../includes/site-recovery-unified-installer-command-parameters.md)]


### <a name="create-a-mysql-credentials-file"></a><span data-ttu-id="0db5f-124">Utwórz plik poświadczeń MySql</span><span class="sxs-lookup"><span data-stu-id="0db5f-124">Create a MySql credentials file</span></span>
<span data-ttu-id="0db5f-125">Parametr MySQLCredsFilePath przyjmuje pliku jako dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="0db5f-125">MySQLCredsFilePath parameter takes a file as input.</span></span> <span data-ttu-id="0db5f-126">Tworzenie pliku hello przy użyciu hello następujący format i przekaż go jako parametr wejściowy MySQLCredsFilePath.</span><span class="sxs-lookup"><span data-stu-id="0db5f-126">Create hello file using hello following format and pass it as input MySQLCredsFilePath parameter.</span></span>
```
[MySQLCredentials]
MySQLRootPassword = "Password>"
MySQLUserPassword = "Password"
```
### <a name="create-a-proxy-settings-configuration-file"></a><span data-ttu-id="0db5f-127">Utwórz plik konfiguracji ustawień serwera proxy</span><span class="sxs-lookup"><span data-stu-id="0db5f-127">Create a proxy settings configuration file</span></span>
<span data-ttu-id="0db5f-128">Parametr ProxySettingsFilePath przyjmuje pliku jako dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="0db5f-128">ProxySettingsFilePath parameter takes a file as input.</span></span> <span data-ttu-id="0db5f-129">Tworzenie pliku hello przy użyciu hello następujący format i przekaż go jako parametr wejściowy ProxySettingsFilePath.</span><span class="sxs-lookup"><span data-stu-id="0db5f-129">Create hello file using hello following format and pass it as input ProxySettingsFilePath parameter.</span></span>

```
[ProxySettings]
ProxyAuthentication = "Yes/No"
Proxy IP = "IP Address"
ProxyPort = "Port"
ProxyUserName="UserName"
ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-configuration-server"></a><span data-ttu-id="0db5f-130">Modyfikowanie ustawień konfiguracji serwera proxy</span><span class="sxs-lookup"><span data-stu-id="0db5f-130">Modifying proxy settings for Configuration Server</span></span>
1. <span data-ttu-id="0db5f-131">Tooyour logowania serwera konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="0db5f-131">Login tooyour Configuration Server.</span></span>
2. <span data-ttu-id="0db5f-132">Uruchamianie cspsconfigtool.exe hello za pomocą skrótu hello na użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0db5f-132">Launch hello cspsconfigtool.exe using hello shortcut on your.</span></span>
3. <span data-ttu-id="0db5f-133">Kliknij przycisk hello **rejestracji magazynu** kartę.</span><span class="sxs-lookup"><span data-stu-id="0db5f-133">Click hello **Vault Registration** tab.</span></span>
4. <span data-ttu-id="0db5f-134">Pobranie nowego pliku magazynu rejestracji z portalu hello i przekazują je jako narzędzie toohello wejściowego.</span><span class="sxs-lookup"><span data-stu-id="0db5f-134">Download a new Vault Registration file from hello portal and provide it as input toohello tool.</span></span>

  ![serwer w przypadku konfiguracji rejestru](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
5. <span data-ttu-id="0db5f-136">Podaj nowe szczegóły serwera Proxy hello i kliknij przycisk hello **zarejestrować** przycisku.</span><span class="sxs-lookup"><span data-stu-id="0db5f-136">Provide hello new Proxy Server details and click hello **Register** button.</span></span>
6. <span data-ttu-id="0db5f-137">Otwórz okno poleceń programu PowerShell administratora.</span><span class="sxs-lookup"><span data-stu-id="0db5f-137">Open an Admin PowerShell command window.</span></span>
7. <span data-ttu-id="0db5f-138">Uruchom następujące polecenie hello</span><span class="sxs-lookup"><span data-stu-id="0db5f-138">Run hello following command</span></span>
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```

  >[!WARNING]
  <span data-ttu-id="0db5f-139">Jeśli proces skalowania w poziomie serwery podłączone toothis konfiguracji serwera, należy za[napraw hello ustawienia serwera proxy na wszystkich serwerach proces skalowania w poziomie hello](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#modifying-proxy-settings-for-scale-out-process-server) w danym wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="0db5f-139">If you have Scale-out Process servers attached toothis Configuration Server, you need too[fix hello proxy settings on all hello scale-out process servers](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#modifying-proxy-settings-for-scale-out-process-server) in your deployment.</span></span>

## <a name="re-register-a-configuration-server-with-hello-same-recovery-services-vault"></a><span data-ttu-id="0db5f-140">Zarejestruj ponownie serwer konfiguracji hello tego samego magazynu usług odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="0db5f-140">Re-register a Configuration Server with hello same Recovery Services Vault</span></span>
  1. <span data-ttu-id="0db5f-141">Tooyour logowania serwera konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="0db5f-141">Login tooyour Configuration Server.</span></span>
  2. <span data-ttu-id="0db5f-142">Uruchom program hello cspsconfigtool.exe za pomocą hello skrótu na pulpicie.</span><span class="sxs-lookup"><span data-stu-id="0db5f-142">Launch hello cspsconfigtool.exe using hello shortcut on your desktop.</span></span>
  3. <span data-ttu-id="0db5f-143">Kliknij przycisk hello **rejestracji magazynu** kartę.</span><span class="sxs-lookup"><span data-stu-id="0db5f-143">Click hello **Vault Registration** tab.</span></span>
  4. <span data-ttu-id="0db5f-144">Pobranie nowego pliku rejestracji z portalu hello i przekazują je jako narzędzie toohello wejściowego.</span><span class="sxs-lookup"><span data-stu-id="0db5f-144">Download a new Registration file from hello portal and provide it as input toohello tool.</span></span>
        <span data-ttu-id="0db5f-145">![serwer w przypadku konfiguracji rejestru](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)</span><span class="sxs-lookup"><span data-stu-id="0db5f-145">![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)</span></span>
  5. <span data-ttu-id="0db5f-146">Podaj szczegóły serwera Proxy hello, a następnie kliknij przycisk hello **zarejestrować** przycisku.</span><span class="sxs-lookup"><span data-stu-id="0db5f-146">Provide hello Proxy Server details and click hello **Register** button.</span></span>  
  6. <span data-ttu-id="0db5f-147">Otwórz okno poleceń programu PowerShell administratora.</span><span class="sxs-lookup"><span data-stu-id="0db5f-147">Open an Admin PowerShell command window.</span></span>
  7. <span data-ttu-id="0db5f-148">Uruchom następujące polecenie hello</span><span class="sxs-lookup"><span data-stu-id="0db5f-148">Run hello following command</span></span>

      ```
      $pwd = ConvertTo-SecureString -String MyProxyUserPassword
      Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
      net stop obengine
      net start obengine
      ```

  >[!WARNING]
  <span data-ttu-id="0db5f-149">Jeśli proces skalowania w poziomie serwery podłączone toothis konfiguracji serwera, należy za[ponownie zarejestrować wszystkie serwery proces skalowania w poziomie hello](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#re-registering-a-scale-out-process-server) w danym wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="0db5f-149">If you have Scale-out Process servers attached toothis Configuration Server, you need too[re-register all hello scale-out process servers](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#re-registering-a-scale-out-process-server) in your deployment.</span></span>

## <a name="registering-a-configuration-server-with-a-different-recovery-services-vault"></a><span data-ttu-id="0db5f-150">Rejestrowanie serwera konfiguracji w innym magazynie usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="0db5f-150">Registering a Configuration Server with a different Recovery Services Vault.</span></span>
1. <span data-ttu-id="0db5f-151">Tooyour logowania serwera konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="0db5f-151">Login tooyour Configuration Server.</span></span>
2. <span data-ttu-id="0db5f-152">z wiersza polecenia z uprawnieniami administratora uruchom polecenie hello</span><span class="sxs-lookup"><span data-stu-id="0db5f-152">from an admin command prompt, run hello command</span></span>

```
reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
net stop dra
```
3. <span data-ttu-id="0db5f-153">Uruchamianie cspsconfigtool.exe hello za pomocą skrótu hello na użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0db5f-153">Launch hello cspsconfigtool.exe using hello shortcut on your.</span></span>
4. <span data-ttu-id="0db5f-154">Kliknij przycisk hello **rejestracji magazynu** kartę.</span><span class="sxs-lookup"><span data-stu-id="0db5f-154">Click hello **Vault Registration** tab.</span></span>
5. <span data-ttu-id="0db5f-155">Pobranie nowego pliku rejestracji z portalu hello i przekazują je jako narzędzie toohello wejściowego.</span><span class="sxs-lookup"><span data-stu-id="0db5f-155">Download a new Registration file from hello portal and provide it as input toohello tool.</span></span>

    ![serwer w przypadku konfiguracji rejestru](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
6. <span data-ttu-id="0db5f-157">Podaj szczegóły serwera Proxy hello, a następnie kliknij przycisk hello **zarejestrować** przycisku.</span><span class="sxs-lookup"><span data-stu-id="0db5f-157">Provide hello Proxy Server details and click hello **Register** button.</span></span>  
7. <span data-ttu-id="0db5f-158">Otwórz okno poleceń programu PowerShell administratora.</span><span class="sxs-lookup"><span data-stu-id="0db5f-158">Open an Admin PowerShell command window.</span></span>
8. <span data-ttu-id="0db5f-159">Uruchom następujące polecenie hello</span><span class="sxs-lookup"><span data-stu-id="0db5f-159">Run hello following command</span></span>
    ```
    $pwd = ConvertTo-SecureString -String MyProxyUserPassword
    Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
    net stop obengine
    net start obengine
    ```

## <a name="decommissioning-a-configuration-server"></a><span data-ttu-id="0db5f-160">Wycofanie z eksploatacji serwera konfiguracji</span><span class="sxs-lookup"><span data-stu-id="0db5f-160">Decommissioning a Configuration Server</span></span>
<span data-ttu-id="0db5f-161">Upewnij się, poniżej hello przed rozpoczęciem likwidowania serwera konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="0db5f-161">Ensure hello following before you start decommissioning your Configuration Server.</span></span>
1. <span data-ttu-id="0db5f-162">Wyłącz ochronę dla wszystkich maszyn wirtualnych na tym serwerze konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="0db5f-162">Disable protection for all virtual machines under this Configuration Server.</span></span>
2. <span data-ttu-id="0db5f-163">Usuń skojarzenie wszystkich zasad replikacji z powitania serwera konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="0db5f-163">Disassociate all Replication policies from hello Configuration Server.</span></span>
3. <span data-ttu-id="0db5f-164">Usuń wszystkie hosty serwerów/vSphere Vcenter, które są toohello skojarzone serwerem konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="0db5f-164">Delete all vCenters servers/vSphere hosts that are associated toohello Configuration Server.</span></span>

### <a name="delete-hello-configuration-server-from-azure-portal"></a><span data-ttu-id="0db5f-165">Usuń powitania serwera konfiguracji z portalu Azure</span><span class="sxs-lookup"><span data-stu-id="0db5f-165">Delete hello Configuration Server from Azure portal</span></span>
1. <span data-ttu-id="0db5f-166">W portalu Azure Przejdź zbyt**infrastruktura usługi Site Recovery** > **serwery konfiguracji** hello magazynu menu.</span><span class="sxs-lookup"><span data-stu-id="0db5f-166">In Azure portal, browse too**Site Recovery Infrastructure** > **Configuration Servers** from hello Vault menu.</span></span>
2. <span data-ttu-id="0db5f-167">Kliknij przycisk powitania serwera konfiguracji, które mają toodecommission.</span><span class="sxs-lookup"><span data-stu-id="0db5f-167">Click hello Configuration Server that you want toodecommission.</span></span>
3. <span data-ttu-id="0db5f-168">Na stronie szczegółów hello konfiguracji serwera kliknij przycisk Usuń hello.</span><span class="sxs-lookup"><span data-stu-id="0db5f-168">On hello Configuration Server's details page, click hello Delete button.</span></span>

  ![Usuwanie konfiguracji serwera](./media/site-recovery-vmware-to-azure-manage-configuration-server/delete-configuration-server.PNG)
4. <span data-ttu-id="0db5f-170">Kliknij przycisk **tak** tooconfirm hello usunięcia powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="0db5f-170">Click **Yes** tooconfirm hello deletion of hello server.</span></span>

  >[!WARNING]
  <span data-ttu-id="0db5f-171">Jeśli masz maszyny wirtualne, zasady replikacji lub hostów serwerów/vSphere vCenter skojarzone z tym serwerem konfiguracji, nie można usunąć serwera hello.</span><span class="sxs-lookup"><span data-stu-id="0db5f-171">If you have any virtual machines, Replication policies or vCenter servers/vSphere hosts associated with this Configuration Server, you cannot delete hello server.</span></span> <span data-ttu-id="0db5f-172">Przed podjęciem próby toodelete hello magazynu, należy usunąć te jednostki.</span><span class="sxs-lookup"><span data-stu-id="0db5f-172">Delete these entities before you try toodelete hello vault.</span></span>

### <a name="uninstall-hello-configuration-server-software-and-its-dependencies"></a><span data-ttu-id="0db5f-173">Odinstaluj powitania serwera konfiguracji oprogramowania i jego zależności</span><span class="sxs-lookup"><span data-stu-id="0db5f-173">Uninstall hello Configuration Server software and its dependencies</span></span>
  > [!TIP]
  <span data-ttu-id="0db5f-174">Jeśli planujesz ponownie hello tooreuse konfiguracji serwera z usługą Azure Site Recovery, następnie można pominąć toostep 4 bezpośrednio</span><span class="sxs-lookup"><span data-stu-id="0db5f-174">If you plan tooreuse hello Configuration Server with Azure Site Recovery again, then you can skip toostep 4 directly</span></span>

1. <span data-ttu-id="0db5f-175">Zaloguj się na toohello serwer konfiguracji jako Administrator.</span><span class="sxs-lookup"><span data-stu-id="0db5f-175">Log on toohello Configuration Server as an Administrator.</span></span>
2. <span data-ttu-id="0db5f-176">Otwórz Panel sterowania > Program > Odinstaluj programy</span><span class="sxs-lookup"><span data-stu-id="0db5f-176">Open up Control Panel > Program > Uninstall Programs</span></span>
3. <span data-ttu-id="0db5f-177">Odinstaluj programy hello w hello w następującej kolejności:</span><span class="sxs-lookup"><span data-stu-id="0db5f-177">Uninstall hello programs in hello following sequence:</span></span>
  * <span data-ttu-id="0db5f-178">Agent usług Microsoft Azure Recovery Services</span><span class="sxs-lookup"><span data-stu-id="0db5f-178">Microsoft Azure Recovery Services Agent</span></span>
  * <span data-ttu-id="0db5f-179">Microsoft Azure Site odzyskiwania mobilności usługi/główny serwer docelowy</span><span class="sxs-lookup"><span data-stu-id="0db5f-179">Microsoft Azure Site Recovery Mobility Service/Master Target server</span></span>
  * <span data-ttu-id="0db5f-180">Dostawcy usługi Microsoft Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="0db5f-180">Microsoft Azure Site Recovery Provider</span></span>
  * <span data-ttu-id="0db5f-181">Serwer procesu/serwera konfiguracji odzyskiwania witryny Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="0db5f-181">Microsoft Azure Site Recovery Configuration Server/Process Server</span></span>
  * <span data-ttu-id="0db5f-182">Microsoft Azure Site odzyskiwania konfiguracji serwera zależności</span><span class="sxs-lookup"><span data-stu-id="0db5f-182">Microsoft Azure Site Recovery Configuration Server Dependencies</span></span>
  * <span data-ttu-id="0db5f-183">Serwer MySQL 5,5</span><span class="sxs-lookup"><span data-stu-id="0db5f-183">MySQL Server 5.5</span></span>
4. <span data-ttu-id="0db5f-184">Uruchom następujące polecenie z hello i wiersza polecenia administratora.</span><span class="sxs-lookup"><span data-stu-id="0db5f-184">Run hello following command from and admin command prompt.</span></span>
  ```
  reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
  ```

## <a name="renew-configuration-server-secure-socket-layerssl-certificates"></a><span data-ttu-id="0db5f-185">Odnów certyfikaty Layer(SSL) SSL serwera konfiguracji</span><span class="sxs-lookup"><span data-stu-id="0db5f-185">Renew Configuration Server Secure Socket Layer(SSL) Certificates</span></span>
<span data-ttu-id="0db5f-186">powitania serwera konfiguracji ma wbudowane serwer sieci Web, która organizuje działania hello hello usługi mobilności serwerów procesu i docelowego elementu głównego serwery połączone toohello serwera konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="0db5f-186">hello Configuration Server has an inbuilt webserver, which orchestrates hello activities of hello Mobility Service, Process Servers, and Master Target servers connected toohello Configuration Server.</span></span> <span data-ttu-id="0db5f-187">Serwer konfiguracji Hello serwer sieci Web używa tooauthenticate certyfikatu SSL klientów.</span><span class="sxs-lookup"><span data-stu-id="0db5f-187">hello Configuration Server's webserver uses an SSL certificate tooauthenticate its clients.</span></span> <span data-ttu-id="0db5f-188">Ten certyfikat ma okres ważności trzech lat i mogą być odnawiane w dowolnej chwili za pomocą hello następujące metody:</span><span class="sxs-lookup"><span data-stu-id="0db5f-188">This certificate has an expiry of three years and can be renewed at any time using hello following method:</span></span>

> [!WARNING]
<span data-ttu-id="0db5f-189">Okresu ważności certyfikatu można wykonywać tylko w wersji 9.4.XXXX. X lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="0db5f-189">Certificate expiry can be performed only on version 9.4.XXXX.X or higher.</span></span> <span data-ttu-id="0db5f-190">Uaktualnij wszystkie hello składniki usługi Azure Site Recovery (serwer konfiguracji, serwer przetwarzania, głównego serwera docelowego, usługa mobilności) przed rozpoczęciem hello odnowić certyfikaty w przepływie pracy.</span><span class="sxs-lookup"><span data-stu-id="0db5f-190">Upgrade all hello Azure Site Recovery components (Configuration Server, Process Server, Master Target Server, Mobility Service) before you start hello Renew Certificates workflow.</span></span>

1. <span data-ttu-id="0db5f-191">Na hello portalu Azure, przejdź tooyour magazynu > infrastruktura usługi Site Recovery > serwer konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="0db5f-191">On hello Azure portal, browse tooyour Vault > Site Recovery Infrastructure > Configuration Server.</span></span>
2. <span data-ttu-id="0db5f-192">Kliknij serwer konfiguracji hello, dla których potrzebujesz toorenew hello certyfikat SSL do.</span><span class="sxs-lookup"><span data-stu-id="0db5f-192">Click hello Configuration Server for which you need toorenew hello SSL Certificate for.</span></span>
3. <span data-ttu-id="0db5f-193">W obszarze hello kondycji serwera konfiguracji widać datę wygaśnięcia hello hello certyfikatu SSL.</span><span class="sxs-lookup"><span data-stu-id="0db5f-193">Under hello Configuration Server health, you can see hello expiry date for hello SSL Certificate.</span></span>
4. <span data-ttu-id="0db5f-194">Odnów certyfikat hello klikając hello **odnowić certyfikaty** akcji, jak pokazano w powitania po obrazu:</span><span class="sxs-lookup"><span data-stu-id="0db5f-194">Renew hello certificate by clicking hello **Renew Certificates** action as shown in hello following image:</span></span>

  ![Usuwanie konfiguracji serwera](./media/site-recovery-vmware-to-azure-manage-configuration-server/renew-cert-page.png)

### <a name="secure-socket-layer-certificate-expiry-warning"></a><span data-ttu-id="0db5f-196">Secure Socket Layer ostrzeżenie o wygaśnięciu certyfikatu</span><span class="sxs-lookup"><span data-stu-id="0db5f-196">Secure Socket Layer certificate expiry warning</span></span>

> [!NOTE]
<span data-ttu-id="0db5f-197">Witaj ważności certyfikatu SSL dla wszystkich instalacji, które wystąpiły przed maj 2016 ustawiono tooone roku.</span><span class="sxs-lookup"><span data-stu-id="0db5f-197">hello SSL Certificate's validity for all installations that happened before May 2016 was set tooone year.</span></span> <span data-ttu-id="0db5f-198">Wyświetlanie wyświetlane w portalu Azure hello powiadomienia o wygasaniu certyfikatów zostały uruchomione.</span><span class="sxs-lookup"><span data-stu-id="0db5f-198">you have started seeing certificate expiry notifications showing up in hello Azure portal.</span></span>

1. <span data-ttu-id="0db5f-199">Jeśli certyfikat SSL serwera konfiguracji hello mają tooexpire w hello przyszłych dwóch miesięcy, usługa hello jest uruchamiana powiadamiania użytkowników za pośrednictwem hello portalu Azure i poczty e-mail (należy toobe subskrybowane tooAzure usługi Site Recovery powiadomienia).</span><span class="sxs-lookup"><span data-stu-id="0db5f-199">If hello Configuration Server's SSL certificate is going tooexpire in hello next two months, hello service starts notifying users via hello Azure portal & email (you need toobe subscribed tooAzure Site Recovery notifications).</span></span> <span data-ttu-id="0db5f-200">Możesz uruchomić wyświetlany na stronie zasobów magazynu hello transparencie powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="0db5f-200">You start seeing a notification banner on hello Vault's resource page.</span></span>

  ![certyfikat powiadomień](./media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-renew-notification.png)
2. <span data-ttu-id="0db5f-202">Kliknij przycisk hello transparent tooget dodatkowe szczegóły dotyczące hello okresu ważności certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="0db5f-202">Click hello banner tooget additional details on hello Certificate expiry.</span></span>

  ![Szczegóły certyfikatu](./media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-expiry-details.png)

  >[!TIP]
  <span data-ttu-id="0db5f-204">Jeśli zamiast **odnowić teraz** przycisk widzisz **Uaktualnij teraz** przycisku.</span><span class="sxs-lookup"><span data-stu-id="0db5f-204">If instead of a **Renew Now** button you see an **Upgrade Now** button.</span></span> <span data-ttu-id="0db5f-205">Oznacza to, czy niektóre składniki w danym środowisku, które nie zostały jeszcze uaktualniony too9.4.xxxx.x lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="0db5f-205">This means that there are some components in your environment that have not yet been upgraded too9.4.xxxx.x or higher versions.</span></span>

## <a name="sizing-requirements-for-a-configuration-server"></a><span data-ttu-id="0db5f-206">Ustawianie rozmiaru wymagania dotyczące serwera konfiguracji</span><span class="sxs-lookup"><span data-stu-id="0db5f-206">Sizing requirements for a Configuration Server</span></span>

| <span data-ttu-id="0db5f-207">**PROCESOR CPU**</span><span class="sxs-lookup"><span data-stu-id="0db5f-207">**CPU**</span></span> | <span data-ttu-id="0db5f-208">**Pamięci**</span><span class="sxs-lookup"><span data-stu-id="0db5f-208">**Memory**</span></span> | <span data-ttu-id="0db5f-209">**Rozmiar pamięci podręcznej dysku**</span><span class="sxs-lookup"><span data-stu-id="0db5f-209">**Cache disk size**</span></span> | <span data-ttu-id="0db5f-210">**Częstotliwość zmian danych**</span><span class="sxs-lookup"><span data-stu-id="0db5f-210">**Data change rate**</span></span> | <span data-ttu-id="0db5f-211">**Chronione maszyny**</span><span class="sxs-lookup"><span data-stu-id="0db5f-211">**Protected machines**</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="0db5f-212">8 Vcpu (2 sockets * 4 rdzenie @ 2,5 GHz)</span><span class="sxs-lookup"><span data-stu-id="0db5f-212">8 vCPUs (2 sockets * 4 cores @ 2.5 GHz)</span></span> |<span data-ttu-id="0db5f-213">16 GB</span><span class="sxs-lookup"><span data-stu-id="0db5f-213">16 GB</span></span> |<span data-ttu-id="0db5f-214">300 GB</span><span class="sxs-lookup"><span data-stu-id="0db5f-214">300 GB</span></span> |<span data-ttu-id="0db5f-215">500 GB lub mniej</span><span class="sxs-lookup"><span data-stu-id="0db5f-215">500 GB or less</span></span> |<span data-ttu-id="0db5f-216">Replikowanie maszyn mniej niż 100.</span><span class="sxs-lookup"><span data-stu-id="0db5f-216">Replicate fewer than 100 machines.</span></span> |
| <span data-ttu-id="0db5f-217">12 Vcpu (2 sockets * 6 rdzeni @ 2,5 GHz)</span><span class="sxs-lookup"><span data-stu-id="0db5f-217">12 vCPUs (2 sockets * 6 cores @ 2.5 GHz)</span></span> |<span data-ttu-id="0db5f-218">18 GB</span><span class="sxs-lookup"><span data-stu-id="0db5f-218">18 GB</span></span> |<span data-ttu-id="0db5f-219">600 GB</span><span class="sxs-lookup"><span data-stu-id="0db5f-219">600 GB</span></span> |<span data-ttu-id="0db5f-220">TB too1 500 GB</span><span class="sxs-lookup"><span data-stu-id="0db5f-220">500 GB too1 TB</span></span> |<span data-ttu-id="0db5f-221">Replikują między 100 150 maszyn.</span><span class="sxs-lookup"><span data-stu-id="0db5f-221">Replicate between 100-150 machines.</span></span> |
| <span data-ttu-id="0db5f-222">16 Vcpu (2 sockets * 8 rdzeni @ 2,5 GHz)</span><span class="sxs-lookup"><span data-stu-id="0db5f-222">16 vCPUs (2 sockets * 8 cores @ 2.5 GHz)</span></span> |<span data-ttu-id="0db5f-223">32 GB</span><span class="sxs-lookup"><span data-stu-id="0db5f-223">32 GB</span></span> |<span data-ttu-id="0db5f-224">1 TB</span><span class="sxs-lookup"><span data-stu-id="0db5f-224">1 TB</span></span> |<span data-ttu-id="0db5f-225">1 TB too2 TB</span><span class="sxs-lookup"><span data-stu-id="0db5f-225">1 TB too2 TB</span></span> |<span data-ttu-id="0db5f-226">Replikują między 150 – 200 maszyn.</span><span class="sxs-lookup"><span data-stu-id="0db5f-226">Replicate between 150-200 machines.</span></span> |

  >[!TIP]
  <span data-ttu-id="0db5f-227">Jeśli codziennych zmian ilości danych przekracza 2 TB, lub planujesz tooreplicate ponad 200 maszyn wirtualnych, zalecane jest toodeploy procesu dodatkowe serwery tooload saldo hello ruch związany z replikacją.</span><span class="sxs-lookup"><span data-stu-id="0db5f-227">If your daily data churn exceeds 2 TB, or you plan tooreplicate more than 200 virtual machines, it is recommended toodeploy additional process servers tooload balance hello replication traffic.</span></span> <span data-ttu-id="0db5f-228">Dowiedz się więcej na temat sposobu serwery toodeploy proces skalowania w poziomie.</span><span class="sxs-lookup"><span data-stu-id="0db5f-228">Learn more about How toodeploy Scale-out Process severs.</span></span>


## <a name="common-issues"></a><span data-ttu-id="0db5f-229">Typowe problemy</span><span class="sxs-lookup"><span data-stu-id="0db5f-229">Common issues</span></span>
[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]
