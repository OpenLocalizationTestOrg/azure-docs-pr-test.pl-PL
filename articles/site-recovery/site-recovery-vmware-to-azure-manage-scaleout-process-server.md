---
title: " Zarządzanie serwerem proces skalowania w poziomie w usłudze Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób tooset Konfigurowanie i zarządzanie serwerem proces skalowania w poziomie w usłudze Azure Site Recovery."
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
ms.openlocfilehash: 3d72f9c2c7014a4ff2fa2af168aa55ad1452eae5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-scale-out-process-server"></a><span data-ttu-id="d38ee-103">Zarządzanie serwerem proces skalowania w poziomie</span><span class="sxs-lookup"><span data-stu-id="d38ee-103">Manage a Scale-out Process Server</span></span>

<span data-ttu-id="d38ee-104">Serwer przetwarzania skalowalnego w poziomie działa jako koordynatora do transferu danych między hello usługi Site Recovery i infrastruktury lokalnej.</span><span class="sxs-lookup"><span data-stu-id="d38ee-104">Scale-out Process Server acts as a coordinator for data transfer between hello Site Recovery services and your on-premises infrastructure.</span></span> <span data-ttu-id="d38ee-105">W tym artykule opisano, jak można skonfigurować, konfigurowania i zarządzania serwera przetwarzania skalowalnego w poziomie.</span><span class="sxs-lookup"><span data-stu-id="d38ee-105">This article describes how you can set up, configure, and manage a Scale-out Process Server.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d38ee-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d38ee-106">Prerequisites</span></span>
<span data-ttu-id="d38ee-107">następujące Hello są zalecane hello sprzętu, oprogramowania i sieci tooset wymagana jest konfiguracja serwera proces skalowania w poziomie.</span><span class="sxs-lookup"><span data-stu-id="d38ee-107">hello following are hello recommended hardware, software, and network configuration required tooset up a Scale-out Process Server.</span></span>

> [!NOTE]
> <span data-ttu-id="d38ee-108">[Planowanie pojemności](site-recovery-capacity-planner.md) tooensure ważnym krokiem wdrażania hello skalowalnego w poziomie serwera przetwarzania konfiguracji z tego pakietu jest wymagań obciążenia.</span><span class="sxs-lookup"><span data-stu-id="d38ee-108">[Capacity planning](site-recovery-capacity-planner.md) is an important step tooensure that you deploy hello Scale-out Process Server with a configuration that suites your load requirements.</span></span> <span data-ttu-id="d38ee-109">Przeczytaj więcej na temat [skalowanie właściwości dla skalowalnego w poziomie serwera procesu](#sizing-requirements-for-a-configuration-server).</span><span class="sxs-lookup"><span data-stu-id="d38ee-109">Read more about [Scaling characteristics for a Scale-out Process Server](#sizing-requirements-for-a-configuration-server).</span></span>

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-hello-scale-out-process-server-software"></a><span data-ttu-id="d38ee-110">Pobieranie oprogramowania skalowalnego w poziomie serwera przetwarzania hello</span><span class="sxs-lookup"><span data-stu-id="d38ee-110">Downloading hello Scale-out Process Server software</span></span>
1. <span data-ttu-id="d38ee-111">Zaloguj się na toohello Azure tooyour portalu i przeglądania magazynu usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="d38ee-111">Log on toohello Azure portal and browse tooyour Recovery Services Vault.</span></span>
2. <span data-ttu-id="d38ee-112">Przeglądaj zbyt**infrastruktura usługi Site Recovery** > **serwery konfiguracji** (w przypadku VMware i maszyn fizycznych).</span><span class="sxs-lookup"><span data-stu-id="d38ee-112">Browse too**Site Recovery Infrastructure** > **Configuration Servers** (under For VMware & Physical Machines).</span></span>
3. <span data-ttu-id="d38ee-113">Wybierz z konfiguracji serwera toodrill w dół do strony szczegółów hello konfiguracji serwera.</span><span class="sxs-lookup"><span data-stu-id="d38ee-113">Select your configuration server toodrill down into hello configuration server's details page.</span></span>
4. <span data-ttu-id="d38ee-114">Kliknij przycisk hello **+ serwera przetwarzania** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d38ee-114">Click hello **+ Process Server** button.</span></span>
5. <span data-ttu-id="d38ee-115">W hello **proces dodawania serwera** wybierz pozycję **wdrażanie skalowalnego w poziomie proces serwera lokalnego** opcję hello **wybierz miejsce toodeploy serwera przetwarzania** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="d38ee-115">In hello **Add Process server** page, select **Deploy a Scale-out Process Server on-premises** option from hello **Choose where you want toodeploy your process server** drop-down.</span></span>

  ![Dodaj stronę serwerów](./media/site-recovery-vmware-to-azure-manage-scaleout-process-server/add-process-server.png)
6. <span data-ttu-id="d38ee-117">Kliknij przycisk hello **hello pobierania Instalatora Microsoft Azure Site Recovery Unified** łącze toodownload hello najnowszej wersji hello skalowalnego w poziomie serwera procesu instalacji.</span><span class="sxs-lookup"><span data-stu-id="d38ee-117">Click hello **Download hello Microsoft Azure Site Recovery Unified Setup** link toodownload hello latest version of hello Scale-out Process Server installation.</span></span>

  > [!WARNING]
  <span data-ttu-id="d38ee-118">Witaj wersji serwera przetwarzania skalowalnego w poziomie powinny być takie same tooor wcześniejsza niż wersja serwera konfiguracji hello w swoim środowisku.</span><span class="sxs-lookup"><span data-stu-id="d38ee-118">hello version of your Scale-out Process Server should be equal tooor lesser than hello Configuration Server version running in your environment.</span></span> <span data-ttu-id="d38ee-119">Zgodność wersji tooensure prosty sposób jest toouse hello tego samego bitów Instalator że używane tooinstall lub zaktualizowania serwera konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="d38ee-119">A simple way tooensure version compatibility is toouse hello same installer bits that you recently used tooinstall/update your Configuration Server.</span></span>

## <a name="installing-and-registering-a-scale-out-process-server-from-gui"></a><span data-ttu-id="d38ee-120">Instalowanie i rejestrowanie serwera przetwarzania skalowalnego w poziomie z graficznym interfejsem użytkownika</span><span class="sxs-lookup"><span data-stu-id="d38ee-120">Installing and registering a Scale-out Process Server from GUI</span></span>
<span data-ttu-id="d38ee-121">Jeśli masz tooscale limit wdrożenia ponad 200 maszyn źródłowych lub całkowity dzienny churn — liczba więcej niż 2 TB, należy procesu dodatkowe serwery toohandle hello ruchu woluminu.</span><span class="sxs-lookup"><span data-stu-id="d38ee-121">If you have tooscale out your deployment beyond 200 source machines, or a total daily churn rate of more than 2 TB, you need additional process servers toohandle hello traffic volume.</span></span>

<span data-ttu-id="d38ee-122">Sprawdź hello [rozmiaru zalecenia dotyczące serwerów procesu](#size-recommendations-for-the-process-server), a następnie wykonaj te instrukcje tooset hello procesu serwera.</span><span class="sxs-lookup"><span data-stu-id="d38ee-122">Check hello [size recommendations for process servers](#size-recommendations-for-the-process-server), and then follow these instructions tooset up hello process server.</span></span> <span data-ttu-id="d38ee-123">Po skonfigurowaniu serwera hello, migracja toouse maszyny źródłowej go.</span><span class="sxs-lookup"><span data-stu-id="d38ee-123">After setting up hello server, you migrate source machines toouse it.</span></span>

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-add-process-server.md)]


## <a name="installing-and-registering-a-scale-out-process-server-using-command-line"></a><span data-ttu-id="d38ee-124">Instalowanie i rejestrowanie serwera proces skalowania w poziomie przy użyciu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="d38ee-124">Installing and registering a Scale-out Process Server using command-line</span></span>

```
UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address toobe used for data transfer] [/CSIP <IP address of CS toobe registered with>] [/PassphraseFilePath <Passphrase file path>]
```

### <a name="sample-usage"></a><span data-ttu-id="d38ee-125">Przykładowe zastosowanie</span><span class="sxs-lookup"><span data-stu-id="d38ee-125">Sample usage</span></span>
```
MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /xC:\Temp\Extracted
cd C:\Temp\Extracted
UNIFIEDSETUP.EXE /AcceptThirdpartyEULA /servermode "PS" /InstallLocation "D:\" /EnvType "VMWare" /CSIP "10.150.24.119" /PassphraseFilePath "C:\Users\Administrator\Desktop\Passphrase.txt" /DataTransferSecurePort 443
```

### <a name="scale-out-process-server-installer-command-line-arguments"></a><span data-ttu-id="d38ee-126">Serwer przetwarzania skalowalnego w poziomie Instalator argumenty wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="d38ee-126">Scale-out Process Server installer command-line arguments.</span></span>
[!INCLUDE [site-recovery-unified-setup-parameters](../../includes/site-recovery-unified-installer-command-parameters.md)]


### <a name="create-a-proxy-settings-configuration-file"></a><span data-ttu-id="d38ee-127">Utwórz plik konfiguracji ustawień serwera proxy</span><span class="sxs-lookup"><span data-stu-id="d38ee-127">Create a proxy settings configuration file</span></span>
<span data-ttu-id="d38ee-128">Parametr ProxySettingsFilePath przyjmuje pliku jako dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="d38ee-128">ProxySettingsFilePath parameter takes a file as input.</span></span> <span data-ttu-id="d38ee-129">Tworzenie pliku przy użyciu hello następujący format i przekaż go jako parametr wejściowy ProxySettingsFilePath.</span><span class="sxs-lookup"><span data-stu-id="d38ee-129">Create file using hello following format and pass it as input ProxySettingsFilePath parameter.</span></span>
```
* [ProxySettings]
* ProxyAuthentication = "Yes/No"
* Proxy IP = "IP Address"
* ProxyPort = "Port"
* ProxyUserName="UserName"
* ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-scale-out-process-server"></a><span data-ttu-id="d38ee-130">Modyfikowanie ustawień serwera proxy dla serwera przetwarzania skalowalnego w poziomie</span><span class="sxs-lookup"><span data-stu-id="d38ee-130">Modifying proxy settings for Scale-out Process Server</span></span>
1. <span data-ttu-id="d38ee-131">Zaloguj się do serwera przetwarzania skalowalnego w poziomie.</span><span class="sxs-lookup"><span data-stu-id="d38ee-131">Login  into your Scale-out Process Server.</span></span>
2. <span data-ttu-id="d38ee-132">Otwórz okno poleceń programu PowerShell administratora.</span><span class="sxs-lookup"><span data-stu-id="d38ee-132">Open an Admin PowerShell command window.</span></span>
3. <span data-ttu-id="d38ee-133">Uruchom następujące polecenie hello</span><span class="sxs-lookup"><span data-stu-id="d38ee-133">Run hello following command</span></span>
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber –ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```
4. <span data-ttu-id="d38ee-134">Następnie przeglądanie katalogu toohello **%PROGRAMDATA%\ASR\Agent** i hello uruchom następujące polecenie</span><span class="sxs-lookup"><span data-stu-id="d38ee-134">Next browse toohello directory **%PROGRAMDATA%\ASR\Agent** and run hello following command</span></span>
  ```
  cmd
  cdpcli.exe --registermt

  net stop obengine

  net start obengine

  exit
  ```

## <a name="re-registering-a-scale-out-process-server"></a><span data-ttu-id="d38ee-135">Ponowne rejestrowanie serwera proces skalowania w poziomie</span><span class="sxs-lookup"><span data-stu-id="d38ee-135">Re-registering a Scale-out Process Server</span></span>
[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

* <span data-ttu-id="d38ee-136">Następnie otwórz wiersz polecenia administratora.</span><span class="sxs-lookup"><span data-stu-id="d38ee-136">Next open an Admin command prompt.</span></span>
* <span data-ttu-id="d38ee-137">Przeglądanie katalogu toohello **%PROGRAMDATA%\ASR\Agent** i uruchom polecenie hello</span><span class="sxs-lookup"><span data-stu-id="d38ee-137">Browse toohello directory **%PROGRAMDATA%\ASR\Agent** and run hello command</span></span>

```
cdpcli.exe --registermt

net stop obengine

net start obengine
```

## <a name="upgrading-a-scale-out-process-server"></a><span data-ttu-id="d38ee-138">Uaktualnianie serwera proces skalowania w poziomie</span><span class="sxs-lookup"><span data-stu-id="d38ee-138">Upgrading a Scale-out Process Server</span></span>
[!INCLUDE [site-recovery-vmware-upgrade -process-server](../../includes/site-recovery-vmware-upgrade-process-server-internal.md)]

## <a name="decommissioning-a-scale-out-process-server"></a><span data-ttu-id="d38ee-139">Wycofanie z eksploatacji serwera proces skalowania w poziomie</span><span class="sxs-lookup"><span data-stu-id="d38ee-139">Decommissioning a Scale-out Process Server</span></span>
1. <span data-ttu-id="d38ee-140">Upewnij się, że:</span><span class="sxs-lookup"><span data-stu-id="d38ee-140">Ensure that:</span></span>
  - <span data-ttu-id="d38ee-141">Stan połączenia serwera konfiguracji jest pokazywana jako **połączony** w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="d38ee-141">Configuration Server's connection state shows as **Connected** in hello Azure portal</span></span>
  - <span data-ttu-id="d38ee-142">Serwer przetwarzania jest nadal toocommunicate z powitania serwera konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="d38ee-142">Process Server's is still able toocommunicate with hello Configuration server.</span></span>
2. <span data-ttu-id="d38ee-143">Zaloguj się jako administrator toohello serwera przetwarzania</span><span class="sxs-lookup"><span data-stu-id="d38ee-143">Log in toohello process server as an administrator</span></span>
3. <span data-ttu-id="d38ee-144">Otwórz Panel sterowania > Program > Odinstaluj programy</span><span class="sxs-lookup"><span data-stu-id="d38ee-144">Open up Control Panel > Program > Uninstall Programs</span></span>
4. <span data-ttu-id="d38ee-145">Odinstaluj programy hello w sekwencji hello podane po:</span><span class="sxs-lookup"><span data-stu-id="d38ee-145">Uninstall hello programs in hello sequence given following:</span></span>
  * <span data-ttu-id="d38ee-146">Serwer procesu/serwera konfiguracji odzyskiwania witryny Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="d38ee-146">Microsoft Azure Site Recovery Configuration Server/Process Server</span></span>
  * <span data-ttu-id="d38ee-147">Microsoft Azure Site odzyskiwania konfiguracji serwera zależności</span><span class="sxs-lookup"><span data-stu-id="d38ee-147">Microsoft Azure Site Recovery Configuration Server Dependencies</span></span>
  * <span data-ttu-id="d38ee-148">Agent usług Microsoft Azure Recovery Services</span><span class="sxs-lookup"><span data-stu-id="d38ee-148">Microsoft Azure Recovery Services Agent</span></span>

<span data-ttu-id="d38ee-149">Może upłynąć minut up too15 tooreflect usunięcia serwera przetwarzania hello w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="d38ee-149">It can take up-too15 minutes for hello Process Server deletion tooreflect in hello Azure portal.</span></span>

  > [!NOTE]
  <span data-ttu-id="d38ee-150">Jeśli serwer przetwarzania hello jest toocommunicate z hello konfiguracji serwera (stan połączenia w portalu jest odłączony), wówczas należy toofollow hello następujące kroki toopurge go z powitania serwera konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="d38ee-150">If hello Process server is unable toocommunicate with hello Configuration Server (Connection State in portal is Disconnected), then you need toofollow hello following steps toopurge it from hello Configuration Server.</span></span>

## <a name="unregistering-a-disconnected-scale-out-process-server-from-a-configuration-server"></a><span data-ttu-id="d38ee-151">Wyrejestrowywanie odłączony serwer proces skalowania w poziomie z serwera konfiguracji</span><span class="sxs-lookup"><span data-stu-id="d38ee-151">Unregistering a disconnected Scale-out Process server from a Configuration Server</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]

## <a name="sizing-requirements-for-a-scale-out-process-server"></a><span data-ttu-id="d38ee-152">Ustawianie rozmiaru wymagania dotyczące serwera przetwarzania skalowalnego w poziomie</span><span class="sxs-lookup"><span data-stu-id="d38ee-152">Sizing requirements for a Scale-out Process Server</span></span>

| <span data-ttu-id="d38ee-153">**Serwer przetwarzania dodatkowe**</span><span class="sxs-lookup"><span data-stu-id="d38ee-153">**Additional process server**</span></span> | <span data-ttu-id="d38ee-154">**Rozmiar pamięci podręcznej dysku**</span><span class="sxs-lookup"><span data-stu-id="d38ee-154">**Cache disk size**</span></span> | <span data-ttu-id="d38ee-155">**Częstotliwość zmian danych**</span><span class="sxs-lookup"><span data-stu-id="d38ee-155">**Data change rate**</span></span> | <span data-ttu-id="d38ee-156">**Chronione maszyny**</span><span class="sxs-lookup"><span data-stu-id="d38ee-156">**Protected machines**</span></span> |
| --- | --- | --- | --- |
|<span data-ttu-id="d38ee-157">4 Vcpu (2 sockets * 2 rdzenie @ 2,5 GHz), 8 GB pamięci</span><span class="sxs-lookup"><span data-stu-id="d38ee-157">4 vCPUs (2 sockets * 2 cores @ 2.5 GHz), 8-GB memory</span></span> |<span data-ttu-id="d38ee-158">300 GB</span><span class="sxs-lookup"><span data-stu-id="d38ee-158">300 GB</span></span> |<span data-ttu-id="d38ee-159">250 GB lub mniej</span><span class="sxs-lookup"><span data-stu-id="d38ee-159">250 GB or less</span></span> |<span data-ttu-id="d38ee-160">Replikowanie maszyn 85 lub mniej.</span><span class="sxs-lookup"><span data-stu-id="d38ee-160">Replicate 85 or less machines.</span></span> |
|<span data-ttu-id="d38ee-161">8 Vcpu (2 sockets * 4 rdzenie @ 2,5 GHz), 12 GB pamięci RAM</span><span class="sxs-lookup"><span data-stu-id="d38ee-161">8 vCPUs (2 sockets * 4 cores @ 2.5 GHz), 12-GB memory</span></span> |<span data-ttu-id="d38ee-162">600 GB</span><span class="sxs-lookup"><span data-stu-id="d38ee-162">600 GB</span></span> |<span data-ttu-id="d38ee-163">TB too1 250 GB</span><span class="sxs-lookup"><span data-stu-id="d38ee-163">250 GB too1 TB</span></span> |<span data-ttu-id="d38ee-164">Replikują między 85 150 maszyny.</span><span class="sxs-lookup"><span data-stu-id="d38ee-164">Replicate between 85-150 machines.</span></span> |
|<span data-ttu-id="d38ee-165">12 Vcpu (2 sockets * 6 rdzeni @ 2,5 GHz) 24 GB pamięci</span><span class="sxs-lookup"><span data-stu-id="d38ee-165">12 vCPUs (2 sockets * 6 cores @ 2.5 GHz) 24-GB memory</span></span> |<span data-ttu-id="d38ee-166">1 TB</span><span class="sxs-lookup"><span data-stu-id="d38ee-166">1 TB</span></span> |<span data-ttu-id="d38ee-167">1 TB too2 TB</span><span class="sxs-lookup"><span data-stu-id="d38ee-167">1 TB too2 TB</span></span> |<span data-ttu-id="d38ee-168">Replikują między 150 225 komputerów.</span><span class="sxs-lookup"><span data-stu-id="d38ee-168">Replicate between 150-225 machines.</span></span> |
