---
title: "aaaGet wprowadzenie do języka Python i usług Azure Cloud Services | Dokumentacja firmy Microsoft"
description: "Omówienie używania programu Python Tools dla usług w chmurze Azure toocreate programu Visual Studio w tym ról sieć web i proces roboczy."
services: cloud-services
documentationcenter: python
author: thraka
manager: timlt
editor: 
ms.assetid: 5489405d-6fa9-4b11-a161-609103cbdc18
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: hero-article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: f5fd85e754839f146abe912351c59dc4a148c990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="python-web-and-worker-roles-with-python-tools-for-visual-studio"></a>Role Sieć Web i Proces roboczy języka Python z programem Python Tools for Visual Studio

Ten artykuł zawiera omówienie sposobu użycia ról Sieć Web i Proces roboczy języka Python za pomocą narzędzi [Python Tools for Visual Studio][Python Tools for Visual Studio]. Dowiedz się, jak toouse toocreate programu Visual Studio i wdrażanie podstawowe usługi w chmurze, która używa języka Python.

## <a name="prerequisites"></a>Wymagania wstępne
* [Program Visual Studio w wersji 2013, 2015 lub 2017](https://www.visualstudio.com/)
* [Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS)
* [Azure SDK Tools for VS 2013][Azure SDK Tools for VS 2013] lub  
[Azure SDK Tools for VS 2015][Azure SDK Tools for VS 2015] lub  
[Azure SDK Tools for VS 2017][Azure SDK Tools for VS 2017]
* [32-bitowe środowisko Python w wersji 2.7][Python 2.7 32-bit] lub [32-bitowe środowisko Python w wersji 3.5][Python 3.5 32-bit]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="what-are-python-web-and-worker-roles"></a>Co to są role Sieć Web i Proces roboczy języka Python?
Platforma Azure udostępnia trzy modele obliczeniowe na potrzeby uruchamiania aplikacji: [funkcja Web Apps w usłudze Azure App Service][execution model-web sites], [Azure Virtual Machines][execution model-vms] i [Azure Cloud Services][execution model-cloud services]. Wszystkie trzy modele obsługują język Python. Usługi Cloud Services, które obejmują role Sieć Web i Proces roboczy, udostępniają rozwiązanie typu *Platforma jako usługa (Platform as a Service, PaaS)*. W ramach usługi w chmurze roli sieci web zapewnia dedykowany Internet Information Services (IIS) w sieci web serwera toohost frontonu sieci web aplikacji, natomiast roli procesu roboczego można uruchamiać asynchroniczne, długotrwałe lub ciągłe zadania niezależne interakcji z użytkownikiem lub danych wejściowych.

Aby uzyskać więcej informacji, zobacz [Co to jest usługa w chmurze?]

> [!NOTE]
> *Szukasz toobuild prosty witryny sieci Web?*
> Jeśli scenariusz obejmuje tylko prosty witryny sieci Web frontonu, rozważ użycie lekkiej funkcji Web Apps hello w usłudze Azure App Service. Możesz łatwo przeprowadzić uaktualnienie tooa usługi w chmurze rozwoju witryny sieci Web lub zmiany wymagań. Zobacz hello <a href="/develop/python/">Centrum deweloperów języka Python</a> dla artykułów o programowaniu hello funkcja Web Apps w usłudze Azure App Service.
> <br />
> 
> 

## <a name="project-creation"></a>Tworzenie projektu
W programie Visual Studio, można wybrać **usługi w chmurze Azure** w hello **nowy projekt** okna dialogowego, w obszarze **Python**.

![Okno dialogowe Nowy projekt](./media/cloud-services-python-ptvs/new-project-cloud-service.png)

W Kreatorze usługi w chmurze Azure hello można utworzyć nową sieć web i proces roboczy.

![Okno dialogowe Usługa w chmurze platformy Azure](./media/cloud-services-python-ptvs/new-service-wizard.png)

Szablon roli proces roboczy Hello zawiera schematyczny kod tooconnect tooan kontem magazynu platformy Azure lub usługi Azure Service Bus.

![Rozwiązanie usługi w chmurze](./media/cloud-services-python-ptvs/worker.png)

W dowolnym momencie można dodać sieci web lub procesu roboczego ról tooan istniejącą usługę w chmurze.  Możesz wybrać tooadd istniejących projektów w rozwiązaniu lub utworzyć nowe.

![Polecenie Dodaj rolę](./media/cloud-services-python-ptvs/add-new-or-existing-role.png)

Usługa w chmurze może zawierać role zaimplementowane w różnych językach.  Na przykład można mieć rolę Sieć Web języka Python zaimplementowaną za pomocą środowiska Django, języka Python lub roli Proces roboczy języka C#.  Między rolami można się w łatwy sposób komunikować za pomocą kolejek usługi Service Bus lub kolejek magazynu.

## <a name="install-python-on-hello-cloud-service"></a>Zainstaluj Python na powitania usługi w chmurze
> [!WARNING]
> Hello Instalatora skrypty, które są zainstalowane z programem Visual Studio (w czasie hello ostatniej aktualizacji w tym artykule) nie działają. W tej sekcji opisano sposób obejścia problemu.
> 
> 

Hello główny problem z skryptów instalacji hello jest, czy należy instalować python. Najpierw należy zdefiniować dwa [uruchamiania zadań](cloud-services-startup-tasks.md) w hello [ServiceDefinition.csdef](cloud-services-model-and-package.md#servicedefinitioncsdef) pliku. pierwszym zadaniem Hello (**PrepPython.ps1**) pobiera i instaluje środowisko uruchomieniowe języka Python hello. drugie zadanie Hello (**PipInstaller.ps1**) uruchamia pip tooinstall może mieć zależności.

następujące skrypty Hello napisanych przeznaczonych dla języka Python 3.5. Jeśli chcesz toouse hello wersji 2.x python, hello zestaw **PYTHON2** zmiennej pliku zbyt**na** hello dwa uruchamiania zadań i zadań środowiska uruchomieniowego hello: `<Variable name="PYTHON2" value="<mark>on</mark>" />`.

```xml
<Startup>

  <Task executionContext="elevated" taskType="simple" commandLine="bin\ps.cmd PrepPython.ps1">
    <Environment>
      <Variable name="EMULATED">
        <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
      </Variable>
      <Variable name="PYTHON2" value="off" />
    </Environment>
  </Task>

  <Task executionContext="elevated" taskType="simple" commandLine="bin\ps.cmd PipInstaller.ps1">
    <Environment>
      <Variable name="EMULATED">
        <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
      </Variable>
      <Variable name="PYTHON2" value="off" />
    </Environment>

  </Task>

</Startup>
```

Witaj **PYTHON2** i **PYPATH** zmienne należy dodać zadanie uruchamiania procesu roboczego toohello. Witaj **PYPATH** zmienna jest używana tylko w przypadku hello **PYTHON2** zmienna jest ustawiona zbyt**na**.

```xml
<Runtime>
  <Environment>
    <Variable name="EMULATED">
      <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
    </Variable>
    <Variable name="PYTHON2" value="off" />
    <Variable name="PYPATH" value="%SystemDrive%\Python27" />
  </Environment>
  <EntryPoint>
    <ProgramEntryPoint commandLine="bin\ps.cmd LaunchWorker.ps1" setReadyOnProcessStart="true" />
  </EntryPoint>
</Runtime>
```

#### <a name="sample-servicedefinitioncsdef"></a>Przykładowy plik ServiceDefinition.csdef
```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceDefinition name="AzureCloudServicePython" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition" schemaVersion="2015-04.2.6">
  <WorkerRole name="WorkerRole1" vmsize="Small">
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" />
      <Setting name="Python2" />
    </ConfigurationSettings>
    <Startup>
      <Task executionContext="elevated" taskType="simple" commandLine="bin\ps.cmd PrepPython.ps1">
        <Environment>
          <Variable name="EMULATED">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
          </Variable>
          <Variable name="PYTHON2" value="off" />
        </Environment>
      </Task>
      <Task executionContext="elevated" taskType="simple" commandLine="bin\ps.cmd PipInstaller.ps1">
        <Environment>
          <Variable name="EMULATED">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
          </Variable>
          <Variable name="PYTHON2" value="off" />
        </Environment>
      </Task>
    </Startup>
    <Runtime>
      <Environment>
        <Variable name="EMULATED">
          <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
        </Variable>
        <Variable name="PYTHON2" value="off" />
        <Variable name="PYPATH" value="%SystemDrive%\Python27" />
      </Environment>
      <EntryPoint>
        <ProgramEntryPoint commandLine="bin\ps.cmd LaunchWorker.ps1" setReadyOnProcessStart="true" />
      </EntryPoint>
    </Runtime>
    <Imports>
      <Import moduleName="RemoteAccess" />
      <Import moduleName="RemoteForwarder" />
    </Imports>
  </WorkerRole>
</ServiceDefinition>
```



Następnie należy utworzyć hello **PrepPython.ps1** i **PipInstaller.ps1** pliki w hello **. / bin** folderu roli użytkownika.

#### <a name="preppythonps1"></a>PrepPython.ps1
Ten skrypt instaluje język Python. Jeśli hello **PYTHON2** zmienna środowiskowa jest ustawiona zbyt**na**, Python 2.7 jest zainstalowany, a następnie w przeciwnym razie Python 3.5 jest zainstalowana.

```powershell
$is_emulated = $env:EMULATED -eq "true"
$is_python2 = $env:PYTHON2 -eq "on"
$nl = [Environment]::NewLine

if (-not $is_emulated){
    Write-Output "Checking if python is installed...$nl"
    if ($is_python2) {
        & "${env:SystemDrive}\Python27\python.exe"  -V | Out-Null
    }
    else {
        py -V | Out-Null
    }

    if (-not $?) {

        $url = "https://www.python.org/ftp/python/3.5.2/python-3.5.2-amd64.exe"
        $outFile = "${env:TEMP}\python-3.5.2-amd64.exe"

        if ($is_python2) {
            $url = "https://www.python.org/ftp/python/2.7.12/python-2.7.12.amd64.msi"
            $outFile = "${env:TEMP}\python-2.7.12.amd64.msi"
        }

        Write-Output "Not found, downloading $url too$outFile$nl"
        Invoke-WebRequest $url -OutFile $outFile
        Write-Output "Installing$nl"

        if ($is_python2) {
            Start-Process msiexec.exe -ArgumentList "/q", "/i", "$outFile", "ALLUSERS=1" -Wait
        }
        else {
            Start-Process "$outFile" -ArgumentList "/quiet", "InstallAllUsers=1" -Wait
        }

        Write-Output "Done$nl"
    }
    else {
        Write-Output "Already installed"
    }
}
```

#### <a name="pipinstallerps1"></a>PipInstaller.ps1
Ten skrypt wymaga się pip i instaluje wszystkie zależności hello w hello **requirements.txt** pliku. Jeśli hello **PYTHON2** zmienna środowiskowa jest ustawiona zbyt**na**, Python 2.7 zostanie użyty, w przeciwnym razie Python 3.5 jest używana.

```powershell
$is_emulated = $env:EMULATED -eq "true"
$is_python2 = $env:PYTHON2 -eq "on"
$nl = [Environment]::NewLine

if (-not $is_emulated){
    Write-Output "Checking if requirements.txt exists$nl"
    if (Test-Path ..\requirements.txt) {
        Write-Output "Found. Processing pip$nl"

        if ($is_python2) {
            & "${env:SystemDrive}\Python27\python.exe" -m pip install -r ..\requirements.txt
        }
        else {
            py -m pip install -r ..\requirements.txt
        }

        Write-Output "Done$nl"
    }
    else {
        Write-Output "Not found$nl"
    }
}
```

#### <a name="modify-launchworkerps1"></a>Modyfikowanie skryptu LaunchWorker.ps1
> [!NOTE]
> W przypadku hello **roli procesu roboczego** projektu, **LauncherWorker.ps1** plik jest plikiem uruchamiania hello tooexecute wymagane. W **roli sieci web** projekt, hello uruchamiania pliku zamiast zdefiniowano we właściwościach projektu hello.
> 
> 

Witaj **bin\LaunchWorker.ps1** został pierwotnie utworzony toodo dużo pracy przygotowania, ale naprawdę nie działa. Zamień zawartość hello w tym pliku hello następującego skryptu.

Ten skrypt wymaga hello **worker.py** plik z projektu języka python. Jeśli hello **PYTHON2** zmienna środowiskowa jest ustawiona zbyt**na**, Python 2.7 zostanie użyty, w przeciwnym razie Python 3.5 jest używana.

```powershell
$is_emulated = $env:EMULATED -eq "true"
$is_python2 = $env:PYTHON2 -eq "on"
$nl = [Environment]::NewLine

if (-not $is_emulated)
{
    Write-Output "Running worker.py$nl"

    if ($is_python2) {
        cd..
        iex "$env:PYPATH\python.exe worker.py"
    }
    else {
        cd..
        iex "py worker.py"
    }
}
else
{
    Write-Output "Running (EMULATED) worker.py$nl"

    # Customize tooyour local dev environment

    if ($is_python2) {
        cd..
        iex "$env:PYPATH\python.exe worker.py"
    }
    else {
        cd..
        iex "py worker.py"
    }
}
```

#### <a name="pscmd"></a>ps.cmd
Szablony Visual Studio Hello powinien utworzyć **ps.cmd** pliku w hello **. / bin** folderu. Ten skrypt powłoki uwidacznia hello PowerShell skrypty otoki powyżej i umożliwia rejestrowanie na podstawie nazwy hello hello otoki środowiska PowerShell o nazwie. Jeśli ten plik nie został utworzony, jego zawartość powinna wyglądać następująco. 

```bat
@echo off

cd /D %~dp0

if not exist "%DiagnosticStore%\LogFiles" mkdir "%DiagnosticStore%\LogFiles"
%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe -ExecutionPolicy Unrestricted -File %* >> "%DiagnosticStore%\LogFiles\%~n1.txt" 2>> "%DiagnosticStore%\LogFiles\%~n1.err.txt"
```



## <a name="run-locally"></a>Uruchamianie lokalnie
Jeśli ustawisz projekt usługi w chmurze jako projekt startowy hello i naciśnij klawisz F5, usługa w chmurze hello jest uruchamiany w lokalnym emulatorze platformy Azure hello.

Mimo że PTVS obsługuje uruchamianie w emulatorze hello, debugowania (na przykład punktów przerwania) nie działa.

toodebug poszczególnych ról sieci web i proces roboczy, można ustawić hello projekt roli jako projekt startowy hello i to zamiast debugowania.  Można również ustawić wiele projektów startowych.  Kliknij prawym przyciskiem myszy rozwiązanie hello, a następnie wybierz **Ustaw projekty startowe**.

![Właściwości projektu startowego rozwiązania](./media/cloud-services-python-ptvs/startup.png)

## <a name="publish-tooazure"></a>Publikowanie tooAzure
toopublish, kliknij prawym przyciskiem myszy projekt usługi w chmurze hello w rozwiązaniu hello, a następnie wybierz **publikowania**.

![Logowanie na potrzeby publikowania na platformie Microsoft Azure](./media/cloud-services-python-ptvs/publish-sign-in.png)

Postępuj zgodnie z hello kreatora. Jeśli trzeba, włącz pulpit zdalny. Pulpit zdalny jest przydatne, gdy będziesz potrzebować toodebug coś.

Po zakończeniu konfigurowania ustawień kliknij pozycję **Publikuj**.

Niektóre postęp jest wyświetlany w oknie danych wyjściowych hello, a następnie pojawi się okno Dziennik aktywności platformy Azure Microsoft hello.

![Okno Dziennik aktywności platformy Microsoft Azure](./media/cloud-services-python-ptvs/publish-activity-log.png)

Wdrożenie ma toocomplete kilka minut, następnie sieci web i/lub uruchamiania roli proces roboczy na platformie Azure!

### <a name="investigate-logs"></a>Sprawdzanie dzienników
Po maszyny wirtualnej usługi chmury hello jest uruchamiany i instaluje Python, można przyjrzeć się toofind dzienniki hello jakiekolwiek komunikaty o błędach. Te dzienniki znajdują się w hello **C:\Resources\Directory\\\LogFiles {roli}** folderu. **PrepPython.err.txt** ma co najmniej jeden błąd w nim z po hello skrypt próbuje toodetect, jeśli jest zainstalowana Python i **PipInstaller.err.txt** może skarżą się o nieaktualną wersją pip.

## <a name="next-steps"></a>Następne kroki
Aby uzyskać szczegółowe informacje na temat pracy z role sieć web i proces roboczy w narzędzia Python Tools for Visual Studio zobacz dokumentację PTVS hello:

* [Projekty usługi w chmurze][Cloud Service Projects]

Aby uzyskać więcej informacji o korzystaniu z sieci web i proces roboczy role, takie jak przy użyciu usługi Azure Storage lub Service Bus usług Azure, zobacz następujące artykuły hello:

* [Blob Service][Blob Service]
* [Table Service][Table Service]
* [Queue Service][Queue Service]
* [Kolejki usługi Service Bus][Service Bus Queues]
* [Tematy usługi Service Bus][Service Bus Topics]

<!--Link references-->

[Co to jest usługa w chmurze?]: cloud-services-choose-me.md
[execution model-web sites]: ../app-service-web/app-service-web-overview.md
[execution model-vms]:../virtual-machines/windows/overview.md
[execution model-cloud services]: cloud-services-choose-me.md
[Python Developer Center]: /develop/python/

[Blob Service]:../storage/blobs/storage-python-how-to-use-blob-storage.md
[Queue Service]: ../storage/queues/storage-python-how-to-use-queue-storage.md
[Table Service]:../cosmos-db/table-storage-how-to-use-python.md
[Service Bus Queues]: ../service-bus-messaging/service-bus-python-how-to-use-queues.md
[Service Bus Topics]: ../service-bus-messaging/service-bus-python-how-to-use-topics-subscriptions.md


<!--External Link references-->

[Python Tools for Visual Studio]: http://aka.ms/ptvs
[Python Tools for Visual Studio Documentation]: http://aka.ms/ptvsdocs
[Cloud Service Projects]: http://go.microsoft.com/fwlink/?LinkId=624028
[Azure SDK Tools for VS 2013]: http://go.microsoft.com/fwlink/?LinkId=746482
[Azure SDK Tools for VS 2015]: http://go.microsoft.com/fwlink/?LinkId=746481
[Azure SDK Tools for VS 2017]: http://go.microsoft.com/fwlink/?LinkId=746483
[Python 2.7 32-bit]: https://www.python.org/downloads/
[Python 3.5 32-bit]: https://www.python.org/downloads/
