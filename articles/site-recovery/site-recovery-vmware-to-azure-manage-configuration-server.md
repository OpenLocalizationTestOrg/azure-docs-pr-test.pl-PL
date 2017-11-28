---
title: " Zarządzanie serwerem konfiguracji w usłudze Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób i zarządzanie serwerem konfiguracji."
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
ms.openlocfilehash: 36da8c7d0f3ace194522e5288f26069cf46d470e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-a-configuration-server"></a><span data-ttu-id="d655d-103">Zarządzanie serwerem konfiguracji</span><span class="sxs-lookup"><span data-stu-id="d655d-103">Manage a Configuration Server</span></span>

<span data-ttu-id="d655d-104">Serwer konfiguracji pełni funkcję koordynatora między usługi Site Recovery i infrastruktury lokalnej.</span><span class="sxs-lookup"><span data-stu-id="d655d-104">Configuration Server acts as a coordinator between the Site Recovery services and your on-premises infrastructure.</span></span> <span data-ttu-id="d655d-105">W tym artykule opisano, jak można skonfigurować, skonfigurować i zarządzać serwerem konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="d655d-105">This article describes how you can set up, configure, and manage the Configuration Server.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d655d-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d655d-106">Prerequisites</span></span>
<span data-ttu-id="d655d-107">Poniżej przedstawiono minimalne wymagania dotyczące sprzętu, oprogramowania i konfiguracji sieci wymagane do skonfigurowania serwera konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="d655d-107">The following are the minimum hardware, software, and network configuration required to set up a Configuration Server.</span></span>

> [!NOTE]
> <span data-ttu-id="d655d-108">[Planowanie pojemności](site-recovery-capacity-planner.md) jest to ważny krok, aby zapobiec wdrażaniu serwera konfiguracji z konfiguracją tego zestawy wymagań obciążenia.</span><span class="sxs-lookup"><span data-stu-id="d655d-108">[Capacity planning](site-recovery-capacity-planner.md) is an important step to ensure that you deploy the Configuration Server with a configuration that suites your load requirements.</span></span> <span data-ttu-id="d655d-109">Przeczytaj więcej na temat [zmiany rozmiaru wymagania dotyczące serwera konfiguracji](#sizing-requirements-for-a-configuration-server).</span><span class="sxs-lookup"><span data-stu-id="d655d-109">Read more about [Sizing requirements for a Configuration Server](#sizing-requirements-for-a-configuration-server).</span></span>

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-the-configuration-server-software"></a><span data-ttu-id="d655d-110">Pobieranie oprogramowania serwera konfiguracji</span><span class="sxs-lookup"><span data-stu-id="d655d-110">Downloading the Configuration Server software</span></span>
1. <span data-ttu-id="d655d-111">Zaloguj się do portalu Azure i przejdź do magazynu usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="d655d-111">Log on to the Azure portal and browse to your Recovery Services Vault.</span></span>
2. <span data-ttu-id="d655d-112">Przejdź do **infrastrukturę odzyskiwania lokacji** > **serwery konfiguracji** (w obszarze VMware i maszyn fizycznych).</span><span class="sxs-lookup"><span data-stu-id="d655d-112">Browse to **Site Recovery Infrastructure** > **Configuration Servers** (under For VMware & Physical Machines).</span></span>

  ![Dodaj stronę serwerów](./media/site-recovery-vmware-to-azure-manage-configuration-server/AddServers.png)
3. <span data-ttu-id="d655d-114">Kliknij przycisk **+ serwery** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d655d-114">Click the **+Servers** button.</span></span>
4. <span data-ttu-id="d655d-115">Na **Dodaj serwer** kliknij przycisk pobierania, aby pobrać klucz rejestracji.</span><span class="sxs-lookup"><span data-stu-id="d655d-115">On the **Add Server** page, click the Download button to download the Registration key.</span></span> <span data-ttu-id="d655d-116">Ten klucz jest wymagane podczas instalacji serwera konfiguracji, aby zarejestrować go z usługą Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="d655d-116">You need this key during the Configuration Server installation to register it with Azure Site Recovery service.</span></span>
5. <span data-ttu-id="d655d-117">Kliknij przycisk **Pobierz Instalatora Microsoft Azure Site Recovery Unified** łącze, aby pobrać najnowszą wersję serwera konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="d655d-117">Click the **Download the Microsoft Azure Site Recovery Unified Setup** link to download the latest version of the Configuration Server.</span></span>

  ![Strona pobierania](./media/site-recovery-vmware-to-azure-manage-configuration-server/downloadcs.png)

  > [!TIP]
  <span data-ttu-id="d655d-119">Można pobrać najnowszą wersję serwera konfiguracji bezpośrednio z [strony pobierania witryny Microsoft Download Center](http://aka.ms/unifiedsetup)</span><span class="sxs-lookup"><span data-stu-id="d655d-119">Latest version of the Configuration Server can be downloaded directly from [Microsoft Download Center download page](http://aka.ms/unifiedsetup)</span></span>

## <a name="installing-and-registering-a-configuration-server-from-gui"></a><span data-ttu-id="d655d-120">Instalowanie i rejestrowanie konfiguracji serwer z graficznym interfejsem użytkownika</span><span class="sxs-lookup"><span data-stu-id="d655d-120">Installing and Registering a Configuration Server from GUI</span></span>
[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

## <a name="installing-and-registering-a-configuration-server-using-command-line"></a><span data-ttu-id="d655d-121">Instalowanie i rejestrowanie serwera konfiguracji przy użyciu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="d655d-121">Installing and registering a Configuration Server using Command line</span></span>

  ```
  UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address to be used for data transfer] [/CSIP <IP address of CS to be registered with>] [/PassphraseFilePath <Passphrase file path>]
  ```

### <a name="sample-usage"></a><span data-ttu-id="d655d-122">Przykładowe zastosowanie</span><span class="sxs-lookup"><span data-stu-id="d655d-122">Sample usage</span></span>
  ```
  MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /xC:\Temp\Extracted
  cd C:\Temp\Extracted
  UNIFIEDSETUP.EXE /AcceptThirdpartyEULA /servermode "CS" /InstallLocation "D:\" /MySQLCredsFilePath "C:\Temp\MySQLCredentialsfile.txt" /VaultCredsFilePath "C:\Temp\MyVault.vaultcredentials" /EnvType "VMWare"
  ```


### <a name="configuration-server-installer-command-line-arguments"></a><span data-ttu-id="d655d-123">Serwer konfiguracji Instalator argumenty wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="d655d-123">Configuration Server installer command-line arguments.</span></span>
[!INCLUDE [site-recovery-unified-setup-parameters](../../includes/site-recovery-unified-installer-command-parameters.md)]


### <a name="create-a-mysql-credentials-file"></a><span data-ttu-id="d655d-124">Utwórz plik poświadczeń MySql</span><span class="sxs-lookup"><span data-stu-id="d655d-124">Create a MySql credentials file</span></span>
<span data-ttu-id="d655d-125">Parametr MySQLCredsFilePath przyjmuje pliku jako dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="d655d-125">MySQLCredsFilePath parameter takes a file as input.</span></span> <span data-ttu-id="d655d-126">Utwórz plik w następującym formacie, a następnie przekaż go jako parametr wejściowy MySQLCredsFilePath.</span><span class="sxs-lookup"><span data-stu-id="d655d-126">Create the file using the following format and pass it as input MySQLCredsFilePath parameter.</span></span>
```
[MySQLCredentials]
MySQLRootPassword = "Password>"
MySQLUserPassword = "Password"
```
### <a name="create-a-proxy-settings-configuration-file"></a><span data-ttu-id="d655d-127">Utwórz plik konfiguracji ustawień serwera proxy</span><span class="sxs-lookup"><span data-stu-id="d655d-127">Create a proxy settings configuration file</span></span>
<span data-ttu-id="d655d-128">Parametr ProxySettingsFilePath przyjmuje pliku jako dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="d655d-128">ProxySettingsFilePath parameter takes a file as input.</span></span> <span data-ttu-id="d655d-129">Utwórz plik w następującym formacie, a następnie przekaż go jako parametr wejściowy ProxySettingsFilePath.</span><span class="sxs-lookup"><span data-stu-id="d655d-129">Create the file using the following format and pass it as input ProxySettingsFilePath parameter.</span></span>

```
[ProxySettings]
ProxyAuthentication = "Yes/No"
Proxy IP = "IP Address"
ProxyPort = "Port"
ProxyUserName="UserName"
ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-configuration-server"></a><span data-ttu-id="d655d-130">Modyfikowanie ustawień konfiguracji serwera proxy</span><span class="sxs-lookup"><span data-stu-id="d655d-130">Modifying proxy settings for Configuration Server</span></span>
1. <span data-ttu-id="d655d-131">Zaloguj się do serwera konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="d655d-131">Login to your Configuration Server.</span></span>
2. <span data-ttu-id="d655d-132">Uruchamianie cspsconfigtool.exe za pomocą skrótu na użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d655d-132">Launch the cspsconfigtool.exe using the shortcut on your.</span></span>
3. <span data-ttu-id="d655d-133">Kliknij przycisk **rejestracji magazynu** kartę.</span><span class="sxs-lookup"><span data-stu-id="d655d-133">Click the **Vault Registration** tab.</span></span>
4. <span data-ttu-id="d655d-134">Pobranie nowego pliku magazynu rejestracji z portalu i udostępnij go jako dane wejściowe do narzędzia.</span><span class="sxs-lookup"><span data-stu-id="d655d-134">Download a new Vault Registration file from the portal and provide it as input to the tool.</span></span>

  ![serwer w przypadku konfiguracji rejestru](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
5. <span data-ttu-id="d655d-136">Podaj nowe szczegóły serwera Proxy i kliknij przycisk **zarejestrować** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d655d-136">Provide the new Proxy Server details and click the **Register** button.</span></span>
6. <span data-ttu-id="d655d-137">Otwórz okno poleceń programu PowerShell administratora.</span><span class="sxs-lookup"><span data-stu-id="d655d-137">Open an Admin PowerShell command window.</span></span>
7. <span data-ttu-id="d655d-138">Uruchom następujące polecenie</span><span class="sxs-lookup"><span data-stu-id="d655d-138">Run the following command</span></span>
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```

  >[!WARNING]
  <span data-ttu-id="d655d-139">Jeśli masz dołączony do tego serwera konfiguracji serwerów proces skalowania w poziomie należy [Popraw ustawienia serwera proxy na wszystkich serwerach proces skalowania w poziomie](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#modifying-proxy-settings-for-scale-out-process-server) w danym wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="d655d-139">If you have Scale-out Process servers attached to this Configuration Server, you need to [fix the proxy settings on all the scale-out process servers](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#modifying-proxy-settings-for-scale-out-process-server) in your deployment.</span></span>

## <a name="re-register-a-configuration-server-with-the-same-recovery-services-vault"></a><span data-ttu-id="d655d-140">Zarejestruj ponownie serwer konfiguracji z tego samego magazynu usług odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="d655d-140">Re-register a Configuration Server with the same Recovery Services Vault</span></span>
  1. <span data-ttu-id="d655d-141">Zaloguj się do serwera konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="d655d-141">Login to your Configuration Server.</span></span>
  2. <span data-ttu-id="d655d-142">Uruchom cspsconfigtool.exe za pomocą skrótu na pulpicie.</span><span class="sxs-lookup"><span data-stu-id="d655d-142">Launch the cspsconfigtool.exe using the shortcut on your desktop.</span></span>
  3. <span data-ttu-id="d655d-143">Kliknij przycisk **rejestracji magazynu** kartę.</span><span class="sxs-lookup"><span data-stu-id="d655d-143">Click the **Vault Registration** tab.</span></span>
  4. <span data-ttu-id="d655d-144">Pobranie nowego pliku rejestracji z portalu i udostępnij go jako dane wejściowe do narzędzia.</span><span class="sxs-lookup"><span data-stu-id="d655d-144">Download a new Registration file from the portal and provide it as input to the tool.</span></span>
        <span data-ttu-id="d655d-145">![serwer w przypadku konfiguracji rejestru](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)</span><span class="sxs-lookup"><span data-stu-id="d655d-145">![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)</span></span>
  5. <span data-ttu-id="d655d-146">Podaj szczegóły serwera Proxy, a następnie kliknij przycisk **zarejestrować** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d655d-146">Provide the Proxy Server details and click the **Register** button.</span></span>  
  6. <span data-ttu-id="d655d-147">Otwórz okno poleceń programu PowerShell administratora.</span><span class="sxs-lookup"><span data-stu-id="d655d-147">Open an Admin PowerShell command window.</span></span>
  7. <span data-ttu-id="d655d-148">Uruchom następujące polecenie</span><span class="sxs-lookup"><span data-stu-id="d655d-148">Run the following command</span></span>

      ```
      $pwd = ConvertTo-SecureString -String MyProxyUserPassword
      Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
      net stop obengine
      net start obengine
      ```

  >[!WARNING]
  <span data-ttu-id="d655d-149">Jeśli masz dołączony do tego serwera konfiguracji serwerów proces skalowania w poziomie należy [ponownie zarejestrować serwery proces skalowania w poziomie](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#re-registering-a-scale-out-process-server) w danym wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="d655d-149">If you have Scale-out Process servers attached to this Configuration Server, you need to [re-register all the scale-out process servers](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#re-registering-a-scale-out-process-server) in your deployment.</span></span>

## <a name="registering-a-configuration-server-with-a-different-recovery-services-vault"></a><span data-ttu-id="d655d-150">Rejestrowanie serwera konfiguracji w innym magazynie usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="d655d-150">Registering a Configuration Server with a different Recovery Services Vault.</span></span>
1. <span data-ttu-id="d655d-151">Zaloguj się do serwera konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="d655d-151">Login to your Configuration Server.</span></span>
2. <span data-ttu-id="d655d-152">z wiersza polecenia z uprawnieniami administratora uruchom polecenie</span><span class="sxs-lookup"><span data-stu-id="d655d-152">from an admin command prompt, run the command</span></span>

```
reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
net stop dra
```
3. <span data-ttu-id="d655d-153">Uruchamianie cspsconfigtool.exe za pomocą skrótu na użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d655d-153">Launch the cspsconfigtool.exe using the shortcut on your.</span></span>
4. <span data-ttu-id="d655d-154">Kliknij przycisk **rejestracji magazynu** kartę.</span><span class="sxs-lookup"><span data-stu-id="d655d-154">Click the **Vault Registration** tab.</span></span>
5. <span data-ttu-id="d655d-155">Pobranie nowego pliku rejestracji z portalu i udostępnij go jako dane wejściowe do narzędzia.</span><span class="sxs-lookup"><span data-stu-id="d655d-155">Download a new Registration file from the portal and provide it as input to the tool.</span></span>

    ![serwer w przypadku konfiguracji rejestru](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
6. <span data-ttu-id="d655d-157">Podaj szczegóły serwera Proxy, a następnie kliknij przycisk **zarejestrować** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d655d-157">Provide the Proxy Server details and click the **Register** button.</span></span>  
7. <span data-ttu-id="d655d-158">Otwórz okno poleceń programu PowerShell administratora.</span><span class="sxs-lookup"><span data-stu-id="d655d-158">Open an Admin PowerShell command window.</span></span>
8. <span data-ttu-id="d655d-159">Uruchom następujące polecenie</span><span class="sxs-lookup"><span data-stu-id="d655d-159">Run the following command</span></span>
    ```
    $pwd = ConvertTo-SecureString -String MyProxyUserPassword
    Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
    net stop obengine
    net start obengine
    ```

## <a name="decommissioning-a-configuration-server"></a><span data-ttu-id="d655d-160">Wycofanie z eksploatacji serwera konfiguracji</span><span class="sxs-lookup"><span data-stu-id="d655d-160">Decommissioning a Configuration Server</span></span>
<span data-ttu-id="d655d-161">Upewnij się przed rozpoczęciem likwidowania serwera konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="d655d-161">Ensure the following before you start decommissioning your Configuration Server.</span></span>
1. <span data-ttu-id="d655d-162">Wyłącz ochronę dla wszystkich maszyn wirtualnych na tym serwerze konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="d655d-162">Disable protection for all virtual machines under this Configuration Server.</span></span>
2. <span data-ttu-id="d655d-163">Usuń skojarzenie wszystkich zasad replikacji z serwera konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="d655d-163">Disassociate all Replication policies from the Configuration Server.</span></span>
3. <span data-ttu-id="d655d-164">Usuń wszystkie hosty serwerów/vSphere Vcenter, które są skojarzone z serwerem konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="d655d-164">Delete all vCenters servers/vSphere hosts that are associated to the Configuration Server.</span></span>

### <a name="delete-the-configuration-server-from-azure-portal"></a><span data-ttu-id="d655d-165">Usuń serwer konfiguracji z portalu Azure</span><span class="sxs-lookup"><span data-stu-id="d655d-165">Delete the Configuration Server from Azure portal</span></span>
1. <span data-ttu-id="d655d-166">W portalu Azure, przejdź do **infrastruktura usługi Site Recovery** > **serwery konfiguracji** w menu magazynu.</span><span class="sxs-lookup"><span data-stu-id="d655d-166">In Azure portal, browse to **Site Recovery Infrastructure** > **Configuration Servers** from the Vault menu.</span></span>
2. <span data-ttu-id="d655d-167">Kliknij serwer konfiguracji, który ma zostać zlikwidowany.</span><span class="sxs-lookup"><span data-stu-id="d655d-167">Click the Configuration Server that you want to decommission.</span></span>
3. <span data-ttu-id="d655d-168">Na stronie Szczegóły serwera konfiguracji kliknij przycisk Usuń.</span><span class="sxs-lookup"><span data-stu-id="d655d-168">On the Configuration Server's details page, click the Delete button.</span></span>

  ![Usuwanie konfiguracji serwera](./media/site-recovery-vmware-to-azure-manage-configuration-server/delete-configuration-server.PNG)
4. <span data-ttu-id="d655d-170">Kliknij przycisk **tak** o potwierdzenie usunięcia serwera.</span><span class="sxs-lookup"><span data-stu-id="d655d-170">Click **Yes** to confirm the deletion of the server.</span></span>

  >[!WARNING]
  <span data-ttu-id="d655d-171">Jeśli masz maszyny wirtualne, zasady replikacji lub hostów serwerów/vSphere vCenter skojarzone z tym serwerem konfiguracji, nie można usunąć serwera.</span><span class="sxs-lookup"><span data-stu-id="d655d-171">If you have any virtual machines, Replication policies or vCenter servers/vSphere hosts associated with this Configuration Server, you cannot delete the server.</span></span> <span data-ttu-id="d655d-172">Przed usunięciem magazynu, należy usunąć te jednostki.</span><span class="sxs-lookup"><span data-stu-id="d655d-172">Delete these entities before you try to delete the vault.</span></span>

### <a name="uninstall-the-configuration-server-software-and-its-dependencies"></a><span data-ttu-id="d655d-173">Odinstaluj oprogramowanie serwera konfiguracji i jego zależności</span><span class="sxs-lookup"><span data-stu-id="d655d-173">Uninstall the Configuration Server software and its dependencies</span></span>
  > [!TIP]
  <span data-ttu-id="d655d-174">Jeśli planujesz ponowne serwerze konfiguracji z usługą Azure Site Recovery, następnie można przejść do kroku 4 bezpośrednio</span><span class="sxs-lookup"><span data-stu-id="d655d-174">If you plan to reuse the Configuration Server with Azure Site Recovery again, then you can skip to step 4 directly</span></span>

1. <span data-ttu-id="d655d-175">Zaloguj się jako Administrator serwera konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="d655d-175">Log on to the Configuration Server as an Administrator.</span></span>
2. <span data-ttu-id="d655d-176">Otwórz Panel sterowania > Program > Odinstaluj programy</span><span class="sxs-lookup"><span data-stu-id="d655d-176">Open up Control Panel > Program > Uninstall Programs</span></span>
3. <span data-ttu-id="d655d-177">Należy odinstalować te programy w następującej kolejności:</span><span class="sxs-lookup"><span data-stu-id="d655d-177">Uninstall the programs in the following sequence:</span></span>
  * <span data-ttu-id="d655d-178">Agent usług Microsoft Azure Recovery Services</span><span class="sxs-lookup"><span data-stu-id="d655d-178">Microsoft Azure Recovery Services Agent</span></span>
  * <span data-ttu-id="d655d-179">Microsoft Azure Site odzyskiwania mobilności usługi/główny serwer docelowy</span><span class="sxs-lookup"><span data-stu-id="d655d-179">Microsoft Azure Site Recovery Mobility Service/Master Target server</span></span>
  * <span data-ttu-id="d655d-180">Dostawcy usługi Microsoft Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="d655d-180">Microsoft Azure Site Recovery Provider</span></span>
  * <span data-ttu-id="d655d-181">Serwer procesu/serwera konfiguracji odzyskiwania witryny Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="d655d-181">Microsoft Azure Site Recovery Configuration Server/Process Server</span></span>
  * <span data-ttu-id="d655d-182">Microsoft Azure Site odzyskiwania konfiguracji serwera zależności</span><span class="sxs-lookup"><span data-stu-id="d655d-182">Microsoft Azure Site Recovery Configuration Server Dependencies</span></span>
  * <span data-ttu-id="d655d-183">Serwer MySQL 5,5</span><span class="sxs-lookup"><span data-stu-id="d655d-183">MySQL Server 5.5</span></span>
4. <span data-ttu-id="d655d-184">Uruchom następujące polecenie z i wiersza polecenia administratora.</span><span class="sxs-lookup"><span data-stu-id="d655d-184">Run the following command from and admin command prompt.</span></span>
  ```
  reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
  ```

## <a name="renew-configuration-server-secure-socket-layerssl-certificates"></a><span data-ttu-id="d655d-185">Odnów certyfikaty Layer(SSL) SSL serwera konfiguracji</span><span class="sxs-lookup"><span data-stu-id="d655d-185">Renew Configuration Server Secure Socket Layer(SSL) Certificates</span></span>
<span data-ttu-id="d655d-186">Serwer konfiguracji ma wbudowane serwer sieci Web, która organizuje działania serwerów usługi mobilności, serwerów przetwarzania i główny cel, połączenie z serwerem konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="d655d-186">The Configuration Server has an inbuilt webserver, which orchestrates the activities of the Mobility Service, Process Servers, and Master Target servers connected to the Configuration Server.</span></span> <span data-ttu-id="d655d-187">Serwer konfiguracji serwer sieci Web używa certyfikatu SSL do uwierzytelniania klientów.</span><span class="sxs-lookup"><span data-stu-id="d655d-187">The Configuration Server's webserver uses an SSL certificate to authenticate its clients.</span></span> <span data-ttu-id="d655d-188">Ten certyfikat ma upływie trzech lat i mogą być odnawiane w dowolnej chwili za pomocą następujących metod:</span><span class="sxs-lookup"><span data-stu-id="d655d-188">This certificate has an expiry of three years and can be renewed at any time using the following method:</span></span>

> [!WARNING]
<span data-ttu-id="d655d-189">Okresu ważności certyfikatu można wykonywać tylko w wersji 9.4.XXXX. X lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="d655d-189">Certificate expiry can be performed only on version 9.4.XXXX.X or higher.</span></span> <span data-ttu-id="d655d-190">Uaktualnij wszystkie składniki usługi Azure Site Recovery (serwer konfiguracji, serwer przetwarzania, głównego serwera docelowego, usługa mobilności) przed rozpoczęciem odnowić certyfikaty przepływ pracy.</span><span class="sxs-lookup"><span data-stu-id="d655d-190">Upgrade all the Azure Site Recovery components (Configuration Server, Process Server, Master Target Server, Mobility Service) before you start the Renew Certificates workflow.</span></span>

1. <span data-ttu-id="d655d-191">W portalu Azure, przejdź do magazynu > infrastruktura usługi Site Recovery > serwer konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="d655d-191">On the Azure portal, browse to your Vault > Site Recovery Infrastructure > Configuration Server.</span></span>
2. <span data-ttu-id="d655d-192">Kliknij serwer konfiguracji, dla którego należy odnowić certyfikat protokołu SSL.</span><span class="sxs-lookup"><span data-stu-id="d655d-192">Click the Configuration Server for which you need to renew the SSL Certificate for.</span></span>
3. <span data-ttu-id="d655d-193">W obszarze kondycji serwera konfiguracji można zobaczyć datę wygaśnięcia certyfikatu SSL.</span><span class="sxs-lookup"><span data-stu-id="d655d-193">Under the Configuration Server health, you can see the expiry date for the SSL Certificate.</span></span>
4. <span data-ttu-id="d655d-194">Odnów certyfikat, klikając **odnowić certyfikaty** akcji, jak pokazano na poniższej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="d655d-194">Renew the certificate by clicking the **Renew Certificates** action as shown in the following image:</span></span>

  ![Usuwanie konfiguracji serwera](./media/site-recovery-vmware-to-azure-manage-configuration-server/renew-cert-page.png)

### <a name="secure-socket-layer-certificate-expiry-warning"></a><span data-ttu-id="d655d-196">Secure Socket Layer ostrzeżenie o wygaśnięciu certyfikatu</span><span class="sxs-lookup"><span data-stu-id="d655d-196">Secure Socket Layer certificate expiry warning</span></span>

> [!NOTE]
<span data-ttu-id="d655d-197">Ważność certyfikatu protokołu SSL dla wszystkich instalacji, które wystąpiły przed maj 2016 została ustawiona na jeden rok.</span><span class="sxs-lookup"><span data-stu-id="d655d-197">The SSL Certificate's validity for all installations that happened before May 2016 was set to one year.</span></span> <span data-ttu-id="d655d-198">Rozpoczęto wyświetlać powiadomienia o wygasaniu certyfikatów wyświetlane w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="d655d-198">you have started seeing certificate expiry notifications showing up in the Azure portal.</span></span>

1. <span data-ttu-id="d655d-199">Jeśli certyfikat SSL serwera konfiguracji jest wkrótce wygaśnie w ciągu przyszłych dwóch miesięcy, Usługa uruchamia powiadamianie użytkowników przy użyciu portalu Azure i poczty e-mail (należy do subskrypcji powiadomień usługi Azure Site Recovery).</span><span class="sxs-lookup"><span data-stu-id="d655d-199">If the Configuration Server's SSL certificate is going to expire in the next two months, the service starts notifying users via the Azure portal & email (you need to be subscribed to Azure Site Recovery notifications).</span></span> <span data-ttu-id="d655d-200">Możesz uruchomić wyświetlanie transparencie powiadomienia na stronie zasobów magazynu.</span><span class="sxs-lookup"><span data-stu-id="d655d-200">You start seeing a notification banner on the Vault's resource page.</span></span>

  ![certyfikat powiadomień](./media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-renew-notification.png)
2. <span data-ttu-id="d655d-202">Kliknij przycisk transparentu, aby uzyskać więcej informacji o wygaśnięciu certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="d655d-202">Click the banner to get additional details on the Certificate expiry.</span></span>

  ![Szczegóły certyfikatu](./media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-expiry-details.png)

  >[!TIP]
  <span data-ttu-id="d655d-204">Jeśli zamiast **odnowić teraz** przycisk widzisz **Uaktualnij teraz** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d655d-204">If instead of a **Renew Now** button you see an **Upgrade Now** button.</span></span> <span data-ttu-id="d655d-205">Oznacza to, że są niektóre składniki w danym środowisku, które nie zostały jeszcze uaktualnione do 9.4.xxxx.x lub nowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="d655d-205">This means that there are some components in your environment that have not yet been upgraded to 9.4.xxxx.x or higher versions.</span></span>

## <a name="sizing-requirements-for-a-configuration-server"></a><span data-ttu-id="d655d-206">Ustawianie rozmiaru wymagania dotyczące serwera konfiguracji</span><span class="sxs-lookup"><span data-stu-id="d655d-206">Sizing requirements for a Configuration Server</span></span>

| <span data-ttu-id="d655d-207">**PROCESOR CPU**</span><span class="sxs-lookup"><span data-stu-id="d655d-207">**CPU**</span></span> | <span data-ttu-id="d655d-208">**Pamięci**</span><span class="sxs-lookup"><span data-stu-id="d655d-208">**Memory**</span></span> | <span data-ttu-id="d655d-209">**Rozmiar pamięci podręcznej dysku**</span><span class="sxs-lookup"><span data-stu-id="d655d-209">**Cache disk size**</span></span> | <span data-ttu-id="d655d-210">**Częstotliwość zmian danych**</span><span class="sxs-lookup"><span data-stu-id="d655d-210">**Data change rate**</span></span> | <span data-ttu-id="d655d-211">**Chronione maszyny**</span><span class="sxs-lookup"><span data-stu-id="d655d-211">**Protected machines**</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="d655d-212">8 Vcpu (2 sockets * 4 rdzenie @ 2,5 GHz)</span><span class="sxs-lookup"><span data-stu-id="d655d-212">8 vCPUs (2 sockets * 4 cores @ 2.5 GHz)</span></span> |<span data-ttu-id="d655d-213">16 GB</span><span class="sxs-lookup"><span data-stu-id="d655d-213">16 GB</span></span> |<span data-ttu-id="d655d-214">300 GB</span><span class="sxs-lookup"><span data-stu-id="d655d-214">300 GB</span></span> |<span data-ttu-id="d655d-215">500 GB lub mniej</span><span class="sxs-lookup"><span data-stu-id="d655d-215">500 GB or less</span></span> |<span data-ttu-id="d655d-216">Replikowanie maszyn mniej niż 100.</span><span class="sxs-lookup"><span data-stu-id="d655d-216">Replicate fewer than 100 machines.</span></span> |
| <span data-ttu-id="d655d-217">12 Vcpu (2 sockets * 6 rdzeni @ 2,5 GHz)</span><span class="sxs-lookup"><span data-stu-id="d655d-217">12 vCPUs (2 sockets * 6 cores @ 2.5 GHz)</span></span> |<span data-ttu-id="d655d-218">18 GB</span><span class="sxs-lookup"><span data-stu-id="d655d-218">18 GB</span></span> |<span data-ttu-id="d655d-219">600 GB</span><span class="sxs-lookup"><span data-stu-id="d655d-219">600 GB</span></span> |<span data-ttu-id="d655d-220">500 GB do 1 TB</span><span class="sxs-lookup"><span data-stu-id="d655d-220">500 GB to 1 TB</span></span> |<span data-ttu-id="d655d-221">Replikują między 100 150 maszyn.</span><span class="sxs-lookup"><span data-stu-id="d655d-221">Replicate between 100-150 machines.</span></span> |
| <span data-ttu-id="d655d-222">16 Vcpu (2 sockets * 8 rdzeni @ 2,5 GHz)</span><span class="sxs-lookup"><span data-stu-id="d655d-222">16 vCPUs (2 sockets * 8 cores @ 2.5 GHz)</span></span> |<span data-ttu-id="d655d-223">32 GB</span><span class="sxs-lookup"><span data-stu-id="d655d-223">32 GB</span></span> |<span data-ttu-id="d655d-224">1 TB</span><span class="sxs-lookup"><span data-stu-id="d655d-224">1 TB</span></span> |<span data-ttu-id="d655d-225">1 TB do 2 TB</span><span class="sxs-lookup"><span data-stu-id="d655d-225">1 TB to 2 TB</span></span> |<span data-ttu-id="d655d-226">Replikują między 150 – 200 maszyn.</span><span class="sxs-lookup"><span data-stu-id="d655d-226">Replicate between 150-200 machines.</span></span> |

  >[!TIP]
  <span data-ttu-id="d655d-227">Jeśli codziennych zmian ilości danych przekracza 2 TB lub planowana jest replikacja ponad 200 maszyn wirtualnych, zalecane jest wdrażanie serwerów dodatkowych procesów na potrzeby ruchu związanego z replikacją równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="d655d-227">If your daily data churn exceeds 2 TB, or you plan to replicate more than 200 virtual machines, it is recommended to deploy additional process servers to load balance the replication traffic.</span></span> <span data-ttu-id="d655d-228">Dowiedz się więcej na temat sposobu wdrażania proces skalowania w poziomie serwery.</span><span class="sxs-lookup"><span data-stu-id="d655d-228">Learn more about How to deploy Scale-out Process severs.</span></span>


## <a name="common-issues"></a><span data-ttu-id="d655d-229">Typowe problemy</span><span class="sxs-lookup"><span data-stu-id="d655d-229">Common issues</span></span>
[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]
