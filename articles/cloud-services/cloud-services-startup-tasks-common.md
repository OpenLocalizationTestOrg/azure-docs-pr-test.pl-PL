---
title: "zadania uruchamiania aaaCommon dla usług w chmurze | Dokumentacja firmy Microsoft"
description: "Niektóre przykłady typowych zadań uruchamiania może być tooperform w roli sieci web usługi w chmurze lub roli proces roboczy."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: a7095dad-1ee7-4141-bc6a-ef19a6e570f1
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: c80fac4079439410dfc3795e4bce0fbc07dbbfab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="common-cloud-service-startup-tasks"></a>Typowe zadania uruchamiania usługi w chmurze
W tym artykule przedstawiono kilka przykładów typowych zadań uruchamiania może być tooperform w usłudze w chmurze. Przed rozpoczęciem rolę, można użyć operacji tooperform zadania uruchamiania. Operacje można tooperform obejmują instalowania składnika, rejestrowanie składników modelu COM, ustawienie kluczy rejestru lub uruchamia proces wymagającą dużo czasu. 

Zobacz [w tym artykule](cloud-services-startup-tasks.md) toounderstand sposób działania uruchamiania zadań, a w szczególności jak toocreate hello wpisów, które definiują zadanie uruchamiania.

> [!NOTE]
> Zadania uruchamiania nie są stosowane tooVirtual maszyny, tylko tooCloud usługi sieci Web i proces roboczy.
> 

## <a name="define-environment-variables-before-a-role-starts"></a>Zdefiniuj zmienne środowiskowe, przed rozpoczęciem roli
Zmienne środowiskowe zdefiniowane dla określonego zadania, należy użyć hello [środowiska] element wewnątrz hello [zadań] elementu.

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
    <WorkerRole name="WorkerRole1">
        ...
        <Startup>
            <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple">
                <Environment>
                    <Variable name="MyEnvironmentVariable" value="MyVariableValue" />
                </Environment>
            </Task>
        </Startup>
    </WorkerRole>
</ServiceDefinition>
```

Zmienne można również użyć [prawidłową wartość wyrażenia XPath Azure](cloud-services-role-config-xpath.md) tooreference coś o hello wdrożenia. Zamiast hello `value` atrybutu, zdefiniuj [RoleInstanceValue] element podrzędny.

```xml
<Variable name="PathToStartupStorage">
    <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='StartupLocalStorage']/@path" />
</Variable>
```


## <a name="configure-iis-startup-with-appcmdexe"></a>Konfigurowanie uruchomienia usług IIS przy użyciu AppCmd.exe
Witaj [AppCmd.exe](https://technet.microsoft.com/library/jj635852.aspx) narzędzia wiersza polecenia mogą być używane toomanage ustawień usług IIS podczas uruchamiania na platformie Azure. *AppCmd.exe* zawiera ustawienia tooconfiguration wygodny, wiersza polecenia dostępu do użycia w uruchomienia zadania na platformie Azure. Przy użyciu *AppCmd.exe*, ustawienia witryny sieci Web mogą być dodane, zmodyfikowane lub usunięte dla witryn i aplikacji.

Istnieje jednak kilka rzeczy toowatch limit dla użycie hello *AppCmd.exe* jako zadanie uruchamiania:

* Uruchamianie zadania mogą być uruchamiane w więcej niż raz między ponownego uruchomienia. Na przykład, gdy rola odtwarzana.
* Jeśli *AppCmd.exe* akcja jest wykonywana więcej niż raz, może generować wystąpił błąd. Na przykład za podjęciem tooadd sekcji*Web.config* dwukrotnie można wygenerować wystąpił błąd.
* Uruchamianie zadań zakończy się niepowodzeniem, jeśli zwracają kod wyjścia równy zero lub **errorlevel**. Na przykład, jeśli *AppCmd.exe* generuje błąd.

Witaj toocheck dobrym rozwiązaniem jest **errorlevel** po wywołaniu *AppCmd.exe*, jest łatwe toodo w przypadku zbyt zawijać wywołania hello*AppCmd.exe* z *.cmd*  pliku. W przypadku wykrycia znanego **errorlevel** odpowiedzi, możesz go zignorować lub przekaż go ponownie.

Witaj errorlevel zwrócony przez *AppCmd.exe* są wymienione w pliku pliku winerror.h hello, a także będą widoczne na [MSDN](https://msdn.microsoft.com/library/windows/desktop/ms681382.aspx).

### <a name="example-of-managing-hello-error-level"></a>Przykład zarządzanie hello poziom błędu
W tym przykładzie dodaje sekcji kompresji i kompresji objęcia JSON toohello *Web.config* pliku z powodu błędu obsługi i rejestrowania.

Witaj odpowiednich sekcji hello [ServiceDefinition.csdef] plików są wyświetlane w tym miejscu, które obejmują ustawienie hello [executionContext](https://msdn.microsoft.com/library/azure/gg557552.aspx#Task) atrybutu zbyt`elevated` toogive *AppCmd.exe*  wystarczające uprawnienia toochange hello ustawienia w hello *Web.config* pliku:

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
    <WorkerRole name="WorkerRole1">
        ...
        <Startup>
            <Task commandLine="Startup.cmd" executionContext="elevated" taskType="simple" />
        </Startup>
    </WorkerRole>
</ServiceDefinition>
```

Witaj *Startup.cmd* partii używa pliku *AppCmd.exe* tooadd sekcji kompresji i kompresji objęcia JSON toohello *Web.config* pliku. Oczekiwano Hello **errorlevel** 183 ustawiono toozero przy użyciu hello Sprawdź. Wywołanie pliku EXE programu wiersza polecenia. Nieoczekiwany errorlevels są rejestrowane tooStartupErrorLog.txt.

```cmd
REM   *** Add a compression section toohello Web.config file. ***
%windir%\system32\inetsrv\appcmd set config /section:urlCompression /doDynamicCompression:True /commit:apphost >> "%TEMP%\StartupLog.txt" 2>&1

REM   ERRORLEVEL 183 occurs when trying tooadd a section that already exists. This error is expected if this
REM   batch file were executed twice. This can occur and must be accounted for in a Azure startup
REM   task. toohandle this situation, set hello ERRORLEVEL toozero by using hello Verify command. hello Verify
REM   command will safely set hello ERRORLEVEL toozero.
IF %ERRORLEVEL% EQU 183 DO VERIFY > NUL

REM   If hello ERRORLEVEL is not zero at this point, some other error occurred.
IF %ERRORLEVEL% NEQ 0 (
    ECHO Error adding a compression section toohello Web.config file. >> "%TEMP%\StartupLog.txt" 2>&1
    GOTO ErrorExit
)

REM   *** Add compression for json. ***
%windir%\system32\inetsrv\appcmd set config  -section:system.webServer/httpCompression /+"dynamicTypes.[mimeType='application/json; charset=utf-8',enabled='True']" /commit:apphost >> "%TEMP%\StartupLog.txt" 2>&1
IF %ERRORLEVEL% EQU 183 VERIFY > NUL
IF %ERRORLEVEL% NEQ 0 (
    ECHO Error adding hello JSON compression type toohello Web.config file. >> "%TEMP%\StartupLog.txt" 2>&1
    GOTO ErrorExit
)

REM   *** Exit batch file. ***
EXIT /b 0

REM   *** Log error and exit ***
:ErrorExit
REM   Report hello date, time, and ERRORLEVEL of hello error.
DATE /T >> "%TEMP%\StartupLog.txt" 2>&1
TIME /T >> "%TEMP%\StartupLog.txt" 2>&1
ECHO An error occurred during startup. ERRORLEVEL = %ERRORLEVEL% >> "%TEMP%\StartupLog.txt" 2>&1
EXIT %ERRORLEVEL%
```

## <a name="add-firewall-rules"></a>Dodawanie reguł zapory
Na platformie Azure czy skutecznie dwóch zapory. pierwszy zapory Hello steruje połączeń między maszyną wirtualną hello i hello poza world. Zapora jest kontrolowany przez hello [punkty końcowe] element hello [ServiceDefinition.csdef] pliku.

drugi zapory Hello steruje połączeń między hello maszyny wirtualnej i hello procesów w ramach maszyny wirtualnej. Zapora może być kontrolowane przez hello `netsh advfirewall firewall` narzędzia wiersza polecenia.

Platforma Azure tworzy reguły zapory dla procesów hello uruchomionych w ramach poszczególnych ról. Na przykład po uruchomieniu usługi lub program Azure automatycznie tworzy tooallow reguły zapory na potrzeby hello toocommunicate tej usługi z hello Internet. Jeśli utworzysz usługę, która jest uruchamiana przez proces poza roli użytkownika (np. usługi COM + lub zaplanowanych zadań systemu Windows), jednak toomanually Tworzenie usługi toothat dostępu tooallow reguły zapory. Te reguły zapory można tworzyć za pomocą zadania uruchamiania.

Zadanie uruchamiania, która tworzy regułę zapory muszą mieć [executionContext][zadań] z **z podwyższonym poziomem uprawnień**. Dodaj powitania po uruchamiania zadań toohello [ServiceDefinition.csdef] pliku.

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
    <WorkerRole name="WorkerRole1">
        ...
        <Startup>
            <Task commandLine="AddFirewallRules.cmd" executionContext="elevated" taskType="simple" />
        </Startup>
    </WorkerRole>
</ServiceDefinition>
```

reguły zapory hello tooadd, należy użyć odpowiedniego hello `netsh advfirewall firewall` poleceń w pliku wsadowym uruchamiania. W tym przykładzie zadanie uruchamiania hello wymaga zabezpieczeń i szyfrowania dla portu TCP 80.

```cmd
REM   Add a firewall rule in a startup task.

REM   Add an inbound rule requiring security and encryption for TCP port 80 traffic.
netsh advfirewall firewall add rule name="Require Encryption for Inbound TCP/80" protocol=TCP dir=in localport=80 security=authdynenc action=allow >> "%TEMP%\StartupLog.txt" 2>&1

REM   If an error occurred, return hello errorlevel.
EXIT /B %errorlevel%
```

## <a name="block-a-specific-ip-address"></a>Blok określonego adresu IP
Zestaw tooa sieci web platformy Azure roli dostęp z określonych adresów IP można ograniczyć, modyfikując programu IIS **web.config** pliku. Należy również toouse pliku polecenia, który umożliwia odblokowanie hello **ipSecurity** sekcji hello **ApplicationHost.config** pliku.

hello odblokowywania toodo **ipSecurity** sekcji hello **ApplicationHost.config** plików, tworzenie pliku poleceń, który jest uruchamiany podczas uruchamiania roli. Utwórz folder na głównym poziomie hello roli sieci web o nazwie **uruchamiania** i, w tym folderze utwórz plik wsadowy o nazwie **startup.cmd**. Dodaj projekt programu Visual Studio tooyour tego pliku i ustaw właściwości hello zbyt**zawsze Kopiuj** tooensure jest on dołączony do pakietu.

Dodaj powitania po uruchamiania zadań toohello [ServiceDefinition.csdef] pliku.

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
    <WebRole name="WebRole1">
        ...
        <Startup>
            <Task commandLine="startup.cmd" executionContext="elevated" />
        </Startup>
    </WebRole>
</ServiceDefinition>
```

Dodaj to polecenie toohello **startup.cmd** pliku:

```cmd
@echo off
@echo Installing "IPv4 Address and Domain Restrictions" feature 
powershell -ExecutionPolicy Unrestricted -command "Install-WindowsFeature Web-IP-Security"
@echo Unlocking configuration for "IPv4 Address and Domain Restrictions" feature 
%windir%\system32\inetsrv\AppCmd.exe unlock config -section:system.webServer/security/ipSecurity
```

To zadanie sprawia, że hello **startup.cmd** partii toobe pliku uruchamiać za każdym razem hello roli sieci web został zainicjowany, zapewnienie, że hello wymagane **ipSecurity** sekcja jest odblokowane.

Na koniec zmodyfikuj hello [sekcja system.webServer](http://www.iis.net/configreference/system.webserver/security/ipsecurity#005) roli sieci web **web.config** pliku tooadd listę adresów IP, które mają prawo dostępu, jak pokazano w hello poniższy przykład:

Ten przykładowy konfiguracji **umożliwia** wszystkie adresy IP tooaccess hello serwera, z wyjątkiem Witaj dwie zdefiniowany

```xml
<system.webServer>
    <security>
    <!--Unlisted IP addresses are granted access-->
    <ipSecurity>
        <!--hello following IP addresses are denied access-->
        <add allowed="false" ipAddress="192.168.100.1" subnetMask="255.255.0.0" />
        <add allowed="false" ipAddress="192.168.100.2" subnetMask="255.255.0.0" />
    </ipSecurity>
    </security>
</system.webServer>
```

Ten przykład konfiguracji **nie zezwala na** wszystkie adresy IP z uzyskiwania dostępu do serwera hello z wyjątkiem hello dwa zdefiniowane.

```xml
<system.webServer>
    <security>
    <!--Unlisted IP addresses are denied access-->
    <ipSecurity allowUnlisted="false">
        <!--hello following IP addresses are granted access-->
        <add allowed="true" ipAddress="192.168.100.1" subnetMask="255.255.0.0" />
        <add allowed="true" ipAddress="192.168.100.2" subnetMask="255.255.0.0" />
    </ipSecurity>
    </security>
</system.webServer>
```

## <a name="create-a-powershell-startup-task"></a>Utwórz zadanie uruchamiania programu PowerShell
Skrypty programu Windows PowerShell nie należy wywoływać bezpośrednio w hello [ServiceDefinition.csdef] pliku, ale może być wywoływany z w pliku wsadowym uruchamiania.

PowerShell (domyślnie) uruchamiać niepodpisane skrypty. Jeśli nie zarejestrujesz skrypt należy tooconfigure PowerShell toorun niepodpisanych skryptów. toorun niepodpisanych skryptów, hello **ExecutionPolicy** musi być ustawiona zbyt**bez ograniczeń**. Witaj **ExecutionPolicy** ustawienie użycia opiera się na powitania wersję środowiska Windows PowerShell.

```cmd
REM   Run an unsigned PowerShell script and log hello output
PowerShell -ExecutionPolicy Unrestricted .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   If an error occurred, return hello errorlevel.
EXIT /B %errorlevel%
```

Jeśli używasz systemu operacyjnego gościa, który uruchamia program PowerShell 2.0 jest lub 1.0 można wymusić toorun w wersji 2, a jeśli jest niedostępny, użyj wersji 1.

```cmd
REM   Attempt tooset hello execution policy by using PowerShell version 2.0 syntax.
PowerShell -Version 2.0 -ExecutionPolicy Unrestricted .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   If PowerShell version 2.0 isn't available. Set hello execution policy by using hello PowerShell
IF %ERRORLEVEL% EQU -393216 (
   PowerShell -Command "Set-ExecutionPolicy Unrestricted" >> "%TEMP%\StartupLog.txt" 2>&1
   PowerShell .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1
)

REM   If an error occurred, return hello errorlevel.
EXIT /B %errorlevel%
```

## <a name="create-files-in-local-storage-from-a-startup-task"></a>Tworzenie plików w magazynie lokalnym z zadanie uruchamiania
Można użyć toostore zasobu lokalnego magazynu plików utworzonych przez zadanie uruchamiania, który jest dostępny później przez aplikację.

toocreate hello zasobów magazynu lokalnego, Dodaj [LocalResources] toohello sekcji [ServiceDefinition.csdef] pliku, a następnie dodaj hello [LocalStorage] element podrzędny. Nadaj unikatową nazwę i odpowiedni rozmiar zasobu lokalnego magazynu hello uruchomienia zadania.

toouse zasobu magazynu lokalnego uruchomienia zadania, należy toocreate lokalizacja zasobu środowiska zmiennej tooreference hello magazynu lokalnego. Następnie hello uruchamiania zadań i aplikacji hello są stanie tooread i zapisać pliki toohello magazynu lokalnego zasobu.

Witaj odpowiednich sekcji hello **ServiceDefinition.csdef** plików są wyświetlane tutaj:

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <WorkerRole name="WorkerRole1">
    ...

    <LocalResources>
      <LocalStorage name="StartupLocalStorage" sizeInMB="5"/>
    </LocalResources>

    <Startup>
      <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple">
        <Environment>
          <Variable name="PathToStartupStorage">
            <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='StartupLocalStorage']/@path" />
          </Variable>
        </Environment>
      </Task>
    </Startup>
  </WorkerRole>
</ServiceDefinition>
```

Na przykład to **Startup.cmd** plik wsadowy używa hello **PathToStartupStorage** pliku hello toocreate zmiennej środowiska **MyTest.txt** w magazynie lokalnym hello Lokalizacja.

```cmd
REM   Create a simple text file.

ECHO This text will go into hello MyTest.txt file which will be in hello    >  "%PathToStartupStorage%\MyTest.txt"
ECHO path pointed tooby hello PathToStartupStorage environment variable.  >> "%PathToStartupStorage%\MyTest.txt"
ECHO hello contents of hello PathToStartupStorage environment variable is   >> "%PathToStartupStorage%\MyTest.txt"
ECHO "%PathToStartupStorage%".                                          >> "%PathToStartupStorage%\MyTest.txt"

REM   Exit hello batch file with ERRORLEVEL 0.

EXIT /b 0
```

Magazyn lokalny folder mogą korzystać z hello Azure SDK, za pomocą hello [GetLocalResource](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) metody.

```csharp
string localStoragePath = Microsoft.WindowsAzure.ServiceRuntime.RoleEnvironment.GetLocalResource("StartupLocalStorage").RootPath;

string fileContent = System.IO.File.ReadAllText(System.IO.Path.Combine(localStoragePath, "MyTestFile.txt"));
```

## <a name="run-in-hello-emulator-or-cloud"></a>Uruchamianie w emulatorze hello lub w chmurze
Program może wykonywać inne czynności działającego w toowhen chmury porównaniu hello, którego emulatora obliczeń hello uruchomienia zadania. Na przykład można toouse świeżą kopię danych SQL tylko wtedy, gdy działa w emulatorze hello. Lub może być toodo optymalizacji wydajności chmury hello nie muszą toodo podczas uruchamiania w emulatorze hello.

Ta możliwość tooperform różne akcje na powitania emulator obliczeń i hello chmury można osiągnąć, tworząc zmienną środowiskową w hello [ServiceDefinition.csdef] pliku. Następnie można przetestować tej zmiennej środowiskowej dla wartości w zadania uruchamiania.

Zmienna środowiskowa hello toocreate, Dodaj hello [zmiennej]/[RoleInstanceValue] element i utworzyć wartość wyrażenia XPath `/RoleEnvironment/Deployment/@emulated`. Witaj wartość hello **ComputeEmulatorRunning %** jest zmienna środowiskowa `true` podczas uruchamiania na powitania emulatora obliczeń, i `false` podczas uruchamiania w chmurze hello.

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <WorkerRole name="WorkerRole1">

    ...

    <Startup>
      <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple">
        <Environment>
          <Variable name="ComputeEmulatorRunning">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
          </Variable>
        </Environment>
      </Task>
    </Startup>

  </WorkerRole>
</ServiceDefinition>
```

zadanie Hello teraz sprawdzić hello **ComputeEmulatorRunning %** tooperform zmiennej akcji innego środowiska w oparciu o Określa, czy jest uruchomiona rola hello w hello w chmurze lub hello emulatora. Oto .cmd skrypt powłoki, który sprawdza, czy tej zmiennej środowiskowej.

```cmd
REM   Check if this task is running on hello compute emulator.

IF "%ComputeEmulatorRunning%" == "true" (
    REM   This task is running on hello compute emulator. Perform tasks that must be run only in hello compute emulator.
) ELSE (
    REM   This task is running on hello cloud. Perform tasks that must be run only in hello cloud.
)
```


## <a name="detect-that-your-task-has-already-run"></a>Wykryj, czy zadanie zostało już uruchomione
Rola Hello może odtworzyć bez ponownego uruchomienia komputera powoduje ponownie Twoje toorun zadania uruchamiania. Nie ma żadnych tooindicate flagi, że zadanie zostało już uruchomione na hello hosting maszyny Wirtualnej. Może być niektórych zadań, których nie ma znaczenia, że uruchomione wiele razy. Jednak może wystąpić sytuacja, w którym ma być tooprevent zadania uruchamiania więcej niż raz.

Hello najprostszy sposób toodetect który zadania został już uruchomiony jest toocreate pliku w hello **% TEMP %** folder po pomyślnym zakończeniu operacji hello zadań i jej przyjrzeć hello początek hello zadań. Poniżej przedstawiono przykładowy skrypt powłoki cmd nie.

```cmd
REM   If Task1_Success.txt exists, then Application 1 is already installed.
IF EXIST "%RoleRoot%\Task1_Success.txt" (
  ECHO Application 1 is already installed. Exiting. >> "%TEMP%\StartupLog.txt" 2>&1
  GOTO Finish
)

REM   Run your real exe task
ECHO Running XYZ >> "%TEMP%\StartupLog.txt" 2>&1
"%PathToApp1Install%\setup.exe" >> "%TEMP%\StartupLog.txt" 2>&1

IF %ERRORLEVEL% EQU 0 (
  REM   hello application installed without error. Create a file tooindicate that hello task
  REM   does not need toobe run again.

  ECHO This line will create a file tooindicate that Application 1 installed correctly. > "%RoleRoot%\Task1_Success.txt"

) ELSE (
  REM   An error occurred. Log hello error and exit with hello error code.

  DATE /T >> "%TEMP%\StartupLog.txt" 2>&1
  TIME /T >> "%TEMP%\StartupLog.txt" 2>&1
  ECHO  An error occurred running task 1. Errorlevel = %ERRORLEVEL%. >> "%TEMP%\StartupLog.txt" 2>&1

  EXIT %ERRORLEVEL%
)

:Finish

REM   Exit normally.
EXIT /B 0
```

## <a name="task-best-practices"></a>Najlepsze rozwiązania w zakresie zadania
Poniżej przedstawiono najważniejsze wskazówki, które należy wykonać podczas konfigurowania zadania dla roli użytkownika sieci web lub procesu roboczego.

### <a name="always-log-startup-activities"></a>Zawsze dziennika uruchomienia działania
Visual Studio nie zapewnia toostep debugera za pomocą plików wsadowych, więc jest dobrym tooget jak najwięcej danych operacji hello pliki wsadowe, jak to możliwe. Rejestrowanie hello dane wyjściowe pliki wsadowe, zarówno **stdout** i **stderr**, można podać ważne informacje podczas próby toodebug i Usuń pliki wsadowe. toolog zarówno **stdout** i **stderr** toohello StartupLog.txt pliku w hello katalog wskazywany tooby hello **% TEMP %** zmiennej środowiskowej, Dodaj tekst hello `>>  "%TEMP%\\StartupLog.txt" 2>&1`toohello koniec określonych wierszy można mają toolog. Na przykład tooexecute setup.exe w hello **PathToApp1Install %** katalogu:

    "%PathToApp1Install%\setup.exe" >> "%TEMP%\StartupLog.txt" 2>&1

toosimplify dane xml można tworzyć otoka *cmd* pliku, który wywołuje wszystkie uruchamiania zadań wraz z rejestrowania i zapewnia hello udziałów każdego zadania podrzędnego samego zmiennych środowiskowych.

Może być jednak irytujących toouse `>> "%TEMP%\StartupLog.txt" 2>&1` na końcu hello każdego uruchomienia zadania. Rejestrowanie zadania można wymusić przez utworzenie otoka obsługuje rejestrowanie dla Ciebie. Tej otoki wywołuje plik wsadowy rzeczywistych hello ma toorun. Żadnych danych wyjściowych z pliku wsadowego docelowego hello będzie przekierowany toohello *Startuplog.txt* pliku.

Witaj poniższy przykład pokazuje, jak tooredirect wszystkie dane wyjściowe z pliku wsadowego uruchamiania. W tym przykładzie plik ServerDefinition.csdef hello tworzy zadanie uruchamiania, który wywołuje *logwrap.cmd*. *logwrap.cmd* wywołania *Startup2.cmd*, przekierowywanie wszystkie dane wyjściowe zbyt**% TEMP %\\StartupLog.txt**.

ServiceDefinition.cmd:

```xml
<Startup>
    <Task commandLine="logwrap.cmd startup2.cmd" executionContext="limited" taskType="simple" />
</Startup>
```

**logwrap.cmd:**

```cmd
@ECHO OFF

REM   logwrap.cmd calls passed in batch file, redirecting all output toohello StartupLog.txt log file.

ECHO [%date% %time%] == START logwrap.cmd ============================================== >> "%TEMP%\StartupLog.txt" 2>&1
ECHO [%date% %time%] Running %1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   Call hello child command batch file, redirecting all output toohello StartupLog.txt log file.
START /B /WAIT %1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   Log hello completion of child command.
ECHO [%date% %time%] Done >> "%TEMP%\StartupLog.txt" 2>&1

IF %ERRORLEVEL% EQU 0 (

   REM   No errors occurred. Exit logwrap.cmd normally.
   ECHO [%date% %time%] == END logwrap.cmd ================================================ >> "%TEMP%\StartupLog.txt" 2>&1
   ECHO.  >> "%TEMP%\StartupLog.txt" 2>&1
   EXIT /B 0

) ELSE (

   REM   Log hello error.
   ECHO [%date% %time%] An error occurred. hello ERRORLEVEL = %ERRORLEVEL%.  >> "%TEMP%\StartupLog.txt" 2>&1
   ECHO [%date% %time%] == END logwrap.cmd ================================================ >> "%TEMP%\StartupLog.txt" 2>&1
   ECHO.  >> "%TEMP%\StartupLog.txt" 2>&1
   EXIT /B %ERRORLEVEL%

)
```

**Startup2.cmd:**

```cmd
@ECHO OFF

REM   This is hello batch file where hello startup steps should be performed. Because of the
REM   way Startup2.cmd was called, all commands and their outputs will be stored in the
REM   StartupLog.txt file in hello directory pointed tooby hello TEMP environment variable.

REM   If an error occurs, hello following command will pass hello ERRORLEVEL back toothe
REM   calling batch file.

ECHO [%date% %time%] Some log information about this task
ECHO [%date% %time%] Some more log information about this task

EXIT %ERRORLEVEL%
```

Przykładowe dane wyjściowe w hello **StartupLog.txt** pliku:

```txt
[Mon 10/17/2016 20:24:46.75] == START logwrap.cmd ============================================== 
[Mon 10/17/2016 20:24:46.75] Running command1.cmd 
[Mon 10/17/2016 20:24:46.77] Some log information about this task
[Mon 10/17/2016 20:24:46.77] Some more log information about this task
[Mon 10/17/2016 20:24:46.77] Done 
[Mon 10/17/2016 20:24:46.77] == END logwrap.cmd ================================================ 
```

> [!TIP]
> Witaj **StartupLog.txt** plik znajduje się w hello *C:\Resources\temp\\\RoleTemp {identyfikator roli}* folderu.
> 
> 

### <a name="set-executioncontext-appropriately-for-startup-tasks"></a>Ustaw executionContext odpowiednio do uruchamiania zadań
Ustaw uprawnienia odpowiednio do hello uruchomienia zadania. Czasami uruchamiania zadań należy uruchomić z podwyższonym poziomem uprawnień, nawet jeśli roli hello jest uruchamiany z normalnym uprawnieniami.

Witaj [executionContext][zadań] atrybut ustawia poziom uprawnień hello hello uruchomienia zadania. Przy użyciu `executionContext="limited"` oznacza, że zadanie uruchamiania hello ma hello poziomu uprawnień roli hello. Przy użyciu `executionContext="elevated"` oznacza hello zadanie uruchamiania ma uprawnienia administratora, co pozwala hello uruchomienia zadania administratora tooperform zadanie bez nadawania roli tooyour uprawnienia administratora.

Przykładem zadanie uruchamiania, który wymaga pełnych uprawnień jest zadanie uruchamiania, która używa **AppCmd.exe** tooconfigure usług IIS. **AppCmd.exe** wymaga `executionContext="elevated"`.

### <a name="use-hello-appropriate-tasktype"></a>Użyć odpowiednich taskType hello
Witaj [taskType][zadań] atrybut Określa zadanie uruchamiania hello sposób hello jest wykonywana. Istnieją trzy wartości: **proste**, **tła**, i **pierwszego planu**. Witaj zadania tła i pierwszego planu są uruchamiane asynchronicznie, a następnie hello prostych zadań są wykonywane synchronicznie pojedynczo.

Z **proste** uruchomienia zadania, można ustawić hello kolejność uruchamiania zadań hello według kolejności hello, w których hello zadania są wymienione w pliku ServiceDefinition.csdef hello. Jeśli **proste** zadań kończy się niezerowy kod zakończenia, a następnie hello zatrzymuje procedury uruchamiania i nie można uruchomić hello roli.

Witaj różnica między **tła** uruchamiania zadań i **pierwszego planu** uruchomienia zadania oznacza, że **pierwszego planu** zadania Zachowaj hello roli uruchomiony do momentu hello  **pierwszego planu** zakończeniem zadania. Oznacza to też, że jeśli hello **pierwszego planu** zawiesza się zadania lub awarii hello rola nie jest odtwarzana do hello **pierwszego planu** wymusza zadań zamknięte. Z tego powodu **tła** zadania są zalecane dla asynchronicznego uruchamiania zadań, o ile nie muszą tej funkcji hello **pierwszego planu** zadań.

### <a name="end-batch-files-with-exit-b-0"></a>Pliki wsadowe zakończenia z /B zakończenia 0
Witaj roli uruchamia się tylko jeśli hello **errorlevel** z każdej z prostego uruchamiania zadań wynosi zero. Nie wszystkie programy ustawić hello **errorlevel** (kod zakończenia) poprawnie, więc plik wsadowy hello powinna kończyć `EXIT /B 0` Jeżeli wszystko działa prawidłowo.

Brak `EXIT /B 0` na powitania koniec pliku wsadowego uruchamiania jest częstą przyczyną ról, które nie są uruchamiane.

> [!NOTE]
> I zaobserwowany tej partii zagnieżdżone pliki czasami rozłączaj po użyciu hello `/B` parametru. Możesz się upewnić, że ten problem zawieszenie nie odbywa się jeśli inny plik wsadowy wymaga bieżącego pliku wsadowego, takich jak użycie hello toomake [otoki dziennika](#always-log-startup-activities). W przypadku pominięcia hello `/B` parametru w tym przypadku.
> 
> 

### <a name="expect-startup-tasks-toorun-more-than-once"></a>Oczekiwane uruchamiania zadań toorun więcej niż raz
Nie wszystkie odtwarza roli obejmować ponowne uruchomienie komputera, ale wszystkie odtwarza roli obejmują uruchomione wszystkie zadania uruchamiania. Oznacza to, że uruchamiania zadań musi być możliwe toorun wielokrotnie między uruchamiany ponownie bez problemów. Jest to omówione w hello [powyższej sekcji](#detect-that-your-task-has-already-run).

### <a name="use-local-storage-toostore-files-that-must-be-accessed-in-hello-role"></a>Użyj magazynu lokalnego toostore pliki, które muszą być dostępne w roli hello
Toocopy lub tworzenie pliku podczas uruchamiania zadania następnie jest dostępny tooyour roli, a następnie tego pliku muszą być umieszczone w lokalnej pamięci masowej. Zobacz hello [powyższej sekcji](#create-files-in-local-storage-from-a-startup-task).

## <a name="next-steps"></a>Następne kroki
Przejrzyj chmury hello [z modelu i pakietu](cloud-services-model-and-package.md)

Dowiedz się więcej na temat [zadania](cloud-services-startup-tasks.md) pracy.

[Tworzenie i wdrażanie](cloud-services-how-to-create-deploy-portal.md) pakietu usługi w chmurze.

[ServiceDefinition.csdef]: cloud-services-model-and-package.md#csdef
[zadań]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Task
[Startup]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Startup
[Runtime]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Runtime
[środowiska]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Environment
[zmiennej]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Variable
[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue
[RoleEnvironment]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx
[Punkty końcowe]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Endpoints
[LocalStorage]: https://msdn.microsoft.com/library/azure/gg557552.aspx#LocalStorage
[LocalResources]: https://msdn.microsoft.com/library/azure/gg557552.aspx#LocalResources
[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue
