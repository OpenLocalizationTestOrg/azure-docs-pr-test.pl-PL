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
# <a name="install-net-on-azure-cloud-services-roles"></a>Zainstaluj program .NET w przypadku ról usługi w chmurze Azure
W tym artykule opisano, jak tooinstall wersje programu .NET Framework, które nie pochodzą z hello Azure systemu operacyjnego gościa. Można użyć .NET na powitania systemu operacyjnego gościa tooconfigure role usługi w chmurze sieci web i proces roboczy.

Na przykład można zainstalować .NET 4.6.1 na powitania systemu operacyjnego gościa z rodziny 4, które nie pochodzą z dowolną wersją .NET 4.6. (hello rodziny systemów operacyjnych gościa 5 pochodzą z .NET 4.6). Najnowsze informacje o hello na powitania wersjami systemu operacyjnego gościa Azure, zobacz hello [wiadomości wersji systemu operacyjnego gościa Azure](cloud-services-guestos-update-matrix.md). 

>[!IMPORTANT]
>Hello Azure SDK 2.9 zawiera ograniczenia dotyczące wdrażania .NET 4.6 rodziny systemów operacyjnych gościa hello, 4 lub starszym. Poprawka dla ograniczenia hello jest dostępna na powitania [Microsoft Docs](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9) lokacji.

tooinstall .NET na poszczególnych ról sieci web i proces roboczy obejmują hello Instalator sieci web .NET w ramach projektu usługi w chmurze. Uruchom Instalator hello jako część zadania uruchamiania hello roli. 

## <a name="add-hello-net-installer-tooyour-project"></a>Dodaj projekt tooyour Instalator .NET hello
Instalator sieci web hello toodownload dla hello .NET Framework, wybierz wersję hello, które mają tooinstall:

* [Instalator sieci web .NET 4.7](http://go.microsoft.com/fwlink/?LinkId=825298)
* [Instalator sieci web .NET 4.6.1](http://go.microsoft.com/fwlink/?LinkId=671729)

Instalator hello tooadd *web* roli:
  1. W **Eksploratora rozwiązań**w obszarze **ról** w projekcie usługi chmury, kliknij prawym przyciskiem myszy użytkownika *web* rolę i wybierz **Dodaj**  >  **Nowy Folder**. Utwórz folder o nazwie **bin**.
  2. Kliknij prawym przyciskiem myszy hello bin folder i wybierz **Dodaj** > **istniejący element**. Wybierz Instalatora .NET hello i dodaj go otworzyć folder bin toohello.
  
Instalator hello tooadd *procesu roboczego* roli:
* Kliknij prawym przyciskiem myszy użytkownika *procesu roboczego* rolę i wybierz **Dodaj** > **istniejący element**. Wybierz Instalatora .NET hello i dodaj go toohello roli. 

Kiedy pliki są dodawane w ten sposób toohello roli folder zawartości, są automatycznie dodawane pakiet usługi w chmurze tooyour. Witaj pliki są następnie spójne lokalizacji tooa wdrożone na maszynie wirtualnej hello. Powtórz ten proces dla każdej roli sieci web i proces roboczy w usłudze w chmurze, aby wszystkie role mają kopię hello Instalatora.

> [!NOTE]
> .NET 4.6.1 należy zainstalować na swojej roli usługi w chmurze, nawet jeśli jest przeznaczony dla aplikacji .NET 4.6. Witaj systemu operacyjnego gościa zawiera hello wiedzy [aktualizacji 3098779](https://support.microsoft.com/kb/3098779) i [aktualizacji 3097997](https://support.microsoft.com/kb/3097997). Problemy mogą wystąpić przy uruchamianiu aplikacji platformy .NET, jeśli .NET 4.6 zostanie zainstalowana na powitania aktualizacje bazy wiedzy Knowledge Base. tooavoid te problemy, należy zainstalować .NET 4.6.1 zamiast wersji 4.6. Aby uzyskać więcej informacji, zobacz hello [artykułu bazy wiedzy 3118750](https://support.microsoft.com/kb/3118750).
> 
> 

![Zawartość roli z plików Instalatora][1]

## <a name="define-startup-tasks-for-your-roles"></a>Definiowanie zadań uruchomienia dla poszczególnych ról
Przed rozpoczęciem rolę, można użyć operacji tooperform zadania uruchamiania. Instalowanie hello .NET Framework, jako części hello uruchomienia zadania gwarantuje, że framework hello jest zainstalowany, przed uruchomieniem kodu aplikacji. Aby uzyskać więcej informacji na temat uruchamiania zadań, zobacz [uruchamiać zadania uruchamiania na platformie Azure](cloud-services-startup-tasks.md). 

1. Dodaj poniższe plik ServiceDefinition.csdef toohello zawartości w obszarze hello hello **sieć Web** lub **proces roboczy** węzła dla wszystkich ról:
   
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
   
    Witaj konfiguracji uruchamia hello konsoli polecenie `install.cmd` z tooinstall uprawnień administratora hello .NET Framework. tworzy również konfiguracji Hello **LocalStorage** elementu o nazwie **NETFXInstall**. skryptu uruchomieniowego Hello ustawia toouse folderu tymczasowego hello tego zasobu magazynu lokalnego. 
    
    > [!IMPORTANT]
    > tooensure poprawną instalację platformy hello rozmiar hello zestawu tooat ten zasób najmniej 1024 MB.
    
    Aby uzyskać więcej informacji na temat uruchamiania zadań, zobacz [wspólne usługi w chmurze Azure uruchamiania zadań](cloud-services-startup-tasks-common.md).

2. Utwórz plik o nazwie **install.cmd** i dodaj następujące hello Zainstaluj plik toohello skryptu.

    skrypt Hello sprawdza, czy hello określonej wersji programu .NET Framework hello jest już zainstalowana na maszynie hello badając hello rejestru. Jeśli nie jest zainstalowana wersja .NET hello, Instalator sieci web .NET hello jest otwarty. toohelp rozwiązać wszelkie napotkane problemy, skrypt hello rejestruje wszystkie działania toohello pliku startuptasklog-(bieżącą datę i godzinę) .txt przechowywanego w **InstallLogs** Magazyn lokalny.

    > [!IMPORTANT]
    > Użyj edytora tekstów podstawowe, takie jak Windows toocreate hello install.cmd Notatnika. Jeśli używasz programu Visual Studio toocreate plik tekstowy i zmienić too.cmd rozszerzenia hello, hello plików może nadal zawierać znacznik kolejności bajtów UTF-8. Znak ten może spowodować błąd, gdy hello pierwszego wiersza hello skrypt jest uruchamiany. tooavoid ten błąd, upewnij hello pierwszego wiersza hello skryptu REM — instrukcja, który był pomijany przez hello bajtów kolejności przetwarzania. 
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
   > Ten skrypt pokazuje, jak tooinstall .NET 4.5.2 lub wersji 4.6 ciągłość działania, nawet wtedy, gdy jest już dostępny na .NET 4.5.2 hello Azure systemu operacyjnego gościa. Należy bezpośrednio zainstalować .NET 4.6.1 zamiast wersji 4.6, zgodnie z opisem w hello [artykułu bazy wiedzy 3118750](https://support.microsoft.com/kb/3118750).
   > 
   > 

3. Dodaj rolę tooeach plików install.cmd hello przy użyciu **Dodaj** > **istniejący element** w **Eksploratora rozwiązań** zgodnie z opisem we wcześniejszej części tego tematu. 

    Po zakończeniu tego kroku wszystkie role powinny mieć plik Instalatora .NET hello i hello install.cmd pliku.

   ![Zawartość roli przy użyciu wszystkich plików][2]

## <a name="configure-diagnostics-tootransfer-startup-logs-tooblob-storage"></a>Konfigurowanie diagnostyki tootransfer uruchamiania dzienniki tooBlob magazynu
toosimplify rozwiązywania problemów z instalacją, można skonfigurować tootransfer diagnostyki Azure wszystkie pliki dziennika wygenerowane przez hello uruchamiania skryptu lub hello magazynu obiektów Blob tooAzure Instalator .NET. Przy użyciu tej metody, można wyświetlić dzienniki hello przez pobieranie plików dziennika hello z magazynu obiektów Blob zamiast tooremote pulpitu do hello roli.

Diagnostyka tooconfigure, otwórz plik diagnostics.wadcfgx hello i Dodaj powitania po zawartości w obszarze hello **katalogów** węzła: 

```xml 
<DataSources>
 <DirectoryConfiguration containerName="netfx-install">
  <LocalResource name="NETFXInstall" relativePath="log"/>
 </DirectoryConfiguration>
</DataSources>
```

Plik XML konfiguruje diagnostyki tootransfer hello pliki w katalogu dziennika hello hello **NETFXInstall** toohello zasobów konta magazynu diagnostyki w hello **netfx instalacji** kontenera obiektów blob.

## <a name="deploy-your-cloud-service"></a>Wdrażanie usługi w chmurze
Podczas wdrażania usługi w chmurze hello uruchamiania zadań zainstalować hello .NET Framework, jeśli to nie jest jeszcze zainstalowana. Role usługi w chmurze są hello *zajęty* stanu podczas instalowania hello framework. Witaj framework instalacja wymaga ponownego uruchomienia, również może być ponownie hello usługi ról. 

## <a name="additional-resources"></a>Dodatkowe zasoby
* [Instalowanie hello .NET Framework][Installing hello .NET Framework]
* [Określanie, które wersje programu .NET Framework są zainstalowane][How to: Determine Which .NET Framework Versions Are Installed]
* [Rozwiązywanie problemów z instalacja programu .NET Framework][Troubleshooting .NET Framework Installations]

[How to: Determine Which .NET Framework Versions Are Installed]: https://msdn.microsoft.com/library/hh925568.aspx
[Installing hello .NET Framework]: https://msdn.microsoft.com/library/5a4x27ek.aspx
[Troubleshooting .NET Framework Installations]: https://msdn.microsoft.com/library/hh925569.aspx

<!--Image references-->
[1]: ./media/cloud-services-dotnet-install-dotnet/rolecontentwithinstallerfiles.png
[2]: ./media/cloud-services-dotnet-install-dotnet/rolecontentwithallfiles.png
