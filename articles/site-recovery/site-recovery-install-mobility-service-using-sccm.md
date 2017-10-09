---
title: "Instalacja usługi mobilności dla usługi Azure Site Recovery przy użyciu narzędzia wdrażania oprogramowania aaaAutomate | Dokumentacja firmy Microsoft"
description: "Ten artykuł pomaga zautomatyzować instalacji usługi mobilności za pomocą narzędzia wdrażania oprogramowania takich jak System Center Configuration Manager."
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: 6c883c6d5308dcec6e0628b0c2196b3a12e08ebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="automate-mobility-service-installation-by-using-software-deployment-tools"></a><span data-ttu-id="72b50-103">Proces instalacji usługi mobilności przy użyciu narzędzia wdrażania oprogramowania</span><span class="sxs-lookup"><span data-stu-id="72b50-103">Automate Mobility Service installation by using software deployment tools</span></span>

>[!IMPORTANT]
<span data-ttu-id="72b50-104">Tym dokumencie przyjęto założenie, używana jest wersja **9.9.4510.1** lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="72b50-104">This document assumes you are using version **9.9.4510.1** or higher.</span></span>

<span data-ttu-id="72b50-105">Ten artykuł zawiera przykład sposobu użycia programu System Center Configuration Manager toodeploy hello usługa mobilności Azure Site Recovery w centrum danych.</span><span class="sxs-lookup"><span data-stu-id="72b50-105">This article provides you an example of how you can use System Center Configuration Manager toodeploy hello Azure Site Recovery Mobility Service in your datacenter.</span></span> <span data-ttu-id="72b50-106">Przy użyciu narzędzia wdrażania oprogramowania Configuration Manager — podobnie jak ma hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="72b50-106">Using a software deployment tool like Configuration Manager has hello following advantages:</span></span>
* <span data-ttu-id="72b50-107">Planowanie wdrożenia i aktualizacji, podczas okna zaplanowanej konserwacji dla aktualizacji oprogramowania</span><span class="sxs-lookup"><span data-stu-id="72b50-107">Scheduling deployment of fresh installations and upgrades, during your planned maintenance window for software updates</span></span>
* <span data-ttu-id="72b50-108">Skalowanie toohundreds wdrożenia serwerów jednocześnie</span><span class="sxs-lookup"><span data-stu-id="72b50-108">Scaling deployment toohundreds of servers simultaneously</span></span>


> [!NOTE]
> <span data-ttu-id="72b50-109">W tym artykule wykorzystano działaniem wdrażania programu System Center Configuration Manager 2012 R2 toodemonstrate hello.</span><span class="sxs-lookup"><span data-stu-id="72b50-109">This article uses System Center Configuration Manager 2012 R2 toodemonstrate hello deployment activity.</span></span> <span data-ttu-id="72b50-110">Instalacja usługi mobilności może również zautomatyzować przy użyciu [usługi Automatyzacja Azure i konfiguracji żądanego stanu](site-recovery-automate-mobility-service-install.md).</span><span class="sxs-lookup"><span data-stu-id="72b50-110">You could also automate Mobility Service installation by using [Azure Automation and Desired State Configuration](site-recovery-automate-mobility-service-install.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="72b50-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="72b50-111">Prerequisites</span></span>
1. <span data-ttu-id="72b50-112">Narzędzia wdrażania oprogramowania, takie jak programu Configuration Manager, który jest już wdrożony w środowisku.</span><span class="sxs-lookup"><span data-stu-id="72b50-112">A software deployment tool, like Configuration Manager, that is already deployed in your environment.</span></span>
  <span data-ttu-id="72b50-113">Utwórz dwa [kolekcje urządzeń](https://technet.microsoft.com/library/gg682169.aspx), jeden dla wszystkich **serwerów z systemem Windows**i drugi dla wszystkich **serwerów z systemem Linux**, mają tooprotect przy użyciu usługi Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="72b50-113">Create two [device collections](https://technet.microsoft.com/library/gg682169.aspx), one for all **Windows servers**, and another for all **Linux servers**, that you want tooprotect by using Site Recovery.</span></span>
3. <span data-ttu-id="72b50-114">Serwer konfiguracji jest już zarejestrowany z usługą Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="72b50-114">A configuration server that is already registered with Site Recovery.</span></span>
4. <span data-ttu-id="72b50-115">Bezpiecznej sieci udział plików (Server Message Block udziału) można uzyskać, sprawdzając powitania serwera programu Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="72b50-115">A secure network file share (Server Message Block share) that can be accessed by hello Configuration Manager server.</span></span>

## <a name="deploy-mobility-service-on-computers-running-windows"></a><span data-ttu-id="72b50-116">Wdrażanie usługi mobilności na komputerach z systemem Windows</span><span class="sxs-lookup"><span data-stu-id="72b50-116">Deploy Mobility Service on computers running Windows</span></span>
> [!NOTE]
> <span data-ttu-id="72b50-117">W tym artykule założono, że hello adres IP serwera konfiguracji hello jest 192.168.3.121 i że hello bezpiecznego sieciowego udziału plików jest \\\ContosoSecureFS\MobilityServiceInstallers.</span><span class="sxs-lookup"><span data-stu-id="72b50-117">This article assumes that hello IP address of hello configuration server is 192.168.3.121, and that hello secure network file share is \\\ContosoSecureFS\MobilityServiceInstallers.</span></span>

### <a name="step-1-prepare-for-deployment"></a><span data-ttu-id="72b50-118">Krok 1: Przygotowanie do wdrożenia</span><span class="sxs-lookup"><span data-stu-id="72b50-118">Step 1: Prepare for deployment</span></span>
1. <span data-ttu-id="72b50-119">Utwórz folder w udziale sieciowym hello i nadaj jej nazwę **MobSvcWindows**.</span><span class="sxs-lookup"><span data-stu-id="72b50-119">Create a folder on hello network share, and name it **MobSvcWindows**.</span></span>
2. <span data-ttu-id="72b50-120">Zaloguj się tooyour serwer konfiguracji i otwórz administracyjny wiersz polecenia.</span><span class="sxs-lookup"><span data-stu-id="72b50-120">Sign in tooyour configuration server, and open an administrative command prompt.</span></span>
3. <span data-ttu-id="72b50-121">Uruchom hello następujące polecenia toogenerate pliku hasło:</span><span class="sxs-lookup"><span data-stu-id="72b50-121">Run hello following commands toogenerate a passphrase file:</span></span>

    `cd %ProgramData%\ASR\home\svsystems\bin`

    `genpassphrase.exe -v > MobSvc.passphrase`
4. <span data-ttu-id="72b50-122">Kopiuj hello **MobSvc.passphrase** pliku do hello **MobSvcWindows** folderu w udziale sieciowym.</span><span class="sxs-lookup"><span data-stu-id="72b50-122">Copy hello **MobSvc.passphrase** file into hello **MobSvcWindows** folder on your network share.</span></span>
5. <span data-ttu-id="72b50-123">Przeglądaj toohello repozytorium Instalatora na serwerze konfiguracji hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="72b50-123">Browse toohello installer repository on hello configuration server by running hello following command:</span></span>

   `cd %ProgramData%\ASR\home\svsystems\puhsinstallsvc\repository`

6. <span data-ttu-id="72b50-124">Kopiuj hello  **automatycznego odzyskiwania systemu Microsoft\_UA\_*wersji*\_Windows\_GA\_*data* \_ Release.exe** toohello **MobSvcWindows** folderu w udziale sieciowym.</span><span class="sxs-lookup"><span data-stu-id="72b50-124">Copy hello **Microsoft-ASR\_UA\_*version*\_Windows\_GA\_*date*\_Release.exe** toohello **MobSvcWindows** folder on your network share.</span></span>
7. <span data-ttu-id="72b50-125">Skopiuj hello następującego kodu i zapisz go jako **install.bat** do hello **MobSvcWindows** folderu.</span><span class="sxs-lookup"><span data-stu-id="72b50-125">Copy hello following code, and save it as **install.bat** into hello **MobSvcWindows** folder.</span></span>

   > [!NOTE]
   > <span data-ttu-id="72b50-126">Zastąp symbole zastępcze hello [CSIP] w tym skrypcie hello rzeczywiste wartości hello adres IP serwera konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="72b50-126">Replace hello [CSIP] placeholders in this script with hello actual values of hello IP address of your configuration server.</span></span>

```DOS
Time /t >> C:\Temp\logfile.log
REM ==================================================
REM ==== Clean up hello folders ========================
RMDIR /S /q %temp%\MobSvc
MKDIR %Temp%\MobSvc
MKDIR C:\Temp
REM ==================================================

REM ==== Copy new files ==============================
COPY M*.* %Temp%\MobSvc
CD %Temp%\MobSvc
REN Micro*.exe MobSvcInstaller.exe
REM ==================================================

REM ==== Extract hello installer =======================
MobSvcInstaller.exe /q /x:%Temp%\MobSvc\Extracted
REM ==== Wait 10s for extraction toocomplete =========
TIMEOUT /t 10
REM =================================================

REM ==== Perform installation =======================
REM =================================================

CD %Temp%\MobSvc\Extracted
whoami >> C:\Temp\logfile.log
SET PRODKEY=HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall
REG QUERY %PRODKEY%\{275197FC-14FD-4560-A5EB-38217F80CBD1}
IF NOT %ERRORLEVEL% EQU 0 (
    echo "Product is not installed. Goto INSTALL." >> C:\Temp\logfile.log
    GOTO :INSTALL
) ELSE (
    echo "Product is installed." >> C:\Temp\logfile.log

    echo "Checking for Post-install action status." >> C:\Temp\logfile.log
    GOTO :POSTINSTALLCHECK
)

:POSTINSTALLCHECK
    REG QUERY "HKLM\SOFTWARE\Wow6432Node\InMage Systems\Installed Products\5" /v "PostInstallActions" | Find "Succeeded"
    If %ERRORLEVEL% EQU 0 (
        echo "Post-install actions succeeded. Checking for Configuration status." >> C:\Temp\logfile.log
        GOTO :CONFIGURATIONCHECK
    ) ELSE (
        echo "Post-install actions didn't succeed. Goto INSTALL." >> C:\Temp\logfile.log
        GOTO :INSTALL
    )

:CONFIGURATIONCHECK
    REG QUERY "HKLM\SOFTWARE\Wow6432Node\InMage Systems\Installed Products\5" /v "AgentConfigurationStatus" | Find "Succeeded"
    If %ERRORLEVEL% EQU 0 (
        echo "Configuration has succeeded. Goto UPGRADE." >> C:\Temp\logfile.log
        GOTO :UPGRADE
    ) ELSE (
        echo "Configuration didn't succeed. Goto CONFIGURE." >> C:\Temp\logfile.log
        GOTO :CONFIGURE
    )


:INSTALL
    echo "Perform installation." >> C:\Temp\logfile.log
    UnifiedAgent.exe /Role MS /InstallLocation "C:\Program Files (x86)\Microsoft Azure Site Recovery" /Platform "VmWare" /Silent
    IF %ERRORLEVEL% EQU 0 (
        echo "Installation has succeeded." >> C:\Temp\logfile.log
        (GOTO :CONFIGURE)
    ) ELSE (
        echo "Installation has failed." >> C:\Temp\logfile.log
        GOTO :ENDSCRIPT
    )

:CONFIGURE
    echo "Perform configuration." >> C:\Temp\logfile.log
    cd "C:\Program Files (x86)\Microsoft Azure Site Recovery\agent"
    UnifiedAgentConfigurator.exe  /CSEndPoint "[CSIP]" /PassphraseFilePath %Temp%\MobSvc\MobSvc.passphrase
    IF %ERRORLEVEL% EQU 0 (
        echo "Configuration has succeeded." >> C:\Temp\logfile.log
    ) ELSE (
        echo "Configuration has failed." >> C:\Temp\logfile.log
    )
    GOTO :ENDSCRIPT

:UPGRADE
    echo "Perform upgrade." >> C:\Temp\logfile.log
    UnifiedAgent.exe /Platform "VmWare" /Silent
    IF %ERRORLEVEL% EQU 0 (
        echo "Upgrade has succeeded." >> C:\Temp\logfile.log
    ) ELSE (
        echo "Upgrade has failed." >> C:\Temp\logfile.log
    )
    GOTO :ENDSCRIPT

:ENDSCRIPT
    echo "End of script." >> C:\Temp\logfile.log


```

### <a name="step-2-create-a-package"></a><span data-ttu-id="72b50-127">Krok 2: Tworzenie pakietu</span><span class="sxs-lookup"><span data-stu-id="72b50-127">Step 2: Create a package</span></span>

1. <span data-ttu-id="72b50-128">Zaloguj się w konsoli programu Configuration Manager tooyour.</span><span class="sxs-lookup"><span data-stu-id="72b50-128">Sign in tooyour Configuration Manager console.</span></span>
2. <span data-ttu-id="72b50-129">Przeglądaj zbyt**Biblioteka oprogramowania** > **Zarządzanie aplikacjami** > **pakiety**.</span><span class="sxs-lookup"><span data-stu-id="72b50-129">Browse too**Software Library** > **Application Management** > **Packages**.</span></span>
3. <span data-ttu-id="72b50-130">Kliknij prawym przyciskiem myszy **pakiety**i wybierz **tworzenia pakietu**.</span><span class="sxs-lookup"><span data-stu-id="72b50-130">Right-click **Packages**, and select **Create Package**.</span></span>
4. <span data-ttu-id="72b50-131">Podaj wartości hello nazwę, opis, producenta, język i wersję.</span><span class="sxs-lookup"><span data-stu-id="72b50-131">Provide values for hello name, description, manufacturer, language, and version.</span></span>
5. <span data-ttu-id="72b50-132">Wybierz hello **ten pakiet zawiera pliki źródłowe** pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="72b50-132">Select hello **This package contains source files** check box.</span></span>
6. <span data-ttu-id="72b50-133">Kliknij przycisk **Przeglądaj**i wybierz hello udziału sieciowego przechowywania hello Instalatora (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcWindows).</span><span class="sxs-lookup"><span data-stu-id="72b50-133">Click **Browse**, and select hello network share where hello installer is stored (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcWindows).</span></span>

  ![Kreator zrzut ekranu tworzenia pakietu i programu](./media/site-recovery-install-mobility-service-using-sccm/create_sccm_package.png)

7. <span data-ttu-id="72b50-135">Na powitania **wybierz hello program typ, który toocreate** wybierz pozycję **Program standardowy**i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="72b50-135">On hello **Choose hello program type that you want toocreate** page, select **Standard Program**, and click **Next**.</span></span>

  ![Kreator zrzut ekranu tworzenia pakietu i programu](./media/site-recovery-install-mobility-service-using-sccm/sccm-standard-program.png)

8. <span data-ttu-id="72b50-137">Na powitania **Podaj informacje dotyczące tego programu standardowego** , podaj następujące dane wejściowe hello i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="72b50-137">On hello **Specify information about this standard program** page, provide hello following inputs, and click **Next**.</span></span> <span data-ttu-id="72b50-138">(hello inne dane wejściowe można użyć wartości domyślnych).</span><span class="sxs-lookup"><span data-stu-id="72b50-138">(hello other inputs can use their default values.)</span></span>

  | <span data-ttu-id="72b50-139">**Nazwa parametru**</span><span class="sxs-lookup"><span data-stu-id="72b50-139">**Parameter name**</span></span> | <span data-ttu-id="72b50-140">**Wartość**</span><span class="sxs-lookup"><span data-stu-id="72b50-140">**Value**</span></span> |
  |--|--|
  | <span data-ttu-id="72b50-141">Nazwa</span><span class="sxs-lookup"><span data-stu-id="72b50-141">Name</span></span> | <span data-ttu-id="72b50-142">Zainstaluj usługę mobilności platformy Microsoft Azure (system Windows)</span><span class="sxs-lookup"><span data-stu-id="72b50-142">Install Microsoft Azure Mobility Service (Windows)</span></span> |
  | <span data-ttu-id="72b50-143">Wiersz polecenia</span><span class="sxs-lookup"><span data-stu-id="72b50-143">Command line</span></span> | <span data-ttu-id="72b50-144">Install.bat</span><span class="sxs-lookup"><span data-stu-id="72b50-144">install.bat</span></span> |
  | <span data-ttu-id="72b50-145">Program można uruchomić</span><span class="sxs-lookup"><span data-stu-id="72b50-145">Program can run</span></span> | <span data-ttu-id="72b50-146">Określa, czy użytkownik jest zalogowany</span><span class="sxs-lookup"><span data-stu-id="72b50-146">Whether or not a user is logged on</span></span> |

  ![Kreator zrzut ekranu tworzenia pakietu i programu](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties.png)

9. <span data-ttu-id="72b50-148">Na następnej stronie powitania wybierz hello systemów operacyjnych.</span><span class="sxs-lookup"><span data-stu-id="72b50-148">On hello next page, select hello target operating systems.</span></span> <span data-ttu-id="72b50-149">Tylko w systemie Windows Server 2012 R2, Windows Server 2012 i Windows Server 2008 R2 można zainstalować usługi mobilności.</span><span class="sxs-lookup"><span data-stu-id="72b50-149">Mobility Service can be installed only on Windows Server 2012 R2, Windows Server 2012, and Windows Server 2008 R2.</span></span>

  ![Kreator zrzut ekranu tworzenia pakietu i programu](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2.png)

10. <span data-ttu-id="72b50-151">toocomplete hello kreatora, kliknij przycisk **dalej** dwa razy.</span><span class="sxs-lookup"><span data-stu-id="72b50-151">toocomplete hello wizard, click **Next** twice.</span></span>


> [!NOTE]
> <span data-ttu-id="72b50-152">skrypt Hello obsługuje zarówno nowe instalacje agentów usługi mobilności i aktualizuje tooagents, które zostały już zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="72b50-152">hello script supports both new installations of Mobility Service agents and updates tooagents that are already installed.</span></span>

### <a name="step-3-deploy-hello-package"></a><span data-ttu-id="72b50-153">Krok 3: Wdrażanie pakietu hello</span><span class="sxs-lookup"><span data-stu-id="72b50-153">Step 3: Deploy hello package</span></span>
1. <span data-ttu-id="72b50-154">W konsoli programu Configuration Manager hello, kliknij prawym przyciskiem myszy pakiet, a następnie wybierz **Dystrybuuj zawartość**.</span><span class="sxs-lookup"><span data-stu-id="72b50-154">In hello Configuration Manager console, right-click your package, and select **Distribute Content**.</span></span>
  <span data-ttu-id="72b50-155">![Zrzut ekranu programu Configuration Manager konsoli](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span><span class="sxs-lookup"><span data-stu-id="72b50-155">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span></span>
2. <span data-ttu-id="72b50-156">Wybierz hello  **[punktów dystrybucji](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)**  na toowhich pakietów hello powinien zostać skopiowany.</span><span class="sxs-lookup"><span data-stu-id="72b50-156">Select hello **[distribution points](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)** on toowhich hello packages should be copied.</span></span>
3. <span data-ttu-id="72b50-157">Kreator hello ukończone.</span><span class="sxs-lookup"><span data-stu-id="72b50-157">Complete hello wizard.</span></span> <span data-ttu-id="72b50-158">Hello pakietu, a następnie rozpoczyna replikację toohello określonych punktów dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="72b50-158">hello package then starts replicating toohello specified distribution points.</span></span>
4. <span data-ttu-id="72b50-159">Po dystrybucji pakietów hello jest gotowe, kliknij prawym przyciskiem myszy pakiet hello i wybierz opcję **Wdróż**.</span><span class="sxs-lookup"><span data-stu-id="72b50-159">After hello package distribution is done, right-click hello package, and select **Deploy**.</span></span>
  <span data-ttu-id="72b50-160">![Zrzut ekranu programu Configuration Manager konsoli](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span><span class="sxs-lookup"><span data-stu-id="72b50-160">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span></span>
5. <span data-ttu-id="72b50-161">Wybierz kolekcję urządzeń systemu Windows Server hello utworzonego w sekcji wymagania wstępne hello jako hello kolekcję docelową dla wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="72b50-161">Select hello Windows Server device collection you created in hello prerequisites section as hello target collection for deployment.</span></span>

  ![Kreator zrzut ekranu wdrażania oprogramowania](./media/site-recovery-install-mobility-service-using-sccm/sccm-select-target-collection.png)

6. <span data-ttu-id="72b50-163">Na powitania **określ miejsce docelowe zawartości hello** wybierz opcję sieci **punktów dystrybucji**.</span><span class="sxs-lookup"><span data-stu-id="72b50-163">On hello **Specify hello content destination** page, select your **Distribution Points**.</span></span>
7. <span data-ttu-id="72b50-164">Na powitania **toocontrol ustawienia Określ sposób wdrażania tego oprogramowania** upewnij się, że celem hello jest **wymagane**.</span><span class="sxs-lookup"><span data-stu-id="72b50-164">On hello **Specify settings toocontrol how this software is deployed** page, ensure that hello purpose is **Required**.</span></span>

  ![Kreator zrzut ekranu wdrażania oprogramowania](./media/site-recovery-install-mobility-service-using-sccm/sccm-deploy-select-purpose.png)

8. <span data-ttu-id="72b50-166">Na powitania **hello Określ harmonogram tego wdrożenia** Określ harmonogram.</span><span class="sxs-lookup"><span data-stu-id="72b50-166">On hello **Specify hello schedule for this deployment** page, specify a schedule.</span></span> <span data-ttu-id="72b50-167">Aby uzyskać więcej informacji, zobacz [planowania pakietów](https://technet.microsoft.com/library/gg682178.aspx).</span><span class="sxs-lookup"><span data-stu-id="72b50-167">For more information, see [scheduling packages](https://technet.microsoft.com/library/gg682178.aspx).</span></span>
9. <span data-ttu-id="72b50-168">Na powitania **punktów dystrybucji** Skonfiguruj właściwości hello zgodnie z potrzebami toohello centrum danych.</span><span class="sxs-lookup"><span data-stu-id="72b50-168">On hello **Distribution Points** page, configure hello properties according toohello needs of your datacenter.</span></span> <span data-ttu-id="72b50-169">Następnie wykonaj hello kreatora.</span><span class="sxs-lookup"><span data-stu-id="72b50-169">Then complete hello wizard.</span></span>

> [!TIP]
> <span data-ttu-id="72b50-170">tooavoid konieczne ponowne uruchomienie, harmonogram instalacji pakietu hello podczas z comiesięcznej konserwacji lub okna aktualizacji oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="72b50-170">tooavoid unnecessary reboots, schedule hello package installation during your monthly maintenance window or software updates window.</span></span>

<span data-ttu-id="72b50-171">Możesz monitorować postęp wdrażania hello za pomocą konsoli programu Configuration Manager hello.</span><span class="sxs-lookup"><span data-stu-id="72b50-171">You can monitor hello deployment progress by using hello Configuration Manager console.</span></span> <span data-ttu-id="72b50-172">Przejdź za**monitorowanie** > **wdrożeń** > *[nazwa pakietu]*.</span><span class="sxs-lookup"><span data-stu-id="72b50-172">Go too**Monitoring** > **Deployments** > *[your package name]*.</span></span>

  ![Zrzut ekranu Menedżera konfiguracji opcji toomonitor wdrożenia](./media/site-recovery-install-mobility-service-using-sccm/report.PNG)

## <a name="deploy-mobility-service-on-computers-running-linux"></a><span data-ttu-id="72b50-174">Wdrażanie usługi mobilności na komputerach z systemem Linux</span><span class="sxs-lookup"><span data-stu-id="72b50-174">Deploy Mobility Service on computers running Linux</span></span>
> [!NOTE]
> <span data-ttu-id="72b50-175">W tym artykule założono, że hello adres IP serwera konfiguracji hello jest 192.168.3.121 i że hello bezpiecznego sieciowego udziału plików jest \\\ContosoSecureFS\MobilityServiceInstallers.</span><span class="sxs-lookup"><span data-stu-id="72b50-175">This article assumes that hello IP address of hello configuration server is 192.168.3.121, and that hello secure network file share is \\\ContosoSecureFS\MobilityServiceInstallers.</span></span>

### <a name="step-1-prepare-for-deployment"></a><span data-ttu-id="72b50-176">Krok 1: Przygotowanie do wdrożenia</span><span class="sxs-lookup"><span data-stu-id="72b50-176">Step 1: Prepare for deployment</span></span>
1. <span data-ttu-id="72b50-177">Utwórz folder w udziale sieciowym hello i nazywa je jako **MobSvcLinux**.</span><span class="sxs-lookup"><span data-stu-id="72b50-177">Create a folder on hello network share, and name it as **MobSvcLinux**.</span></span>
2. <span data-ttu-id="72b50-178">Zaloguj się tooyour serwer konfiguracji i otwórz administracyjny wiersz polecenia.</span><span class="sxs-lookup"><span data-stu-id="72b50-178">Sign in tooyour configuration server, and open an administrative command prompt.</span></span>
3. <span data-ttu-id="72b50-179">Uruchom hello następujące polecenia toogenerate pliku hasło:</span><span class="sxs-lookup"><span data-stu-id="72b50-179">Run hello following commands toogenerate a passphrase file:</span></span>

    `cd %ProgramData%\ASR\home\svsystems\bin`

    `genpassphrase.exe -v > MobSvc.passphrase`
4. <span data-ttu-id="72b50-180">Kopiuj hello **MobSvc.passphrase** pliku do hello **MobSvcLinux** folderu w udziale sieciowym.</span><span class="sxs-lookup"><span data-stu-id="72b50-180">Copy hello **MobSvc.passphrase** file into hello **MobSvcLinux** folder on your network share.</span></span>
5. <span data-ttu-id="72b50-181">Przeglądaj toohello repozytorium Instalatora na serwerze konfiguracji hello, uruchamiając polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="72b50-181">Browse toohello installer repository on hello configuration server by running hello command:</span></span>

   `cd %ProgramData%\ASR\home\svsystems\puhsinstallsvc\repository`

6. <span data-ttu-id="72b50-182">Kopiuj hello następujące pliki toohello **MobSvcLinux** folderu w udziale sieciowym:</span><span class="sxs-lookup"><span data-stu-id="72b50-182">Copy hello following files toohello **MobSvcLinux** folder on your network share:</span></span>
   * <span data-ttu-id="72b50-183">Usługa ASR Microsoft\_UA\*RHEL6 64*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="72b50-183">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span></span>
   * <span data-ttu-id="72b50-184">Usługa ASR Microsoft\_UA\*RHEL7 64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="72b50-184">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span></span>
   * <span data-ttu-id="72b50-185">Usługa ASR Microsoft\_UA\*SLES11-SP3-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="72b50-185">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span></span>
   * <span data-ttu-id="72b50-186">Usługa ASR Microsoft\_UA\*SLES11-SP4-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="72b50-186">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span></span>
   * <span data-ttu-id="72b50-187">Usługa ASR Microsoft\_UA\*OL6 64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="72b50-187">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span></span>
   * <span data-ttu-id="72b50-188">Usługa ASR Microsoft\_UA\*UBUNTU-14.04-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="72b50-188">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span></span>


7. <span data-ttu-id="72b50-189">Skopiuj hello następującego kodu i zapisz go jako **install_linux.sh** do hello **MobSvcLinux** folderu.</span><span class="sxs-lookup"><span data-stu-id="72b50-189">Copy hello following code, and save it as **install_linux.sh** into hello **MobSvcLinux** folder.</span></span>
   > [!NOTE]
   > <span data-ttu-id="72b50-190">Zastąp symbole zastępcze hello [CSIP] w tym skrypcie hello rzeczywiste wartości hello adres IP serwera konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="72b50-190">Replace hello [CSIP] placeholders in this script with hello actual values of hello IP address of your configuration server.</span></span>

```Bash
#!/usr/bin/env bash

rm -rf /tmp/MobSvc
mkdir -p /tmp/MobSvc
INSTALL_DIR='/usr/local/ASR'
VX_VERSION_FILE='/usr/local/.vx_version'

echo "=============================" >> /tmp/MobSvc/sccm.log
echo `date` >> /tmp/MobSvc/sccm.log
echo "=============================" >> /tmp/MobSvc/sccm.log

if [ -f /etc/oracle-release ] && [ -f /etc/redhat-release ]; then
    if grep -q 'Oracle Linux Server release 6.*' /etc/oracle-release; then
        if uname -a | grep -q x86_64; then
            OS="OL6-64"
            echo $OS >> /tmp/MobSvc/sccm.log
            cp *OL6*.tar.gz /tmp/MobSvc
        fi
    fi
elif [ -f /etc/redhat-release ]; then
    if grep -q 'Red Hat Enterprise Linux Server release 6.* (Santiago)' /etc/redhat-release || \
        grep -q 'CentOS Linux release 6.* (Final)' /etc/redhat-release || \
        grep -q 'CentOS release 6.* (Final)' /etc/redhat-release; then
        if uname -a | grep -q x86_64; then
            OS="RHEL6-64"
            echo $OS >> /tmp/MobSvc/sccm.log
            cp *RHEL6*.tar.gz /tmp/MobSvc
        fi
    elif grep -q 'Red Hat Enterprise Linux Server release 7.* (Maipo)' /etc/redhat-release || \
        grep -q 'CentOS Linux release 7.* (Core)' /etc/redhat-release; then
        if uname -a | grep -q x86_64; then
            OS="RHEL7-64"
            echo $OS >> /tmp/MobSvc/sccm.log
            cp *RHEL7*.tar.gz /tmp/MobSvc
                fi
    fi
elif [ -f /etc/SuSE-release ] && grep -q 'VERSION = 11' /etc/SuSE-release; then
    if grep -q "SUSE Linux Enterprise Server 11" /etc/SuSE-release && grep -q 'PATCHLEVEL = 3' /etc/SuSE-release; then
        if uname -a | grep -q x86_64; then
            OS="SLES11-SP3-64"
            echo $OS >> /tmp/MobSvc/sccm.log
            cp *SLES11-SP3*.tar.gz /tmp/MobSvc
        fi
    elif grep -q "SUSE Linux Enterprise Server 11" /etc/SuSE-release && grep -q 'PATCHLEVEL = 4' /etc/SuSE-release; then
        if uname -a | grep -q x86_64; then
            OS="SLES11-SP4-64"
            echo $OS >> /tmp/MobSvc/sccm.log
            cp *SLES11-SP4*.tar.gz /tmp/MobSvc
        fi
    fi
elif [ -f /etc/lsb-release ] ; then
    if grep -q 'DISTRIB_RELEASE=14.04' /etc/lsb-release ; then
       if uname -a | grep -q x86_64; then
           OS="UBUNTU-14.04-64"
           echo $OS >> /tmp/MobSvc/sccm.log
           cp *UBUNTU-14*.tar.gz /tmp/MobSvc
       fi
    fi
else
    exit 1
fi

if [ -z "$OS" ]; then
    exit 1
fi

Install()
{
    echo "Perform Installation." >> /tmp/MobSvc/sccm.log
    ./install -q -d ${INSTALL_DIR} -r MS -v VmWare
    RET_VAL=$?
    echo "Installation Returncode: $RET_VAL" >> /tmp/MobSvc/sccm.log
    if [ $RET_VAL -eq 0 ]; then
        echo "Installation has succeeded. Proceed tooconfiguration." >> /tmp/MobSvc/sccm.log
        Configure
    else
        echo "Installation has failed." >> /tmp/MobSvc/sccm.log
        exit $RET_VAL
    fi
}

Configure()
{
    echo "Perform configuration." >> /tmp/MobSvc/sccm.log
    ${INSTALL_DIR}/Vx/bin/UnifiedAgentConfigurator.sh -i [CSIP] -P MobSvc.passphrase
    RET_VAL=$?
    echo "Configuration Returncode: $RET_VAL" >> /tmp/MobSvc/sccm.log
    if [ $RET_VAL -eq 0 ]; then
        echo "Configuration has succeeded." >> /tmp/MobSvc/sccm.log
    else
        echo "Configuration has failed." >> /tmp/MobSvc/sccm.log
        exit $RET_VAL
    fi
}

Upgrade()
{
    echo "Perform Upgrade." >> /tmp/MobSvc/sccm.log
    ./install -q -v VmWare
    RET_VAL=$?
    echo "Upgrade Returncode: $RET_VAL" >> /tmp/MobSvc/sccm.log
    if [ $RET_VAL -eq 0 ]; then
        echo "Upgrade has succeeded." >> /tmp/MobSvc/sccm.log
    else
        echo "Upgrade has failed." >> /tmp/MobSvc/sccm.log
        exit $RET_VAL
    fi
}

cp MobSvc.passphrase /tmp/MobSvc
cd /tmp/MobSvc

tar -zxvf *.tar.gz

if [ -e ${VX_VERSION_FILE} ]; then
    echo "${VX_VERSION_FILE} exists. Checking for configuration status." >> /tmp/MobSvc/sccm.log
    agent_configuration=$(grep ^AGENT_CONFIGURATION_STATUS "${VX_VERSION_FILE}" | cut -d"=" -f2 | tr -d " ")
    echo "agent_configuration=$agent_configuration" >> /tmp/MobSvc/sccm.log
     if [ "$agent_configuration" == "Succeeded" ]; then
        echo "Agent is already configured. Proceed tooUpgrade." >> /tmp/MobSvc/sccm.log
        Upgrade
    else
        echo "Agent is not configured. Proceed tooConfigure." >> /tmp/MobSvc/sccm.log
        Configure
    fi
else
    Install
fi

cd /tmp

```

### <a name="step-2-create-a-package"></a><span data-ttu-id="72b50-191">Krok 2: Tworzenie pakietu</span><span class="sxs-lookup"><span data-stu-id="72b50-191">Step 2: Create a package</span></span>

1. <span data-ttu-id="72b50-192">Zaloguj się w konsoli programu Configuration Manager tooyour.</span><span class="sxs-lookup"><span data-stu-id="72b50-192">Sign in  tooyour Configuration Manager console.</span></span>
2. <span data-ttu-id="72b50-193">Przeglądaj zbyt**Biblioteka oprogramowania** > **Zarządzanie aplikacjami** > **pakiety**.</span><span class="sxs-lookup"><span data-stu-id="72b50-193">Browse too**Software Library** > **Application Management** > **Packages**.</span></span>
3. <span data-ttu-id="72b50-194">Kliknij prawym przyciskiem myszy **pakiety**i wybierz **tworzenia pakietu**.</span><span class="sxs-lookup"><span data-stu-id="72b50-194">Right-click **Packages**, and select **Create Package**.</span></span>
4. <span data-ttu-id="72b50-195">Podaj wartości hello nazwę, opis, producenta, język i wersję.</span><span class="sxs-lookup"><span data-stu-id="72b50-195">Provide values for hello name, description, manufacturer, language, and version.</span></span>
5. <span data-ttu-id="72b50-196">Wybierz hello **ten pakiet zawiera pliki źródłowe** pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="72b50-196">Select hello **This package contains source files** check box.</span></span>
6. <span data-ttu-id="72b50-197">Kliknij przycisk **Przeglądaj**i wybierz hello udziału sieciowego przechowywania hello Instalatora (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcLinux).</span><span class="sxs-lookup"><span data-stu-id="72b50-197">Click **Browse**, and select hello network share where hello installer is stored (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcLinux).</span></span>

  ![Kreator zrzut ekranu tworzenia pakietu i programu](./media/site-recovery-install-mobility-service-using-sccm/create_sccm_package-linux.png)

7. <span data-ttu-id="72b50-199">Na powitania **wybierz hello program typ, który toocreate** wybierz pozycję **Program standardowy**i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="72b50-199">On hello **Choose hello program type that you want toocreate** page, select **Standard Program**, and click **Next**.</span></span>

  ![Kreator zrzut ekranu tworzenia pakietu i programu](./media/site-recovery-install-mobility-service-using-sccm/sccm-standard-program.png)

8. <span data-ttu-id="72b50-201">Na powitania **Podaj informacje dotyczące tego programu standardowego** , podaj następujące dane wejściowe hello i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="72b50-201">On hello **Specify information about this standard program** page, provide hello following inputs, and click **Next**.</span></span> <span data-ttu-id="72b50-202">(hello inne dane wejściowe można użyć wartości domyślnych).</span><span class="sxs-lookup"><span data-stu-id="72b50-202">(hello other inputs can use their default values.)</span></span>

    | <span data-ttu-id="72b50-203">**Nazwa parametru**</span><span class="sxs-lookup"><span data-stu-id="72b50-203">**Parameter name**</span></span> | <span data-ttu-id="72b50-204">**Wartość**</span><span class="sxs-lookup"><span data-stu-id="72b50-204">**Value**</span></span> |
  |--|--|
  | <span data-ttu-id="72b50-205">Nazwa</span><span class="sxs-lookup"><span data-stu-id="72b50-205">Name</span></span> | <span data-ttu-id="72b50-206">Zainstaluj usługę mobilności platformy Microsoft Azure (Linux)</span><span class="sxs-lookup"><span data-stu-id="72b50-206">Install Microsoft Azure Mobility Service (Linux)</span></span> |
  | <span data-ttu-id="72b50-207">Wiersz polecenia</span><span class="sxs-lookup"><span data-stu-id="72b50-207">Command line</span></span> | <span data-ttu-id="72b50-208">./install_linux.sh</span><span class="sxs-lookup"><span data-stu-id="72b50-208">./install_linux.sh</span></span> |
  | <span data-ttu-id="72b50-209">Program można uruchomić</span><span class="sxs-lookup"><span data-stu-id="72b50-209">Program can run</span></span> | <span data-ttu-id="72b50-210">Określa, czy użytkownik jest zalogowany</span><span class="sxs-lookup"><span data-stu-id="72b50-210">Whether or not a user is logged on</span></span> |

  ![Kreator zrzut ekranu tworzenia pakietu i programu](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-linux.png)

9. <span data-ttu-id="72b50-212">Na następnej stronie powitania, wybierz **ten program można uruchomić na dowolnej platformie**.</span><span class="sxs-lookup"><span data-stu-id="72b50-212">On hello next page, select **This program can run on any platform**.</span></span>
  <span data-ttu-id="72b50-213">![Kreator zrzut ekranu tworzenia pakietu i programu](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2-linux.png)</span><span class="sxs-lookup"><span data-stu-id="72b50-213">![Screenshot of Create Package and Program wizard](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2-linux.png)</span></span>

10. <span data-ttu-id="72b50-214">toocomplete hello kreatora, kliknij przycisk **dalej** dwa razy.</span><span class="sxs-lookup"><span data-stu-id="72b50-214">toocomplete hello wizard, click **Next** twice.</span></span>

> [!NOTE]
> <span data-ttu-id="72b50-215">skrypt Hello obsługuje zarówno nowe instalacje agentów usługi mobilności i aktualizuje tooagents, które zostały już zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="72b50-215">hello script supports both new installations of Mobility Service agents and updates tooagents that are already installed.</span></span>

### <a name="step-3-deploy-hello-package"></a><span data-ttu-id="72b50-216">Krok 3: Wdrażanie pakietu hello</span><span class="sxs-lookup"><span data-stu-id="72b50-216">Step 3: Deploy hello package</span></span>
1. <span data-ttu-id="72b50-217">W konsoli programu Configuration Manager hello, kliknij prawym przyciskiem myszy pakiet, a następnie wybierz **Dystrybuuj zawartość**.</span><span class="sxs-lookup"><span data-stu-id="72b50-217">In hello Configuration Manager console, right-click your package, and select **Distribute Content**.</span></span>
  <span data-ttu-id="72b50-218">![Zrzut ekranu programu Configuration Manager konsoli](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span><span class="sxs-lookup"><span data-stu-id="72b50-218">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span></span>
2. <span data-ttu-id="72b50-219">Wybierz hello  **[punktów dystrybucji](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)**  na toowhich pakietów hello powinien zostać skopiowany.</span><span class="sxs-lookup"><span data-stu-id="72b50-219">Select hello **[distribution points](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)** on toowhich hello packages should be copied.</span></span>
3. <span data-ttu-id="72b50-220">Kreator hello ukończone.</span><span class="sxs-lookup"><span data-stu-id="72b50-220">Complete hello wizard.</span></span> <span data-ttu-id="72b50-221">Hello pakietu, a następnie rozpoczyna replikację toohello określonych punktów dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="72b50-221">hello package then starts replicating toohello specified distribution points.</span></span>
4. <span data-ttu-id="72b50-222">Po dystrybucji pakietów hello jest gotowe, kliknij prawym przyciskiem myszy pakiet hello i wybierz opcję **Wdróż**.</span><span class="sxs-lookup"><span data-stu-id="72b50-222">After hello package distribution is done, right-click hello package, and select **Deploy**.</span></span>
  <span data-ttu-id="72b50-223">![Zrzut ekranu programu Configuration Manager konsoli](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span><span class="sxs-lookup"><span data-stu-id="72b50-223">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span></span>
5. <span data-ttu-id="72b50-224">Wybierz hello Linux Server kolekcji urządzeń, który został utworzony w sekcji wymagania wstępne hello jako hello kolekcję docelową dla wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="72b50-224">Select hello Linux Server device collection you created in hello prerequisites section as hello target collection for deployment.</span></span>

  ![Kreator zrzut ekranu wdrażania oprogramowania](./media/site-recovery-install-mobility-service-using-sccm/sccm-select-target-collection-linux.png)

6. <span data-ttu-id="72b50-226">Na powitania **określ miejsce docelowe zawartości hello** wybierz opcję sieci **punktów dystrybucji**.</span><span class="sxs-lookup"><span data-stu-id="72b50-226">On hello **Specify hello content destination** page, select your **Distribution Points**.</span></span>
7. <span data-ttu-id="72b50-227">Na powitania **toocontrol ustawienia Określ sposób wdrażania tego oprogramowania** upewnij się, że celem hello jest **wymagane**.</span><span class="sxs-lookup"><span data-stu-id="72b50-227">On hello **Specify settings toocontrol how this software is deployed** page, ensure that hello purpose is **Required**.</span></span>

  ![Kreator zrzut ekranu wdrażania oprogramowania](./media/site-recovery-install-mobility-service-using-sccm/sccm-deploy-select-purpose.png)

8. <span data-ttu-id="72b50-229">Na powitania **hello Określ harmonogram tego wdrożenia** Określ harmonogram.</span><span class="sxs-lookup"><span data-stu-id="72b50-229">On hello **Specify hello schedule for this deployment** page, specify a schedule.</span></span> <span data-ttu-id="72b50-230">Aby uzyskać więcej informacji, zobacz [planowania pakietów](https://technet.microsoft.com/library/gg682178.aspx).</span><span class="sxs-lookup"><span data-stu-id="72b50-230">For more information, see [scheduling packages](https://technet.microsoft.com/library/gg682178.aspx).</span></span>
9. <span data-ttu-id="72b50-231">Na powitania **punktów dystrybucji** Skonfiguruj właściwości hello zgodnie z potrzebami toohello centrum danych.</span><span class="sxs-lookup"><span data-stu-id="72b50-231">On hello **Distribution Points** page, configure hello properties according toohello needs of your datacenter.</span></span> <span data-ttu-id="72b50-232">Następnie wykonaj hello kreatora.</span><span class="sxs-lookup"><span data-stu-id="72b50-232">Then complete hello wizard.</span></span>

<span data-ttu-id="72b50-233">Pobiera zainstalować usługi mobilności na powitania serwera kolekcji urządzeń systemu Linux, zgodnie z toohello harmonogram, który został skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="72b50-233">Mobility Service gets installed on hello Linux Server Device Collection, according toohello schedule you configured.</span></span>

## <a name="other-methods-tooinstall-mobility-service"></a><span data-ttu-id="72b50-234">Inne metody tooinstall usługi mobilności</span><span class="sxs-lookup"><span data-stu-id="72b50-234">Other methods tooinstall Mobility Service</span></span>
<span data-ttu-id="72b50-235">Poniżej przedstawiono niektóre inne opcje instalacji usługi mobilności:</span><span class="sxs-lookup"><span data-stu-id="72b50-235">Here are some other options for installing Mobility Service:</span></span>
* [<span data-ttu-id="72b50-236">Ręczna instalacja przy użyciu graficznego interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="72b50-236">Manual Installation using GUI</span></span>](http://aka.ms/mobsvcmanualinstall)
* [<span data-ttu-id="72b50-237">Ręczna instalacja przy użyciu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="72b50-237">Manual Installation using command-line</span></span>](http://aka.ms/mobsvcmanualinstallcli)
* [<span data-ttu-id="72b50-238">Wypychana instalacja przy użyciu konfiguracji serwera</span><span class="sxs-lookup"><span data-stu-id="72b50-238">Push Installation using configuration server </span></span>](http://aka.ms/pushinstall)
* [<span data-ttu-id="72b50-239">Instalacji zautomatyzowanej przy użyciu usługi Automatyzacja Azure & konfiguracji żądanego stanu</span><span class="sxs-lookup"><span data-stu-id="72b50-239">Automated Installation using Azure Automation & Desired State Configuration </span></span>](http://aka.ms/mobsvcdscinstall)

## <a name="uninstall-mobility-service"></a><span data-ttu-id="72b50-240">Odinstaluj usługę mobilności</span><span class="sxs-lookup"><span data-stu-id="72b50-240">Uninstall Mobility Service</span></span>
<span data-ttu-id="72b50-241">Można utworzyć toouninstall pakietów programu Configuration Manager usługi mobilności.</span><span class="sxs-lookup"><span data-stu-id="72b50-241">You can create Configuration Manager packages toouninstall Mobility Service.</span></span> <span data-ttu-id="72b50-242">Witaj Użyj następującego skryptu toodo tak:</span><span class="sxs-lookup"><span data-stu-id="72b50-242">Use hello following script toodo so:</span></span>

```
Time /t >> C:\logfile.log
REM ==================================================
REM ==== Check if Mob Svc is already installed =======
REM ==== If not installed no operation required ========
REM ==== Else run uninstall command =====================
REM ==== {275197FC-14FD-4560-A5EB-38217F80CBD1} is ====
REM ==== guid for Mob Svc Installer ====================
whoami >> C:\logfile.log
NET START | FIND "InMage Scout Application Service"
IF  %ERRORLEVEL% EQU 1 (GOTO :INSTALL) ELSE GOTO :UNINSTALL
:NOOPERATION
                echo "No Operation Required." >> c:\logfile.log
                GOTO :ENDSCRIPT
:UNINSTALL
                echo "Uninstall" >> C:\logfile.log
                MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
:ENDSCRIPT

```

## <a name="next-steps"></a><span data-ttu-id="72b50-243">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="72b50-243">Next steps</span></span>
<span data-ttu-id="72b50-244">Teraz można przystąpić zbyt[Włącz ochronę](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-vmware-to-azure#step-6-replicate-applications) maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="72b50-244">You are now ready too[enable protection](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-vmware-to-azure#step-6-replicate-applications) for your virtual machines.</span></span>
