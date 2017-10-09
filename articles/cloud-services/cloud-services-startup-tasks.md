---
title: "Uruchamianie zadań w usług Azure Cloud Services aaaRun | Dokumentacja firmy Microsoft"
description: "Zadania uruchamiania pomóc w przygotowaniu środowiska usługi chmury dla aplikacji. To jest przedstawienie sposobu uruchamiania zadań pracy i w jaki sposób toomake ich"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 886939be-4b5b-49cc-9a6e-2172e3c133e9
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: 3391a5d7434164f59972b8e497e5c34e33409543
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-and-run-startup-tasks-for-a-cloud-service"></a><span data-ttu-id="62910-104">Sposób uruchamiania tooconfigure i uruchom zadania dla usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="62910-104">How tooconfigure and run startup tasks for a cloud service</span></span>
<span data-ttu-id="62910-105">Przed rozpoczęciem rolę, można użyć operacji tooperform zadania uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="62910-105">You can use startup tasks tooperform operations before a role starts.</span></span> <span data-ttu-id="62910-106">Operacje można tooperform obejmują instalowania składnika, rejestrowanie składników modelu COM, ustawienie kluczy rejestru lub uruchamia proces wymagającą dużo czasu.</span><span class="sxs-lookup"><span data-stu-id="62910-106">Operations that you might want tooperform include installing a component, registering COM components, setting registry keys, or starting a long running process.</span></span>

> [!NOTE]
> <span data-ttu-id="62910-107">Zadania uruchamiania nie są stosowane tooVirtual maszyny, tylko tooCloud usługi sieci Web i proces roboczy.</span><span class="sxs-lookup"><span data-stu-id="62910-107">Startup tasks are not applicable tooVirtual Machines, only tooCloud Service Web and Worker roles.</span></span>
> 
> 

## <a name="how-startup-tasks-work"></a><span data-ttu-id="62910-108">Sposób działania uruchamiania zadań</span><span class="sxs-lookup"><span data-stu-id="62910-108">How startup tasks work</span></span>
<span data-ttu-id="62910-109">Uruchamianie zadania są działaniach wykonywanych przed rozpocząć role są definiowane w hello [ServiceDefinition.csdef] pliku przy użyciu hello [zadań] elementu w obrębie hello [uruchamiania]elementu.</span><span class="sxs-lookup"><span data-stu-id="62910-109">Startup tasks are actions that are taken before your roles begin and are defined in hello [ServiceDefinition.csdef] file by using hello [Task] element within hello [Startup] element.</span></span> <span data-ttu-id="62910-110">Często uruchomienia zadania są pliki wsadowe, ale można je również aplikacji konsoli lub pliki wsadowe, które uruchomić skrypty programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="62910-110">Frequently startup tasks are batch files, but they can also be console applications, or batch files that start PowerShell scripts.</span></span>

<span data-ttu-id="62910-111">Zmienne środowiskowe przekazywania informacji do uruchomienia zadania, a Magazyn lokalny może być używane toopass informacji poza zadanie uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="62910-111">Environment variables pass information into a startup task, and local storage can be used toopass information out of a startup task.</span></span> <span data-ttu-id="62910-112">Na przykład, wartość zmiennej środowiskowej można określić hello ścieżki tooa program ma tooinstall i toolocal magazynu, który można następnie zostać odczytany później przez role można zapisywać pliki.</span><span class="sxs-lookup"><span data-stu-id="62910-112">For example, an environment variable can specify hello path tooa program you want tooinstall, and files can be written toolocal storage that can then be read later by your roles.</span></span>

<span data-ttu-id="62910-113">Zadania uruchamiania można rejestrować informacje i błędy toohello katalogu określonego przez hello **TEMP** zmiennej środowiskowej.</span><span class="sxs-lookup"><span data-stu-id="62910-113">Your startup task can log information and errors toohello directory specified by hello **TEMP** environment variable.</span></span> <span data-ttu-id="62910-114">W trakcie zadania uruchamiania hello hello **TEMP** zmiennej środowiskowej rozpoznaje toohello *C:\\zasobów\\temp\\[identyfikator guid]. [ rolename]\\RoleTemp* katalogu podczas uruchamiania w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="62910-114">During hello startup task, hello **TEMP** environment variable resolves toohello *C:\\Resources\\temp\\[guid].[rolename]\\RoleTemp* directory when running on hello cloud.</span></span>

<span data-ttu-id="62910-115">Uruchamianie zadania mogą być również wykonywane kilka razy między ponownego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="62910-115">Startup tasks can also be executed several times between reboots.</span></span> <span data-ttu-id="62910-116">Na przykład hello uruchamiania zadanie zostanie uruchomione zawsze, gdy rola hello jest odtwarzana i odtwarza roli nie może zawierać zawsze ponowne uruchomienie komputera.</span><span class="sxs-lookup"><span data-stu-id="62910-116">For example, hello startup task will be run each time hello role recycles, and role recycles may not always include a reboot.</span></span> <span data-ttu-id="62910-117">Uruchamianie zadania mają być zapisywane w sposób umożliwiający ich toorun bez problemów.</span><span class="sxs-lookup"><span data-stu-id="62910-117">Startup tasks should be written in a way that allows them toorun several times without problems.</span></span>

<span data-ttu-id="62910-118">Zadania uruchamiania musi kończyć się **errorlevel** (lub kod zakończenia) o wartości zero dla hello uruchomienia procesu toocomplete.</span><span class="sxs-lookup"><span data-stu-id="62910-118">Startup tasks must end with an **errorlevel** (or exit code) of zero for hello startup process toocomplete.</span></span> <span data-ttu-id="62910-119">Jeśli zadanie uruchamiania kończy się na inną niż zero **errorlevel**, hello roli nie zostaną uruchomione.</span><span class="sxs-lookup"><span data-stu-id="62910-119">If a startup task ends with a non-zero **errorlevel**, hello role will not start.</span></span>

## <a name="role-startup-order"></a><span data-ttu-id="62910-120">Kolejność uruchamiania roli</span><span class="sxs-lookup"><span data-stu-id="62910-120">Role startup order</span></span>
<span data-ttu-id="62910-121">Hello poniżej przedstawiono procedury uruchamiania roli hello na platformie Azure:</span><span class="sxs-lookup"><span data-stu-id="62910-121">hello following lists hello role startup procedure in Azure:</span></span>

1. <span data-ttu-id="62910-122">wystąpienie Hello jest oznaczony jako **uruchamianie** i nie odbiera ruch.</span><span class="sxs-lookup"><span data-stu-id="62910-122">hello instance is marked as **Starting** and does not receive traffic.</span></span>
2. <span data-ttu-id="62910-123">Wszystkie zadania uruchamiania są wykonywane zgodnie z tootheir **taskType** atrybutu.</span><span class="sxs-lookup"><span data-stu-id="62910-123">All startup tasks are executed according tootheir **taskType** attribute.</span></span>
   
   * <span data-ttu-id="62910-124">Witaj **proste** zadania są wykonywane synchronicznie, pojedynczo.</span><span class="sxs-lookup"><span data-stu-id="62910-124">hello **simple** tasks are executed synchronously, one at a time.</span></span>
   * <span data-ttu-id="62910-125">Witaj **tła** i **pierwszego planu** zadania są toohello wprowadzenie asynchronicznie, równoległe uruchomienia zadania.</span><span class="sxs-lookup"><span data-stu-id="62910-125">hello **background** and **foreground** tasks are started asynchronously, parallel toohello startup task.</span></span>  
     
     > [!WARNING]
     > <span data-ttu-id="62910-126">Usługi IIS może nie być pełni skonfigurowany na etapie hello uruchamiania zadań w procesie uruchamiania hello, dlatego dane specyficzne dla roli nie może być dostępne.</span><span class="sxs-lookup"><span data-stu-id="62910-126">IIS may not be fully configured during hello startup task stage in hello startup process, so role-specific data may not be available.</span></span> <span data-ttu-id="62910-127">Uruchamianie zadań, które wymagają dane specyficzne dla roli, należy użyć [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx).</span><span class="sxs-lookup"><span data-stu-id="62910-127">Startup tasks that require role-specific data should use [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx).</span></span>
     > 
     > 
3. <span data-ttu-id="62910-128">Proces hosta roli Hello jest uruchomiona i hello witryny w usługach IIS.</span><span class="sxs-lookup"><span data-stu-id="62910-128">hello role host process is started and hello site is created in IIS.</span></span>
4. <span data-ttu-id="62910-129">Witaj [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) metoda jest wywoływana.</span><span class="sxs-lookup"><span data-stu-id="62910-129">hello [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) method is called.</span></span>
5. <span data-ttu-id="62910-130">wystąpienie Hello jest oznaczony jako **gotowe** i ruch jest kierowany toohello wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="62910-130">hello instance is marked as **Ready** and traffic is routed toohello instance.</span></span>
6. <span data-ttu-id="62910-131">Witaj [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.Run](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) metoda jest wywoływana.</span><span class="sxs-lookup"><span data-stu-id="62910-131">hello [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.Run](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method is called.</span></span>

## <a name="example-of-a-startup-task"></a><span data-ttu-id="62910-132">Przykład zadania uruchamiania</span><span class="sxs-lookup"><span data-stu-id="62910-132">Example of a startup task</span></span>
<span data-ttu-id="62910-133">Uruchamianie zadania są definiowane w hello [ServiceDefinition.csdef] pliku w hello **zadań** elementu.</span><span class="sxs-lookup"><span data-stu-id="62910-133">Startup tasks are defined in hello [ServiceDefinition.csdef] file, in hello **Task** element.</span></span> <span data-ttu-id="62910-134">Witaj **commandLine** atrybut określa nazwę hello oraz parametry partii uruchamiania hello plików lub konsoli polecenie hello **executionContext** atrybut określa poziom uprawnień hello hello uruchamiania zadania i hello **taskType** atrybut określa, jak hello zadania zostaną wykonane.</span><span class="sxs-lookup"><span data-stu-id="62910-134">hello **commandLine** attribute specifies hello name and parameters of hello startup batch file or console command, hello **executionContext** attribute specifies hello privilege level of hello startup task, and hello **taskType** attribute specifies how hello task will be executed.</span></span>

<span data-ttu-id="62910-135">W tym przykładzie wartość zmiennej środowiskowej **MyVersionNumber**, jest tworzony dla hello uruchomienia zadania i ustaw wartość toohello "**1.0.0.0**".</span><span class="sxs-lookup"><span data-stu-id="62910-135">In this example, an environment variable, **MyVersionNumber**, is created for hello startup task and set toohello value "**1.0.0.0**".</span></span>

<span data-ttu-id="62910-136">**ServiceDefinition.csdef**:</span><span class="sxs-lookup"><span data-stu-id="62910-136">**ServiceDefinition.csdef**:</span></span>

```xml
<Startup>
    <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" >
        <Environment>
            <Variable name="MyVersionNumber" value="1.0.0.0" />
        </Environment>
    </Task>
</Startup>
```

<span data-ttu-id="62910-137">W hello poniższy przykład, hello **Startup.cmd** plik wsadowy zapisuje wiersz powitania "hello bieżąca wersja to 1.0.0.0" toohello StartupLog.txt pliku w katalogu hello określonej przez zmienną środowiskową TEMP hello.</span><span class="sxs-lookup"><span data-stu-id="62910-137">In hello following example, hello **Startup.cmd** batch file writes hello line "hello current version is 1.0.0.0" toohello StartupLog.txt file in hello directory specified by hello TEMP environment variable.</span></span> <span data-ttu-id="62910-138">Witaj `EXIT /B 0` wiersza zapewnia kończy zadanie uruchamiania tego hello **errorlevel** o wartości zero.</span><span class="sxs-lookup"><span data-stu-id="62910-138">hello `EXIT /B 0` line ensures that hello startup task ends with an **errorlevel** of zero.</span></span>

```cmd
ECHO hello current version is %MyVersionNumber% >> "%TEMP%\StartupLog.txt" 2>&1
EXIT /B 0
```

> [!NOTE]
> <span data-ttu-id="62910-139">W programie Visual Studio hello **skopiuj tooOutput katalogu** właściwości uruchamiania pliku wsadowego należy ustawić wartość zbyt**zawsze Kopiuj** toobe się, że plik wsadowy uruchamiania jest prawidłowo wdrożony tooyour projektu na platformie Azure (**approot\\bin** dla ról sieć Web i **approot** dla roli proces roboczy).</span><span class="sxs-lookup"><span data-stu-id="62910-139">In Visual Studio, hello **Copy tooOutput Directory** property for your startup batch file should be set too**Copy Always** toobe sure that your startup batch file is properly deployed tooyour project on Azure (**approot\\bin** for Web roles, and **approot** for worker roles).</span></span>
> 
> 

## <a name="description-of-task-attributes"></a><span data-ttu-id="62910-140">Opis zadania atrybutów</span><span class="sxs-lookup"><span data-stu-id="62910-140">Description of task attributes</span></span>
<span data-ttu-id="62910-141">Witaj poniżej opisano atrybuty hello hello **zadań** element hello [ServiceDefinition.csdef] pliku:</span><span class="sxs-lookup"><span data-stu-id="62910-141">hello following describes hello attributes of hello **Task** element in hello [ServiceDefinition.csdef] file:</span></span>

<span data-ttu-id="62910-142">**commandLine** — Określa wiersz polecenia hello hello uruchomienia zadania:</span><span class="sxs-lookup"><span data-stu-id="62910-142">**commandLine** - Specifies hello command line for hello startup task:</span></span>

* <span data-ttu-id="62910-143">Hello polecenie z parametry opcjonalne wiersza polecenia, który zaczyna się hello uruchamiania zadań.</span><span class="sxs-lookup"><span data-stu-id="62910-143">hello command, with optional command line parameters, which begins hello startup task.</span></span>
* <span data-ttu-id="62910-144">Jest to często filename hello pliku wsadowego cmd i bat.</span><span class="sxs-lookup"><span data-stu-id="62910-144">Frequently this is hello filename of a .cmd or .bat batch file.</span></span>
* <span data-ttu-id="62910-145">zadanie Hello jest względna toohello AppRoot\\folder Bin hello wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="62910-145">hello task is relative toohello AppRoot\\Bin folder for hello deployment.</span></span> <span data-ttu-id="62910-146">Zmienne środowiskowe nie są rozwijane w określeniu ścieżki hello i hello zadania.</span><span class="sxs-lookup"><span data-stu-id="62910-146">Environment variables are not expanded in determining hello path and file of hello task.</span></span> <span data-ttu-id="62910-147">Jeśli rozszerzania środowiska jest wymagana, można utworzyć skrypt .cmd małych wywołującą zadania uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="62910-147">If environment expansion is required, you can create a small .cmd script that calls your startup task.</span></span>
* <span data-ttu-id="62910-148">Może być aplikacji konsoli lub pliku wsadowego, który rozpoczyna się [skrypt programu PowerShell](cloud-services-startup-tasks-common.md#create-a-powershell-startup-task).</span><span class="sxs-lookup"><span data-stu-id="62910-148">Can be a console application or a batch file that starts a [PowerShell script](cloud-services-startup-tasks-common.md#create-a-powershell-startup-task).</span></span>

<span data-ttu-id="62910-149">**executionContext** — określa poziom uprawnień hello hello uruchomienia zadania.</span><span class="sxs-lookup"><span data-stu-id="62910-149">**executionContext** - Specifies hello privilege level for hello startup task.</span></span> <span data-ttu-id="62910-150">poziom uprawnień Hello może być ograniczony lub z podwyższonym poziomem uprawnień:</span><span class="sxs-lookup"><span data-stu-id="62910-150">hello privilege level can be limited or elevated:</span></span>

* <span data-ttu-id="62910-151">**ograniczone**</span><span class="sxs-lookup"><span data-stu-id="62910-151">**limited**</span></span>  
  <span data-ttu-id="62910-152">zadanie uruchamiania Hello jest uruchamiany z hello takie same uprawnienia w roli hello.</span><span class="sxs-lookup"><span data-stu-id="62910-152">hello startup task runs with hello same privileges as hello role.</span></span> <span data-ttu-id="62910-153">Gdy hello **executionContext** atrybutu hello [środowiska uruchomieniowego] element jest również **ograniczone**, uprawnienia użytkownika będą używane.</span><span class="sxs-lookup"><span data-stu-id="62910-153">When hello **executionContext** attribute for hello [Runtime] element is also **limited**, then user privileges are used.</span></span>
* <span data-ttu-id="62910-154">**z podwyższonym poziomem uprawnień**</span><span class="sxs-lookup"><span data-stu-id="62910-154">**elevated**</span></span>  
  <span data-ttu-id="62910-155">zadanie uruchamiania Hello jest uruchamiany z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="62910-155">hello startup task runs with administrator privileges.</span></span> <span data-ttu-id="62910-156">Dzięki temu zadania uruchamiania programów tooinstall, wprowadzić zmiany w konfiguracji usług IIS, wykonywanie zmiany w rejestrze i innych zadań poziomu administratora bez zwiększania hello poziom uprawnień roli hello, sama.</span><span class="sxs-lookup"><span data-stu-id="62910-156">This allows startup tasks tooinstall programs, make IIS configuration changes, perform registry changes, and other administrator level tasks, without increasing hello privilege level of hello role itself.</span></span>  

> [!NOTE]
> <span data-ttu-id="62910-157">Witaj poziom uprawnień zadania uruchamiania nie jest konieczne toobe hello sam rolę hello samej siebie.</span><span class="sxs-lookup"><span data-stu-id="62910-157">hello privilege level of a startup task does not need toobe hello same as hello role itself.</span></span>
> 
> 

<span data-ttu-id="62910-158">**taskType** — określa sposób uruchamiania zadań hello jest wykonywana.</span><span class="sxs-lookup"><span data-stu-id="62910-158">**taskType** - Specifies hello way a startup task is executed.</span></span>

* <span data-ttu-id="62910-159">**proste**</span><span class="sxs-lookup"><span data-stu-id="62910-159">**simple**</span></span>  
  <span data-ttu-id="62910-160">Zadania są wykonywane synchronicznie, pojedynczo, w kolejności hello określone w hello [ServiceDefinition.csdef] pliku.</span><span class="sxs-lookup"><span data-stu-id="62910-160">Tasks are executed synchronously, one at a time, in hello order specified in hello [ServiceDefinition.csdef] file.</span></span> <span data-ttu-id="62910-161">Gdy dla jednego **proste** kończy zadanie uruchamiania **errorlevel** zero, obok hello **proste** jest wykonywane zadanie uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="62910-161">When one **simple** startup task ends with an **errorlevel** of zero, hello next **simple** startup task is executed.</span></span> <span data-ttu-id="62910-162">Jeśli nie ma już **proste** uruchamiania zadań tooexecute, następnie roli hello, sama zostanie uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="62910-162">If there are no more **simple** startup tasks tooexecute, then hello role itself will be started.</span></span>   
  
  > [!NOTE]
  > <span data-ttu-id="62910-163">Jeśli hello **proste** zadań kończy się na inną niż zero **errorlevel**, wystąpienie hello zostanie zablokowana.</span><span class="sxs-lookup"><span data-stu-id="62910-163">If hello **simple** task ends with a non-zero **errorlevel**, hello instance will be blocked.</span></span> <span data-ttu-id="62910-164">Kolejne **proste** uruchamiania zadań i roli hello, nie zostaną uruchomione.</span><span class="sxs-lookup"><span data-stu-id="62910-164">Subsequent **simple** startup tasks, and hello role itself, will not start.</span></span>
  > 
  > 
  
    <span data-ttu-id="62910-165">tooensure, który plik wsadowy kończy się wyrazem **errorlevel** zero, wykonaj polecenie hello `EXIT /B 0` na końcu hello procesu pliku wsadowego.</span><span class="sxs-lookup"><span data-stu-id="62910-165">tooensure that your batch file ends with an **errorlevel** of zero, execute hello command `EXIT /B 0` at hello end of your batch file process.</span></span>
* <span data-ttu-id="62910-166">**tła**</span><span class="sxs-lookup"><span data-stu-id="62910-166">**background**</span></span>  
  <span data-ttu-id="62910-167">Zadania są wykonywane asynchronicznie, równolegle z hello uruchamiania hello roli.</span><span class="sxs-lookup"><span data-stu-id="62910-167">Tasks are executed asynchronously, in parallel with hello startup of hello role.</span></span>
* <span data-ttu-id="62910-168">**pierwszego planu**</span><span class="sxs-lookup"><span data-stu-id="62910-168">**foreground**</span></span>  
  <span data-ttu-id="62910-169">Zadania są wykonywane asynchronicznie, równolegle z hello uruchamiania hello roli.</span><span class="sxs-lookup"><span data-stu-id="62910-169">Tasks are executed asynchronously, in parallel with hello startup of hello role.</span></span> <span data-ttu-id="62910-170">Witaj Najważniejsza różnica między **pierwszego planu** i **tła** zadania oznacza, że **pierwszego planu** zadań uniemożliwia hello rolę z lub do czasu hello zadania zamykania zakończone.</span><span class="sxs-lookup"><span data-stu-id="62910-170">hello key difference between a **foreground** and a **background** task is that a **foreground** task prevents hello role from recycling or shutting down until hello task has ended.</span></span> <span data-ttu-id="62910-171">Witaj **tła** zadania nie ma to ograniczenie.</span><span class="sxs-lookup"><span data-stu-id="62910-171">hello **background** tasks do not have this restriction.</span></span>

## <a name="environment-variables"></a><span data-ttu-id="62910-172">Zmienne środowiskowe</span><span class="sxs-lookup"><span data-stu-id="62910-172">Environment variables</span></span>
<span data-ttu-id="62910-173">Zmienne środowiskowe to sposób toopass informacji tooa uruchomienia zadania.</span><span class="sxs-lookup"><span data-stu-id="62910-173">Environment variables are a way toopass information tooa startup task.</span></span> <span data-ttu-id="62910-174">Na przykład możesz umieścić hello ścieżki tooa blob zawierający program tooinstall, lub numery portów, które będzie używać swojej roli lub funkcji toocontrol ustawienia zadania uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="62910-174">For example, you can put hello path tooa blob that contains a program tooinstall, or port numbers that your role will use, or settings toocontrol features of your startup task.</span></span>

<span data-ttu-id="62910-175">Istnieją dwa rodzaje zmiennych środowiskowych dla zadania uruchamiania; zmienne środowiskowe statyczne i zmiennych środowiskowych na podstawie elementów członkowskich z hello [ RoleEnvironment] klasy.</span><span class="sxs-lookup"><span data-stu-id="62910-175">There are two kinds of environment variables for startup tasks; static environment variables and environment variables based on members of hello [RoleEnvironment] class.</span></span> <span data-ttu-id="62910-176">Są w hello [środowiska] sekcji hello [ServiceDefinition.csdef] pliku, a oba hello użyj [zmiennej] elementu i **nazwa** atrybut.</span><span class="sxs-lookup"><span data-stu-id="62910-176">Both are in hello [Environment] section of hello [ServiceDefinition.csdef] file, and both use hello [Variable] element and **name** attribute.</span></span>

<span data-ttu-id="62910-177">Witaj używa zmiennych statycznych środowiska **wartość** atrybutu hello [zmiennej] elementu.</span><span class="sxs-lookup"><span data-stu-id="62910-177">Static environment variables uses hello **value** attribute of hello [Variable] element.</span></span> <span data-ttu-id="62910-178">w powyższym przykładzie Hello tworzy zmienną środowiskową hello **MyVersionNumber** , który ma wartość statyczny "**1.0.0.0**".</span><span class="sxs-lookup"><span data-stu-id="62910-178">hello example above creates hello environment variable **MyVersionNumber** which has a static value of "**1.0.0.0**".</span></span> <span data-ttu-id="62910-179">Innym przykładem może być toocreate **StagingOrProduction** zmiennej środowiskowej, którą można ręcznie ustawić toovalues z "**przemieszczania**"lub"**produkcji**" tooperform uruchamianie różnych działań na podstawie hello wartości hello **StagingOrProduction** zmiennej środowiskowej.</span><span class="sxs-lookup"><span data-stu-id="62910-179">Another example would be toocreate a **StagingOrProduction** environment variable which you can manually set toovalues of "**staging**" or "**production**" tooperform different startup actions based on hello value of hello **StagingOrProduction** environment variable.</span></span>

<span data-ttu-id="62910-180">Zmienne środowiskowe oparte na elementach członkowskich klasy RoleEnvironment hello nie używaj hello **wartość** atrybutu hello [zmiennej] elementu.</span><span class="sxs-lookup"><span data-stu-id="62910-180">Environment variables based on members of hello RoleEnvironment class do not use hello **value** attribute of hello [Variable] element.</span></span> <span data-ttu-id="62910-181">Zamiast tego hello [RoleInstanceValue] elementu podrzędnego z odpowiednią hello **XPath** wartość atrybutu, są używane toocreate zmienną środowiskową oparte na elemencie członkowskim hello [ RoleEnvironment] klasy.</span><span class="sxs-lookup"><span data-stu-id="62910-181">Instead, hello [RoleInstanceValue] child element, with hello appropriate **XPath** attribute value, are used toocreate an environment variable based on a specific member of hello [RoleEnvironment] class.</span></span> <span data-ttu-id="62910-182">Wartości hello **XPath** różnych atrybutów tooaccess [ RoleEnvironment] wartości można znaleźć [tutaj](cloud-services-role-config-xpath.md).</span><span class="sxs-lookup"><span data-stu-id="62910-182">Values for hello **XPath** attribute tooaccess various [RoleEnvironment] values can be found [here](cloud-services-role-config-xpath.md).</span></span>

<span data-ttu-id="62910-183">Na przykład toocreate zmienną środowiskową, który jest "**true**" gdy wystąpienie hello działa w emulatorze obliczeń hello, i "**false**" podczas uruchamiania w chmurze hello, użyj następujących hello [zmiennej] i [RoleInstanceValue] elementy:</span><span class="sxs-lookup"><span data-stu-id="62910-183">For example, toocreate an environment variable that is "**true**" when hello instance is running in hello compute emulator, and "**false**" when running in hello cloud, use hello following [Variable] and [RoleInstanceValue] elements:</span></span>

```xml
<Startup>
    <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple">
        <Environment>

            <!-- Create hello environment variable that informs hello startup task whether it is running
                in hello Compute Emulator or in hello cloud. "%ComputeEmulatorRunning%"=="true" when
                running in hello Compute Emulator, "%ComputeEmulatorRunning%"=="false" when running
                in hello cloud. -->

            <Variable name="ComputeEmulatorRunning">
                <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
            </Variable>

        </Environment>
    </Task>
</Startup>
```

## <a name="next-steps"></a><span data-ttu-id="62910-184">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="62910-184">Next steps</span></span>
<span data-ttu-id="62910-185">Dowiedz się, jak tooperform niektórych [typowe zadania uruchamiania](cloud-services-startup-tasks-common.md) z usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="62910-185">Learn how tooperform some [common startup tasks](cloud-services-startup-tasks-common.md) with your Cloud Service.</span></span>

<span data-ttu-id="62910-186">[Pakiet](cloud-services-model-and-package.md) usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="62910-186">[Package](cloud-services-model-and-package.md) your Cloud Service.</span></span>  

[ServiceDefinition.csdef]: cloud-services-model-and-package.md#csdef
[zadań]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Task
[uruchamiania]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Startup
[środowiska uruchomieniowego]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Runtime
[środowiska]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Environment
[zmiennej]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Variable
[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue
[ RoleEnvironment]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx
