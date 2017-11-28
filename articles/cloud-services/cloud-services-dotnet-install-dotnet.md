---
title: "aaaInstall .NET z ról, usług Azure Cloud Services | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak zainstalować toomanually hello .NET Framework na role usługi w chmurze sieci web i proces roboczy"
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
ms.openlocfilehash: 45f0f30221292f98c591511b091b02ebe1c1272c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-net-on-azure-cloud-services-roles"></a><span data-ttu-id="c192a-103">Zainstaluj program .NET w przypadku ról usługi w chmurze Azure</span><span class="sxs-lookup"><span data-stu-id="c192a-103">Install .NET on Azure Cloud Services roles</span></span>
<span data-ttu-id="c192a-104">W tym artykule opisano, jak tooinstall wersje programu .NET Framework, które nie pochodzą z hello Azure systemu operacyjnego gościa.</span><span class="sxs-lookup"><span data-stu-id="c192a-104">This article describes how tooinstall versions of .NET Framework that don't come with hello Azure Guest OS.</span></span> <span data-ttu-id="c192a-105">Można użyć .NET na powitania systemu operacyjnego gościa tooconfigure role usługi w chmurze sieci web i proces roboczy.</span><span class="sxs-lookup"><span data-stu-id="c192a-105">You can use .NET on hello Guest OS tooconfigure your cloud service web and worker roles.</span></span>

<span data-ttu-id="c192a-106">Na przykład można zainstalować .NET 4.6.1 na powitania systemu operacyjnego gościa z rodziny 4, które nie pochodzą z dowolną wersją .NET 4.6.</span><span class="sxs-lookup"><span data-stu-id="c192a-106">For example, you can install .NET 4.6.1 on hello Guest OS family 4, which doesn't come with any release of .NET 4.6.</span></span> <span data-ttu-id="c192a-107">(hello rodziny systemów operacyjnych gościa 5 pochodzą z .NET 4.6). Najnowsze informacje o hello na powitania wersjami systemu operacyjnego gościa Azure, zobacz hello [wiadomości wersji systemu operacyjnego gościa Azure](cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="c192a-107">(hello Guest OS family 5 does come with .NET 4.6.) For hello latest information on hello Azure Guest OS releases, see hello [Azure Guest OS release news](cloud-services-guestos-update-matrix.md).</span></span> 

>[!IMPORTANT]
><span data-ttu-id="c192a-108">Hello Azure SDK 2.9 zawiera ograniczenia dotyczące wdrażania .NET 4.6 rodziny systemów operacyjnych gościa hello, 4 lub starszym.</span><span class="sxs-lookup"><span data-stu-id="c192a-108">hello Azure SDK 2.9 contains a restriction on deploying .NET 4.6 on hello Guest OS family 4 or earlier.</span></span> <span data-ttu-id="c192a-109">Poprawka dla ograniczenia hello jest dostępna na powitania [Microsoft Docs](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9) lokacji.</span><span class="sxs-lookup"><span data-stu-id="c192a-109">A fix for hello restriction is available on hello [Microsoft Docs](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9) site.</span></span>

<span data-ttu-id="c192a-110">tooinstall .NET na poszczególnych ról sieci web i proces roboczy obejmują hello Instalator sieci web .NET w ramach projektu usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="c192a-110">tooinstall .NET on your web and worker roles, include hello .NET web installer as part of your cloud service project.</span></span> <span data-ttu-id="c192a-111">Uruchom Instalator hello jako część zadania uruchamiania hello roli.</span><span class="sxs-lookup"><span data-stu-id="c192a-111">Start hello installer as part of hello role's startup tasks.</span></span> 

## <a name="add-hello-net-installer-tooyour-project"></a><span data-ttu-id="c192a-112">Dodaj projekt tooyour Instalator .NET hello</span><span class="sxs-lookup"><span data-stu-id="c192a-112">Add hello .NET installer tooyour project</span></span>
<span data-ttu-id="c192a-113">Instalator sieci web hello toodownload dla hello .NET Framework, wybierz wersję hello, które mają tooinstall:</span><span class="sxs-lookup"><span data-stu-id="c192a-113">toodownload hello web installer for hello .NET Framework, choose hello version that you want tooinstall:</span></span>

* [<span data-ttu-id="c192a-114">Instalator sieci web .NET 4.7</span><span class="sxs-lookup"><span data-stu-id="c192a-114">.NET 4.7 web installer</span></span>](http://go.microsoft.com/fwlink/?LinkId=825298)
* [<span data-ttu-id="c192a-115">Instalator sieci web .NET 4.6.1</span><span class="sxs-lookup"><span data-stu-id="c192a-115">.NET 4.6.1 web installer</span></span>](http://go.microsoft.com/fwlink/?LinkId=671729)

<span data-ttu-id="c192a-116">Instalator hello tooadd *web* roli:</span><span class="sxs-lookup"><span data-stu-id="c192a-116">tooadd hello installer for a *web* role:</span></span>
  1. <span data-ttu-id="c192a-117">W **Eksploratora rozwiązań**w obszarze **ról** w projekcie usługi chmury, kliknij prawym przyciskiem myszy użytkownika *web* rolę i wybierz **Dodaj**  >  **Nowy Folder**.</span><span class="sxs-lookup"><span data-stu-id="c192a-117">In **Solution Explorer**, under **Roles** in your cloud service project, right-click your *web* role and select **Add** > **New Folder**.</span></span> <span data-ttu-id="c192a-118">Utwórz folder o nazwie **bin**.</span><span class="sxs-lookup"><span data-stu-id="c192a-118">Create a folder named **bin**.</span></span>
  2. <span data-ttu-id="c192a-119">Kliknij prawym przyciskiem myszy hello bin folder i wybierz **Dodaj** > **istniejący element**.</span><span class="sxs-lookup"><span data-stu-id="c192a-119">Right-click hello bin folder and select **Add** > **Existing Item**.</span></span> <span data-ttu-id="c192a-120">Wybierz Instalatora .NET hello i dodaj go otworzyć folder bin toohello.</span><span class="sxs-lookup"><span data-stu-id="c192a-120">Select hello .NET installer and add it toohello bin folder.</span></span>
  
<span data-ttu-id="c192a-121">Instalator hello tooadd *procesu roboczego* roli:</span><span class="sxs-lookup"><span data-stu-id="c192a-121">tooadd hello installer for a *worker* role:</span></span>
* <span data-ttu-id="c192a-122">Kliknij prawym przyciskiem myszy użytkownika *procesu roboczego* rolę i wybierz **Dodaj** > **istniejący element**.</span><span class="sxs-lookup"><span data-stu-id="c192a-122">Right-click your *worker* role and select **Add** > **Existing Item**.</span></span> <span data-ttu-id="c192a-123">Wybierz Instalatora .NET hello i dodaj go toohello roli.</span><span class="sxs-lookup"><span data-stu-id="c192a-123">Select hello .NET installer and add it toohello role.</span></span> 

<span data-ttu-id="c192a-124">Kiedy pliki są dodawane w ten sposób toohello roli folder zawartości, są automatycznie dodawane pakiet usługi w chmurze tooyour.</span><span class="sxs-lookup"><span data-stu-id="c192a-124">When files are added in this way toohello role content folder, they're automatically added tooyour cloud service package.</span></span> <span data-ttu-id="c192a-125">Witaj pliki są następnie spójne lokalizacji tooa wdrożone na maszynie wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="c192a-125">hello files are then deployed tooa consistent location on hello virtual machine.</span></span> <span data-ttu-id="c192a-126">Powtórz ten proces dla każdej roli sieci web i proces roboczy w usłudze w chmurze, aby wszystkie role mają kopię hello Instalatora.</span><span class="sxs-lookup"><span data-stu-id="c192a-126">Repeat this process for each web and worker role in your cloud service so that all roles have a copy of hello installer.</span></span>

> [!NOTE]
> <span data-ttu-id="c192a-127">.NET 4.6.1 należy zainstalować na swojej roli usługi w chmurze, nawet jeśli jest przeznaczony dla aplikacji .NET 4.6.</span><span class="sxs-lookup"><span data-stu-id="c192a-127">You should install .NET 4.6.1 on your cloud service role even if your application targets .NET 4.6.</span></span> <span data-ttu-id="c192a-128">Witaj systemu operacyjnego gościa zawiera hello wiedzy [aktualizacji 3098779](https://support.microsoft.com/kb/3098779) i [aktualizacji 3097997](https://support.microsoft.com/kb/3097997).</span><span class="sxs-lookup"><span data-stu-id="c192a-128">hello Guest OS includes hello Knowledge Base [update 3098779](https://support.microsoft.com/kb/3098779) and [update 3097997](https://support.microsoft.com/kb/3097997).</span></span> <span data-ttu-id="c192a-129">Problemy mogą wystąpić przy uruchamianiu aplikacji platformy .NET, jeśli .NET 4.6 zostanie zainstalowana na powitania aktualizacje bazy wiedzy Knowledge Base.</span><span class="sxs-lookup"><span data-stu-id="c192a-129">Issues can occur when you run your .NET applications if .NET 4.6 is installed on top of hello Knowledge Base updates.</span></span> <span data-ttu-id="c192a-130">tooavoid te problemy, należy zainstalować .NET 4.6.1 zamiast wersji 4.6.</span><span class="sxs-lookup"><span data-stu-id="c192a-130">tooavoid these issues, install .NET 4.6.1 rather than version 4.6.</span></span> <span data-ttu-id="c192a-131">Aby uzyskać więcej informacji, zobacz hello [artykułu bazy wiedzy 3118750](https://support.microsoft.com/kb/3118750).</span><span class="sxs-lookup"><span data-stu-id="c192a-131">For more information, see hello [Knowledge Base article 3118750](https://support.microsoft.com/kb/3118750).</span></span>
> 
> 

![Zawartość roli z plików Instalatora][1]

## <a name="define-startup-tasks-for-your-roles"></a><span data-ttu-id="c192a-133">Definiowanie zadań uruchomienia dla poszczególnych ról</span><span class="sxs-lookup"><span data-stu-id="c192a-133">Define startup tasks for your roles</span></span>
<span data-ttu-id="c192a-134">Przed rozpoczęciem rolę, można użyć operacji tooperform zadania uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="c192a-134">You can use startup tasks tooperform operations before a role starts.</span></span> <span data-ttu-id="c192a-135">Instalowanie hello .NET Framework, jako części hello uruchomienia zadania gwarantuje, że framework hello jest zainstalowany, przed uruchomieniem kodu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c192a-135">Installing hello .NET Framework as part of hello startup task ensures that hello framework is installed before any application code is run.</span></span> <span data-ttu-id="c192a-136">Aby uzyskać więcej informacji na temat uruchamiania zadań, zobacz [uruchamiać zadania uruchamiania na platformie Azure](cloud-services-startup-tasks.md).</span><span class="sxs-lookup"><span data-stu-id="c192a-136">For more information on startup tasks, see [Run startup tasks in Azure](cloud-services-startup-tasks.md).</span></span> 

1. <span data-ttu-id="c192a-137">Dodaj poniższe plik ServiceDefinition.csdef toohello zawartości w obszarze hello hello **sieć Web** lub **proces roboczy** węzła dla wszystkich ról:</span><span class="sxs-lookup"><span data-stu-id="c192a-137">Add hello following content toohello ServiceDefinition.csdef file under hello **WebRole** or **WorkerRole** node for all roles:</span></span>
   
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
   
    <span data-ttu-id="c192a-138">Witaj konfiguracji uruchamia hello konsoli polecenie `install.cmd` z tooinstall uprawnień administratora hello .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="c192a-138">hello preceding configuration runs hello console command `install.cmd` with administrator privileges tooinstall hello .NET Framework.</span></span> <span data-ttu-id="c192a-139">tworzy również konfiguracji Hello **LocalStorage** elementu o nazwie **NETFXInstall**.</span><span class="sxs-lookup"><span data-stu-id="c192a-139">hello configuration also creates a **LocalStorage** element named **NETFXInstall**.</span></span> <span data-ttu-id="c192a-140">skryptu uruchomieniowego Hello ustawia toouse folderu tymczasowego hello tego zasobu magazynu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="c192a-140">hello startup script sets hello temp folder toouse this local storage resource.</span></span> 
    
    > [!IMPORTANT]
    > <span data-ttu-id="c192a-141">tooensure poprawną instalację platformy hello rozmiar hello zestawu tooat ten zasób najmniej 1024 MB.</span><span class="sxs-lookup"><span data-stu-id="c192a-141">tooensure correct installation of hello framework, set hello size of this resource tooat least 1,024 MB.</span></span>
    
    <span data-ttu-id="c192a-142">Aby uzyskać więcej informacji na temat uruchamiania zadań, zobacz [wspólne usługi w chmurze Azure uruchamiania zadań](cloud-services-startup-tasks-common.md).</span><span class="sxs-lookup"><span data-stu-id="c192a-142">For more information about startup tasks, see [Common Azure Cloud Services startup tasks](cloud-services-startup-tasks-common.md).</span></span>

2. <span data-ttu-id="c192a-143">Utwórz plik o nazwie **install.cmd** i dodaj następujące hello Zainstaluj plik toohello skryptu.</span><span class="sxs-lookup"><span data-stu-id="c192a-143">Create a file named **install.cmd** and add hello following install script toohello file.</span></span>

    <span data-ttu-id="c192a-144">skrypt Hello sprawdza, czy hello określonej wersji programu .NET Framework hello jest już zainstalowana na maszynie hello badając hello rejestru.</span><span class="sxs-lookup"><span data-stu-id="c192a-144">hello script checks whether hello specified version of hello .NET Framework is already installed on hello machine by querying hello registry.</span></span> <span data-ttu-id="c192a-145">Jeśli nie jest zainstalowana wersja .NET hello, Instalator sieci web .NET hello jest otwarty.</span><span class="sxs-lookup"><span data-stu-id="c192a-145">If hello .NET version is not installed, then hello .NET web installer is opened.</span></span> <span data-ttu-id="c192a-146">toohelp rozwiązać wszelkie napotkane problemy, skrypt hello rejestruje wszystkie działania toohello pliku startuptasklog-(bieżącą datę i godzinę) .txt przechowywanego w **InstallLogs** Magazyn lokalny.</span><span class="sxs-lookup"><span data-stu-id="c192a-146">toohelp troubleshoot any issues, hello script logs all activity toohello file startuptasklog-(current date and time).txt that is stored in **InstallLogs** local storage.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="c192a-147">Użyj edytora tekstów podstawowe, takie jak Windows toocreate hello install.cmd Notatnika.</span><span class="sxs-lookup"><span data-stu-id="c192a-147">Use a basic text editor like Windows Notepad toocreate hello install.cmd file.</span></span> <span data-ttu-id="c192a-148">Jeśli używasz programu Visual Studio toocreate plik tekstowy i zmienić too.cmd rozszerzenia hello, hello plików może nadal zawierać znacznik kolejności bajtów UTF-8.</span><span class="sxs-lookup"><span data-stu-id="c192a-148">If you use Visual Studio toocreate a text file and change hello extension too.cmd, hello file might still contain a UTF-8 byte order mark.</span></span> <span data-ttu-id="c192a-149">Znak ten może spowodować błąd, gdy hello pierwszego wiersza hello skrypt jest uruchamiany.</span><span class="sxs-lookup"><span data-stu-id="c192a-149">This mark can cause an error when hello first line of hello script is run.</span></span> <span data-ttu-id="c192a-150">tooavoid ten błąd, upewnij hello pierwszego wiersza hello skryptu REM — instrukcja, który był pomijany przez hello bajtów kolejności przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="c192a-150">tooavoid this error, make hello first line of hello script a REM statement that can be skipped by hello byte order processing.</span></span> 
    > 
    >
   
    ```cmd
    REM Set hello value of netfx tooinstall appropriate .NET Framework. 
    REM ***** tooinstall .NET 4.5.2 set hello variable netfx too"NDP452" *****
    REM ***** tooinstall .NET 4.6 set hello variable netfx too"NDP46" *****
    REM ***** tooinstall .NET 4.6.1 set hello variable netfx too"NDP461" *****
    REM ***** tooinstall .NET 4.6.2 set hello variable netfx too"NDP462" *****
    REM ***** tooinstall .NET 4.7 set hello variable netfx too"NDP47" *****
    set netfx="NDP47"

    REM ***** Set script start timestamp *****
    set timehour=%time:~0,2%
    set timestamp=%date:~-4,4%%date:~-10,2%%date:~-7,2%-%timehour: =0%%time:~3,2%
    set "log=install.cmd started %timestamp%."

    REM ***** Exit script if running in Emulator *****
    if %ComputeEmulatorRunning%=="true" goto exit

    REM ***** Needed toocorrectly install .NET 4.6.1, otherwise you may see an out of disk space error *****
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
    echo Restarting toocomplete .NET (%netfx%) installation >> %startuptasklog%
    EXIT /B %ERRORLEVEL%

    :installed
    echo .NET (%netfx%) is installed >> %startuptasklog%

    :end
    echo install.cmd completed: %date:~-4,4%%date:~-10,2%%date:~-7,2%-%timehour: =0%%time:~3,2% >> %startuptasklog%

    :exit
    EXIT /B 0
    ```
   
   > [!NOTE]
   > <span data-ttu-id="c192a-151">Ten skrypt pokazuje, jak tooinstall .NET 4.5.2 lub wersji 4.6 ciągłość działania, nawet wtedy, gdy jest już dostępny na .NET 4.5.2 hello Azure systemu operacyjnego gościa.</span><span class="sxs-lookup"><span data-stu-id="c192a-151">This script shows how tooinstall .NET 4.5.2 or version 4.6 for continuity, even though .NET 4.5.2 is already available on hello Azure Guest OS.</span></span> <span data-ttu-id="c192a-152">Należy bezpośrednio zainstalować .NET 4.6.1 zamiast wersji 4.6, zgodnie z opisem w hello [artykułu bazy wiedzy 3118750](https://support.microsoft.com/kb/3118750).</span><span class="sxs-lookup"><span data-stu-id="c192a-152">You should directly install .NET 4.6.1 rather than version 4.6, as described in hello [Knowledge Base article 3118750](https://support.microsoft.com/kb/3118750).</span></span>
   > 
   > 

3. <span data-ttu-id="c192a-153">Dodaj rolę tooeach plików install.cmd hello przy użyciu **Dodaj** > **istniejący element** w **Eksploratora rozwiązań** zgodnie z opisem we wcześniejszej części tego tematu.</span><span class="sxs-lookup"><span data-stu-id="c192a-153">Add hello install.cmd file tooeach role by using **Add** > **Existing Item** in **Solution Explorer** as described earlier in this topic.</span></span> 

    <span data-ttu-id="c192a-154">Po zakończeniu tego kroku wszystkie role powinny mieć plik Instalatora .NET hello i hello install.cmd pliku.</span><span class="sxs-lookup"><span data-stu-id="c192a-154">After this step is complete, all roles should have hello .NET installer file and hello install.cmd file.</span></span>

   ![Zawartość roli przy użyciu wszystkich plików][2]

## <a name="configure-diagnostics-tootransfer-startup-logs-tooblob-storage"></a><span data-ttu-id="c192a-156">Konfigurowanie diagnostyki tootransfer uruchamiania dzienniki tooBlob magazynu</span><span class="sxs-lookup"><span data-stu-id="c192a-156">Configure Diagnostics tootransfer startup logs tooBlob storage</span></span>
<span data-ttu-id="c192a-157">toosimplify rozwiązywania problemów z instalacją, można skonfigurować tootransfer diagnostyki Azure wszystkie pliki dziennika wygenerowane przez hello uruchamiania skryptu lub hello magazynu obiektów Blob tooAzure Instalator .NET.</span><span class="sxs-lookup"><span data-stu-id="c192a-157">toosimplify troubleshooting installation issues, you can configure Azure Diagnostics tootransfer any log files generated by hello startup script or hello .NET installer tooAzure Blob storage.</span></span> <span data-ttu-id="c192a-158">Przy użyciu tej metody, można wyświetlić dzienniki hello przez pobieranie plików dziennika hello z magazynu obiektów Blob zamiast tooremote pulpitu do hello roli.</span><span class="sxs-lookup"><span data-stu-id="c192a-158">By using this approach, you can view hello logs by downloading hello log files from Blob storage rather than having tooremote desktop into hello role.</span></span>

<span data-ttu-id="c192a-159">Diagnostyka tooconfigure, otwórz plik diagnostics.wadcfgx hello i Dodaj powitania po zawartości w obszarze hello **katalogów** węzła:</span><span class="sxs-lookup"><span data-stu-id="c192a-159">tooconfigure Diagnostics, open hello diagnostics.wadcfgx file and add hello following content under hello **Directories** node:</span></span> 

```xml 
<DataSources>
 <DirectoryConfiguration containerName="netfx-install">
  <LocalResource name="NETFXInstall" relativePath="log"/>
 </DirectoryConfiguration>
</DataSources>
```

<span data-ttu-id="c192a-160">Plik XML konfiguruje diagnostyki tootransfer hello pliki w katalogu dziennika hello hello **NETFXInstall** toohello zasobów konta magazynu diagnostyki w hello **netfx instalacji** kontenera obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="c192a-160">This XML configures Diagnostics tootransfer hello files in hello log directory in hello **NETFXInstall** resource toohello Diagnostics storage account in hello **netfx-install** blob container.</span></span>

## <a name="deploy-your-cloud-service"></a><span data-ttu-id="c192a-161">Wdrażanie usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="c192a-161">Deploy your cloud service</span></span>
<span data-ttu-id="c192a-162">Podczas wdrażania usługi w chmurze hello uruchamiania zadań zainstalować hello .NET Framework, jeśli to nie jest jeszcze zainstalowana.</span><span class="sxs-lookup"><span data-stu-id="c192a-162">When you deploy your cloud service, hello startup tasks install hello .NET Framework if it's not already installed.</span></span> <span data-ttu-id="c192a-163">Role usługi w chmurze są hello *zajęty* stanu podczas instalowania hello framework.</span><span class="sxs-lookup"><span data-stu-id="c192a-163">Your cloud service roles are in hello *busy* state while hello framework is being installed.</span></span> <span data-ttu-id="c192a-164">Witaj framework instalacja wymaga ponownego uruchomienia, również może być ponownie hello usługi ról.</span><span class="sxs-lookup"><span data-stu-id="c192a-164">If hello framework installation requires a restart, hello service roles might also restart.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c192a-165">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="c192a-165">Additional resources</span></span>
* <span data-ttu-id="c192a-166">[Instalowanie hello .NET Framework][Installing hello .NET Framework]</span><span class="sxs-lookup"><span data-stu-id="c192a-166">[Installing hello .NET Framework][Installing hello .NET Framework]</span></span>
* <span data-ttu-id="c192a-167">[Określanie, które wersje programu .NET Framework są zainstalowane][How to: Determine Which .NET Framework Versions Are Installed]</span><span class="sxs-lookup"><span data-stu-id="c192a-167">[Determine which .NET Framework versions are installed][How to: Determine Which .NET Framework Versions Are Installed]</span></span>
* <span data-ttu-id="c192a-168">[Rozwiązywanie problemów z instalacja programu .NET Framework][Troubleshooting .NET Framework Installations]</span><span class="sxs-lookup"><span data-stu-id="c192a-168">[Troubleshooting .NET Framework installations][Troubleshooting .NET Framework Installations]</span></span>

[How to: Determine Which .NET Framework Versions Are Installed]: https://msdn.microsoft.com/library/hh925568.aspx
[Installing hello .NET Framework]: https://msdn.microsoft.com/library/5a4x27ek.aspx
[Troubleshooting .NET Framework Installations]: https://msdn.microsoft.com/library/hh925569.aspx

<!--Image references-->
[1]: ./media/cloud-services-dotnet-install-dotnet/rolecontentwithinstallerfiles.png
[2]: ./media/cloud-services-dotnet-install-dotnet/rolecontentwithallfiles.png
