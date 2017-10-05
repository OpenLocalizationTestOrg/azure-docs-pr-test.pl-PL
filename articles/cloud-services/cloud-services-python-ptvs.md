---
title: "Wprowadzenie do języka Python i usług Azure Cloud Services | Microsoft Docs"
description: "Omówienie sposobu używania programu Python Tools for Visual Studio do tworzenia usług w chmurze platformy Azure, w tym ról Sieć Web i Proces roboczy."
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
ms.openlocfilehash: 7d2bc89943087323e92cf06981bbacaf4b8ff060
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="python-web-and-worker-roles-with-python-tools-for-visual-studio"></a><span data-ttu-id="56d67-103">Role Sieć Web i Proces roboczy języka Python z programem Python Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="56d67-103">Python web and worker roles with Python Tools for Visual Studio</span></span>

<span data-ttu-id="56d67-104">Ten artykuł zawiera omówienie sposobu użycia ról Sieć Web i Proces roboczy języka Python za pomocą narzędzi [Python Tools for Visual Studio][Python Tools for Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="56d67-104">This article provides an overview of using Python web and worker roles using [Python Tools for Visual Studio][Python Tools for Visual Studio].</span></span> <span data-ttu-id="56d67-105">Dowiedz się, jak używać programu Visual Studio do tworzenia i wdrażania podstawowej usługi w chmurze, która używa języka Python.</span><span class="sxs-lookup"><span data-stu-id="56d67-105">Learn how to use Visual Studio to create and deploy a basic Cloud Service that uses Python.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="56d67-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="56d67-106">Prerequisites</span></span>
* [<span data-ttu-id="56d67-107">Program Visual Studio w wersji 2013, 2015 lub 2017</span><span class="sxs-lookup"><span data-stu-id="56d67-107">Visual Studio 2013, 2015, or 2017</span></span>](https://www.visualstudio.com/)
* <span data-ttu-id="56d67-108">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS)</span><span class="sxs-lookup"><span data-stu-id="56d67-108">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS)</span></span>
* <span data-ttu-id="56d67-109">[Azure SDK Tools for VS 2013][Azure SDK Tools for VS 2013] lub</span><span class="sxs-lookup"><span data-stu-id="56d67-109">[Azure SDK Tools for VS 2013][Azure SDK Tools for VS 2013] or</span></span>  
<span data-ttu-id="56d67-110">[Azure SDK Tools for VS 2015][Azure SDK Tools for VS 2015] lub</span><span class="sxs-lookup"><span data-stu-id="56d67-110">[Azure SDK Tools for VS 2015][Azure SDK Tools for VS 2015] or</span></span>  
<span data-ttu-id="56d67-111">[Azure SDK Tools for VS 2017][Azure SDK Tools for VS 2017]</span><span class="sxs-lookup"><span data-stu-id="56d67-111">[Azure SDK Tools for VS 2017][Azure SDK Tools for VS 2017]</span></span>
* <span data-ttu-id="56d67-112">[32-bitowe środowisko Python w wersji 2.7][Python 2.7 32-bit] lub [32-bitowe środowisko Python w wersji 3.5][Python 3.5 32-bit]</span><span class="sxs-lookup"><span data-stu-id="56d67-112">[Python 2.7 32-bit][Python 2.7 32-bit] or [Python 3.5 32-bit][Python 3.5 32-bit]</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="what-are-python-web-and-worker-roles"></a><span data-ttu-id="56d67-113">Co to są role Sieć Web i Proces roboczy języka Python?</span><span class="sxs-lookup"><span data-stu-id="56d67-113">What are Python web and worker roles?</span></span>
<span data-ttu-id="56d67-114">Platforma Azure udostępnia trzy modele obliczeniowe na potrzeby uruchamiania aplikacji: [funkcja Web Apps w usłudze Azure App Service][execution model-web sites], [Azure Virtual Machines][execution model-vms] i [Azure Cloud Services][execution model-cloud services].</span><span class="sxs-lookup"><span data-stu-id="56d67-114">Azure provides three compute models for running applications: [Web Apps feature in Azure App Service][execution model-web sites], [Azure Virtual Machines][execution model-vms], and [Azure Cloud Services][execution model-cloud services].</span></span> <span data-ttu-id="56d67-115">Wszystkie trzy modele obsługują język Python.</span><span class="sxs-lookup"><span data-stu-id="56d67-115">All three models support Python.</span></span> <span data-ttu-id="56d67-116">Usługi Cloud Services, które obejmują role Sieć Web i Proces roboczy, udostępniają rozwiązanie typu *Platforma jako usługa (Platform as a Service, PaaS)*.</span><span class="sxs-lookup"><span data-stu-id="56d67-116">Cloud Services, which include web and worker roles, provide *Platform as a Service (PaaS)*.</span></span> <span data-ttu-id="56d67-117">W ramach usługi w chmurze rola internetowa zapewnia dedykowany serwer internetowy usług Internet Information Services (IIS), natomiast rola procesu roboczego może uruchamiać asynchroniczne, długotrwałe lub ciągłe zadania niezależne od działań użytkownika lub danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="56d67-117">Within a cloud service, a web role provides a dedicated Internet Information Services (IIS) web server to host front end web applications, while a worker role can run asynchronous, long-running, or perpetual tasks independent of user interaction or input.</span></span>

<span data-ttu-id="56d67-118">Aby uzyskać więcej informacji, zobacz [Co to jest usługa w chmurze?]</span><span class="sxs-lookup"><span data-stu-id="56d67-118">For more information, see [What is a Cloud Service?].</span></span>

> [!NOTE]
> <span data-ttu-id="56d67-119">*Chcesz utworzyć prostą witrynę sieci Web?*</span><span class="sxs-lookup"><span data-stu-id="56d67-119">*Looking to build a simple website?*</span></span>
> <span data-ttu-id="56d67-120">Jeśli scenariusz obejmuje tylko prosty fronton witryny internetowej, rozważ użycie lekkiej funkcji Web Apps w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="56d67-120">If your scenario involves just a simple website front end, consider using the lightweight Web Apps feature in Azure App Service.</span></span> <span data-ttu-id="56d67-121">Możesz łatwo przeprowadzić uaktualnienie do usługi w chmurze w przypadku rozwoju witryny sieci Web lub zmiany wymagań.</span><span class="sxs-lookup"><span data-stu-id="56d67-121">You can easily upgrade to a Cloud Service as your website grows and your requirements change.</span></span> <span data-ttu-id="56d67-122">W <a href="/develop/python/">Centrum deweloperów języka Python</a> można znaleźć artykuły, które dotyczą funkcji Web Apps w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="56d67-122">See the <a href="/develop/python/">Python Developer Center</a> for articles that cover development of the Web Apps feature in Azure App Service.</span></span>
> <br />
> 
> 

## <a name="project-creation"></a><span data-ttu-id="56d67-123">Tworzenie projektu</span><span class="sxs-lookup"><span data-stu-id="56d67-123">Project creation</span></span>
<span data-ttu-id="56d67-124">W programie Visual Studio możesz wybrać pozycję **Usługa w chmurze platformy Azure** w oknie dialogowym **Nowy projekt** w obszarze **Python**.</span><span class="sxs-lookup"><span data-stu-id="56d67-124">In Visual Studio, you can select **Azure Cloud Service** in the **New Project** dialog box, under **Python**.</span></span>

![Okno dialogowe Nowy projekt](./media/cloud-services-python-ptvs/new-project-cloud-service.png)

<span data-ttu-id="56d67-126">W Kreatorze usługi w chmurze platformy Azure można utworzyć nowe role Sieć Web i Proces roboczy.</span><span class="sxs-lookup"><span data-stu-id="56d67-126">In the Azure Cloud Service wizard, you can create new web and worker roles.</span></span>

![Okno dialogowe Usługa w chmurze platformy Azure](./media/cloud-services-python-ptvs/new-service-wizard.png)

<span data-ttu-id="56d67-128">Szablon roli procesu roboczego zawiera schematyczny kod służący do nawiązywania połączeń z kontem magazynu Azure lub z usługą Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="56d67-128">The worker role template comes with boilerplate code to connect to an Azure storage account or Azure Service Bus.</span></span>

![Rozwiązanie usługi w chmurze](./media/cloud-services-python-ptvs/worker.png)

<span data-ttu-id="56d67-130">W każdej chwili możliwe jest dodanie roli Sieć Web lub Proces roboczy do istniejącej usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="56d67-130">You can add web or worker roles to an existing cloud service at any time.</span></span>  <span data-ttu-id="56d67-131">Możesz dodawać istniejące projekty do rozwiązania lub tworzyć nowe.</span><span class="sxs-lookup"><span data-stu-id="56d67-131">You can choose to add existing projects in your solution, or create new ones.</span></span>

![Polecenie Dodaj rolę](./media/cloud-services-python-ptvs/add-new-or-existing-role.png)

<span data-ttu-id="56d67-133">Usługa w chmurze może zawierać role zaimplementowane w różnych językach.</span><span class="sxs-lookup"><span data-stu-id="56d67-133">Your cloud service can contain roles implemented in different languages.</span></span>  <span data-ttu-id="56d67-134">Na przykład można mieć rolę Sieć Web języka Python zaimplementowaną za pomocą środowiska Django, języka Python lub roli Proces roboczy języka C#.</span><span class="sxs-lookup"><span data-stu-id="56d67-134">For example, you can have a Python web role implemented using Django, with Python, or with C# worker roles.</span></span>  <span data-ttu-id="56d67-135">Między rolami można się w łatwy sposób komunikować za pomocą kolejek usługi Service Bus lub kolejek magazynu.</span><span class="sxs-lookup"><span data-stu-id="56d67-135">You can easily communicate between your roles using Service Bus queues or storage queues.</span></span>

## <a name="install-python-on-the-cloud-service"></a><span data-ttu-id="56d67-136">Instalowanie języka Python w usłudze w chmurze</span><span class="sxs-lookup"><span data-stu-id="56d67-136">Install Python on the cloud service</span></span>
> [!WARNING]
> <span data-ttu-id="56d67-137">Skrypty instalacji instalowane z programem Visual Studio (w momencie ostatniej aktualizacji artykułu) nie działają.</span><span class="sxs-lookup"><span data-stu-id="56d67-137">The setup scripts that are installed with Visual Studio (at the time this article was last updated) do not work.</span></span> <span data-ttu-id="56d67-138">W tej sekcji opisano sposób obejścia problemu.</span><span class="sxs-lookup"><span data-stu-id="56d67-138">This section describes a workaround.</span></span>
> 
> 

<span data-ttu-id="56d67-139">Główny problem ze skryptami instalacji polega na tym, że nie instalują one środowiska Python.</span><span class="sxs-lookup"><span data-stu-id="56d67-139">The main problem with the setup scripts is that they do not install python.</span></span> <span data-ttu-id="56d67-140">Najpierw należy zdefiniować dwa [zadania uruchamiania](cloud-services-startup-tasks.md) w pliku [ServiceDefinition.csdef](cloud-services-model-and-package.md#servicedefinitioncsdef).</span><span class="sxs-lookup"><span data-stu-id="56d67-140">First, define two [startup tasks](cloud-services-startup-tasks.md) in the [ServiceDefinition.csdef](cloud-services-model-and-package.md#servicedefinitioncsdef) file.</span></span> <span data-ttu-id="56d67-141">Pierwsze zadanie (**PrepPython.ps1**) pobiera i instaluje środowiska uruchomieniowe języka Python.</span><span class="sxs-lookup"><span data-stu-id="56d67-141">The first task (**PrepPython.ps1**) downloads and installs the Python runtime.</span></span> <span data-ttu-id="56d67-142">Drugie zadanie (**PipInstaller.ps1**) uruchamia mechanizm pip, aby zainstalować wszystkie zależności.</span><span class="sxs-lookup"><span data-stu-id="56d67-142">The second task (**PipInstaller.ps1**) runs pip to install any dependencies you may have.</span></span>

<span data-ttu-id="56d67-143">Poniższe skrypty zostały napisane dla języka Python 3.5.</span><span class="sxs-lookup"><span data-stu-id="56d67-143">The following scripts were written targeting Python 3.5.</span></span> <span data-ttu-id="56d67-144">Jeśli chcesz korzystać z wersji 2.x języka Python, ustaw plik zmiennej **PYTHON2** na **on** dla dwóch zadań uruchamiania i zadania środowiska uruchomieniowego: `<Variable name="PYTHON2" value="<mark>on</mark>" />`.</span><span class="sxs-lookup"><span data-stu-id="56d67-144">If you want to use the version 2.x of python, set the **PYTHON2** variable file to **on** for the two startup tasks and the runtime task: `<Variable name="PYTHON2" value="<mark>on</mark>" />`.</span></span>

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

<span data-ttu-id="56d67-145">Zmienne **PYTHON2** i **PYPATH** muszą zostać dodane do zadania uruchamiania procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="56d67-145">The **PYTHON2** and **PYPATH** variables must be added to the worker startup task.</span></span> <span data-ttu-id="56d67-146">Zmienna **PYPATH** jest używana tylko wtedy, gdy zmienna **PYTHON2** jest ustawiona na wartość **on**.</span><span class="sxs-lookup"><span data-stu-id="56d67-146">The **PYPATH** variable is only used if the **PYTHON2** variable is set to **on**.</span></span>

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

#### <a name="sample-servicedefinitioncsdef"></a><span data-ttu-id="56d67-147">Przykładowy plik ServiceDefinition.csdef</span><span class="sxs-lookup"><span data-stu-id="56d67-147">Sample ServiceDefinition.csdef</span></span>
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



<span data-ttu-id="56d67-148">Następnie należy utworzyć pliki **PrepPython.ps1** i **PipInstaller.ps1** w folderze **./bin** roli użytkownika.</span><span class="sxs-lookup"><span data-stu-id="56d67-148">Next, create the **PrepPython.ps1** and **PipInstaller.ps1** files in the **./bin** folder of your role.</span></span>

#### <a name="preppythonps1"></a><span data-ttu-id="56d67-149">PrepPython.ps1</span><span class="sxs-lookup"><span data-stu-id="56d67-149">PrepPython.ps1</span></span>
<span data-ttu-id="56d67-150">Ten skrypt instaluje język Python.</span><span class="sxs-lookup"><span data-stu-id="56d67-150">This script installs python.</span></span> <span data-ttu-id="56d67-151">Jeśli zmienna środowiskowa **PYTHON2** jest ustawiona na wartość **on**, jest zainstalowane środowisko Python 2.7. W przeciwnym razie jest zainstalowane środowisko Python 3.5.</span><span class="sxs-lookup"><span data-stu-id="56d67-151">If the **PYTHON2** environment variable is set to **on**, then Python 2.7 is installed, otherwise Python 3.5 is installed.</span></span>

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

        Write-Output "Not found, downloading $url to $outFile$nl"
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

#### <a name="pipinstallerps1"></a><span data-ttu-id="56d67-152">PipInstaller.ps1</span><span class="sxs-lookup"><span data-stu-id="56d67-152">PipInstaller.ps1</span></span>
<span data-ttu-id="56d67-153">Ten skrypt wywołuje kod pip i instaluje wszystkie zależności w pliku **requirements.txt**.</span><span class="sxs-lookup"><span data-stu-id="56d67-153">This script calls up pip and installs all of the dependencies in the **requirements.txt** file.</span></span> <span data-ttu-id="56d67-154">Jeśli zmienna środowiskowa **PYTHON2** jest ustawiona na wartość **on**, jest używane środowisko Python 2.7. W przeciwnym razie jest używane środowisko Python 3.5.</span><span class="sxs-lookup"><span data-stu-id="56d67-154">If the **PYTHON2** environment variable is set to **on**, then Python 2.7 is used, otherwise Python 3.5 is used.</span></span>

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

#### <a name="modify-launchworkerps1"></a><span data-ttu-id="56d67-155">Modyfikowanie skryptu LaunchWorker.ps1</span><span class="sxs-lookup"><span data-stu-id="56d67-155">Modify LaunchWorker.ps1</span></span>
> [!NOTE]
> <span data-ttu-id="56d67-156">W przypadku projektu **roli procesu roboczego** plik **LauncherWorker.ps1** jest wymagany do wykonania pliku uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="56d67-156">In the case of a **worker role** project, **LauncherWorker.ps1** file is required to execute the startup file.</span></span> <span data-ttu-id="56d67-157">W projektach **roli sieci Web** plik uruchamiania jest zdefiniowany we właściwościach projektu.</span><span class="sxs-lookup"><span data-stu-id="56d67-157">In a **web role** project, the startup file is instead defined in the project properties.</span></span>
> 
> 

<span data-ttu-id="56d67-158">Skrypt **Bin\LaunchWorker.ps1** pierwotnie został utworzony w celu wykonywania działań przygotowawczych, ale w praktyce nie działa.</span><span class="sxs-lookup"><span data-stu-id="56d67-158">The **bin\LaunchWorker.ps1** was originally created to do a lot of prep work but it doesn't really work.</span></span> <span data-ttu-id="56d67-159">Zastąp zawartość tego pliku następującym skryptem.</span><span class="sxs-lookup"><span data-stu-id="56d67-159">Replace the contents in that file with the following script.</span></span>

<span data-ttu-id="56d67-160">Ten skrypt wywołuje plik **worker.py** z projektu języka Python.</span><span class="sxs-lookup"><span data-stu-id="56d67-160">This script calls the **worker.py** file from your python project.</span></span> <span data-ttu-id="56d67-161">Jeśli zmienna środowiskowa **PYTHON2** jest ustawiona na wartość **on**, jest używane środowisko Python 2.7. W przeciwnym razie jest używane środowisko Python 3.5.</span><span class="sxs-lookup"><span data-stu-id="56d67-161">If the **PYTHON2** environment variable is set to **on**, then Python 2.7 is used, otherwise Python 3.5 is used.</span></span>

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

    # Customize to your local dev environment

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

#### <a name="pscmd"></a><span data-ttu-id="56d67-162">ps.cmd</span><span class="sxs-lookup"><span data-stu-id="56d67-162">ps.cmd</span></span>
<span data-ttu-id="56d67-163">Szablony Visual Studio powinny utworzyć plik **ps.cmd** w folderze **./bin**.</span><span class="sxs-lookup"><span data-stu-id="56d67-163">The Visual Studio templates should have created a **ps.cmd** file in the **./bin** folder.</span></span> <span data-ttu-id="56d67-164">Ten skrypt powłoki wywołuje powyższe skrypty otoki PowerShell i zapewnia rejestrowanie na podstawie nazwy wywołanej otoki PowerShell.</span><span class="sxs-lookup"><span data-stu-id="56d67-164">This shell script calls out the PowerShell wrapper scripts above and provides logging based on the name of the PowerShell wrapper called.</span></span> <span data-ttu-id="56d67-165">Jeśli ten plik nie został utworzony, jego zawartość powinna wyglądać następująco.</span><span class="sxs-lookup"><span data-stu-id="56d67-165">If this file wasn't created, here is what should be in it.</span></span> 

```bat
@echo off

cd /D %~dp0

if not exist "%DiagnosticStore%\LogFiles" mkdir "%DiagnosticStore%\LogFiles"
%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe -ExecutionPolicy Unrestricted -File %* >> "%DiagnosticStore%\LogFiles\%~n1.txt" 2>> "%DiagnosticStore%\LogFiles\%~n1.err.txt"
```



## <a name="run-locally"></a><span data-ttu-id="56d67-166">Uruchamianie lokalnie</span><span class="sxs-lookup"><span data-stu-id="56d67-166">Run locally</span></span>
<span data-ttu-id="56d67-167">Jeśli ustawisz projekt usługi w chmurze jako projekt startowy i naciśniesz klawisz F5, usługa w chmurze zostanie uruchomiona w lokalnym emulatorze platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="56d67-167">If you set your cloud service project as the startup project and press F5, the cloud service runs in the local Azure emulator.</span></span>

<span data-ttu-id="56d67-168">Mimo że program PTVS obsługuje uruchamianie w emulatorze, debugowanie nie działa (dotyczy to na przykład punktów przerwania).</span><span class="sxs-lookup"><span data-stu-id="56d67-168">Although PTVS supports launching in the emulator, debugging (for example, breakpoints) does not work.</span></span>

<span data-ttu-id="56d67-169">Aby debugować role Sieć Web i Proces roboczy, możesz ustawić projekt roli jako projekt startowy i debugować go zamiast ról.</span><span class="sxs-lookup"><span data-stu-id="56d67-169">To debug your web and worker roles, you can set the role project as the startup project and debug that instead.</span></span>  <span data-ttu-id="56d67-170">Można również ustawić wiele projektów startowych.</span><span class="sxs-lookup"><span data-stu-id="56d67-170">You can also set multiple startup projects.</span></span>  <span data-ttu-id="56d67-171">Kliknij prawym przyciskiem myszy rozwiązanie, a następnie wybierz pozycję **Ustaw projekty startowe**.</span><span class="sxs-lookup"><span data-stu-id="56d67-171">Right-click the solution and then select **Set StartUp Projects**.</span></span>

![Właściwości projektu startowego rozwiązania](./media/cloud-services-python-ptvs/startup.png)

## <a name="publish-to-azure"></a><span data-ttu-id="56d67-173">Publikowanie na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="56d67-173">Publish to Azure</span></span>
<span data-ttu-id="56d67-174">Aby przeprowadzić publikowanie, kliknij prawym przyciskiem myszy projekt usługi w chmurze w rozwiązaniu, a następnie wybierz pozycję **Publikuj**.</span><span class="sxs-lookup"><span data-stu-id="56d67-174">To publish, right-click the cloud service project in the solution and then select **Publish**.</span></span>

![Logowanie na potrzeby publikowania na platformie Microsoft Azure](./media/cloud-services-python-ptvs/publish-sign-in.png)

<span data-ttu-id="56d67-176">Postępuj zgodnie z poleceniami kreatora.</span><span class="sxs-lookup"><span data-stu-id="56d67-176">Follow the wizard.</span></span> <span data-ttu-id="56d67-177">Jeśli trzeba, włącz pulpit zdalny.</span><span class="sxs-lookup"><span data-stu-id="56d67-177">If you need to, enable remote desktop.</span></span> <span data-ttu-id="56d67-178">Pulpit zdalny jest przydatny w przypadku konieczności debugowania elementów.</span><span class="sxs-lookup"><span data-stu-id="56d67-178">Remote desktop is helpful when you need to debug something.</span></span>

<span data-ttu-id="56d67-179">Po zakończeniu konfigurowania ustawień kliknij pozycję **Publikuj**.</span><span class="sxs-lookup"><span data-stu-id="56d67-179">When you are done configuring settings, click **Publish**.</span></span>

<span data-ttu-id="56d67-180">W oknie danych wyjściowych jest wyświetlany postęp, a następnie zostanie wyświetlone okno Dziennik aktywności platformy Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="56d67-180">Some progress appears in the output window, then you'll see the Microsoft Azure Activity Log window.</span></span>

![Okno Dziennik aktywności platformy Microsoft Azure](./media/cloud-services-python-ptvs/publish-activity-log.png)

<span data-ttu-id="56d67-182">Wdrożenie potrwa kilka minut, a następnie rola internetowa i/lub procesu roboczego będą działać na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="56d67-182">Deployment takes several minutes to complete, then your web and/or worker roles run on Azure!</span></span>

### <a name="investigate-logs"></a><span data-ttu-id="56d67-183">Sprawdzanie dzienników</span><span class="sxs-lookup"><span data-stu-id="56d67-183">Investigate logs</span></span>
<span data-ttu-id="56d67-184">Po uruchomieniu maszyny wirtualnej usługi w chmurze i zainstalowaniu języka Python można sprawdzić dzienniki pod kątem komunikatów o błędach.</span><span class="sxs-lookup"><span data-stu-id="56d67-184">After the cloud service virtual machine starts up and installs Python, you can look at the logs to find any failure messages.</span></span> <span data-ttu-id="56d67-185">Te dzienniki znajdują się w folderze **C:\Resources\Directory\\{rola}\LogFiles**.</span><span class="sxs-lookup"><span data-stu-id="56d67-185">These logs are located in the **C:\Resources\Directory\\{role}\LogFiles** folder.</span></span> <span data-ttu-id="56d67-186">Plik **PrepPython.err.txt** zawiera co najmniej jeden błąd zwracany, gdy skrypt próbuje wykryć instalację środowiska Python, a plik **PipInstaller.err.txt** może zgłaszać błąd nieaktualnej wersji kodu pip.</span><span class="sxs-lookup"><span data-stu-id="56d67-186">**PrepPython.err.txt** has at least one error in it from when the script tries to detect if Python is installed and **PipInstaller.err.txt** may complain about an outdated version of pip.</span></span>

## <a name="next-steps"></a><span data-ttu-id="56d67-187">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="56d67-187">Next steps</span></span>
<span data-ttu-id="56d67-188">Bardziej szczegółowe informacje na temat pracy z rolami Sieć Web i Proces roboczy w ramach programu Python Tools for Visual Studio zawiera dokumentacja programu PTVS:</span><span class="sxs-lookup"><span data-stu-id="56d67-188">For more detailed information about working with web and worker roles in Python Tools for Visual Studio, see the PTVS documentation:</span></span>

* <span data-ttu-id="56d67-189">[Projekty usługi w chmurze][Cloud Service Projects]</span><span class="sxs-lookup"><span data-stu-id="56d67-189">[Cloud Service Projects][Cloud Service Projects]</span></span>

<span data-ttu-id="56d67-190">Więcej szczegółów dotyczących korzystania z usług Azure na podstawie roli internetowej i roli procesu roboczego, na przykład używania usługi Azure Storage lub Service Bus, można znaleźć w następujących artykułach:</span><span class="sxs-lookup"><span data-stu-id="56d67-190">For more details about using Azure services from your web and worker roles, such as using Azure Storage or Service Bus, see the following articles:</span></span>

* <span data-ttu-id="56d67-191">[Blob Service][Blob Service]</span><span class="sxs-lookup"><span data-stu-id="56d67-191">[Blob Service][Blob Service]</span></span>
* <span data-ttu-id="56d67-192">[Table Service][Table Service]</span><span class="sxs-lookup"><span data-stu-id="56d67-192">[Table Service][Table Service]</span></span>
* <span data-ttu-id="56d67-193">[Queue Service][Queue Service]</span><span class="sxs-lookup"><span data-stu-id="56d67-193">[Queue Service][Queue Service]</span></span>
* <span data-ttu-id="56d67-194">[Kolejki usługi Service Bus][Service Bus Queues]</span><span class="sxs-lookup"><span data-stu-id="56d67-194">[Service Bus Queues][Service Bus Queues]</span></span>
* <span data-ttu-id="56d67-195">[Tematy usługi Service Bus][Service Bus Topics]</span><span class="sxs-lookup"><span data-stu-id="56d67-195">[Service Bus Topics][Service Bus Topics]</span></span>

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
