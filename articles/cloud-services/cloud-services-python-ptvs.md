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
# <a name="python-web-and-worker-roles-with-python-tools-for-visual-studio"></a><span data-ttu-id="d602e-103">Role Sieć Web i Proces roboczy języka Python z programem Python Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d602e-103">Python web and worker roles with Python Tools for Visual Studio</span></span>

<span data-ttu-id="d602e-104">Ten artykuł zawiera omówienie sposobu użycia ról Sieć Web i Proces roboczy języka Python za pomocą narzędzi [Python Tools for Visual Studio][Python Tools for Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="d602e-104">This article provides an overview of using Python web and worker roles using [Python Tools for Visual Studio][Python Tools for Visual Studio].</span></span> <span data-ttu-id="d602e-105">Dowiedz się, jak toouse toocreate programu Visual Studio i wdrażanie podstawowe usługi w chmurze, która używa języka Python.</span><span class="sxs-lookup"><span data-stu-id="d602e-105">Learn how toouse Visual Studio toocreate and deploy a basic Cloud Service that uses Python.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d602e-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d602e-106">Prerequisites</span></span>
* [<span data-ttu-id="d602e-107">Program Visual Studio w wersji 2013, 2015 lub 2017</span><span class="sxs-lookup"><span data-stu-id="d602e-107">Visual Studio 2013, 2015, or 2017</span></span>](https://www.visualstudio.com/)
* <span data-ttu-id="d602e-108">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS)</span><span class="sxs-lookup"><span data-stu-id="d602e-108">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS)</span></span>
* <span data-ttu-id="d602e-109">[Azure SDK Tools for VS 2013][Azure SDK Tools for VS 2013] lub</span><span class="sxs-lookup"><span data-stu-id="d602e-109">[Azure SDK Tools for VS 2013][Azure SDK Tools for VS 2013] or</span></span>  
<span data-ttu-id="d602e-110">[Azure SDK Tools for VS 2015][Azure SDK Tools for VS 2015] lub</span><span class="sxs-lookup"><span data-stu-id="d602e-110">[Azure SDK Tools for VS 2015][Azure SDK Tools for VS 2015] or</span></span>  
<span data-ttu-id="d602e-111">[Azure SDK Tools for VS 2017][Azure SDK Tools for VS 2017]</span><span class="sxs-lookup"><span data-stu-id="d602e-111">[Azure SDK Tools for VS 2017][Azure SDK Tools for VS 2017]</span></span>
* <span data-ttu-id="d602e-112">[32-bitowe środowisko Python w wersji 2.7][Python 2.7 32-bit] lub [32-bitowe środowisko Python w wersji 3.5][Python 3.5 32-bit]</span><span class="sxs-lookup"><span data-stu-id="d602e-112">[Python 2.7 32-bit][Python 2.7 32-bit] or [Python 3.5 32-bit][Python 3.5 32-bit]</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="what-are-python-web-and-worker-roles"></a><span data-ttu-id="d602e-113">Co to są role Sieć Web i Proces roboczy języka Python?</span><span class="sxs-lookup"><span data-stu-id="d602e-113">What are Python web and worker roles?</span></span>
<span data-ttu-id="d602e-114">Platforma Azure udostępnia trzy modele obliczeniowe na potrzeby uruchamiania aplikacji: [funkcja Web Apps w usłudze Azure App Service][execution model-web sites], [Azure Virtual Machines][execution model-vms] i [Azure Cloud Services][execution model-cloud services].</span><span class="sxs-lookup"><span data-stu-id="d602e-114">Azure provides three compute models for running applications: [Web Apps feature in Azure App Service][execution model-web sites], [Azure Virtual Machines][execution model-vms], and [Azure Cloud Services][execution model-cloud services].</span></span> <span data-ttu-id="d602e-115">Wszystkie trzy modele obsługują język Python.</span><span class="sxs-lookup"><span data-stu-id="d602e-115">All three models support Python.</span></span> <span data-ttu-id="d602e-116">Usługi Cloud Services, które obejmują role Sieć Web i Proces roboczy, udostępniają rozwiązanie typu *Platforma jako usługa (Platform as a Service, PaaS)*.</span><span class="sxs-lookup"><span data-stu-id="d602e-116">Cloud Services, which include web and worker roles, provide *Platform as a Service (PaaS)*.</span></span> <span data-ttu-id="d602e-117">W ramach usługi w chmurze roli sieci web zapewnia dedykowany Internet Information Services (IIS) w sieci web serwera toohost frontonu sieci web aplikacji, natomiast roli procesu roboczego można uruchamiać asynchroniczne, długotrwałe lub ciągłe zadania niezależne interakcji z użytkownikiem lub danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="d602e-117">Within a cloud service, a web role provides a dedicated Internet Information Services (IIS) web server toohost front end web applications, while a worker role can run asynchronous, long-running, or perpetual tasks independent of user interaction or input.</span></span>

<span data-ttu-id="d602e-118">Aby uzyskać więcej informacji, zobacz [Co to jest usługa w chmurze?]</span><span class="sxs-lookup"><span data-stu-id="d602e-118">For more information, see [What is a Cloud Service?].</span></span>

> [!NOTE]
> <span data-ttu-id="d602e-119">*Szukasz toobuild prosty witryny sieci Web?*</span><span class="sxs-lookup"><span data-stu-id="d602e-119">*Looking toobuild a simple website?*</span></span>
> <span data-ttu-id="d602e-120">Jeśli scenariusz obejmuje tylko prosty witryny sieci Web frontonu, rozważ użycie lekkiej funkcji Web Apps hello w usłudze Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="d602e-120">If your scenario involves just a simple website front end, consider using hello lightweight Web Apps feature in Azure App Service.</span></span> <span data-ttu-id="d602e-121">Możesz łatwo przeprowadzić uaktualnienie tooa usługi w chmurze rozwoju witryny sieci Web lub zmiany wymagań.</span><span class="sxs-lookup"><span data-stu-id="d602e-121">You can easily upgrade tooa Cloud Service as your website grows and your requirements change.</span></span> <span data-ttu-id="d602e-122">Zobacz hello <a href="/develop/python/">Centrum deweloperów języka Python</a> dla artykułów o programowaniu hello funkcja Web Apps w usłudze Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="d602e-122">See hello <a href="/develop/python/">Python Developer Center</a> for articles that cover development of hello Web Apps feature in Azure App Service.</span></span>
> <br />
> 
> 

## <a name="project-creation"></a><span data-ttu-id="d602e-123">Tworzenie projektu</span><span class="sxs-lookup"><span data-stu-id="d602e-123">Project creation</span></span>
<span data-ttu-id="d602e-124">W programie Visual Studio, można wybrać **usługi w chmurze Azure** w hello **nowy projekt** okna dialogowego, w obszarze **Python**.</span><span class="sxs-lookup"><span data-stu-id="d602e-124">In Visual Studio, you can select **Azure Cloud Service** in hello **New Project** dialog box, under **Python**.</span></span>

![Okno dialogowe Nowy projekt](./media/cloud-services-python-ptvs/new-project-cloud-service.png)

<span data-ttu-id="d602e-126">W Kreatorze usługi w chmurze Azure hello można utworzyć nową sieć web i proces roboczy.</span><span class="sxs-lookup"><span data-stu-id="d602e-126">In hello Azure Cloud Service wizard, you can create new web and worker roles.</span></span>

![Okno dialogowe Usługa w chmurze platformy Azure](./media/cloud-services-python-ptvs/new-service-wizard.png)

<span data-ttu-id="d602e-128">Szablon roli proces roboczy Hello zawiera schematyczny kod tooconnect tooan kontem magazynu platformy Azure lub usługi Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="d602e-128">hello worker role template comes with boilerplate code tooconnect tooan Azure storage account or Azure Service Bus.</span></span>

![Rozwiązanie usługi w chmurze](./media/cloud-services-python-ptvs/worker.png)

<span data-ttu-id="d602e-130">W dowolnym momencie można dodać sieci web lub procesu roboczego ról tooan istniejącą usługę w chmurze.</span><span class="sxs-lookup"><span data-stu-id="d602e-130">You can add web or worker roles tooan existing cloud service at any time.</span></span>  <span data-ttu-id="d602e-131">Możesz wybrać tooadd istniejących projektów w rozwiązaniu lub utworzyć nowe.</span><span class="sxs-lookup"><span data-stu-id="d602e-131">You can choose tooadd existing projects in your solution, or create new ones.</span></span>

![Polecenie Dodaj rolę](./media/cloud-services-python-ptvs/add-new-or-existing-role.png)

<span data-ttu-id="d602e-133">Usługa w chmurze może zawierać role zaimplementowane w różnych językach.</span><span class="sxs-lookup"><span data-stu-id="d602e-133">Your cloud service can contain roles implemented in different languages.</span></span>  <span data-ttu-id="d602e-134">Na przykład można mieć rolę Sieć Web języka Python zaimplementowaną za pomocą środowiska Django, języka Python lub roli Proces roboczy języka C#.</span><span class="sxs-lookup"><span data-stu-id="d602e-134">For example, you can have a Python web role implemented using Django, with Python, or with C# worker roles.</span></span>  <span data-ttu-id="d602e-135">Między rolami można się w łatwy sposób komunikować za pomocą kolejek usługi Service Bus lub kolejek magazynu.</span><span class="sxs-lookup"><span data-stu-id="d602e-135">You can easily communicate between your roles using Service Bus queues or storage queues.</span></span>

## <a name="install-python-on-hello-cloud-service"></a><span data-ttu-id="d602e-136">Zainstaluj Python na powitania usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="d602e-136">Install Python on hello cloud service</span></span>
> [!WARNING]
> <span data-ttu-id="d602e-137">Hello Instalatora skrypty, które są zainstalowane z programem Visual Studio (w czasie hello ostatniej aktualizacji w tym artykule) nie działają.</span><span class="sxs-lookup"><span data-stu-id="d602e-137">hello setup scripts that are installed with Visual Studio (at hello time this article was last updated) do not work.</span></span> <span data-ttu-id="d602e-138">W tej sekcji opisano sposób obejścia problemu.</span><span class="sxs-lookup"><span data-stu-id="d602e-138">This section describes a workaround.</span></span>
> 
> 

<span data-ttu-id="d602e-139">Hello główny problem z skryptów instalacji hello jest, czy należy instalować python.</span><span class="sxs-lookup"><span data-stu-id="d602e-139">hello main problem with hello setup scripts is that they do not install python.</span></span> <span data-ttu-id="d602e-140">Najpierw należy zdefiniować dwa [uruchamiania zadań](cloud-services-startup-tasks.md) w hello [ServiceDefinition.csdef](cloud-services-model-and-package.md#servicedefinitioncsdef) pliku.</span><span class="sxs-lookup"><span data-stu-id="d602e-140">First, define two [startup tasks](cloud-services-startup-tasks.md) in hello [ServiceDefinition.csdef](cloud-services-model-and-package.md#servicedefinitioncsdef) file.</span></span> <span data-ttu-id="d602e-141">pierwszym zadaniem Hello (**PrepPython.ps1**) pobiera i instaluje środowisko uruchomieniowe języka Python hello.</span><span class="sxs-lookup"><span data-stu-id="d602e-141">hello first task (**PrepPython.ps1**) downloads and installs hello Python runtime.</span></span> <span data-ttu-id="d602e-142">drugie zadanie Hello (**PipInstaller.ps1**) uruchamia pip tooinstall może mieć zależności.</span><span class="sxs-lookup"><span data-stu-id="d602e-142">hello second task (**PipInstaller.ps1**) runs pip tooinstall any dependencies you may have.</span></span>

<span data-ttu-id="d602e-143">następujące skrypty Hello napisanych przeznaczonych dla języka Python 3.5.</span><span class="sxs-lookup"><span data-stu-id="d602e-143">hello following scripts were written targeting Python 3.5.</span></span> <span data-ttu-id="d602e-144">Jeśli chcesz toouse hello wersji 2.x python, hello zestaw **PYTHON2** zmiennej pliku zbyt**na** hello dwa uruchamiania zadań i zadań środowiska uruchomieniowego hello: `<Variable name="PYTHON2" value="<mark>on</mark>" />`.</span><span class="sxs-lookup"><span data-stu-id="d602e-144">If you want toouse hello version 2.x of python, set hello **PYTHON2** variable file too**on** for hello two startup tasks and hello runtime task: `<Variable name="PYTHON2" value="<mark>on</mark>" />`.</span></span>

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

<span data-ttu-id="d602e-145">Witaj **PYTHON2** i **PYPATH** zmienne należy dodać zadanie uruchamiania procesu roboczego toohello.</span><span class="sxs-lookup"><span data-stu-id="d602e-145">hello **PYTHON2** and **PYPATH** variables must be added toohello worker startup task.</span></span> <span data-ttu-id="d602e-146">Witaj **PYPATH** zmienna jest używana tylko w przypadku hello **PYTHON2** zmienna jest ustawiona zbyt**na**.</span><span class="sxs-lookup"><span data-stu-id="d602e-146">hello **PYPATH** variable is only used if hello **PYTHON2** variable is set too**on**.</span></span>

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

#### <a name="sample-servicedefinitioncsdef"></a><span data-ttu-id="d602e-147">Przykładowy plik ServiceDefinition.csdef</span><span class="sxs-lookup"><span data-stu-id="d602e-147">Sample ServiceDefinition.csdef</span></span>
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



<span data-ttu-id="d602e-148">Następnie należy utworzyć hello **PrepPython.ps1** i **PipInstaller.ps1** pliki w hello **. / bin** folderu roli użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d602e-148">Next, create hello **PrepPython.ps1** and **PipInstaller.ps1** files in hello **./bin** folder of your role.</span></span>

#### <a name="preppythonps1"></a><span data-ttu-id="d602e-149">PrepPython.ps1</span><span class="sxs-lookup"><span data-stu-id="d602e-149">PrepPython.ps1</span></span>
<span data-ttu-id="d602e-150">Ten skrypt instaluje język Python.</span><span class="sxs-lookup"><span data-stu-id="d602e-150">This script installs python.</span></span> <span data-ttu-id="d602e-151">Jeśli hello **PYTHON2** zmienna środowiskowa jest ustawiona zbyt**na**, Python 2.7 jest zainstalowany, a następnie w przeciwnym razie Python 3.5 jest zainstalowana.</span><span class="sxs-lookup"><span data-stu-id="d602e-151">If hello **PYTHON2** environment variable is set too**on**, then Python 2.7 is installed, otherwise Python 3.5 is installed.</span></span>

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

#### <a name="pipinstallerps1"></a><span data-ttu-id="d602e-152">PipInstaller.ps1</span><span class="sxs-lookup"><span data-stu-id="d602e-152">PipInstaller.ps1</span></span>
<span data-ttu-id="d602e-153">Ten skrypt wymaga się pip i instaluje wszystkie zależności hello w hello **requirements.txt** pliku.</span><span class="sxs-lookup"><span data-stu-id="d602e-153">This script calls up pip and installs all of hello dependencies in hello **requirements.txt** file.</span></span> <span data-ttu-id="d602e-154">Jeśli hello **PYTHON2** zmienna środowiskowa jest ustawiona zbyt**na**, Python 2.7 zostanie użyty, w przeciwnym razie Python 3.5 jest używana.</span><span class="sxs-lookup"><span data-stu-id="d602e-154">If hello **PYTHON2** environment variable is set too**on**, then Python 2.7 is used, otherwise Python 3.5 is used.</span></span>

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

#### <a name="modify-launchworkerps1"></a><span data-ttu-id="d602e-155">Modyfikowanie skryptu LaunchWorker.ps1</span><span class="sxs-lookup"><span data-stu-id="d602e-155">Modify LaunchWorker.ps1</span></span>
> [!NOTE]
> <span data-ttu-id="d602e-156">W przypadku hello **roli procesu roboczego** projektu, **LauncherWorker.ps1** plik jest plikiem uruchamiania hello tooexecute wymagane.</span><span class="sxs-lookup"><span data-stu-id="d602e-156">In hello case of a **worker role** project, **LauncherWorker.ps1** file is required tooexecute hello startup file.</span></span> <span data-ttu-id="d602e-157">W **roli sieci web** projekt, hello uruchamiania pliku zamiast zdefiniowano we właściwościach projektu hello.</span><span class="sxs-lookup"><span data-stu-id="d602e-157">In a **web role** project, hello startup file is instead defined in hello project properties.</span></span>
> 
> 

<span data-ttu-id="d602e-158">Witaj **bin\LaunchWorker.ps1** został pierwotnie utworzony toodo dużo pracy przygotowania, ale naprawdę nie działa.</span><span class="sxs-lookup"><span data-stu-id="d602e-158">hello **bin\LaunchWorker.ps1** was originally created toodo a lot of prep work but it doesn't really work.</span></span> <span data-ttu-id="d602e-159">Zamień zawartość hello w tym pliku hello następującego skryptu.</span><span class="sxs-lookup"><span data-stu-id="d602e-159">Replace hello contents in that file with hello following script.</span></span>

<span data-ttu-id="d602e-160">Ten skrypt wymaga hello **worker.py** plik z projektu języka python.</span><span class="sxs-lookup"><span data-stu-id="d602e-160">This script calls hello **worker.py** file from your python project.</span></span> <span data-ttu-id="d602e-161">Jeśli hello **PYTHON2** zmienna środowiskowa jest ustawiona zbyt**na**, Python 2.7 zostanie użyty, w przeciwnym razie Python 3.5 jest używana.</span><span class="sxs-lookup"><span data-stu-id="d602e-161">If hello **PYTHON2** environment variable is set too**on**, then Python 2.7 is used, otherwise Python 3.5 is used.</span></span>

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

#### <a name="pscmd"></a><span data-ttu-id="d602e-162">ps.cmd</span><span class="sxs-lookup"><span data-stu-id="d602e-162">ps.cmd</span></span>
<span data-ttu-id="d602e-163">Szablony Visual Studio Hello powinien utworzyć **ps.cmd** pliku w hello **. / bin** folderu.</span><span class="sxs-lookup"><span data-stu-id="d602e-163">hello Visual Studio templates should have created a **ps.cmd** file in hello **./bin** folder.</span></span> <span data-ttu-id="d602e-164">Ten skrypt powłoki uwidacznia hello PowerShell skrypty otoki powyżej i umożliwia rejestrowanie na podstawie nazwy hello hello otoki środowiska PowerShell o nazwie.</span><span class="sxs-lookup"><span data-stu-id="d602e-164">This shell script calls out hello PowerShell wrapper scripts above and provides logging based on hello name of hello PowerShell wrapper called.</span></span> <span data-ttu-id="d602e-165">Jeśli ten plik nie został utworzony, jego zawartość powinna wyglądać następująco.</span><span class="sxs-lookup"><span data-stu-id="d602e-165">If this file wasn't created, here is what should be in it.</span></span> 

```bat
@echo off

cd /D %~dp0

if not exist "%DiagnosticStore%\LogFiles" mkdir "%DiagnosticStore%\LogFiles"
%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe -ExecutionPolicy Unrestricted -File %* >> "%DiagnosticStore%\LogFiles\%~n1.txt" 2>> "%DiagnosticStore%\LogFiles\%~n1.err.txt"
```



## <a name="run-locally"></a><span data-ttu-id="d602e-166">Uruchamianie lokalnie</span><span class="sxs-lookup"><span data-stu-id="d602e-166">Run locally</span></span>
<span data-ttu-id="d602e-167">Jeśli ustawisz projekt usługi w chmurze jako projekt startowy hello i naciśnij klawisz F5, usługa w chmurze hello jest uruchamiany w lokalnym emulatorze platformy Azure hello.</span><span class="sxs-lookup"><span data-stu-id="d602e-167">If you set your cloud service project as hello startup project and press F5, hello cloud service runs in hello local Azure emulator.</span></span>

<span data-ttu-id="d602e-168">Mimo że PTVS obsługuje uruchamianie w emulatorze hello, debugowania (na przykład punktów przerwania) nie działa.</span><span class="sxs-lookup"><span data-stu-id="d602e-168">Although PTVS supports launching in hello emulator, debugging (for example, breakpoints) does not work.</span></span>

<span data-ttu-id="d602e-169">toodebug poszczególnych ról sieci web i proces roboczy, można ustawić hello projekt roli jako projekt startowy hello i to zamiast debugowania.</span><span class="sxs-lookup"><span data-stu-id="d602e-169">toodebug your web and worker roles, you can set hello role project as hello startup project and debug that instead.</span></span>  <span data-ttu-id="d602e-170">Można również ustawić wiele projektów startowych.</span><span class="sxs-lookup"><span data-stu-id="d602e-170">You can also set multiple startup projects.</span></span>  <span data-ttu-id="d602e-171">Kliknij prawym przyciskiem myszy rozwiązanie hello, a następnie wybierz **Ustaw projekty startowe**.</span><span class="sxs-lookup"><span data-stu-id="d602e-171">Right-click hello solution and then select **Set StartUp Projects**.</span></span>

![Właściwości projektu startowego rozwiązania](./media/cloud-services-python-ptvs/startup.png)

## <a name="publish-tooazure"></a><span data-ttu-id="d602e-173">Publikowanie tooAzure</span><span class="sxs-lookup"><span data-stu-id="d602e-173">Publish tooAzure</span></span>
<span data-ttu-id="d602e-174">toopublish, kliknij prawym przyciskiem myszy projekt usługi w chmurze hello w rozwiązaniu hello, a następnie wybierz **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="d602e-174">toopublish, right-click hello cloud service project in hello solution and then select **Publish**.</span></span>

![Logowanie na potrzeby publikowania na platformie Microsoft Azure](./media/cloud-services-python-ptvs/publish-sign-in.png)

<span data-ttu-id="d602e-176">Postępuj zgodnie z hello kreatora.</span><span class="sxs-lookup"><span data-stu-id="d602e-176">Follow hello wizard.</span></span> <span data-ttu-id="d602e-177">Jeśli trzeba, włącz pulpit zdalny.</span><span class="sxs-lookup"><span data-stu-id="d602e-177">If you need to, enable remote desktop.</span></span> <span data-ttu-id="d602e-178">Pulpit zdalny jest przydatne, gdy będziesz potrzebować toodebug coś.</span><span class="sxs-lookup"><span data-stu-id="d602e-178">Remote desktop is helpful when you need toodebug something.</span></span>

<span data-ttu-id="d602e-179">Po zakończeniu konfigurowania ustawień kliknij pozycję **Publikuj**.</span><span class="sxs-lookup"><span data-stu-id="d602e-179">When you are done configuring settings, click **Publish**.</span></span>

<span data-ttu-id="d602e-180">Niektóre postęp jest wyświetlany w oknie danych wyjściowych hello, a następnie pojawi się okno Dziennik aktywności platformy Azure Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="d602e-180">Some progress appears in hello output window, then you'll see hello Microsoft Azure Activity Log window.</span></span>

![Okno Dziennik aktywności platformy Microsoft Azure](./media/cloud-services-python-ptvs/publish-activity-log.png)

<span data-ttu-id="d602e-182">Wdrożenie ma toocomplete kilka minut, następnie sieci web i/lub uruchamiania roli proces roboczy na platformie Azure!</span><span class="sxs-lookup"><span data-stu-id="d602e-182">Deployment takes several minutes toocomplete, then your web and/or worker roles run on Azure!</span></span>

### <a name="investigate-logs"></a><span data-ttu-id="d602e-183">Sprawdzanie dzienników</span><span class="sxs-lookup"><span data-stu-id="d602e-183">Investigate logs</span></span>
<span data-ttu-id="d602e-184">Po maszyny wirtualnej usługi chmury hello jest uruchamiany i instaluje Python, można przyjrzeć się toofind dzienniki hello jakiekolwiek komunikaty o błędach.</span><span class="sxs-lookup"><span data-stu-id="d602e-184">After hello cloud service virtual machine starts up and installs Python, you can look at hello logs toofind any failure messages.</span></span> <span data-ttu-id="d602e-185">Te dzienniki znajdują się w hello **C:\Resources\Directory\\\LogFiles {roli}** folderu.</span><span class="sxs-lookup"><span data-stu-id="d602e-185">These logs are located in hello **C:\Resources\Directory\\{role}\LogFiles** folder.</span></span> <span data-ttu-id="d602e-186">**PrepPython.err.txt** ma co najmniej jeden błąd w nim z po hello skrypt próbuje toodetect, jeśli jest zainstalowana Python i **PipInstaller.err.txt** może skarżą się o nieaktualną wersją pip.</span><span class="sxs-lookup"><span data-stu-id="d602e-186">**PrepPython.err.txt** has at least one error in it from when hello script tries toodetect if Python is installed and **PipInstaller.err.txt** may complain about an outdated version of pip.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d602e-187">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d602e-187">Next steps</span></span>
<span data-ttu-id="d602e-188">Aby uzyskać szczegółowe informacje na temat pracy z role sieć web i proces roboczy w narzędzia Python Tools for Visual Studio zobacz dokumentację PTVS hello:</span><span class="sxs-lookup"><span data-stu-id="d602e-188">For more detailed information about working with web and worker roles in Python Tools for Visual Studio, see hello PTVS documentation:</span></span>

* <span data-ttu-id="d602e-189">[Projekty usługi w chmurze][Cloud Service Projects]</span><span class="sxs-lookup"><span data-stu-id="d602e-189">[Cloud Service Projects][Cloud Service Projects]</span></span>

<span data-ttu-id="d602e-190">Aby uzyskać więcej informacji o korzystaniu z sieci web i proces roboczy role, takie jak przy użyciu usługi Azure Storage lub Service Bus usług Azure, zobacz następujące artykuły hello:</span><span class="sxs-lookup"><span data-stu-id="d602e-190">For more details about using Azure services from your web and worker roles, such as using Azure Storage or Service Bus, see hello following articles:</span></span>

* <span data-ttu-id="d602e-191">[Blob Service][Blob Service]</span><span class="sxs-lookup"><span data-stu-id="d602e-191">[Blob Service][Blob Service]</span></span>
* <span data-ttu-id="d602e-192">[Table Service][Table Service]</span><span class="sxs-lookup"><span data-stu-id="d602e-192">[Table Service][Table Service]</span></span>
* <span data-ttu-id="d602e-193">[Queue Service][Queue Service]</span><span class="sxs-lookup"><span data-stu-id="d602e-193">[Queue Service][Queue Service]</span></span>
* <span data-ttu-id="d602e-194">[Kolejki usługi Service Bus][Service Bus Queues]</span><span class="sxs-lookup"><span data-stu-id="d602e-194">[Service Bus Queues][Service Bus Queues]</span></span>
* <span data-ttu-id="d602e-195">[Tematy usługi Service Bus][Service Bus Topics]</span><span class="sxs-lookup"><span data-stu-id="d602e-195">[Service Bus Topics][Service Bus Topics]</span></span>

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
