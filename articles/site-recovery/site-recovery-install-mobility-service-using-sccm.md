---
title: "Proces instalacji usługi mobilności dla usługi Azure Site Recovery przy użyciu narzędzia wdrażania oprogramowania | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 49b72cd306aa91f114af7688f02d95db6f6eca05
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="automate-mobility-service-installation-by-using-software-deployment-tools"></a><span data-ttu-id="39e7c-103">Proces instalacji usługi mobilności przy użyciu narzędzia wdrażania oprogramowania</span><span class="sxs-lookup"><span data-stu-id="39e7c-103">Automate Mobility Service installation by using software deployment tools</span></span>

>[!IMPORTANT]
<span data-ttu-id="39e7c-104">Tym dokumencie przyjęto założenie, używana jest wersja **9.9.4510.1** lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="39e7c-104">This document assumes you are using version **9.9.4510.1** or higher.</span></span>

<span data-ttu-id="39e7c-105">Ten artykuł zawiera przykładowy sposób użycia programu System Center Configuration Manager do wdrażania usługi mobilności Azure Site Recovery w centrum danych.</span><span class="sxs-lookup"><span data-stu-id="39e7c-105">This article provides you an example of how you can use System Center Configuration Manager to deploy the Azure Site Recovery Mobility Service in your datacenter.</span></span> <span data-ttu-id="39e7c-106">Przy użyciu narzędzia wdrażania oprogramowania, np. programu Configuration Manager ma następujące zalety:</span><span class="sxs-lookup"><span data-stu-id="39e7c-106">Using a software deployment tool like Configuration Manager has the following advantages:</span></span>
* <span data-ttu-id="39e7c-107">Planowanie wdrożenia i aktualizacji, podczas okna zaplanowanej konserwacji dla aktualizacji oprogramowania</span><span class="sxs-lookup"><span data-stu-id="39e7c-107">Scheduling deployment of fresh installations and upgrades, during your planned maintenance window for software updates</span></span>
* <span data-ttu-id="39e7c-108">Jednocześnie skalowania wdrożenia setki serwerów</span><span class="sxs-lookup"><span data-stu-id="39e7c-108">Scaling deployment to hundreds of servers simultaneously</span></span>


> [!NOTE]
> <span data-ttu-id="39e7c-109">W tym artykule używa programu System Center Configuration Manager 2012 R2 do zaprezentowania działania wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="39e7c-109">This article uses System Center Configuration Manager 2012 R2 to demonstrate the deployment activity.</span></span> <span data-ttu-id="39e7c-110">Instalacja usługi mobilności może również zautomatyzować przy użyciu [usługi Automatyzacja Azure i konfiguracji żądanego stanu](site-recovery-automate-mobility-service-install.md).</span><span class="sxs-lookup"><span data-stu-id="39e7c-110">You could also automate Mobility Service installation by using [Azure Automation and Desired State Configuration](site-recovery-automate-mobility-service-install.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="39e7c-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="39e7c-111">Prerequisites</span></span>
1. <span data-ttu-id="39e7c-112">Narzędzia wdrażania oprogramowania, takie jak programu Configuration Manager, który jest już wdrożony w środowisku.</span><span class="sxs-lookup"><span data-stu-id="39e7c-112">A software deployment tool, like Configuration Manager, that is already deployed in your environment.</span></span>
  <span data-ttu-id="39e7c-113">Utwórz dwa [kolekcje urządzeń](https://technet.microsoft.com/library/gg682169.aspx), jeden dla wszystkich **serwerów z systemem Windows**i drugi dla wszystkich **serwerów z systemem Linux**, chcesz chronić za pomocą usługi Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="39e7c-113">Create two [device collections](https://technet.microsoft.com/library/gg682169.aspx), one for all **Windows servers**, and another for all **Linux servers**, that you want to protect by using Site Recovery.</span></span>
3. <span data-ttu-id="39e7c-114">Serwer konfiguracji jest już zarejestrowany z usługą Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="39e7c-114">A configuration server that is already registered with Site Recovery.</span></span>
4. <span data-ttu-id="39e7c-115">Bezpieczny sieciowego udziału plików (Server Message Block udziału), które są dostępne dla serwera programu Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="39e7c-115">A secure network file share (Server Message Block share) that can be accessed by the Configuration Manager server.</span></span>

## <a name="deploy-mobility-service-on-computers-running-windows"></a><span data-ttu-id="39e7c-116">Wdrażanie usługi mobilności na komputerach z systemem Windows</span><span class="sxs-lookup"><span data-stu-id="39e7c-116">Deploy Mobility Service on computers running Windows</span></span>
> [!NOTE]
> <span data-ttu-id="39e7c-117">W tym artykule przyjęto założenie, że adres IP serwera konfiguracji jest 192.168.3.121 i czy bezpiecznego sieciowego udziału plików jest \\\ContosoSecureFS\MobilityServiceInstallers.</span><span class="sxs-lookup"><span data-stu-id="39e7c-117">This article assumes that the IP address of the configuration server is 192.168.3.121, and that the secure network file share is \\\ContosoSecureFS\MobilityServiceInstallers.</span></span>

### <a name="step-1-prepare-for-deployment"></a><span data-ttu-id="39e7c-118">Krok 1: Przygotowanie do wdrożenia</span><span class="sxs-lookup"><span data-stu-id="39e7c-118">Step 1: Prepare for deployment</span></span>
1. <span data-ttu-id="39e7c-119">Utwórz folder w udziale sieciowym i nadaj jej nazwę **MobSvcWindows**.</span><span class="sxs-lookup"><span data-stu-id="39e7c-119">Create a folder on the network share, and name it **MobSvcWindows**.</span></span>
2. <span data-ttu-id="39e7c-120">Zaloguj się do konfiguracji serwera, a następnie otwórz administracyjny wiersz polecenia.</span><span class="sxs-lookup"><span data-stu-id="39e7c-120">Sign in to your configuration server, and open an administrative command prompt.</span></span>
3. <span data-ttu-id="39e7c-121">Uruchom następujące polecenia, aby wygenerować plik hasło:</span><span class="sxs-lookup"><span data-stu-id="39e7c-121">Run the following commands to generate a passphrase file:</span></span>

    `cd %ProgramData%\ASR\home\svsystems\bin`

    `genpassphrase.exe -v > MobSvc.passphrase`
4. <span data-ttu-id="39e7c-122">Kopiuj **MobSvc.passphrase** pliku do **MobSvcWindows** folderu w udziale sieciowym.</span><span class="sxs-lookup"><span data-stu-id="39e7c-122">Copy the **MobSvc.passphrase** file into the **MobSvcWindows** folder on your network share.</span></span>
5. <span data-ttu-id="39e7c-123">Przejdź do repozytorium Instalatora na serwerze konfiguracji, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="39e7c-123">Browse to the installer repository on the configuration server by running the following command:</span></span>

   `cd %ProgramData%\ASR\home\svsystems\puhsinstallsvc\repository`

6. <span data-ttu-id="39e7c-124">Kopia  **Microsoft ASR\_UA\_*wersji*\_Windows\_GA\_*data* \_Release.exe** do **MobSvcWindows** folderu w udziale sieciowym.</span><span class="sxs-lookup"><span data-stu-id="39e7c-124">Copy the **Microsoft-ASR\_UA\_*version*\_Windows\_GA\_*date*\_Release.exe** to the **MobSvcWindows** folder on your network share.</span></span>
7. <span data-ttu-id="39e7c-125">Skopiuj poniższy kod i zapisz go jako **install.bat** do **MobSvcWindows** folderu.</span><span class="sxs-lookup"><span data-stu-id="39e7c-125">Copy the following code, and save it as **install.bat** into the **MobSvcWindows** folder.</span></span>

   > [!NOTE]
   > <span data-ttu-id="39e7c-126">Zastąp symbole zastępcze [CSIP] w tym skrypcie rzeczywiste wartości adresu IP serwera konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="39e7c-126">Replace the [CSIP] placeholders in this script with the actual values of the IP address of your configuration server.</span></span>

```DOS
Time /t >> C:\Temp\logfile.log
REM ==================================================
REM ==== Clean up the folders ========================
RMDIR /S /q %temp%\MobSvc
MKDIR %Temp%\MobSvc
MKDIR C:\Temp
REM ==================================================

REM ==== Copy new files ==============================
COPY M*.* %Temp%\MobSvc
CD %Temp%\MobSvc
REN Micro*.exe MobSvcInstaller.exe
REM ==================================================

REM ==== Extract the installer =======================
MobSvcInstaller.exe /q /x:%Temp%\MobSvc\Extracted
REM ==== Wait 10s for extraction to complete =========
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

### <a name="step-2-create-a-package"></a><span data-ttu-id="39e7c-127">Krok 2: Tworzenie pakietu</span><span class="sxs-lookup"><span data-stu-id="39e7c-127">Step 2: Create a package</span></span>

1. <span data-ttu-id="39e7c-128">Zaloguj się do konsoli programu Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="39e7c-128">Sign in to your Configuration Manager console.</span></span>
2. <span data-ttu-id="39e7c-129">Przejdź do **Biblioteka oprogramowania** > **Zarządzanie aplikacjami** > **pakiety**.</span><span class="sxs-lookup"><span data-stu-id="39e7c-129">Browse to **Software Library** > **Application Management** > **Packages**.</span></span>
3. <span data-ttu-id="39e7c-130">Kliknij prawym przyciskiem myszy **pakiety**i wybierz **tworzenia pakietu**.</span><span class="sxs-lookup"><span data-stu-id="39e7c-130">Right-click **Packages**, and select **Create Package**.</span></span>
4. <span data-ttu-id="39e7c-131">Podaj wartości dla nazwy, opisu, producenta, język i wersję.</span><span class="sxs-lookup"><span data-stu-id="39e7c-131">Provide values for the name, description, manufacturer, language, and version.</span></span>
5. <span data-ttu-id="39e7c-132">Wybierz **ten pakiet zawiera pliki źródłowe** pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="39e7c-132">Select the **This package contains source files** check box.</span></span>
6. <span data-ttu-id="39e7c-133">Kliknij przycisk **Przeglądaj**i wybierz udziału sieciowego, w którym przechowywana jest Instalator (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcWindows).</span><span class="sxs-lookup"><span data-stu-id="39e7c-133">Click **Browse**, and select the network share where the installer is stored (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcWindows).</span></span>

  ![Kreator zrzut ekranu tworzenia pakietu i programu](./media/site-recovery-install-mobility-service-using-sccm/create_sccm_package.png)

7. <span data-ttu-id="39e7c-135">Na **wybierz typ programu, który chcesz utworzyć** wybierz pozycję **Program standardowy**i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="39e7c-135">On the **Choose the program type that you want to create** page, select **Standard Program**, and click **Next**.</span></span>

  ![Kreator zrzut ekranu tworzenia pakietu i programu](./media/site-recovery-install-mobility-service-using-sccm/sccm-standard-program.png)

8. <span data-ttu-id="39e7c-137">Na **Podaj informacje dotyczące tego programu standardowego** , podaj następujące dane wejściowe i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="39e7c-137">On the **Specify information about this standard program** page, provide the following inputs, and click **Next**.</span></span> <span data-ttu-id="39e7c-138">(Inne dane wejściowe można użyć wartości domyślnych).</span><span class="sxs-lookup"><span data-stu-id="39e7c-138">(The other inputs can use their default values.)</span></span>

  | <span data-ttu-id="39e7c-139">**Nazwa parametru**</span><span class="sxs-lookup"><span data-stu-id="39e7c-139">**Parameter name**</span></span> | <span data-ttu-id="39e7c-140">**Wartość**</span><span class="sxs-lookup"><span data-stu-id="39e7c-140">**Value**</span></span> |
  |--|--|
  | <span data-ttu-id="39e7c-141">Nazwa</span><span class="sxs-lookup"><span data-stu-id="39e7c-141">Name</span></span> | <span data-ttu-id="39e7c-142">Zainstaluj usługę mobilności platformy Microsoft Azure (system Windows)</span><span class="sxs-lookup"><span data-stu-id="39e7c-142">Install Microsoft Azure Mobility Service (Windows)</span></span> |
  | <span data-ttu-id="39e7c-143">Wiersz polecenia</span><span class="sxs-lookup"><span data-stu-id="39e7c-143">Command line</span></span> | <span data-ttu-id="39e7c-144">Install.bat</span><span class="sxs-lookup"><span data-stu-id="39e7c-144">install.bat</span></span> |
  | <span data-ttu-id="39e7c-145">Program można uruchomić</span><span class="sxs-lookup"><span data-stu-id="39e7c-145">Program can run</span></span> | <span data-ttu-id="39e7c-146">Określa, czy użytkownik jest zalogowany</span><span class="sxs-lookup"><span data-stu-id="39e7c-146">Whether or not a user is logged on</span></span> |

  ![Kreator zrzut ekranu tworzenia pakietu i programu](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties.png)

9. <span data-ttu-id="39e7c-148">Na następnej stronie wybierz systemów operacyjnych.</span><span class="sxs-lookup"><span data-stu-id="39e7c-148">On the next page, select the target operating systems.</span></span> <span data-ttu-id="39e7c-149">Tylko w systemie Windows Server 2012 R2, Windows Server 2012 i Windows Server 2008 R2 można zainstalować usługi mobilności.</span><span class="sxs-lookup"><span data-stu-id="39e7c-149">Mobility Service can be installed only on Windows Server 2012 R2, Windows Server 2012, and Windows Server 2008 R2.</span></span>

  ![Kreator zrzut ekranu tworzenia pakietu i programu](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2.png)

10. <span data-ttu-id="39e7c-151">Aby ukończyć pracę kreatora, kliknij przycisk **dalej** dwa razy.</span><span class="sxs-lookup"><span data-stu-id="39e7c-151">To complete the wizard, click **Next** twice.</span></span>


> [!NOTE]
> <span data-ttu-id="39e7c-152">Skrypt obsługuje zarówno nowe instalacje agentów usługi mobilności i aktualizacji agentów, które są już zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="39e7c-152">The script supports both new installations of Mobility Service agents and updates to agents that are already installed.</span></span>

### <a name="step-3-deploy-the-package"></a><span data-ttu-id="39e7c-153">Krok 3: Wdrażanie pakietu</span><span class="sxs-lookup"><span data-stu-id="39e7c-153">Step 3: Deploy the package</span></span>
1. <span data-ttu-id="39e7c-154">W konsoli programu Configuration Manager, kliknij prawym przyciskiem myszy pakiet, a następnie wybierz **Dystrybuuj zawartość**.</span><span class="sxs-lookup"><span data-stu-id="39e7c-154">In the Configuration Manager console, right-click your package, and select **Distribute Content**.</span></span>
  <span data-ttu-id="39e7c-155">![Zrzut ekranu programu Configuration Manager konsoli](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span><span class="sxs-lookup"><span data-stu-id="39e7c-155">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span></span>
2. <span data-ttu-id="39e7c-156">Wybierz  **[punktów dystrybucji](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)**  , do którego powinien zostać skopiowany pakiety.</span><span class="sxs-lookup"><span data-stu-id="39e7c-156">Select the **[distribution points](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)** on to which the packages should be copied.</span></span>
3. <span data-ttu-id="39e7c-157">Ukończ pracę kreatora.</span><span class="sxs-lookup"><span data-stu-id="39e7c-157">Complete the wizard.</span></span> <span data-ttu-id="39e7c-158">Pakiet następnie rozpoczyna replikację do określonych punktach dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="39e7c-158">The package then starts replicating to the specified distribution points.</span></span>
4. <span data-ttu-id="39e7c-159">Po ukończeniu dystrybucji pakietu, kliknij prawym przyciskiem myszy pakiet i wybierz **Wdróż**.</span><span class="sxs-lookup"><span data-stu-id="39e7c-159">After the package distribution is done, right-click the package, and select **Deploy**.</span></span>
  <span data-ttu-id="39e7c-160">![Zrzut ekranu programu Configuration Manager konsoli](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span><span class="sxs-lookup"><span data-stu-id="39e7c-160">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span></span>
5. <span data-ttu-id="39e7c-161">Zaznacz kolekcję urządzeń z systemem Windows Server, utworzony w sekcji wymagania wstępne jako kolekcję docelową dla wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="39e7c-161">Select the Windows Server device collection you created in the prerequisites section as the target collection for deployment.</span></span>

  ![Kreator zrzut ekranu wdrażania oprogramowania](./media/site-recovery-install-mobility-service-using-sccm/sccm-select-target-collection.png)

6. <span data-ttu-id="39e7c-163">Na **określ miejsce docelowe zawartości** wybierz opcję sieci **punktów dystrybucji**.</span><span class="sxs-lookup"><span data-stu-id="39e7c-163">On the **Specify the content destination** page, select your **Distribution Points**.</span></span>
7. <span data-ttu-id="39e7c-164">Na **Określ ustawienia określające sposób wdrażania tego oprogramowania** upewnij się, że celem jest **wymagane**.</span><span class="sxs-lookup"><span data-stu-id="39e7c-164">On the **Specify settings to control how this software is deployed** page, ensure that the purpose is **Required**.</span></span>

  ![Kreator zrzut ekranu wdrażania oprogramowania](./media/site-recovery-install-mobility-service-using-sccm/sccm-deploy-select-purpose.png)

8. <span data-ttu-id="39e7c-166">Na **Określ harmonogram tego wdrożenia** Określ harmonogram.</span><span class="sxs-lookup"><span data-stu-id="39e7c-166">On the **Specify the schedule for this deployment** page, specify a schedule.</span></span> <span data-ttu-id="39e7c-167">Aby uzyskać więcej informacji, zobacz [planowania pakietów](https://technet.microsoft.com/library/gg682178.aspx).</span><span class="sxs-lookup"><span data-stu-id="39e7c-167">For more information, see [scheduling packages](https://technet.microsoft.com/library/gg682178.aspx).</span></span>
9. <span data-ttu-id="39e7c-168">Na **punktów dystrybucji** Skonfiguruj właściwości odpowiednio do potrzeb centrum danych.</span><span class="sxs-lookup"><span data-stu-id="39e7c-168">On the **Distribution Points** page, configure the properties according to the needs of your datacenter.</span></span> <span data-ttu-id="39e7c-169">Następnie Zakończ pracę kreatora.</span><span class="sxs-lookup"><span data-stu-id="39e7c-169">Then complete the wizard.</span></span>

> [!TIP]
> <span data-ttu-id="39e7c-170">Aby uniknąć niepotrzebnych ponowne uruchomienia, należy zaplanować instalacji pakietu podczas z comiesięcznej konserwacji lub okna aktualizacji oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="39e7c-170">To avoid unnecessary reboots, schedule the package installation during your monthly maintenance window or software updates window.</span></span>

<span data-ttu-id="39e7c-171">Możesz monitorować postęp wdrażania przy użyciu konsoli programu Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="39e7c-171">You can monitor the deployment progress by using the Configuration Manager console.</span></span> <span data-ttu-id="39e7c-172">Przejdź do **monitorowanie** > **wdrożeń** > *[nazwa pakietu]*.</span><span class="sxs-lookup"><span data-stu-id="39e7c-172">Go to **Monitoring** > **Deployments** > *[your package name]*.</span></span>

  ![Zrzut ekranu Menedżera konfiguracji możliwość monitorowania wdrożeń](./media/site-recovery-install-mobility-service-using-sccm/report.PNG)

## <a name="deploy-mobility-service-on-computers-running-linux"></a><span data-ttu-id="39e7c-174">Wdrażanie usługi mobilności na komputerach z systemem Linux</span><span class="sxs-lookup"><span data-stu-id="39e7c-174">Deploy Mobility Service on computers running Linux</span></span>
> [!NOTE]
> <span data-ttu-id="39e7c-175">W tym artykule przyjęto założenie, że adres IP serwera konfiguracji jest 192.168.3.121 i czy bezpiecznego sieciowego udziału plików jest \\\ContosoSecureFS\MobilityServiceInstallers.</span><span class="sxs-lookup"><span data-stu-id="39e7c-175">This article assumes that the IP address of the configuration server is 192.168.3.121, and that the secure network file share is \\\ContosoSecureFS\MobilityServiceInstallers.</span></span>

### <a name="step-1-prepare-for-deployment"></a><span data-ttu-id="39e7c-176">Krok 1: Przygotowanie do wdrożenia</span><span class="sxs-lookup"><span data-stu-id="39e7c-176">Step 1: Prepare for deployment</span></span>
1. <span data-ttu-id="39e7c-177">Utwórz folder w udziale sieciowym i nazywa je jako **MobSvcLinux**.</span><span class="sxs-lookup"><span data-stu-id="39e7c-177">Create a folder on the network share, and name it as **MobSvcLinux**.</span></span>
2. <span data-ttu-id="39e7c-178">Zaloguj się do konfiguracji serwera, a następnie otwórz administracyjny wiersz polecenia.</span><span class="sxs-lookup"><span data-stu-id="39e7c-178">Sign in to your configuration server, and open an administrative command prompt.</span></span>
3. <span data-ttu-id="39e7c-179">Uruchom następujące polecenia, aby wygenerować plik hasło:</span><span class="sxs-lookup"><span data-stu-id="39e7c-179">Run the following commands to generate a passphrase file:</span></span>

    `cd %ProgramData%\ASR\home\svsystems\bin`

    `genpassphrase.exe -v > MobSvc.passphrase`
4. <span data-ttu-id="39e7c-180">Kopiuj **MobSvc.passphrase** pliku do **MobSvcLinux** folderu w udziale sieciowym.</span><span class="sxs-lookup"><span data-stu-id="39e7c-180">Copy the **MobSvc.passphrase** file into the **MobSvcLinux** folder on your network share.</span></span>
5. <span data-ttu-id="39e7c-181">Przejdź do repozytorium Instalatora na serwerze konfiguracji, uruchamiając polecenie:</span><span class="sxs-lookup"><span data-stu-id="39e7c-181">Browse to the installer repository on the configuration server by running the command:</span></span>

   `cd %ProgramData%\ASR\home\svsystems\puhsinstallsvc\repository`

6. <span data-ttu-id="39e7c-182">Skopiuj następujące pliki do **MobSvcLinux** folderu w udziale sieciowym:</span><span class="sxs-lookup"><span data-stu-id="39e7c-182">Copy the following files to the **MobSvcLinux** folder on your network share:</span></span>
   * <span data-ttu-id="39e7c-183">Usługa ASR Microsoft\_UA\*RHEL6 64*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="39e7c-183">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span></span>
   * <span data-ttu-id="39e7c-184">Usługa ASR Microsoft\_UA\*RHEL7 64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="39e7c-184">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span></span>
   * <span data-ttu-id="39e7c-185">Usługa ASR Microsoft\_UA\*SLES11-SP3-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="39e7c-185">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span></span>
   * <span data-ttu-id="39e7c-186">Usługa ASR Microsoft\_UA\*SLES11-SP4-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="39e7c-186">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span></span>
   * <span data-ttu-id="39e7c-187">Usługa ASR Microsoft\_UA\*OL6 64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="39e7c-187">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span></span>
   * <span data-ttu-id="39e7c-188">Usługa ASR Microsoft\_UA\*UBUNTU-14.04-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="39e7c-188">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span></span>


7. <span data-ttu-id="39e7c-189">Skopiuj poniższy kod i zapisz go jako **install_linux.sh** do **MobSvcLinux** folderu.</span><span class="sxs-lookup"><span data-stu-id="39e7c-189">Copy the following code, and save it as **install_linux.sh** into the **MobSvcLinux** folder.</span></span>
   > [!NOTE]
   > <span data-ttu-id="39e7c-190">Zastąp symbole zastępcze [CSIP] w tym skrypcie rzeczywiste wartości adresu IP serwera konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="39e7c-190">Replace the [CSIP] placeholders in this script with the actual values of the IP address of your configuration server.</span></span>

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
        echo "Installation has succeeded. Proceed to configuration." >> /tmp/MobSvc/sccm.log
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
        echo "Agent is already configured. Proceed to Upgrade." >> /tmp/MobSvc/sccm.log
        Upgrade
    else
        echo "Agent is not configured. Proceed to Configure." >> /tmp/MobSvc/sccm.log
        Configure
    fi
else
    Install
fi

cd /tmp

```

### <a name="step-2-create-a-package"></a><span data-ttu-id="39e7c-191">Krok 2: Tworzenie pakietu</span><span class="sxs-lookup"><span data-stu-id="39e7c-191">Step 2: Create a package</span></span>

1. <span data-ttu-id="39e7c-192">Zaloguj się do konsoli programu Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="39e7c-192">Sign in  to your Configuration Manager console.</span></span>
2. <span data-ttu-id="39e7c-193">Przejdź do **Biblioteka oprogramowania** > **Zarządzanie aplikacjami** > **pakiety**.</span><span class="sxs-lookup"><span data-stu-id="39e7c-193">Browse to **Software Library** > **Application Management** > **Packages**.</span></span>
3. <span data-ttu-id="39e7c-194">Kliknij prawym przyciskiem myszy **pakiety**i wybierz **tworzenia pakietu**.</span><span class="sxs-lookup"><span data-stu-id="39e7c-194">Right-click **Packages**, and select **Create Package**.</span></span>
4. <span data-ttu-id="39e7c-195">Podaj wartości dla nazwy, opisu, producenta, język i wersję.</span><span class="sxs-lookup"><span data-stu-id="39e7c-195">Provide values for the name, description, manufacturer, language, and version.</span></span>
5. <span data-ttu-id="39e7c-196">Wybierz **ten pakiet zawiera pliki źródłowe** pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="39e7c-196">Select the **This package contains source files** check box.</span></span>
6. <span data-ttu-id="39e7c-197">Kliknij przycisk **Przeglądaj**i wybierz udziału sieciowego, w którym przechowywana jest Instalator (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcLinux).</span><span class="sxs-lookup"><span data-stu-id="39e7c-197">Click **Browse**, and select the network share where the installer is stored (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcLinux).</span></span>

  ![Kreator zrzut ekranu tworzenia pakietu i programu](./media/site-recovery-install-mobility-service-using-sccm/create_sccm_package-linux.png)

7. <span data-ttu-id="39e7c-199">Na **wybierz typ programu, który chcesz utworzyć** wybierz pozycję **Program standardowy**i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="39e7c-199">On the **Choose the program type that you want to create** page, select **Standard Program**, and click **Next**.</span></span>

  ![Kreator zrzut ekranu tworzenia pakietu i programu](./media/site-recovery-install-mobility-service-using-sccm/sccm-standard-program.png)

8. <span data-ttu-id="39e7c-201">Na **Podaj informacje dotyczące tego programu standardowego** , podaj następujące dane wejściowe i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="39e7c-201">On the **Specify information about this standard program** page, provide the following inputs, and click **Next**.</span></span> <span data-ttu-id="39e7c-202">(Inne dane wejściowe można użyć wartości domyślnych).</span><span class="sxs-lookup"><span data-stu-id="39e7c-202">(The other inputs can use their default values.)</span></span>

    | <span data-ttu-id="39e7c-203">**Nazwa parametru**</span><span class="sxs-lookup"><span data-stu-id="39e7c-203">**Parameter name**</span></span> | <span data-ttu-id="39e7c-204">**Wartość**</span><span class="sxs-lookup"><span data-stu-id="39e7c-204">**Value**</span></span> |
  |--|--|
  | <span data-ttu-id="39e7c-205">Nazwa</span><span class="sxs-lookup"><span data-stu-id="39e7c-205">Name</span></span> | <span data-ttu-id="39e7c-206">Zainstaluj usługę mobilności platformy Microsoft Azure (Linux)</span><span class="sxs-lookup"><span data-stu-id="39e7c-206">Install Microsoft Azure Mobility Service (Linux)</span></span> |
  | <span data-ttu-id="39e7c-207">Wiersz polecenia</span><span class="sxs-lookup"><span data-stu-id="39e7c-207">Command line</span></span> | <span data-ttu-id="39e7c-208">./install_linux.sh</span><span class="sxs-lookup"><span data-stu-id="39e7c-208">./install_linux.sh</span></span> |
  | <span data-ttu-id="39e7c-209">Program można uruchomić</span><span class="sxs-lookup"><span data-stu-id="39e7c-209">Program can run</span></span> | <span data-ttu-id="39e7c-210">Określa, czy użytkownik jest zalogowany</span><span class="sxs-lookup"><span data-stu-id="39e7c-210">Whether or not a user is logged on</span></span> |

  ![Kreator zrzut ekranu tworzenia pakietu i programu](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-linux.png)

9. <span data-ttu-id="39e7c-212">Na następnej stronie wybierz **ten program można uruchomić na dowolnej platformie**.</span><span class="sxs-lookup"><span data-stu-id="39e7c-212">On the next page, select **This program can run on any platform**.</span></span>
  <span data-ttu-id="39e7c-213">![Kreator zrzut ekranu tworzenia pakietu i programu](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2-linux.png)</span><span class="sxs-lookup"><span data-stu-id="39e7c-213">![Screenshot of Create Package and Program wizard](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2-linux.png)</span></span>

10. <span data-ttu-id="39e7c-214">Aby ukończyć pracę kreatora, kliknij przycisk **dalej** dwa razy.</span><span class="sxs-lookup"><span data-stu-id="39e7c-214">To complete the wizard, click **Next** twice.</span></span>

> [!NOTE]
> <span data-ttu-id="39e7c-215">Skrypt obsługuje zarówno nowe instalacje agentów usługi mobilności i aktualizacji agentów, które są już zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="39e7c-215">The script supports both new installations of Mobility Service agents and updates to agents that are already installed.</span></span>

### <a name="step-3-deploy-the-package"></a><span data-ttu-id="39e7c-216">Krok 3: Wdrażanie pakietu</span><span class="sxs-lookup"><span data-stu-id="39e7c-216">Step 3: Deploy the package</span></span>
1. <span data-ttu-id="39e7c-217">W konsoli programu Configuration Manager, kliknij prawym przyciskiem myszy pakiet, a następnie wybierz **Dystrybuuj zawartość**.</span><span class="sxs-lookup"><span data-stu-id="39e7c-217">In the Configuration Manager console, right-click your package, and select **Distribute Content**.</span></span>
  <span data-ttu-id="39e7c-218">![Zrzut ekranu programu Configuration Manager konsoli](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span><span class="sxs-lookup"><span data-stu-id="39e7c-218">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span></span>
2. <span data-ttu-id="39e7c-219">Wybierz  **[punktów dystrybucji](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)**  , do którego powinien zostać skopiowany pakiety.</span><span class="sxs-lookup"><span data-stu-id="39e7c-219">Select the **[distribution points](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)** on to which the packages should be copied.</span></span>
3. <span data-ttu-id="39e7c-220">Ukończ pracę kreatora.</span><span class="sxs-lookup"><span data-stu-id="39e7c-220">Complete the wizard.</span></span> <span data-ttu-id="39e7c-221">Pakiet następnie rozpoczyna replikację do określonych punktach dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="39e7c-221">The package then starts replicating to the specified distribution points.</span></span>
4. <span data-ttu-id="39e7c-222">Po ukończeniu dystrybucji pakietu, kliknij prawym przyciskiem myszy pakiet i wybierz **Wdróż**.</span><span class="sxs-lookup"><span data-stu-id="39e7c-222">After the package distribution is done, right-click the package, and select **Deploy**.</span></span>
  <span data-ttu-id="39e7c-223">![Zrzut ekranu programu Configuration Manager konsoli](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span><span class="sxs-lookup"><span data-stu-id="39e7c-223">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span></span>
5. <span data-ttu-id="39e7c-224">Zaznacz kolekcję urządzeń Linux Server utworzonego w sekcji wymagania wstępne jako kolekcję docelową dla wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="39e7c-224">Select the Linux Server device collection you created in the prerequisites section as the target collection for deployment.</span></span>

  ![Kreator zrzut ekranu wdrażania oprogramowania](./media/site-recovery-install-mobility-service-using-sccm/sccm-select-target-collection-linux.png)

6. <span data-ttu-id="39e7c-226">Na **określ miejsce docelowe zawartości** wybierz opcję sieci **punktów dystrybucji**.</span><span class="sxs-lookup"><span data-stu-id="39e7c-226">On the **Specify the content destination** page, select your **Distribution Points**.</span></span>
7. <span data-ttu-id="39e7c-227">Na **Określ ustawienia określające sposób wdrażania tego oprogramowania** upewnij się, że celem jest **wymagane**.</span><span class="sxs-lookup"><span data-stu-id="39e7c-227">On the **Specify settings to control how this software is deployed** page, ensure that the purpose is **Required**.</span></span>

  ![Kreator zrzut ekranu wdrażania oprogramowania](./media/site-recovery-install-mobility-service-using-sccm/sccm-deploy-select-purpose.png)

8. <span data-ttu-id="39e7c-229">Na **Określ harmonogram tego wdrożenia** Określ harmonogram.</span><span class="sxs-lookup"><span data-stu-id="39e7c-229">On the **Specify the schedule for this deployment** page, specify a schedule.</span></span> <span data-ttu-id="39e7c-230">Aby uzyskać więcej informacji, zobacz [planowania pakietów](https://technet.microsoft.com/library/gg682178.aspx).</span><span class="sxs-lookup"><span data-stu-id="39e7c-230">For more information, see [scheduling packages](https://technet.microsoft.com/library/gg682178.aspx).</span></span>
9. <span data-ttu-id="39e7c-231">Na **punktów dystrybucji** Skonfiguruj właściwości odpowiednio do potrzeb centrum danych.</span><span class="sxs-lookup"><span data-stu-id="39e7c-231">On the **Distribution Points** page, configure the properties according to the needs of your datacenter.</span></span> <span data-ttu-id="39e7c-232">Następnie Zakończ pracę kreatora.</span><span class="sxs-lookup"><span data-stu-id="39e7c-232">Then complete the wizard.</span></span>

<span data-ttu-id="39e7c-233">Pobiera zainstalować usługi mobilności na kolekcji urządzeń serwera z systemem Linux zgodnie z harmonogramem, które zostały skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="39e7c-233">Mobility Service gets installed on the Linux Server Device Collection, according to the schedule you configured.</span></span>

## <a name="other-methods-to-install-mobility-service"></a><span data-ttu-id="39e7c-234">Inne metody, aby zainstalować usługi mobilności</span><span class="sxs-lookup"><span data-stu-id="39e7c-234">Other methods to install Mobility Service</span></span>
<span data-ttu-id="39e7c-235">Poniżej przedstawiono niektóre inne opcje instalacji usługi mobilności:</span><span class="sxs-lookup"><span data-stu-id="39e7c-235">Here are some other options for installing Mobility Service:</span></span>
* [<span data-ttu-id="39e7c-236">Ręczna instalacja przy użyciu graficznego interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="39e7c-236">Manual Installation using GUI</span></span>](http://aka.ms/mobsvcmanualinstall)
* [<span data-ttu-id="39e7c-237">Ręczna instalacja przy użyciu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="39e7c-237">Manual Installation using command-line</span></span>](http://aka.ms/mobsvcmanualinstallcli)
* [<span data-ttu-id="39e7c-238">Wypychana instalacja przy użyciu konfiguracji serwera</span><span class="sxs-lookup"><span data-stu-id="39e7c-238">Push Installation using configuration server </span></span>](http://aka.ms/pushinstall)
* [<span data-ttu-id="39e7c-239">Instalacji zautomatyzowanej przy użyciu usługi Automatyzacja Azure & konfiguracji żądanego stanu</span><span class="sxs-lookup"><span data-stu-id="39e7c-239">Automated Installation using Azure Automation & Desired State Configuration </span></span>](http://aka.ms/mobsvcdscinstall)

## <a name="uninstall-mobility-service"></a><span data-ttu-id="39e7c-240">Odinstaluj usługę mobilności</span><span class="sxs-lookup"><span data-stu-id="39e7c-240">Uninstall Mobility Service</span></span>
<span data-ttu-id="39e7c-241">Można utworzyć pakiety programu Configuration Manager można odinstalować usługi mobilności.</span><span class="sxs-lookup"><span data-stu-id="39e7c-241">You can create Configuration Manager packages to uninstall Mobility Service.</span></span> <span data-ttu-id="39e7c-242">Aby to zrobić, użyj następującego skryptu:</span><span class="sxs-lookup"><span data-stu-id="39e7c-242">Use the following script to do so:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="39e7c-243">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="39e7c-243">Next steps</span></span>
<span data-ttu-id="39e7c-244">Teraz można przystąpić do [Włącz ochronę](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-vmware-to-azure#step-6-replicate-applications) maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="39e7c-244">You are now ready to [enable protection](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-vmware-to-azure#step-6-replicate-applications) for your virtual machines.</span></span>
