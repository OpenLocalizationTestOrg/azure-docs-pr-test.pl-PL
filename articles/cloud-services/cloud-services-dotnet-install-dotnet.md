---
title: "Zainstaluj program .NET w przypadku ról usługi w chmurze Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak ręcznie zainstaluj program .NET Framework na role usługi w chmurze sieci web i proces roboczy"
services: cloud-services
documentationcenter: .net
author: thraka
manager: timlt
editor: 
ms.assetid: 8d1243dc-879c-4d1f-9ed0-eecd1f6a6653
ms.service: cloud-services
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: adegeo
ms.openlocfilehash: a9cffa275ae6b9315b821d3160b17a997a1523f7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="install-net-on-azure-cloud-services-roles"></a><span data-ttu-id="639fc-103">Zainstaluj program .NET w przypadku ról usługi w chmurze Azure</span><span class="sxs-lookup"><span data-stu-id="639fc-103">Install .NET on Azure Cloud Services roles</span></span>
<span data-ttu-id="639fc-104">W tym artykule opisano sposób instalowania wersji programu .NET Framework, które nie pochodzą z systemu operacyjnego gościa Azure.</span><span class="sxs-lookup"><span data-stu-id="639fc-104">This article describes how to install versions of .NET Framework that don't come with the Azure Guest OS.</span></span> <span data-ttu-id="639fc-105">Aby skonfigurować role usługi w chmurze sieci web i proces roboczy, można użyć .NET na systemu operacyjnego gościa.</span><span class="sxs-lookup"><span data-stu-id="639fc-105">You can use .NET on the Guest OS to configure your cloud service web and worker roles.</span></span>

<span data-ttu-id="639fc-106">Na przykład można zainstalować .NET 4.6.1 rodziny systemów operacyjnych gościa 4, które nie pochodzą z dowolną wersją .NET 4.6.</span><span class="sxs-lookup"><span data-stu-id="639fc-106">For example, you can install .NET 4.6.1 on the Guest OS family 4, which doesn't come with any release of .NET 4.6.</span></span> <span data-ttu-id="639fc-107">(Rodziny systemów operacyjnych gościa 5 pochodzą z .NET 4.6). Aby uzyskać najnowsze informacje o wersjach systemu operacyjnego gościa Azure, zobacz [wiadomości wersji systemu operacyjnego gościa Azure](cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="639fc-107">(The Guest OS family 5 does come with .NET 4.6.) For the latest information on the Azure Guest OS releases, see the [Azure Guest OS release news](cloud-services-guestos-update-matrix.md).</span></span> 

>[!IMPORTANT]
><span data-ttu-id="639fc-108">Zestaw Azure SDK 2.9 zawiera ograniczenia dotyczące wdrażania .NET 4.6 rodziny systemów operacyjnych gościa, 4 lub starszym.</span><span class="sxs-lookup"><span data-stu-id="639fc-108">The Azure SDK 2.9 contains a restriction on deploying .NET 4.6 on the Guest OS family 4 or earlier.</span></span> <span data-ttu-id="639fc-109">Poprawka dla ograniczenia jest dostępna w [Microsoft Docs](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9) lokacji.</span><span class="sxs-lookup"><span data-stu-id="639fc-109">A fix for the restriction is available on the [Microsoft Docs](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9) site.</span></span>

<span data-ttu-id="639fc-110">Aby zainstalować program .NET w przypadku ról użytkownika sieci web i proces roboczy, należy uwzględnić Instalator sieci web .NET w ramach projektu usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="639fc-110">To install .NET on your web and worker roles, include the .NET web installer as part of your cloud service project.</span></span> <span data-ttu-id="639fc-111">Uruchamianie Instalatora jako część zadania uruchamiania roli.</span><span class="sxs-lookup"><span data-stu-id="639fc-111">Start the installer as part of the role's startup tasks.</span></span> 

## <a name="add-the-net-installer-to-your-project"></a><span data-ttu-id="639fc-112">Dodaj Instalator .NET do projektu</span><span class="sxs-lookup"><span data-stu-id="639fc-112">Add the .NET installer to your project</span></span>
<span data-ttu-id="639fc-113">Aby pobrać Instalatora sieci web dla programu .NET Framework, należy wybrać wersję, która ma zostać zainstalowany:</span><span class="sxs-lookup"><span data-stu-id="639fc-113">To download the web installer for the .NET Framework, choose the version that you want to install:</span></span>

* [<span data-ttu-id="639fc-114">Instalator sieci web .NET 4.7</span><span class="sxs-lookup"><span data-stu-id="639fc-114">.NET 4.7 web installer</span></span>](http://go.microsoft.com/fwlink/?LinkId=825298)
* [<span data-ttu-id="639fc-115">Instalator sieci web .NET 4.6.1</span><span class="sxs-lookup"><span data-stu-id="639fc-115">.NET 4.6.1 web installer</span></span>](http://go.microsoft.com/fwlink/?LinkId=671729)

<span data-ttu-id="639fc-116">Aby dodać Instalatora dla *web* roli:</span><span class="sxs-lookup"><span data-stu-id="639fc-116">To add the installer for a *web* role:</span></span>
  1. <span data-ttu-id="639fc-117">W **Eksploratora rozwiązań**w obszarze **ról** w projekcie usługi chmury, kliknij prawym przyciskiem myszy użytkownika *web* rolę i wybierz **Dodaj**  >  **Nowy Folder**.</span><span class="sxs-lookup"><span data-stu-id="639fc-117">In **Solution Explorer**, under **Roles** in your cloud service project, right-click your *web* role and select **Add** > **New Folder**.</span></span> <span data-ttu-id="639fc-118">Utwórz folder o nazwie **bin**.</span><span class="sxs-lookup"><span data-stu-id="639fc-118">Create a folder named **bin**.</span></span>
  2. <span data-ttu-id="639fc-119">Kliknij prawym przyciskiem myszy bin folder, a następnie wybierz **Dodaj** > **istniejący element**.</span><span class="sxs-lookup"><span data-stu-id="639fc-119">Right-click the bin folder and select **Add** > **Existing Item**.</span></span> <span data-ttu-id="639fc-120">Wybierz Instalatora .NET i dodaj go do folderu bin.</span><span class="sxs-lookup"><span data-stu-id="639fc-120">Select the .NET installer and add it to the bin folder.</span></span>
  
<span data-ttu-id="639fc-121">Aby dodać Instalatora dla *procesu roboczego* roli:</span><span class="sxs-lookup"><span data-stu-id="639fc-121">To add the installer for a *worker* role:</span></span>
* <span data-ttu-id="639fc-122">Kliknij prawym przyciskiem myszy użytkownika *procesu roboczego* rolę i wybierz **Dodaj** > **istniejący element**.</span><span class="sxs-lookup"><span data-stu-id="639fc-122">Right-click your *worker* role and select **Add** > **Existing Item**.</span></span> <span data-ttu-id="639fc-123">Wybierz Instalatora .NET i dodaj go do roli.</span><span class="sxs-lookup"><span data-stu-id="639fc-123">Select the .NET installer and add it to the role.</span></span> 

<span data-ttu-id="639fc-124">Kiedy pliki są dodawane w ten sposób do folderu zawartości roli, są one automatycznie dodawane do pakietu usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="639fc-124">When files are added in this way to the role content folder, they're automatically added to your cloud service package.</span></span> <span data-ttu-id="639fc-125">Następnie wdrażane pliki do lokalizacji spójne na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="639fc-125">The files are then deployed to a consistent location on the virtual machine.</span></span> <span data-ttu-id="639fc-126">Powtórz ten proces dla każdej roli sieci web i proces roboczy w usłudze w chmurze, aby wszystkie role mają kopię Instalatora.</span><span class="sxs-lookup"><span data-stu-id="639fc-126">Repeat this process for each web and worker role in your cloud service so that all roles have a copy of the installer.</span></span>

> [!NOTE]
> <span data-ttu-id="639fc-127">.NET 4.6.1 należy zainstalować na swojej roli usługi w chmurze, nawet jeśli jest przeznaczony dla aplikacji .NET 4.6.</span><span class="sxs-lookup"><span data-stu-id="639fc-127">You should install .NET 4.6.1 on your cloud service role even if your application targets .NET 4.6.</span></span> <span data-ttu-id="639fc-128">Systemu operacyjnego gościa zawiera bazy wiedzy Knowledge Base [aktualizacji 3098779](https://support.microsoft.com/kb/3098779) i [aktualizacji 3097997](https://support.microsoft.com/kb/3097997).</span><span class="sxs-lookup"><span data-stu-id="639fc-128">The Guest OS includes the Knowledge Base [update 3098779](https://support.microsoft.com/kb/3098779) and [update 3097997](https://support.microsoft.com/kb/3097997).</span></span> <span data-ttu-id="639fc-129">Problemy mogą wystąpić przy uruchamianiu aplikacji platformy .NET, jeśli .NET 4.6 zostanie zainstalowana na aktualizacje bazy wiedzy Knowledge Base.</span><span class="sxs-lookup"><span data-stu-id="639fc-129">Issues can occur when you run your .NET applications if .NET 4.6 is installed on top of the Knowledge Base updates.</span></span> <span data-ttu-id="639fc-130">Aby uniknąć tych problemów, należy zainstalować .NET 4.6.1 zamiast wersji 4.6.</span><span class="sxs-lookup"><span data-stu-id="639fc-130">To avoid these issues, install .NET 4.6.1 rather than version 4.6.</span></span> <span data-ttu-id="639fc-131">Aby uzyskać więcej informacji, zobacz [artykułu bazy wiedzy 3118750](https://support.microsoft.com/kb/3118750).</span><span class="sxs-lookup"><span data-stu-id="639fc-131">For more information, see the [Knowledge Base article 3118750](https://support.microsoft.com/kb/3118750).</span></span>
> 
> 

![Zawartość roli z plików Instalatora][1]

## <a name="define-startup-tasks-for-your-roles"></a><span data-ttu-id="639fc-133">Definiowanie zadań uruchomienia dla poszczególnych ról</span><span class="sxs-lookup"><span data-stu-id="639fc-133">Define startup tasks for your roles</span></span>
<span data-ttu-id="639fc-134">Zadania uruchamiania służy do wykonywania operacji przed rozpoczęciem roli.</span><span class="sxs-lookup"><span data-stu-id="639fc-134">You can use startup tasks to perform operations before a role starts.</span></span> <span data-ttu-id="639fc-135">Instalowanie programu .NET Framework jako część zadania uruchamiania zapewnia czy framework jest zainstalowany, przed uruchomieniem kodu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="639fc-135">Installing the .NET Framework as part of the startup task ensures that the framework is installed before any application code is run.</span></span> <span data-ttu-id="639fc-136">Aby uzyskać więcej informacji na temat uruchamiania zadań, zobacz [uruchamiać zadania uruchamiania na platformie Azure](cloud-services-startup-tasks.md).</span><span class="sxs-lookup"><span data-stu-id="639fc-136">For more information on startup tasks, see [Run startup tasks in Azure](cloud-services-startup-tasks.md).</span></span> 

1. <span data-ttu-id="639fc-137">Dodaj następującą zawartość do pliku ServiceDefinition.csdef **sieć Web** lub **proces roboczy** węzła dla wszystkich ról:</span><span class="sxs-lookup"><span data-stu-id="639fc-137">Add the following content to the ServiceDefinition.csdef file under the **WebRole** or **WorkerRole** node for all roles:</span></span>
   
    ```xml
    <LocalResources>
      <LocalStorage name="NETFXInstall" sizeInMB="1024" cleanOnRoleRecycle="false" />
    </LocalResources>    
    <Startup>
      <Task commandLine="install.cmd" executionContext="elevated" taskType="simple">
        <Environment>
          <Variable name="PathToNETFXInstall">
            <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='NETFXInstall']/@path" />
          </Variable>
          <Variable name="ComputeEmulatorRunning">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
          </Variable>
        </Environment>
      </Task>
    </Startup>
    ```
   
    <span data-ttu-id="639fc-138">Tej konfiguracji uruchamia polecenie konsoli `install.cmd` z uprawnieniami administratora do zainstalowania programu .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="639fc-138">The preceding configuration runs the console command `install.cmd` with administrator privileges to install the .NET Framework.</span></span> <span data-ttu-id="639fc-139">Tworzy również konfigurację **LocalStorage** elementu o nazwie **NETFXInstall**.</span><span class="sxs-lookup"><span data-stu-id="639fc-139">The configuration also creates a **LocalStorage** element named **NETFXInstall**.</span></span> <span data-ttu-id="639fc-140">Skrypt uruchamiania ustawia folder tymczasowy, aby użyć tego zasobu magazynu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="639fc-140">The startup script sets the temp folder to use this local storage resource.</span></span> 
    
    > [!IMPORTANT]
    > <span data-ttu-id="639fc-141">W celu zapewnienia prawidłowego zainstalowania platformy, należy ustawić rozmiaru tego zasobu na co najmniej 1024 MB.</span><span class="sxs-lookup"><span data-stu-id="639fc-141">To ensure correct installation of the framework, set the size of this resource to at least 1,024 MB.</span></span>
    
    <span data-ttu-id="639fc-142">Aby uzyskać więcej informacji na temat uruchamiania zadań, zobacz [wspólne usługi w chmurze Azure uruchamiania zadań](cloud-services-startup-tasks-common.md).</span><span class="sxs-lookup"><span data-stu-id="639fc-142">For more information about startup tasks, see [Common Azure Cloud Services startup tasks](cloud-services-startup-tasks-common.md).</span></span>

2. <span data-ttu-id="639fc-143">Utwórz plik o nazwie **install.cmd** i Dodaj poniższy skrypt instalacji do pliku.</span><span class="sxs-lookup"><span data-stu-id="639fc-143">Create a file named **install.cmd** and add the following install script to the file.</span></span>

    <span data-ttu-id="639fc-144">Skrypt sprawdza, czy określonej wersji programu .NET Framework jest już zainstalowana na komputerze, badając rejestru.</span><span class="sxs-lookup"><span data-stu-id="639fc-144">The script checks whether the specified version of the .NET Framework is already installed on the machine by querying the registry.</span></span> <span data-ttu-id="639fc-145">Jeśli nie zainstalowano programu .NET w wersji, Instalator sieci web .NET jest otwarty.</span><span class="sxs-lookup"><span data-stu-id="639fc-145">If the .NET version is not installed, then the .NET web installer is opened.</span></span> <span data-ttu-id="639fc-146">Do rozwiązywania problemów, skrypt logowania wszystkich działań pliku startuptasklog-(bieżącą datę i godzinę) .txt są przechowywane w **InstallLogs** Magazyn lokalny.</span><span class="sxs-lookup"><span data-stu-id="639fc-146">To help troubleshoot any issues, the script logs all activity to the file startuptasklog-(current date and time).txt that is stored in **InstallLogs** local storage.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="639fc-147">Umożliwia utworzenie pliku install.cmd edytorze tekstu podstawowego, takim jak Notatnik systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="639fc-147">Use a basic text editor like Windows Notepad to create the install.cmd file.</span></span> <span data-ttu-id="639fc-148">Jeśli używasz programu Visual Studio Utwórz plik tekstowy i zmień rozszerzenie na .cmd plik nadal może zawierać znacznik kolejności bajtów UTF-8.</span><span class="sxs-lookup"><span data-stu-id="639fc-148">If you use Visual Studio to create a text file and change the extension to .cmd, the file might still contain a UTF-8 byte order mark.</span></span> <span data-ttu-id="639fc-149">Znak ten może spowodować błąd, gdy jest uruchamiany pierwszy wiersz skryptu.</span><span class="sxs-lookup"><span data-stu-id="639fc-149">This mark can cause an error when the first line of the script is run.</span></span> <span data-ttu-id="639fc-150">Aby uniknąć tego błędu, należy w pierwszym wierszu skryptu REM — instrukcja, który był pomijany przez przetwarzanie kolejności bajtów.</span><span class="sxs-lookup"><span data-stu-id="639fc-150">To avoid this error, make the first line of the script a REM statement that can be skipped by the byte order processing.</span></span> 
    > 
    >
   
    ```cmd
    REM Set the value of netfx to install appropriate .NET Framework. 
    REM ***** To install .NET 4.5.2 set the variable netfx to "NDP452" *****
    REM ***** To install .NET 4.6 set the variable netfx to "NDP46" *****
    REM ***** To install .NET 4.6.1 set the variable netfx to "NDP461" *****
    REM ***** To install .NET 4.6.2 set the variable netfx to "NDP462" *****
    REM ***** To install .NET 4.7 set the variable netfx to "NDP47" *****
    set netfx="NDP47"

    REM ***** Set script start timestamp *****
    set timehour=%time:~0,2%
    set timestamp=%date:~-4,4%%date:~-10,2%%date:~-7,2%-%timehour: =0%%time:~3,2%
    set "log=install.cmd started %timestamp%."

    REM ***** Exit script if running in Emulator *****
    if %ComputeEmulatorRunning%=="true" goto exit

    REM ***** Needed to correctly install .NET 4.6.1, otherwise you may see an out of disk space error *****
    set TMP=%PathToNETFXInstall%
    set TEMP=%PathToNETFXInstall%

    REM ***** Setup .NET filenames and registry keys *****
    if %netfx%=="NDP47" goto NDP47
    if %netfx%=="NDP462" goto NDP462
    if %netfx%=="NDP461" goto NDP461
    if %netfx%=="NDP46" goto NDP46
        set "netfxinstallfile=NDP452-KB2901954-Web.exe"
        set netfxregkey="0x5cbf5"
        goto logtimestamp

    :NDP46
    set "netfxinstallfile=NDP46-KB3045560-Web.exe"
    set netfxregkey="0x6004f"
    goto logtimestamp

    :NDP461
    set "netfxinstallfile=NDP461-KB3102438-Web.exe"
    set netfxregkey="0x6040e"
    goto logtimestamp

    :NDP462
    set "netfxinstallfile=NDP462-KB3151802-Web.exe"
    set netfxregkey="0x60632"

    :NDP47
    set "netfxinstallfile=NDP47-KB3186500-Web.exe"
    set netfxregkey="0x707FE"

    :logtimestamp
    REM ***** Setup LogFile with timestamp *****
    md "%PathToNETFXInstall%\log"
    set startuptasklog="%PathToNETFXInstall%log\startuptasklog-%timestamp%.txt"
    set netfxinstallerlog="%PathToNETFXInstall%log\NetFXInstallerLog-%timestamp%"
    echo %log% >> %startuptasklog%
    echo Logfile generated at: %startuptasklog% >> %startuptasklog%
    echo TMP set to: %TMP% >> %startuptasklog%
    echo TEMP set to: %TEMP% >> %startuptasklog%

    REM ***** Check if .NET is installed *****
    echo Checking if .NET (%netfx%) is installed >> %startuptasklog%
    set /A netfxregkeydecimal=%netfxregkey%
    set foundkey=0
    FOR /F "usebackq skip=2 tokens=1,2*" %%A in (`reg query "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\NET Framework Setup\NDP\v4\Full" /v Release 2^>nul`) do @set /A foundkey=%%C
    echo Minimum required key: %netfxregkeydecimal% -- found key: %foundkey% >> %startuptasklog%
    if %foundkey% GEQ %netfxregkeydecimal% goto installed

    REM ***** Installing .NET *****
    echo Installing .NET with commandline: start /wait %~dp0%netfxinstallfile% /q /serialdownload /log %netfxinstallerlog%  /chainingpackage "CloudService Startup Task" >> %startuptasklog%
    start /wait %~dp0%netfxinstallfile% /q /serialdownload /log %netfxinstallerlog% /chainingpackage "CloudService Startup Task" >> %startuptasklog% 2>>&1
    if %ERRORLEVEL%== 0 goto installed
        echo .NET installer exited with code %ERRORLEVEL% >> %startuptasklog%    
        if %ERRORLEVEL%== 3010 goto restart
        if %ERRORLEVEL%== 1641 goto restart
        echo .NET (%netfx%) install failed with Error Code %ERRORLEVEL%. Further logs can be found in %netfxinstallerlog% >> %startuptasklog%

    :restart
    echo Restarting to complete .NET (%netfx%) installation >> %startuptasklog%
    EXIT /B %ERRORLEVEL%

    :installed
    echo .NET (%netfx%) is installed >> %startuptasklog%

    :end
    echo install.cmd completed: %date:~-4,4%%date:~-10,2%%date:~-7,2%-%timehour: =0%%time:~3,2% >> %startuptasklog%

    :exit
    EXIT /B 0
    ```
   
   > [!NOTE]
   > <span data-ttu-id="639fc-151">Ten skrypt pokazuje, jak zainstalować platformę .NET 4.5.2 lub wersji 4.6, aby utrzymać ciągłość, nawet jeśli jest już dostępne w systemie operacyjnym gościa Azure .NET 4.5.2.</span><span class="sxs-lookup"><span data-stu-id="639fc-151">This script shows how to install .NET 4.5.2 or version 4.6 for continuity, even though .NET 4.5.2 is already available on the Azure Guest OS.</span></span> <span data-ttu-id="639fc-152">Należy bezpośrednio zainstalować .NET 4.6.1 zamiast wersji 4.6, zgodnie z opisem w [artykułu bazy wiedzy 3118750](https://support.microsoft.com/kb/3118750).</span><span class="sxs-lookup"><span data-stu-id="639fc-152">You should directly install .NET 4.6.1 rather than version 4.6, as described in the [Knowledge Base article 3118750](https://support.microsoft.com/kb/3118750).</span></span>
   > 
   > 

3. <span data-ttu-id="639fc-153">Dodaj plik install.cmd do każdej roli przy użyciu **Dodaj** > **istniejący element** w **Eksploratora rozwiązań** zgodnie z opisem we wcześniejszej części tego tematu.</span><span class="sxs-lookup"><span data-stu-id="639fc-153">Add the install.cmd file to each role by using **Add** > **Existing Item** in **Solution Explorer** as described earlier in this topic.</span></span> 

    <span data-ttu-id="639fc-154">Po zakończeniu tego kroku wszystkie role powinny mieć plik Instalatora .NET i install.cmd pliku.</span><span class="sxs-lookup"><span data-stu-id="639fc-154">After this step is complete, all roles should have the .NET installer file and the install.cmd file.</span></span>

   ![Zawartość roli przy użyciu wszystkich plików][2]

## <a name="configure-diagnostics-to-transfer-startup-logs-to-blob-storage"></a><span data-ttu-id="639fc-156">Skonfigurować diagnostykę do uruchomienia dzienniki transferu do magazynu obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="639fc-156">Configure Diagnostics to transfer startup logs to Blob storage</span></span>
<span data-ttu-id="639fc-157">Aby ułatwić rozwiązywanie problemów z instalacji, możesz skonfigurować diagnostyki Azure, aby przenieść wszystkie pliki dziennika wygenerowane przez skryptu uruchomieniowego lub Instalator .NET do magazynu obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="639fc-157">To simplify troubleshooting installation issues, you can configure Azure Diagnostics to transfer any log files generated by the startup script or the .NET installer to Azure Blob storage.</span></span> <span data-ttu-id="639fc-158">Przy użyciu tej metody, można wyświetlić dzienniki, pobierania plików dziennika z magazynu obiektów Blob, zamiast konieczności pulpitu zdalnego do roli.</span><span class="sxs-lookup"><span data-stu-id="639fc-158">By using this approach, you can view the logs by downloading the log files from Blob storage rather than having to remote desktop into the role.</span></span>

<span data-ttu-id="639fc-159">Aby skonfigurować diagnostykę, otwórz plik diagnostics.wadcfgx i dodaj następującą zawartość w obszarze **katalogów** węzła:</span><span class="sxs-lookup"><span data-stu-id="639fc-159">To configure Diagnostics, open the diagnostics.wadcfgx file and add the following content under the **Directories** node:</span></span> 

```xml 
<DataSources>
 <DirectoryConfiguration containerName="netfx-install">
  <LocalResource name="NETFXInstall" relativePath="log"/>
 </DirectoryConfiguration>
</DataSources>
```

<span data-ttu-id="639fc-160">Plik XML konfiguruje diagnostyki do transferu plików w katalogu dziennika w **NETFXInstall** zasobów na koncie magazynu diagnostyki w **netfx instalacji** kontenera obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="639fc-160">This XML configures Diagnostics to transfer the files in the log directory in the **NETFXInstall** resource to the Diagnostics storage account in the **netfx-install** blob container.</span></span>

## <a name="deploy-your-cloud-service"></a><span data-ttu-id="639fc-161">Wdrażanie usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="639fc-161">Deploy your cloud service</span></span>
<span data-ttu-id="639fc-162">Podczas wdrażania usługi w chmurze, uruchamiania zadań zainstalowania programu .NET Framework, jeśli to nie jest jeszcze zainstalowana.</span><span class="sxs-lookup"><span data-stu-id="639fc-162">When you deploy your cloud service, the startup tasks install the .NET Framework if it's not already installed.</span></span> <span data-ttu-id="639fc-163">Role usługi w chmurze są w *zajęty* stanu podczas instalowania programu framework.</span><span class="sxs-lookup"><span data-stu-id="639fc-163">Your cloud service roles are in the *busy* state while the framework is being installed.</span></span> <span data-ttu-id="639fc-164">Jeśli instalacja framework wymaga ponownego uruchomienia, role usługi również może być ponownie.</span><span class="sxs-lookup"><span data-stu-id="639fc-164">If the framework installation requires a restart, the service roles might also restart.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="639fc-165">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="639fc-165">Additional resources</span></span>
* <span data-ttu-id="639fc-166">[Instalowanie programu .NET Framework][Installing the .NET Framework]</span><span class="sxs-lookup"><span data-stu-id="639fc-166">[Installing the .NET Framework][Installing the .NET Framework]</span></span>
* <span data-ttu-id="639fc-167">[Określanie, które wersje programu .NET Framework są zainstalowane][How to: Determine Which .NET Framework Versions Are Installed]</span><span class="sxs-lookup"><span data-stu-id="639fc-167">[Determine which .NET Framework versions are installed][How to: Determine Which .NET Framework Versions Are Installed]</span></span>
* <span data-ttu-id="639fc-168">[Rozwiązywanie problemów z instalacja programu .NET Framework][Troubleshooting .NET Framework Installations]</span><span class="sxs-lookup"><span data-stu-id="639fc-168">[Troubleshooting .NET Framework installations][Troubleshooting .NET Framework Installations]</span></span>

[How to: Determine Which .NET Framework Versions Are Installed]: https://msdn.microsoft.com/library/hh925568.aspx
[Installing the .NET Framework]: https://msdn.microsoft.com/library/5a4x27ek.aspx
[Troubleshooting .NET Framework Installations]: https://msdn.microsoft.com/library/hh925569.aspx

<!--Image references-->
[1]: ./media/cloud-services-dotnet-install-dotnet/rolecontentwithinstallerfiles.png
[2]: ./media/cloud-services-dotnet-install-dotnet/rolecontentwithallfiles.png
