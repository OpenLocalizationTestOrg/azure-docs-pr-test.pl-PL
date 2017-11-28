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
# <a name="common-cloud-service-startup-tasks"></a><span data-ttu-id="23261-103">Typowe zadania uruchamiania usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="23261-103">Common Cloud Service startup tasks</span></span>
<span data-ttu-id="23261-104">W tym artykule przedstawiono kilka przykładów typowych zadań uruchamiania może być tooperform w usłudze w chmurze.</span><span class="sxs-lookup"><span data-stu-id="23261-104">This article provides some examples of common startup tasks you may want tooperform in your cloud service.</span></span> <span data-ttu-id="23261-105">Przed rozpoczęciem rolę, można użyć operacji tooperform zadania uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="23261-105">You can use startup tasks tooperform operations before a role starts.</span></span> <span data-ttu-id="23261-106">Operacje można tooperform obejmują instalowania składnika, rejestrowanie składników modelu COM, ustawienie kluczy rejestru lub uruchamia proces wymagającą dużo czasu.</span><span class="sxs-lookup"><span data-stu-id="23261-106">Operations that you might want tooperform include installing a component, registering COM components, setting registry keys, or starting a long running process.</span></span> 

<span data-ttu-id="23261-107">Zobacz [w tym artykule](cloud-services-startup-tasks.md) toounderstand sposób działania uruchamiania zadań, a w szczególności jak toocreate hello wpisów, które definiują zadanie uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="23261-107">See [this article](cloud-services-startup-tasks.md) toounderstand how startup tasks work, and specifically how toocreate hello entries that define a startup task.</span></span>

> [!NOTE]
> <span data-ttu-id="23261-108">Zadania uruchamiania nie są stosowane tooVirtual maszyny, tylko tooCloud usługi sieci Web i proces roboczy.</span><span class="sxs-lookup"><span data-stu-id="23261-108">Startup tasks are not applicable tooVirtual Machines, only tooCloud Service Web and Worker roles.</span></span>
> 

## <a name="define-environment-variables-before-a-role-starts"></a><span data-ttu-id="23261-109">Zdefiniuj zmienne środowiskowe, przed rozpoczęciem roli</span><span class="sxs-lookup"><span data-stu-id="23261-109">Define environment variables before a role starts</span></span>
<span data-ttu-id="23261-110">Zmienne środowiskowe zdefiniowane dla określonego zadania, należy użyć hello [środowiska] element wewnątrz hello [zadań] elementu.</span><span class="sxs-lookup"><span data-stu-id="23261-110">If you need environment variables defined for a specific task, use hello [Environment] element inside hello [Task] element.</span></span>

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

<span data-ttu-id="23261-111">Zmienne można również użyć [prawidłową wartość wyrażenia XPath Azure](cloud-services-role-config-xpath.md) tooreference coś o hello wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="23261-111">Variables can also use a [valid Azure XPath value](cloud-services-role-config-xpath.md) tooreference something about hello deployment.</span></span> <span data-ttu-id="23261-112">Zamiast hello `value` atrybutu, zdefiniuj [RoleInstanceValue] element podrzędny.</span><span class="sxs-lookup"><span data-stu-id="23261-112">Instead of using hello `value` attribute, define a [RoleInstanceValue] child element.</span></span>

```xml
<Variable name="PathToStartupStorage">
    <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='StartupLocalStorage']/@path" />
</Variable>
```


## <a name="configure-iis-startup-with-appcmdexe"></a><span data-ttu-id="23261-113">Konfigurowanie uruchomienia usług IIS przy użyciu AppCmd.exe</span><span class="sxs-lookup"><span data-stu-id="23261-113">Configure IIS startup with AppCmd.exe</span></span>
<span data-ttu-id="23261-114">Witaj [AppCmd.exe](https://technet.microsoft.com/library/jj635852.aspx) narzędzia wiersza polecenia mogą być używane toomanage ustawień usług IIS podczas uruchamiania na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="23261-114">hello [AppCmd.exe](https://technet.microsoft.com/library/jj635852.aspx) command-line tool can be used toomanage IIS settings at startup on Azure.</span></span> <span data-ttu-id="23261-115">*AppCmd.exe* zawiera ustawienia tooconfiguration wygodny, wiersza polecenia dostępu do użycia w uruchomienia zadania na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="23261-115">*AppCmd.exe* provides convenient, command-line access tooconfiguration settings for use in startup tasks on Azure.</span></span> <span data-ttu-id="23261-116">Przy użyciu *AppCmd.exe*, ustawienia witryny sieci Web mogą być dodane, zmodyfikowane lub usunięte dla witryn i aplikacji.</span><span class="sxs-lookup"><span data-stu-id="23261-116">Using *AppCmd.exe*, Website settings can be added, modified, or removed for applications and sites.</span></span>

<span data-ttu-id="23261-117">Istnieje jednak kilka rzeczy toowatch limit dla użycie hello *AppCmd.exe* jako zadanie uruchamiania:</span><span class="sxs-lookup"><span data-stu-id="23261-117">However, there are a few things toowatch out for in hello use of *AppCmd.exe* as a startup task:</span></span>

* <span data-ttu-id="23261-118">Uruchamianie zadania mogą być uruchamiane w więcej niż raz między ponownego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="23261-118">Startup tasks can be run more than once between reboots.</span></span> <span data-ttu-id="23261-119">Na przykład, gdy rola odtwarzana.</span><span class="sxs-lookup"><span data-stu-id="23261-119">For instance, when a role recycles.</span></span>
* <span data-ttu-id="23261-120">Jeśli *AppCmd.exe* akcja jest wykonywana więcej niż raz, może generować wystąpił błąd.</span><span class="sxs-lookup"><span data-stu-id="23261-120">If a *AppCmd.exe* action is performed more than once, it may generate an error.</span></span> <span data-ttu-id="23261-121">Na przykład za podjęciem tooadd sekcji*Web.config* dwukrotnie można wygenerować wystąpił błąd.</span><span class="sxs-lookup"><span data-stu-id="23261-121">For example, attempting tooadd a section too*Web.config* twice could generate an error.</span></span>
* <span data-ttu-id="23261-122">Uruchamianie zadań zakończy się niepowodzeniem, jeśli zwracają kod wyjścia równy zero lub **errorlevel**.</span><span class="sxs-lookup"><span data-stu-id="23261-122">Startup tasks fail if they return a non-zero exit code or **errorlevel**.</span></span> <span data-ttu-id="23261-123">Na przykład, jeśli *AppCmd.exe* generuje błąd.</span><span class="sxs-lookup"><span data-stu-id="23261-123">For example, when *AppCmd.exe* generates an error.</span></span>

<span data-ttu-id="23261-124">Witaj toocheck dobrym rozwiązaniem jest **errorlevel** po wywołaniu *AppCmd.exe*, jest łatwe toodo w przypadku zbyt zawijać wywołania hello*AppCmd.exe* z *.cmd*  pliku.</span><span class="sxs-lookup"><span data-stu-id="23261-124">It is a good practice toocheck hello **errorlevel** after calling *AppCmd.exe*, which is easy toodo if you wrap hello call too*AppCmd.exe* with a *.cmd* file.</span></span> <span data-ttu-id="23261-125">W przypadku wykrycia znanego **errorlevel** odpowiedzi, możesz go zignorować lub przekaż go ponownie.</span><span class="sxs-lookup"><span data-stu-id="23261-125">If you detect a known **errorlevel** response, you can ignore it, or pass it back.</span></span>

<span data-ttu-id="23261-126">Witaj errorlevel zwrócony przez *AppCmd.exe* są wymienione w pliku pliku winerror.h hello, a także będą widoczne na [MSDN](https://msdn.microsoft.com/library/windows/desktop/ms681382.aspx).</span><span class="sxs-lookup"><span data-stu-id="23261-126">hello errorlevel returned by *AppCmd.exe* are listed in hello winerror.h file, and can also be seen on [MSDN](https://msdn.microsoft.com/library/windows/desktop/ms681382.aspx).</span></span>

### <a name="example-of-managing-hello-error-level"></a><span data-ttu-id="23261-127">Przykład zarządzanie hello poziom błędu</span><span class="sxs-lookup"><span data-stu-id="23261-127">Example of managing hello error level</span></span>
<span data-ttu-id="23261-128">W tym przykładzie dodaje sekcji kompresji i kompresji objęcia JSON toohello *Web.config* pliku z powodu błędu obsługi i rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="23261-128">This example adds a compression section and a compression entry for JSON toohello *Web.config* file, with error handling and logging.</span></span>

<span data-ttu-id="23261-129">Witaj odpowiednich sekcji hello [ServiceDefinition.csdef] plików są wyświetlane w tym miejscu, które obejmują ustawienie hello [executionContext](https://msdn.microsoft.com/library/azure/gg557552.aspx#Task) atrybutu zbyt`elevated` toogive *AppCmd.exe*  wystarczające uprawnienia toochange hello ustawienia w hello *Web.config* pliku:</span><span class="sxs-lookup"><span data-stu-id="23261-129">hello relevant sections of hello [ServiceDefinition.csdef] file are shown here, which include setting hello [executionContext](https://msdn.microsoft.com/library/azure/gg557552.aspx#Task) attribute too`elevated` toogive *AppCmd.exe* sufficient permissions toochange hello settings in hello *Web.config* file:</span></span>

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

<span data-ttu-id="23261-130">Witaj *Startup.cmd* partii używa pliku *AppCmd.exe* tooadd sekcji kompresji i kompresji objęcia JSON toohello *Web.config* pliku.</span><span class="sxs-lookup"><span data-stu-id="23261-130">hello *Startup.cmd* batch file uses *AppCmd.exe* tooadd a compression section and a compression entry for JSON toohello *Web.config* file.</span></span> <span data-ttu-id="23261-131">Oczekiwano Hello **errorlevel** 183 ustawiono toozero przy użyciu hello Sprawdź. Wywołanie pliku EXE programu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="23261-131">hello expected **errorlevel** of 183 is set toozero using hello VERIFY.EXE command-line program.</span></span> <span data-ttu-id="23261-132">Nieoczekiwany errorlevels są rejestrowane tooStartupErrorLog.txt.</span><span class="sxs-lookup"><span data-stu-id="23261-132">Unexpected errorlevels are logged tooStartupErrorLog.txt.</span></span>

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

## <a name="add-firewall-rules"></a><span data-ttu-id="23261-133">Dodawanie reguł zapory</span><span class="sxs-lookup"><span data-stu-id="23261-133">Add firewall rules</span></span>
<span data-ttu-id="23261-134">Na platformie Azure czy skutecznie dwóch zapory.</span><span class="sxs-lookup"><span data-stu-id="23261-134">In Azure, there are effectively two firewalls.</span></span> <span data-ttu-id="23261-135">pierwszy zapory Hello steruje połączeń między maszyną wirtualną hello i hello poza world.</span><span class="sxs-lookup"><span data-stu-id="23261-135">hello first firewall controls connections between hello virtual machine and hello outside world.</span></span> <span data-ttu-id="23261-136">Zapora jest kontrolowany przez hello [punkty końcowe] element hello [ServiceDefinition.csdef] pliku.</span><span class="sxs-lookup"><span data-stu-id="23261-136">This firewall is controlled by hello [EndPoints] element in hello [ServiceDefinition.csdef] file.</span></span>

<span data-ttu-id="23261-137">drugi zapory Hello steruje połączeń między hello maszyny wirtualnej i hello procesów w ramach maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="23261-137">hello second firewall controls connections between hello virtual machine and hello processes within that virtual machine.</span></span> <span data-ttu-id="23261-138">Zapora może być kontrolowane przez hello `netsh advfirewall firewall` narzędzia wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="23261-138">This firewall can be controlled by hello `netsh advfirewall firewall` command-line tool.</span></span>

<span data-ttu-id="23261-139">Platforma Azure tworzy reguły zapory dla procesów hello uruchomionych w ramach poszczególnych ról.</span><span class="sxs-lookup"><span data-stu-id="23261-139">Azure creates firewall rules for hello processes started within your roles.</span></span> <span data-ttu-id="23261-140">Na przykład po uruchomieniu usługi lub program Azure automatycznie tworzy tooallow reguły zapory na potrzeby hello toocommunicate tej usługi z hello Internet.</span><span class="sxs-lookup"><span data-stu-id="23261-140">For example, when you start a service or program, Azure automatically creates hello necessary firewall rules tooallow that service toocommunicate with hello Internet.</span></span> <span data-ttu-id="23261-141">Jeśli utworzysz usługę, która jest uruchamiana przez proces poza roli użytkownika (np. usługi COM + lub zaplanowanych zadań systemu Windows), jednak toomanually Tworzenie usługi toothat dostępu tooallow reguły zapory.</span><span class="sxs-lookup"><span data-stu-id="23261-141">However, if you create a service that is started by a process outside your role (like a COM+ service or a Windows Scheduled Task), you need toomanually create a firewall rule tooallow access toothat service.</span></span> <span data-ttu-id="23261-142">Te reguły zapory można tworzyć za pomocą zadania uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="23261-142">These firewall rules can be created by using a startup task.</span></span>

<span data-ttu-id="23261-143">Zadanie uruchamiania, która tworzy regułę zapory muszą mieć [executionContext][zadań] z **z podwyższonym poziomem uprawnień**.</span><span class="sxs-lookup"><span data-stu-id="23261-143">A startup task that creates a firewall rule must have an [executionContext][Task] of **elevated**.</span></span> <span data-ttu-id="23261-144">Dodaj powitania po uruchamiania zadań toohello [ServiceDefinition.csdef] pliku.</span><span class="sxs-lookup"><span data-stu-id="23261-144">Add hello following startup task toohello [ServiceDefinition.csdef] file.</span></span>

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

<span data-ttu-id="23261-145">reguły zapory hello tooadd, należy użyć odpowiedniego hello `netsh advfirewall firewall` poleceń w pliku wsadowym uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="23261-145">tooadd hello firewall rule, you must use hello appropriate `netsh advfirewall firewall` commands in your startup batch file.</span></span> <span data-ttu-id="23261-146">W tym przykładzie zadanie uruchamiania hello wymaga zabezpieczeń i szyfrowania dla portu TCP 80.</span><span class="sxs-lookup"><span data-stu-id="23261-146">In this example, hello startup task requires security and encryption for TCP port 80.</span></span>

```cmd
REM   Add a firewall rule in a startup task.

REM   Add an inbound rule requiring security and encryption for TCP port 80 traffic.
netsh advfirewall firewall add rule name="Require Encryption for Inbound TCP/80" protocol=TCP dir=in localport=80 security=authdynenc action=allow >> "%TEMP%\StartupLog.txt" 2>&1

REM   If an error occurred, return hello errorlevel.
EXIT /B %errorlevel%
```

## <a name="block-a-specific-ip-address"></a><span data-ttu-id="23261-147">Blok określonego adresu IP</span><span class="sxs-lookup"><span data-stu-id="23261-147">Block a specific IP address</span></span>
<span data-ttu-id="23261-148">Zestaw tooa sieci web platformy Azure roli dostęp z określonych adresów IP można ograniczyć, modyfikując programu IIS **web.config** pliku.</span><span class="sxs-lookup"><span data-stu-id="23261-148">You can restrict an Azure web role access tooa set of specified IP addresses by modifying your IIS **web.config** file.</span></span> <span data-ttu-id="23261-149">Należy również toouse pliku polecenia, który umożliwia odblokowanie hello **ipSecurity** sekcji hello **ApplicationHost.config** pliku.</span><span class="sxs-lookup"><span data-stu-id="23261-149">You also need toouse a command file which unlocks hello **ipSecurity** section of hello **ApplicationHost.config** file.</span></span>

<span data-ttu-id="23261-150">hello odblokowywania toodo **ipSecurity** sekcji hello **ApplicationHost.config** plików, tworzenie pliku poleceń, który jest uruchamiany podczas uruchamiania roli.</span><span class="sxs-lookup"><span data-stu-id="23261-150">toodo unlock hello **ipSecurity** section of hello **ApplicationHost.config** file, create a command file that runs at role start.</span></span> <span data-ttu-id="23261-151">Utwórz folder na głównym poziomie hello roli sieci web o nazwie **uruchamiania** i, w tym folderze utwórz plik wsadowy o nazwie **startup.cmd**.</span><span class="sxs-lookup"><span data-stu-id="23261-151">Create a folder at hello root level of your web role called **startup** and, within this folder, create a batch file called **startup.cmd**.</span></span> <span data-ttu-id="23261-152">Dodaj projekt programu Visual Studio tooyour tego pliku i ustaw właściwości hello zbyt**zawsze Kopiuj** tooensure jest on dołączony do pakietu.</span><span class="sxs-lookup"><span data-stu-id="23261-152">Add this file tooyour Visual Studio project and set hello properties too**Copy Always** tooensure that it is included in your package.</span></span>

<span data-ttu-id="23261-153">Dodaj powitania po uruchamiania zadań toohello [ServiceDefinition.csdef] pliku.</span><span class="sxs-lookup"><span data-stu-id="23261-153">Add hello following startup task toohello [ServiceDefinition.csdef] file.</span></span>

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

<span data-ttu-id="23261-154">Dodaj to polecenie toohello **startup.cmd** pliku:</span><span class="sxs-lookup"><span data-stu-id="23261-154">Add this command toohello **startup.cmd** file:</span></span>

```cmd
@echo off
@echo Installing "IPv4 Address and Domain Restrictions" feature 
powershell -ExecutionPolicy Unrestricted -command "Install-WindowsFeature Web-IP-Security"
@echo Unlocking configuration for "IPv4 Address and Domain Restrictions" feature 
%windir%\system32\inetsrv\AppCmd.exe unlock config -section:system.webServer/security/ipSecurity
```

<span data-ttu-id="23261-155">To zadanie sprawia, że hello **startup.cmd** partii toobe pliku uruchamiać za każdym razem hello roli sieci web został zainicjowany, zapewnienie, że hello wymagane **ipSecurity** sekcja jest odblokowane.</span><span class="sxs-lookup"><span data-stu-id="23261-155">This task causes hello **startup.cmd** batch file toobe run every time hello web role is initialized, ensuring that hello required **ipSecurity** section is unlocked.</span></span>

<span data-ttu-id="23261-156">Na koniec zmodyfikuj hello [sekcja system.webServer](http://www.iis.net/configreference/system.webserver/security/ipsecurity#005) roli sieci web **web.config** pliku tooadd listę adresów IP, które mają prawo dostępu, jak pokazano w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="23261-156">Finally, modify hello [system.webServer section](http://www.iis.net/configreference/system.webserver/security/ipsecurity#005) your web role’s **web.config** file tooadd a list of IP addresses that are granted access, as shown in hello following example:</span></span>

<span data-ttu-id="23261-157">Ten przykładowy konfiguracji **umożliwia** wszystkie adresy IP tooaccess hello serwera, z wyjątkiem Witaj dwie zdefiniowany</span><span class="sxs-lookup"><span data-stu-id="23261-157">This sample config **allows** all IPs tooaccess hello server except hello two defined</span></span>

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

<span data-ttu-id="23261-158">Ten przykład konfiguracji **nie zezwala na** wszystkie adresy IP z uzyskiwania dostępu do serwera hello z wyjątkiem hello dwa zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="23261-158">This sample config **denies** all IPs from accessing hello server except for hello two defined.</span></span>

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

## <a name="create-a-powershell-startup-task"></a><span data-ttu-id="23261-159">Utwórz zadanie uruchamiania programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="23261-159">Create a PowerShell startup task</span></span>
<span data-ttu-id="23261-160">Skrypty programu Windows PowerShell nie należy wywoływać bezpośrednio w hello [ServiceDefinition.csdef] pliku, ale może być wywoływany z w pliku wsadowym uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="23261-160">Windows PowerShell scripts cannot be called directly from hello [ServiceDefinition.csdef] file, but they can be invoked from within a startup batch file.</span></span>

<span data-ttu-id="23261-161">PowerShell (domyślnie) uruchamiać niepodpisane skrypty.</span><span class="sxs-lookup"><span data-stu-id="23261-161">PowerShell (by default) does not run unsigned scripts.</span></span> <span data-ttu-id="23261-162">Jeśli nie zarejestrujesz skrypt należy tooconfigure PowerShell toorun niepodpisanych skryptów.</span><span class="sxs-lookup"><span data-stu-id="23261-162">Unless you sign your script, you need tooconfigure PowerShell toorun unsigned scripts.</span></span> <span data-ttu-id="23261-163">toorun niepodpisanych skryptów, hello **ExecutionPolicy** musi być ustawiona zbyt**bez ograniczeń**.</span><span class="sxs-lookup"><span data-stu-id="23261-163">toorun unsigned scripts, hello **ExecutionPolicy** must be set too**Unrestricted**.</span></span> <span data-ttu-id="23261-164">Witaj **ExecutionPolicy** ustawienie użycia opiera się na powitania wersję środowiska Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="23261-164">hello **ExecutionPolicy** setting that you use is based on hello version of Windows PowerShell.</span></span>

```cmd
REM   Run an unsigned PowerShell script and log hello output
PowerShell -ExecutionPolicy Unrestricted .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   If an error occurred, return hello errorlevel.
EXIT /B %errorlevel%
```

<span data-ttu-id="23261-165">Jeśli używasz systemu operacyjnego gościa, który uruchamia program PowerShell 2.0 jest lub 1.0 można wymusić toorun w wersji 2, a jeśli jest niedostępny, użyj wersji 1.</span><span class="sxs-lookup"><span data-stu-id="23261-165">If you're using a Guest OS that is runs PowerShell 2.0 or 1.0 you can force version 2 toorun, and if unavailable, use version 1.</span></span>

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

## <a name="create-files-in-local-storage-from-a-startup-task"></a><span data-ttu-id="23261-166">Tworzenie plików w magazynie lokalnym z zadanie uruchamiania</span><span class="sxs-lookup"><span data-stu-id="23261-166">Create files in local storage from a startup task</span></span>
<span data-ttu-id="23261-167">Można użyć toostore zasobu lokalnego magazynu plików utworzonych przez zadanie uruchamiania, który jest dostępny później przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="23261-167">You can use a local storage resource toostore files created by your startup task that is accessed later by your application.</span></span>

<span data-ttu-id="23261-168">toocreate hello zasobów magazynu lokalnego, Dodaj [LocalResources] toohello sekcji [ServiceDefinition.csdef] pliku, a następnie dodaj hello [LocalStorage] element podrzędny.</span><span class="sxs-lookup"><span data-stu-id="23261-168">toocreate hello local storage resource, add a [LocalResources] section toohello [ServiceDefinition.csdef] file and then add hello [LocalStorage] child element.</span></span> <span data-ttu-id="23261-169">Nadaj unikatową nazwę i odpowiedni rozmiar zasobu lokalnego magazynu hello uruchomienia zadania.</span><span class="sxs-lookup"><span data-stu-id="23261-169">Give hello local storage resource a unique name and an appropriate size for your startup task.</span></span>

<span data-ttu-id="23261-170">toouse zasobu magazynu lokalnego uruchomienia zadania, należy toocreate lokalizacja zasobu środowiska zmiennej tooreference hello magazynu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="23261-170">toouse a local storage resource in your startup task, you need toocreate an environment variable tooreference hello local storage resource location.</span></span> <span data-ttu-id="23261-171">Następnie hello uruchamiania zadań i aplikacji hello są stanie tooread i zapisać pliki toohello magazynu lokalnego zasobu.</span><span class="sxs-lookup"><span data-stu-id="23261-171">Then hello startup task and hello application are able tooread and write files toohello local storage resource.</span></span>

<span data-ttu-id="23261-172">Witaj odpowiednich sekcji hello **ServiceDefinition.csdef** plików są wyświetlane tutaj:</span><span class="sxs-lookup"><span data-stu-id="23261-172">hello relevant sections of hello **ServiceDefinition.csdef** file are shown here:</span></span>

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

<span data-ttu-id="23261-173">Na przykład to **Startup.cmd** plik wsadowy używa hello **PathToStartupStorage** pliku hello toocreate zmiennej środowiska **MyTest.txt** w magazynie lokalnym hello Lokalizacja.</span><span class="sxs-lookup"><span data-stu-id="23261-173">As an example, this **Startup.cmd** batch file uses hello **PathToStartupStorage** environment variable toocreate hello file **MyTest.txt** on hello local storage location.</span></span>

```cmd
REM   Create a simple text file.

ECHO This text will go into hello MyTest.txt file which will be in hello    >  "%PathToStartupStorage%\MyTest.txt"
ECHO path pointed tooby hello PathToStartupStorage environment variable.  >> "%PathToStartupStorage%\MyTest.txt"
ECHO hello contents of hello PathToStartupStorage environment variable is   >> "%PathToStartupStorage%\MyTest.txt"
ECHO "%PathToStartupStorage%".                                          >> "%PathToStartupStorage%\MyTest.txt"

REM   Exit hello batch file with ERRORLEVEL 0.

EXIT /b 0
```

<span data-ttu-id="23261-174">Magazyn lokalny folder mogą korzystać z hello Azure SDK, za pomocą hello [GetLocalResource](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) metody.</span><span class="sxs-lookup"><span data-stu-id="23261-174">You can access local storage folder from hello Azure SDK by using hello [GetLocalResource](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) method.</span></span>

```csharp
string localStoragePath = Microsoft.WindowsAzure.ServiceRuntime.RoleEnvironment.GetLocalResource("StartupLocalStorage").RootPath;

string fileContent = System.IO.File.ReadAllText(System.IO.Path.Combine(localStoragePath, "MyTestFile.txt"));
```

## <a name="run-in-hello-emulator-or-cloud"></a><span data-ttu-id="23261-175">Uruchamianie w emulatorze hello lub w chmurze</span><span class="sxs-lookup"><span data-stu-id="23261-175">Run in hello emulator or cloud</span></span>
<span data-ttu-id="23261-176">Program może wykonywać inne czynności działającego w toowhen chmury porównaniu hello, którego emulatora obliczeń hello uruchomienia zadania.</span><span class="sxs-lookup"><span data-stu-id="23261-176">You can have your startup task perform different steps when it is operating in hello cloud compared toowhen it is in hello compute emulator.</span></span> <span data-ttu-id="23261-177">Na przykład można toouse świeżą kopię danych SQL tylko wtedy, gdy działa w emulatorze hello.</span><span class="sxs-lookup"><span data-stu-id="23261-177">For example, you may want toouse a fresh copy of your SQL data only when running in hello emulator.</span></span> <span data-ttu-id="23261-178">Lub może być toodo optymalizacji wydajności chmury hello nie muszą toodo podczas uruchamiania w emulatorze hello.</span><span class="sxs-lookup"><span data-stu-id="23261-178">Or you may want toodo some performance optimizations for hello cloud that you don't need toodo when running in hello emulator.</span></span>

<span data-ttu-id="23261-179">Ta możliwość tooperform różne akcje na powitania emulator obliczeń i hello chmury można osiągnąć, tworząc zmienną środowiskową w hello [ServiceDefinition.csdef] pliku.</span><span class="sxs-lookup"><span data-stu-id="23261-179">This ability tooperform different actions on hello compute emulator and hello cloud can be accomplished by creating an environment variable in hello [ServiceDefinition.csdef] file.</span></span> <span data-ttu-id="23261-180">Następnie można przetestować tej zmiennej środowiskowej dla wartości w zadania uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="23261-180">You then test that environment variable for a value in your startup task.</span></span>

<span data-ttu-id="23261-181">Zmienna środowiskowa hello toocreate, Dodaj hello [zmiennej]/[RoleInstanceValue] element i utworzyć wartość wyrażenia XPath `/RoleEnvironment/Deployment/@emulated`.</span><span class="sxs-lookup"><span data-stu-id="23261-181">toocreate hello environment variable, add hello [Variable]/[RoleInstanceValue] element and create an XPath value of `/RoleEnvironment/Deployment/@emulated`.</span></span> <span data-ttu-id="23261-182">Witaj wartość hello **ComputeEmulatorRunning %** jest zmienna środowiskowa `true` podczas uruchamiania na powitania emulatora obliczeń, i `false` podczas uruchamiania w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="23261-182">hello value of hello **%ComputeEmulatorRunning%** environment variable is `true` when running on hello compute emulator, and `false` when running on hello cloud.</span></span>

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

<span data-ttu-id="23261-183">zadanie Hello teraz sprawdzić hello **ComputeEmulatorRunning %** tooperform zmiennej akcji innego środowiska w oparciu o Określa, czy jest uruchomiona rola hello w hello w chmurze lub hello emulatora.</span><span class="sxs-lookup"><span data-stu-id="23261-183">hello task can now check hello **%ComputeEmulatorRunning%** environment variable tooperform different actions based on whether hello role is running in hello cloud or hello emulator.</span></span> <span data-ttu-id="23261-184">Oto .cmd skrypt powłoki, który sprawdza, czy tej zmiennej środowiskowej.</span><span class="sxs-lookup"><span data-stu-id="23261-184">Here is a .cmd shell script that checks for that environment variable.</span></span>

```cmd
REM   Check if this task is running on hello compute emulator.

IF "%ComputeEmulatorRunning%" == "true" (
    REM   This task is running on hello compute emulator. Perform tasks that must be run only in hello compute emulator.
) ELSE (
    REM   This task is running on hello cloud. Perform tasks that must be run only in hello cloud.
)
```


## <a name="detect-that-your-task-has-already-run"></a><span data-ttu-id="23261-185">Wykryj, czy zadanie zostało już uruchomione</span><span class="sxs-lookup"><span data-stu-id="23261-185">Detect that your task has already run</span></span>
<span data-ttu-id="23261-186">Rola Hello może odtworzyć bez ponownego uruchomienia komputera powoduje ponownie Twoje toorun zadania uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="23261-186">hello role may recycle without a reboot causing your startup tasks toorun again.</span></span> <span data-ttu-id="23261-187">Nie ma żadnych tooindicate flagi, że zadanie zostało już uruchomione na hello hosting maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="23261-187">There is no flag tooindicate that a task has already run on hello hosting VM.</span></span> <span data-ttu-id="23261-188">Może być niektórych zadań, których nie ma znaczenia, że uruchomione wiele razy.</span><span class="sxs-lookup"><span data-stu-id="23261-188">You may have some tasks where it doesn't matter that they run multiple times.</span></span> <span data-ttu-id="23261-189">Jednak może wystąpić sytuacja, w którym ma być tooprevent zadania uruchamiania więcej niż raz.</span><span class="sxs-lookup"><span data-stu-id="23261-189">However, you may run into a situation where you need tooprevent a task from running more than once.</span></span>

<span data-ttu-id="23261-190">Hello najprostszy sposób toodetect który zadania został już uruchomiony jest toocreate pliku w hello **% TEMP %** folder po pomyślnym zakończeniu operacji hello zadań i jej przyjrzeć hello początek hello zadań.</span><span class="sxs-lookup"><span data-stu-id="23261-190">hello simplest way toodetect that a task has already run is toocreate a file in hello **%TEMP%** folder when hello task is successful and look for it at hello start of hello task.</span></span> <span data-ttu-id="23261-191">Poniżej przedstawiono przykładowy skrypt powłoki cmd nie.</span><span class="sxs-lookup"><span data-stu-id="23261-191">Here is a sample cmd shell script that does that for you.</span></span>

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

## <a name="task-best-practices"></a><span data-ttu-id="23261-192">Najlepsze rozwiązania w zakresie zadania</span><span class="sxs-lookup"><span data-stu-id="23261-192">Task best practices</span></span>
<span data-ttu-id="23261-193">Poniżej przedstawiono najważniejsze wskazówki, które należy wykonać podczas konfigurowania zadania dla roli użytkownika sieci web lub procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="23261-193">Here are some best practices you should follow when configuring task for your web or worker role.</span></span>

### <a name="always-log-startup-activities"></a><span data-ttu-id="23261-194">Zawsze dziennika uruchomienia działania</span><span class="sxs-lookup"><span data-stu-id="23261-194">Always log startup activities</span></span>
<span data-ttu-id="23261-195">Visual Studio nie zapewnia toostep debugera za pomocą plików wsadowych, więc jest dobrym tooget jak najwięcej danych operacji hello pliki wsadowe, jak to możliwe.</span><span class="sxs-lookup"><span data-stu-id="23261-195">Visual Studio does not provide a debugger toostep through batch files, so it's good tooget as much data on hello operation of batch files as possible.</span></span> <span data-ttu-id="23261-196">Rejestrowanie hello dane wyjściowe pliki wsadowe, zarówno **stdout** i **stderr**, można podać ważne informacje podczas próby toodebug i Usuń pliki wsadowe.</span><span class="sxs-lookup"><span data-stu-id="23261-196">Logging hello output of batch files, both **stdout** and **stderr**, can give you important information when trying toodebug and fix batch files.</span></span> <span data-ttu-id="23261-197">toolog zarówno **stdout** i **stderr** toohello StartupLog.txt pliku w hello katalog wskazywany tooby hello **% TEMP %** zmiennej środowiskowej, Dodaj tekst hello `>>  "%TEMP%\\StartupLog.txt" 2>&1`toohello koniec określonych wierszy można mają toolog.</span><span class="sxs-lookup"><span data-stu-id="23261-197">toolog both **stdout** and **stderr** toohello StartupLog.txt file in hello directory pointed tooby hello **%TEMP%** environment variable, add hello text `>>  "%TEMP%\\StartupLog.txt" 2>&1` toohello end of specific lines you want toolog.</span></span> <span data-ttu-id="23261-198">Na przykład tooexecute setup.exe w hello **PathToApp1Install %** katalogu:</span><span class="sxs-lookup"><span data-stu-id="23261-198">For example, tooexecute setup.exe in hello **%PathToApp1Install%** directory:</span></span>

    "%PathToApp1Install%\setup.exe" >> "%TEMP%\StartupLog.txt" 2>&1

<span data-ttu-id="23261-199">toosimplify dane xml można tworzyć otoka *cmd* pliku, który wywołuje wszystkie uruchamiania zadań wraz z rejestrowania i zapewnia hello udziałów każdego zadania podrzędnego samego zmiennych środowiskowych.</span><span class="sxs-lookup"><span data-stu-id="23261-199">toosimplify your xml, you can create a wrapper *cmd* file that calls all of your startup tasks along with logging and ensures each child-task shares hello same environment variables.</span></span>

<span data-ttu-id="23261-200">Może być jednak irytujących toouse `>> "%TEMP%\StartupLog.txt" 2>&1` na końcu hello każdego uruchomienia zadania.</span><span class="sxs-lookup"><span data-stu-id="23261-200">You may find it annoying though toouse `>> "%TEMP%\StartupLog.txt" 2>&1` on hello end of each startup task.</span></span> <span data-ttu-id="23261-201">Rejestrowanie zadania można wymusić przez utworzenie otoka obsługuje rejestrowanie dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="23261-201">You can enforce task logging by creating a wrapper that handles logging for you.</span></span> <span data-ttu-id="23261-202">Tej otoki wywołuje plik wsadowy rzeczywistych hello ma toorun.</span><span class="sxs-lookup"><span data-stu-id="23261-202">This wrapper calls hello real batch file you want toorun.</span></span> <span data-ttu-id="23261-203">Żadnych danych wyjściowych z pliku wsadowego docelowego hello będzie przekierowany toohello *Startuplog.txt* pliku.</span><span class="sxs-lookup"><span data-stu-id="23261-203">Any output from hello target batch file will be redirected toohello *Startuplog.txt* file.</span></span>

<span data-ttu-id="23261-204">Witaj poniższy przykład pokazuje, jak tooredirect wszystkie dane wyjściowe z pliku wsadowego uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="23261-204">hello following example shows how tooredirect all output from a startup batch file.</span></span> <span data-ttu-id="23261-205">W tym przykładzie plik ServerDefinition.csdef hello tworzy zadanie uruchamiania, który wywołuje *logwrap.cmd*.</span><span class="sxs-lookup"><span data-stu-id="23261-205">In this example, hello ServerDefinition.csdef file creates a startup task that calls *logwrap.cmd*.</span></span> <span data-ttu-id="23261-206">*logwrap.cmd* wywołania *Startup2.cmd*, przekierowywanie wszystkie dane wyjściowe zbyt**% TEMP %\\StartupLog.txt**.</span><span class="sxs-lookup"><span data-stu-id="23261-206">*logwrap.cmd* calls *Startup2.cmd*, redirecting all output too**%TEMP%\\StartupLog.txt**.</span></span>

<span data-ttu-id="23261-207">ServiceDefinition.cmd:</span><span class="sxs-lookup"><span data-stu-id="23261-207">ServiceDefinition.cmd:</span></span>

```xml
<Startup>
    <Task commandLine="logwrap.cmd startup2.cmd" executionContext="limited" taskType="simple" />
</Startup>
```

<span data-ttu-id="23261-208">**logwrap.cmd:**</span><span class="sxs-lookup"><span data-stu-id="23261-208">**logwrap.cmd:**</span></span>

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

<span data-ttu-id="23261-209">**Startup2.cmd:**</span><span class="sxs-lookup"><span data-stu-id="23261-209">**Startup2.cmd:**</span></span>

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

<span data-ttu-id="23261-210">Przykładowe dane wyjściowe w hello **StartupLog.txt** pliku:</span><span class="sxs-lookup"><span data-stu-id="23261-210">Sample output in hello **StartupLog.txt** file:</span></span>

```txt
[Mon 10/17/2016 20:24:46.75] == START logwrap.cmd ============================================== 
[Mon 10/17/2016 20:24:46.75] Running command1.cmd 
[Mon 10/17/2016 20:24:46.77] Some log information about this task
[Mon 10/17/2016 20:24:46.77] Some more log information about this task
[Mon 10/17/2016 20:24:46.77] Done 
[Mon 10/17/2016 20:24:46.77] == END logwrap.cmd ================================================ 
```

> [!TIP]
> <span data-ttu-id="23261-211">Witaj **StartupLog.txt** plik znajduje się w hello *C:\Resources\temp\\\RoleTemp {identyfikator roli}* folderu.</span><span class="sxs-lookup"><span data-stu-id="23261-211">hello **StartupLog.txt** file is located in hello *C:\Resources\temp\\{role identifier}\RoleTemp* folder.</span></span>
> 
> 

### <a name="set-executioncontext-appropriately-for-startup-tasks"></a><span data-ttu-id="23261-212">Ustaw executionContext odpowiednio do uruchamiania zadań</span><span class="sxs-lookup"><span data-stu-id="23261-212">Set executionContext appropriately for startup tasks</span></span>
<span data-ttu-id="23261-213">Ustaw uprawnienia odpowiednio do hello uruchomienia zadania.</span><span class="sxs-lookup"><span data-stu-id="23261-213">Set privileges appropriately for hello startup task.</span></span> <span data-ttu-id="23261-214">Czasami uruchamiania zadań należy uruchomić z podwyższonym poziomem uprawnień, nawet jeśli roli hello jest uruchamiany z normalnym uprawnieniami.</span><span class="sxs-lookup"><span data-stu-id="23261-214">Sometimes startup tasks must run with elevated privileges even though hello role runs with normal privileges.</span></span>

<span data-ttu-id="23261-215">Witaj [executionContext][zadań] atrybut ustawia poziom uprawnień hello hello uruchomienia zadania.</span><span class="sxs-lookup"><span data-stu-id="23261-215">hello [executionContext][Task] attribute sets hello privilege level of hello startup task.</span></span> <span data-ttu-id="23261-216">Przy użyciu `executionContext="limited"` oznacza, że zadanie uruchamiania hello ma hello poziomu uprawnień roli hello.</span><span class="sxs-lookup"><span data-stu-id="23261-216">Using `executionContext="limited"` means hello startup task has hello same privilege level as hello role.</span></span> <span data-ttu-id="23261-217">Przy użyciu `executionContext="elevated"` oznacza hello zadanie uruchamiania ma uprawnienia administratora, co pozwala hello uruchomienia zadania administratora tooperform zadanie bez nadawania roli tooyour uprawnienia administratora.</span><span class="sxs-lookup"><span data-stu-id="23261-217">Using `executionContext="elevated"` means hello startup task has administrator privileges, which allows hello startup task tooperform administrator tasks without giving administrator privileges tooyour role.</span></span>

<span data-ttu-id="23261-218">Przykładem zadanie uruchamiania, który wymaga pełnych uprawnień jest zadanie uruchamiania, która używa **AppCmd.exe** tooconfigure usług IIS.</span><span class="sxs-lookup"><span data-stu-id="23261-218">An example of a startup task that requires elevated privileges is a startup task that uses **AppCmd.exe** tooconfigure IIS.</span></span> <span data-ttu-id="23261-219">**AppCmd.exe** wymaga `executionContext="elevated"`.</span><span class="sxs-lookup"><span data-stu-id="23261-219">**AppCmd.exe** requires `executionContext="elevated"`.</span></span>

### <a name="use-hello-appropriate-tasktype"></a><span data-ttu-id="23261-220">Użyć odpowiednich taskType hello</span><span class="sxs-lookup"><span data-stu-id="23261-220">Use hello appropriate taskType</span></span>
<span data-ttu-id="23261-221">Witaj [taskType][zadań] atrybut Określa zadanie uruchamiania hello sposób hello jest wykonywana.</span><span class="sxs-lookup"><span data-stu-id="23261-221">hello [taskType][Task] attribute determines hello way hello startup task is executed.</span></span> <span data-ttu-id="23261-222">Istnieją trzy wartości: **proste**, **tła**, i **pierwszego planu**.</span><span class="sxs-lookup"><span data-stu-id="23261-222">There are three values: **simple**, **background**, and **foreground**.</span></span> <span data-ttu-id="23261-223">Witaj zadania tła i pierwszego planu są uruchamiane asynchronicznie, a następnie hello prostych zadań są wykonywane synchronicznie pojedynczo.</span><span class="sxs-lookup"><span data-stu-id="23261-223">hello background and foreground tasks are started asynchronously, and then hello simple tasks are executed synchronously one at a time.</span></span>

<span data-ttu-id="23261-224">Z **proste** uruchomienia zadania, można ustawić hello kolejność uruchamiania zadań hello według kolejności hello, w których hello zadania są wymienione w pliku ServiceDefinition.csdef hello.</span><span class="sxs-lookup"><span data-stu-id="23261-224">With **simple** startup tasks, you can set hello order in which hello tasks run by hello order in which hello tasks are listed in hello ServiceDefinition.csdef file.</span></span> <span data-ttu-id="23261-225">Jeśli **proste** zadań kończy się niezerowy kod zakończenia, a następnie hello zatrzymuje procedury uruchamiania i nie można uruchomić hello roli.</span><span class="sxs-lookup"><span data-stu-id="23261-225">If a **simple** task ends with a non-zero exit code, then hello startup procedure stops and hello role does not start.</span></span>

<span data-ttu-id="23261-226">Witaj różnica między **tła** uruchamiania zadań i **pierwszego planu** uruchomienia zadania oznacza, że **pierwszego planu** zadania Zachowaj hello roli uruchomiony do momentu hello  **pierwszego planu** zakończeniem zadania.</span><span class="sxs-lookup"><span data-stu-id="23261-226">hello difference between **background** startup tasks and **foreground** startup tasks is that **foreground** tasks keep hello role running until hello **foreground** task ends.</span></span> <span data-ttu-id="23261-227">Oznacza to też, że jeśli hello **pierwszego planu** zawiesza się zadania lub awarii hello rola nie jest odtwarzana do hello **pierwszego planu** wymusza zadań zamknięte.</span><span class="sxs-lookup"><span data-stu-id="23261-227">This also means that if hello **foreground** task hangs or crashes, hello role will not recycle until hello **foreground** task is forced closed.</span></span> <span data-ttu-id="23261-228">Z tego powodu **tła** zadania są zalecane dla asynchronicznego uruchamiania zadań, o ile nie muszą tej funkcji hello **pierwszego planu** zadań.</span><span class="sxs-lookup"><span data-stu-id="23261-228">For this reason, **background** tasks are recommended for asynchronous startup tasks unless you need that feature of hello **foreground** task.</span></span>

### <a name="end-batch-files-with-exit-b-0"></a><span data-ttu-id="23261-229">Pliki wsadowe zakończenia z /B zakończenia 0</span><span class="sxs-lookup"><span data-stu-id="23261-229">End batch files with EXIT /B 0</span></span>
<span data-ttu-id="23261-230">Witaj roli uruchamia się tylko jeśli hello **errorlevel** z każdej z prostego uruchamiania zadań wynosi zero.</span><span class="sxs-lookup"><span data-stu-id="23261-230">hello role will only start if hello **errorlevel** from each of your simple startup task is zero.</span></span> <span data-ttu-id="23261-231">Nie wszystkie programy ustawić hello **errorlevel** (kod zakończenia) poprawnie, więc plik wsadowy hello powinna kończyć `EXIT /B 0` Jeżeli wszystko działa prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="23261-231">Not all programs set hello **errorlevel** (exit code) correctly, so hello batch file should end with an `EXIT /B 0` if everything ran correctly.</span></span>

<span data-ttu-id="23261-232">Brak `EXIT /B 0` na powitania koniec pliku wsadowego uruchamiania jest częstą przyczyną ról, które nie są uruchamiane.</span><span class="sxs-lookup"><span data-stu-id="23261-232">A missing `EXIT /B 0` at hello end of a startup batch file is a common cause of roles that do not start.</span></span>

> [!NOTE]
> <span data-ttu-id="23261-233">I zaobserwowany tej partii zagnieżdżone pliki czasami rozłączaj po użyciu hello `/B` parametru.</span><span class="sxs-lookup"><span data-stu-id="23261-233">I've noticed that nested batch files sometimes hang when using hello `/B` parameter.</span></span> <span data-ttu-id="23261-234">Możesz się upewnić, że ten problem zawieszenie nie odbywa się jeśli inny plik wsadowy wymaga bieżącego pliku wsadowego, takich jak użycie hello toomake [otoki dziennika](#always-log-startup-activities).</span><span class="sxs-lookup"><span data-stu-id="23261-234">You may want toomake sure that this hang problem does not happen if another batch file calls your current batch file, like if you use hello [log wrapper](#always-log-startup-activities).</span></span> <span data-ttu-id="23261-235">W przypadku pominięcia hello `/B` parametru w tym przypadku.</span><span class="sxs-lookup"><span data-stu-id="23261-235">You can omit hello `/B` parameter in this case.</span></span>
> 
> 

### <a name="expect-startup-tasks-toorun-more-than-once"></a><span data-ttu-id="23261-236">Oczekiwane uruchamiania zadań toorun więcej niż raz</span><span class="sxs-lookup"><span data-stu-id="23261-236">Expect startup tasks toorun more than once</span></span>
<span data-ttu-id="23261-237">Nie wszystkie odtwarza roli obejmować ponowne uruchomienie komputera, ale wszystkie odtwarza roli obejmują uruchomione wszystkie zadania uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="23261-237">Not all role recycles include a reboot, but all role recycles include running all startup tasks.</span></span> <span data-ttu-id="23261-238">Oznacza to, że uruchamiania zadań musi być możliwe toorun wielokrotnie między uruchamiany ponownie bez problemów.</span><span class="sxs-lookup"><span data-stu-id="23261-238">This means that startup tasks must be able toorun multiple times between reboots without any problems.</span></span> <span data-ttu-id="23261-239">Jest to omówione w hello [powyższej sekcji](#detect-that-your-task-has-already-run).</span><span class="sxs-lookup"><span data-stu-id="23261-239">This is discussed in hello [preceding section](#detect-that-your-task-has-already-run).</span></span>

### <a name="use-local-storage-toostore-files-that-must-be-accessed-in-hello-role"></a><span data-ttu-id="23261-240">Użyj magazynu lokalnego toostore pliki, które muszą być dostępne w roli hello</span><span class="sxs-lookup"><span data-stu-id="23261-240">Use local storage toostore files that must be accessed in hello role</span></span>
<span data-ttu-id="23261-241">Toocopy lub tworzenie pliku podczas uruchamiania zadania następnie jest dostępny tooyour roli, a następnie tego pliku muszą być umieszczone w lokalnej pamięci masowej.</span><span class="sxs-lookup"><span data-stu-id="23261-241">If you want toocopy or create a file during your startup task that is then accessible tooyour role, then that file must be placed in local storage.</span></span> <span data-ttu-id="23261-242">Zobacz hello [powyższej sekcji](#create-files-in-local-storage-from-a-startup-task).</span><span class="sxs-lookup"><span data-stu-id="23261-242">See hello [preceding section](#create-files-in-local-storage-from-a-startup-task).</span></span>

## <a name="next-steps"></a><span data-ttu-id="23261-243">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="23261-243">Next steps</span></span>
<span data-ttu-id="23261-244">Przejrzyj chmury hello [z modelu i pakietu](cloud-services-model-and-package.md)</span><span class="sxs-lookup"><span data-stu-id="23261-244">Review hello cloud [service model and package](cloud-services-model-and-package.md)</span></span>

<span data-ttu-id="23261-245">Dowiedz się więcej na temat [zadania](cloud-services-startup-tasks.md) pracy.</span><span class="sxs-lookup"><span data-stu-id="23261-245">Learn more about how [Tasks](cloud-services-startup-tasks.md) work.</span></span>

<span data-ttu-id="23261-246">[Tworzenie i wdrażanie](cloud-services-how-to-create-deploy-portal.md) pakietu usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="23261-246">[Create and deploy](cloud-services-how-to-create-deploy-portal.md) your cloud service package.</span></span>

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
