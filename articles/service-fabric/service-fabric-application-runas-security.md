---
title: "aaaLearn o zasady zabezpieczeń Azure mikrousług | Dokumentacja firmy Microsoft"
description: "Omówienie jak toorun aplikacji usługi Service Fabric, w obszarze kont zabezpieczeń lokalnych i systemu, w tym hello SetupEntry punktu, gdzie aplikacja musi tooperform niektóre uprzywilejowany akcji przed rozpoczęciem"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 4242a1eb-a237-459b-afbf-1e06cfa72732
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: mfussell
ms.openlocfilehash: f5afba69e09aa4f3c9efa4d3efc6995c813a1f71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-security-policies-for-your-application"></a><span data-ttu-id="89b88-103">Konfigurowanie zasad zabezpieczeń aplikacji</span><span class="sxs-lookup"><span data-stu-id="89b88-103">Configure security policies for your application</span></span>
<span data-ttu-id="89b88-104">Za pomocą usługi Azure Service Fabric, można zabezpieczyć aplikacji uruchomionych w klastrze hello w obszarze konta innego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="89b88-104">By using Azure Service Fabric, you can secure applications that are running in hello cluster under different user accounts.</span></span> <span data-ttu-id="89b88-105">Sieć szkieletowa usług pomaga również hello bezpiecznych zasobów, które są używane przez aplikacje w czasie hello wdrożenia na kontach użytkowników hello — na przykład, plików, katalogów i certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="89b88-105">Service Fabric also helps secure hello resources that are used by applications at hello time of deployment under hello user accounts--for example, files, directories, and certificates.</span></span> <span data-ttu-id="89b88-106">Dzięki temu uruchamianie aplikacji, nawet w środowisku hostowanej udostępnionego bardziej bezpieczne od siebie nawzajem.</span><span class="sxs-lookup"><span data-stu-id="89b88-106">This makes running applications, even in a shared hosted environment, more secure from one another.</span></span>

<span data-ttu-id="89b88-107">Domyślnie aplikacje sieci szkieletowej usług działać w ramach konta hello, działającą hello proces Fabric.exe.</span><span class="sxs-lookup"><span data-stu-id="89b88-107">By default, Service Fabric applications run under hello account that hello Fabric.exe process runs under.</span></span> <span data-ttu-id="89b88-108">Usługi sieć szkieletowa dostępne są także możliwość hello toorun aplikacji w ramach konta użytkownika lokalnego lub konta system lokalny, które jest określone w manifeście aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="89b88-108">Service Fabric also provides hello capability toorun applications under a local user account or local system account, which is specified within hello application manifest.</span></span> <span data-ttu-id="89b88-109">Obsługiwany system lokalny typy kont to **LocalUser**, **NetworkService**, **Usługa lokalna**, i **LocalSystem**.</span><span class="sxs-lookup"><span data-stu-id="89b88-109">Supported local system account types are **LocalUser**, **NetworkService**, **LocalService**, and **LocalSystem**.</span></span>

 <span data-ttu-id="89b88-110">Jeśli korzystasz z sieci szkieletowej usług w systemie Windows Server w centrum danych przy użyciu hello Autonomiczny Instalator rozszerzenia, można użyć konta domeny usługi Active Directory, łącznie z konta usług zarządzane przez grupę.</span><span class="sxs-lookup"><span data-stu-id="89b88-110">When you're running Service Fabric on Windows Server in your datacenter by using hello standalone installer, you can use Active Directory domain accounts, including group managed service accounts.</span></span>

<span data-ttu-id="89b88-111">Można zdefiniować i Utwórz grupy użytkowników, dzięki czemu można dodać jeden lub więcej użytkowników toobe grupy tooeach zarządza się razem.</span><span class="sxs-lookup"><span data-stu-id="89b88-111">You can define and create user groups so that one or more users can be added tooeach group toobe managed together.</span></span> <span data-ttu-id="89b88-112">Jest to przydatne, gdy jest wielu użytkowników do innej usługi, punkty wejścia i muszą toohave niektórych typowych uprawnień, które są dostępne na poziomie grupy hello.</span><span class="sxs-lookup"><span data-stu-id="89b88-112">This is useful when there are multiple users for different service entry points and they need toohave certain common privileges that are available at hello group level.</span></span>

## <a name="configure-hello-policy-for-a-service-setup-entry-point"></a><span data-ttu-id="89b88-113">Konfigurowanie zasad powitania dla punktu wejścia instalacji usługi</span><span class="sxs-lookup"><span data-stu-id="89b88-113">Configure hello policy for a service setup entry point</span></span>
<span data-ttu-id="89b88-114">Zgodnie z opisem w hello [model aplikacji](service-fabric-application-model.md), hello punktu wejścia instalacji **SetupEntryPoint**, to punkt wejścia uprzywilejowanych uruchamiane przy użyciu hello same poświadczenia jako sieci szkieletowej usług (zazwyczaj hello *NetworkService* konta) przed innymi punktu wejścia.</span><span class="sxs-lookup"><span data-stu-id="89b88-114">As described in hello [application model](service-fabric-application-model.md), hello setup entry point, **SetupEntryPoint**, is a privileged entry point that runs with hello same credentials as Service Fabric (typically hello *NetworkService* account) before any other entry point.</span></span> <span data-ttu-id="89b88-115">plik wykonywalny Hello, który jest określony przez **punktu wejścia** jest zazwyczaj hello długotrwałe usługi hosta.</span><span class="sxs-lookup"><span data-stu-id="89b88-115">hello executable that is specified by **EntryPoint** is typically hello long-running service host.</span></span> <span data-ttu-id="89b88-116">Więc o punktu wejścia instalacji oddzielnych pozwala uniknąć konieczności hosta usługi hello toorun pliku wykonywalnego z wysokiego poziomu uprawnień przez dłuższy czas.</span><span class="sxs-lookup"><span data-stu-id="89b88-116">So having a separate setup entry point avoids having toorun hello service host executable with high privileges for extended periods of time.</span></span> <span data-ttu-id="89b88-117">Witaj wykonywalnego który **punktu wejścia** określa po zakończeniu **SetupEntryPoint** kończy się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="89b88-117">hello executable that **EntryPoint** specifies is run after **SetupEntryPoint** exits successfully.</span></span> <span data-ttu-id="89b88-118">Witaj Wynikowy proces jest monitorowane i ponownie uruchomione i ponownie rozpoczyna się od **SetupEntryPoint** Jeśli kiedykolwiek kończy lub ulegnie awarii.</span><span class="sxs-lookup"><span data-stu-id="89b88-118">hello resulting process is monitored and restarted, and begins again with **SetupEntryPoint** if it ever terminates or crashes.</span></span>

<span data-ttu-id="89b88-119">następujące Hello to przykład manifestu usługi simple czy pokazuje hello SetupEntryPoint i hello główny punkt wejścia dla usługi hello.</span><span class="sxs-lookup"><span data-stu-id="89b88-119">hello following is a simple service manifest example that shows hello SetupEntryPoint and hello main EntryPoint for hello service.</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ServiceManifest Name="MyServiceManifest" Version="SvcManifestVersion1" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Description>An example service manifest</Description>
  <ServiceTypes>
    <StatelessServiceType ServiceTypeName="MyServiceType" />
  </ServiceTypes>
  <CodePackage Name="Code" Version="1.0.0">
    <SetupEntryPoint>
      <ExeHost>
        <Program>MySetup.bat</Program>
        <WorkingFolder>CodePackage</WorkingFolder>
      </ExeHost>
    </SetupEntryPoint>
    <EntryPoint>
      <ExeHost>
        <Program>MyServiceHost.exe</Program>
      </ExeHost>
    </EntryPoint>
  </CodePackage>
  <ConfigPackage Name="Config" Version="1.0.0" />
</ServiceManifest>
```

### <a name="configure-hello-policy-by-using-a-local-account"></a><span data-ttu-id="89b88-120">Konfigurowanie zasad hello za pomocą konta lokalnego</span><span class="sxs-lookup"><span data-stu-id="89b88-120">Configure hello policy by using a local account</span></span>
<span data-ttu-id="89b88-121">Po skonfigurowaniu hello usługi toohave punktu wejścia instalacji można zmienić uprawnienia zabezpieczeń hello, które zostanie uruchomiony w w manifeście aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="89b88-121">After you configure hello service toohave a setup entry point, you can change hello security permissions that it runs under in hello application manifest.</span></span> <span data-ttu-id="89b88-122">Witaj poniższy przykład pokazuje, jak tooconfigure hello toorun usługi, w obszarze uprawnień konta użytkownika administrator.</span><span class="sxs-lookup"><span data-stu-id="89b88-122">hello following example shows how tooconfigure hello service toorun under user administrator account privileges.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="MyApplicationType" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MyServiceTypePkg" ServiceManifestVersion="1.0.0" />
      <ConfigOverrides />
      <Policies>
         <RunAsPolicy CodePackageRef="Code" UserRef="SetupAdminUser" EntryPointType="Setup" />
      </Policies>
   </ServiceManifestImport>
   <Principals>
      <Users>
         <User Name="SetupAdminUser">
            <MemberOf>
               <SystemGroup Name="Administrators" />
            </MemberOf>
         </User>
      </Users>
   </Principals>
</ApplicationManifest>
```

<span data-ttu-id="89b88-123">Najpierw utwórz **podmiotów** sekcji przy użyciu nazwy użytkownika, takie jak SetupAdminUser.</span><span class="sxs-lookup"><span data-stu-id="89b88-123">First, create a **Principals** section with a user name, such as SetupAdminUser.</span></span> <span data-ttu-id="89b88-124">Oznacza to, że użytkownik hello jest elementem członkowskim grupy hello Administratorzy systemu.</span><span class="sxs-lookup"><span data-stu-id="89b88-124">This indicates that hello user is a member of hello Administrators system group.</span></span>

<span data-ttu-id="89b88-125">Następnie w obszarze hello **ServiceManifestImport** skonfiguruj tooapply zasad zbyt tego podmiotu zabezpieczeń**SetupEntryPoint**.</span><span class="sxs-lookup"><span data-stu-id="89b88-125">Next, under hello **ServiceManifestImport** section, configure a policy tooapply this principal too**SetupEntryPoint**.</span></span> <span data-ttu-id="89b88-126">To informuje usługi sieć szkieletowa który hello **MySetup.bat** uruchomieniu pliku, powinien być `RunAs` z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="89b88-126">This tells Service Fabric that when hello **MySetup.bat** file is run, it should be `RunAs` with administrator privileges.</span></span> <span data-ttu-id="89b88-127">Biorąc pod uwagę, że masz *nie* zastosować zasady toohello główny punkt wejścia, kod hello w **MyServiceHost.exe** działa w systemie hello **NetworkService** konta.</span><span class="sxs-lookup"><span data-stu-id="89b88-127">Given that you have *not* applied a policy toohello main entry point, hello code in **MyServiceHost.exe** runs under hello system **NetworkService** account.</span></span> <span data-ttu-id="89b88-128">To konto domyślne hello, które wszystkich punktów wejścia usługi są uruchamiane jako.</span><span class="sxs-lookup"><span data-stu-id="89b88-128">This is hello default account that all service entry points are run as.</span></span>

<span data-ttu-id="89b88-129">Teraz Dodajmy hello pliku MySetup.bat toohello programu Visual Studio projektu tootest hello uprawnienia administratora.</span><span class="sxs-lookup"><span data-stu-id="89b88-129">Let's now add hello file MySetup.bat toohello Visual Studio project tootest hello administrator privileges.</span></span> <span data-ttu-id="89b88-130">W programie Visual Studio kliknij prawym przyciskiem myszy projekt usługi hello i Dodaj nowy plik o nazwie MySetup.bat.</span><span class="sxs-lookup"><span data-stu-id="89b88-130">In Visual Studio, right-click hello service project and add a new file called MySetup.bat.</span></span>

<span data-ttu-id="89b88-131">Następnie sprawdź, czy plik MySetup.bat hello jest uwzględniona w pakiecie usługi hello.</span><span class="sxs-lookup"><span data-stu-id="89b88-131">Next, ensure that hello MySetup.bat file is included in hello service package.</span></span> <span data-ttu-id="89b88-132">Domyślnie nie jest.</span><span class="sxs-lookup"><span data-stu-id="89b88-132">By default, it is not.</span></span> <span data-ttu-id="89b88-133">Wybierz plik hello, kliknij prawym przyciskiem myszy menu kontekstowe hello tooget i wybierz **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="89b88-133">Select hello file, right-click tooget hello context menu, and choose **Properties**.</span></span> <span data-ttu-id="89b88-134">Okno dialogowe właściwości hello, upewnij się, że **skopiuj tooOutput katalogu** ustawiono zbyt**Kopiuj, jeśli nowszy**.</span><span class="sxs-lookup"><span data-stu-id="89b88-134">In hello Properties dialog box, ensure that **Copy tooOutput Directory** is set too**Copy if newer**.</span></span> <span data-ttu-id="89b88-135">Zobacz hello następującego zrzutu ekranu.</span><span class="sxs-lookup"><span data-stu-id="89b88-135">See hello following screenshot.</span></span>

![Visual Studio CopyToOutput SetupEntryPoint pliku wsadowego][image1]

<span data-ttu-id="89b88-137">Teraz Otwórz plik MySetup.bat hello i Dodaj hello następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="89b88-137">Now open hello MySetup.bat file and add hello following commands:</span></span>

```
REM Set a system environment variable. This requires administrator privilege
setx -m TestVariable "MyValue"
echo System TestVariable set too> out.txt
echo %TestVariable% >> out.txt

REM toodelete this system variable us
REM REG delete "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Environment" /v TestVariable /f
```

<span data-ttu-id="89b88-138">Następnie tworzenia i wdrażania hello rozwiązania tooa lokalny klaster projektowy.</span><span class="sxs-lookup"><span data-stu-id="89b88-138">Next, build and deploy hello solution tooa local development cluster.</span></span> <span data-ttu-id="89b88-139">Po uruchomieniu usługi hello, jak pokazano w narzędziu Service Fabric Explorer, można zauważyć, że plik MySetup.bat hello zakończyła się pomyślnie na dwa sposoby.</span><span class="sxs-lookup"><span data-stu-id="89b88-139">After hello service has started, as shown in Service Fabric Explorer, you can see that hello MySetup.bat file was successful in a two ways.</span></span> <span data-ttu-id="89b88-140">Otwórz wiersz polecenia programu PowerShell i wpisz:</span><span class="sxs-lookup"><span data-stu-id="89b88-140">Open a PowerShell command prompt and type:</span></span>

```
PS C:\ [Environment]::GetEnvironmentVariable("TestVariable","Machine")
MyValue
```

<span data-ttu-id="89b88-141">Zanotuj nazwę hello hello węzła, gdy usługa hello została wdrożona i uruchomić w narzędziu Service Fabric Explorer — na przykład 2 węzła.</span><span class="sxs-lookup"><span data-stu-id="89b88-141">Then, note hello name of hello node where hello service was deployed and started in Service Fabric Explorer--for example, Node 2.</span></span> <span data-ttu-id="89b88-142">Następnie przejdź toohello wystąpienia pracy folderu toofind hello out.txt pliku aplikacji pokazujący wartość hello **TestVariable**.</span><span class="sxs-lookup"><span data-stu-id="89b88-142">Next, navigate toohello application instance work folder toofind hello out.txt file that shows hello value of **TestVariable**.</span></span> <span data-ttu-id="89b88-143">Na przykład, jeśli ta usługa została wdrożonej tooNode 2, następnie przejdź toothis ścieżkę hello **MyApplicationType**:</span><span class="sxs-lookup"><span data-stu-id="89b88-143">For example, if this service was deployed tooNode 2, then you can go toothis path for hello **MyApplicationType**:</span></span>

```
C:\SfDevCluster\Data\_App\Node.2\MyApplicationType_App\work\out.txt
```

### <a name="configure-hello-policy-by-using-local-system-accounts"></a><span data-ttu-id="89b88-144">Konfigurowanie zasad hello przy użyciu konta systemu lokalnego</span><span class="sxs-lookup"><span data-stu-id="89b88-144">Configure hello policy by using local system accounts</span></span>
<span data-ttu-id="89b88-145">Często jest preferowana toorun hello uruchomienia skryptu przy użyciu konta systemu lokalnego, a nie konta administratora.</span><span class="sxs-lookup"><span data-stu-id="89b88-145">Often, it's preferable toorun hello startup script by using a local system account rather than an administrator account.</span></span> <span data-ttu-id="89b88-146">Uruchamianie zasad RunAs hello jako członek grupy Administratorzy zwykle nie działa prawidłowo, ponieważ maszyny ma dostęp kontroli użytkownika (UAC) domyślnie włączone powitalne.</span><span class="sxs-lookup"><span data-stu-id="89b88-146">Running hello RunAs policy as a member of hello Administrators group typically doesn’t work well because machines have User Access Control (UAC) enabled by default.</span></span> <span data-ttu-id="89b88-147">W takich przypadkach **hello zaleca hello toorun SetupEntryPoint jako LocalSystem, zamiast jako grupa tooAdministrators dodano użytkownika lokalnego**.</span><span class="sxs-lookup"><span data-stu-id="89b88-147">In such cases, **hello recommendation is toorun hello SetupEntryPoint as LocalSystem, instead of as a local user added tooAdministrators group**.</span></span> <span data-ttu-id="89b88-148">Witaj poniższy przykład przedstawia toorun SetupEntryPoint hello ustawienie jako system lokalny:</span><span class="sxs-lookup"><span data-stu-id="89b88-148">hello following example shows setting hello SetupEntryPoint toorun as LocalSystem:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="MyApplicationType" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MyServiceTypePkg" ServiceManifestVersion="1.0.0" />
      <ConfigOverrides />
      <Policies>
         <RunAsPolicy CodePackageRef="Code" UserRef="SetupLocalSystem" EntryPointType="Setup" />
      </Policies>
   </ServiceManifestImport>
   <Principals>
      <Users>
         <User Name="SetupLocalSystem" AccountType="LocalSystem" />
      </Users>
   </Principals>
</ApplicationManifest>
```

## <a name="start-powershell-commands-from-a-setup-entry-point"></a><span data-ttu-id="89b88-149">Uruchom polecenia programu PowerShell z punktu wejścia instalacji</span><span class="sxs-lookup"><span data-stu-id="89b88-149">Start PowerShell commands from a setup entry point</span></span>
<span data-ttu-id="89b88-150">toorun programu PowerShell z hello **SetupEntryPoint** punktu, możesz uruchomić **PowerShell.exe** w pliku wsadowego, który wskazuje tooa PowerShell plików.</span><span class="sxs-lookup"><span data-stu-id="89b88-150">toorun PowerShell from hello **SetupEntryPoint** point, you can run **PowerShell.exe** in a batch file that points tooa PowerShell file.</span></span> <span data-ttu-id="89b88-151">Najpierw należy dodać projekt usługi toohello plik programu PowerShell — na przykład **MySetup.ps1**.</span><span class="sxs-lookup"><span data-stu-id="89b88-151">First, add a PowerShell file toohello service project--for example, **MySetup.ps1**.</span></span> <span data-ttu-id="89b88-152">Pamiętaj tooset hello *Kopiuj, jeśli nowszy* właściwości, czy plik hello znajduje się również w pakiecie usługi hello.</span><span class="sxs-lookup"><span data-stu-id="89b88-152">Remember tooset hello *Copy if newer* property so that hello file is also included in hello service package.</span></span> <span data-ttu-id="89b88-153">Witaj poniższy przykład przedstawia przykładowy plik partii, która rozpoczyna się plik programu PowerShell o nazwie MySetup.ps1, który określa zmienną środowiskową systemu o nazwie **TestVariable**.</span><span class="sxs-lookup"><span data-stu-id="89b88-153">hello following example shows a sample batch file that starts a PowerShell file called MySetup.ps1, which sets a system environment variable called **TestVariable**.</span></span>

<span data-ttu-id="89b88-154">Toostart MySetup.bat plik programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="89b88-154">MySetup.bat toostart a PowerShell file:</span></span>

```
powershell.exe -ExecutionPolicy Bypass -Command ".\MySetup.ps1"
```

<span data-ttu-id="89b88-155">W pliku programu PowerShell hello Dodaj powitania po tooset zmienną środowiskową systemu:</span><span class="sxs-lookup"><span data-stu-id="89b88-155">In hello PowerShell file, add hello following tooset a system environment variable:</span></span>

```
[Environment]::SetEnvironmentVariable("TestVariable", "MyValue", "Machine")
[Environment]::GetEnvironmentVariable("TestVariable","Machine") > out.txt
```

> [!NOTE]
> <span data-ttu-id="89b88-156">Domyślnie podczas uruchamiania pliku wsadowego hello wygląda w folderze aplikacji hello o nazwie **pracy** plików.</span><span class="sxs-lookup"><span data-stu-id="89b88-156">By default, when hello batch file runs, it looks at hello application folder called **work** for files.</span></span> <span data-ttu-id="89b88-157">W takim przypadku po uruchomieniu MySetup.bat chcemy tego hello toofind MySetup.ps1 w pliku hello sam folder, który jest aplikacji hello **pakietu kodu** folderu.</span><span class="sxs-lookup"><span data-stu-id="89b88-157">In this case, when MySetup.bat runs, we want this toofind hello MySetup.ps1 file in hello same folder, which is hello application **code package** folder.</span></span> <span data-ttu-id="89b88-158">toochange tego folderu, folder roboczy hello zestawu:</span><span class="sxs-lookup"><span data-stu-id="89b88-158">toochange this folder, set hello working folder:</span></span>
> 
> 

```xml
<SetupEntryPoint>
    <ExeHost>
    <Program>MySetup.bat</Program>
    <WorkingFolder>CodePackage</WorkingFolder>
    </ExeHost>
</SetupEntryPoint>
```

## <a name="use-console-redirection-for-local-debugging"></a><span data-ttu-id="89b88-159">Użyj konsoli dla debugowania lokalnego</span><span class="sxs-lookup"><span data-stu-id="89b88-159">Use console redirection for local debugging</span></span>
<span data-ttu-id="89b88-160">Czasami jest przydatne toosee dane wyjściowe konsoli hello uruchamiania skryptu na potrzeby debugowania.</span><span class="sxs-lookup"><span data-stu-id="89b88-160">Occasionally, it's useful toosee hello console output from running a script for debugging purposes.</span></span> <span data-ttu-id="89b88-161">toodo, można ustawić zasad przekierowania konsoli, który zapisuje plik tooa wyjściowy hello.</span><span class="sxs-lookup"><span data-stu-id="89b88-161">toodo this, you can set a console redirection policy, which writes hello output tooa file.</span></span> <span data-ttu-id="89b88-162">Witaj plik wyjściowy nosi nazwę folderu aplikacji napisanych toohello **dziennika** w węźle hello, gdzie aplikacja hello jest wdrożony i uruchom.</span><span class="sxs-lookup"><span data-stu-id="89b88-162">hello file output is written toohello application folder called **log** on hello node where hello application is deployed and run.</span></span> <span data-ttu-id="89b88-163">(Zobacz gdzie toofind to w poprzedzających przykład hello.)</span><span class="sxs-lookup"><span data-stu-id="89b88-163">(See where toofind this in hello preceding example.)</span></span>

> [!WARNING]
> <span data-ttu-id="89b88-164">Nigdy nie używaj zasad przekierowania konsoli hello w aplikacji, która jest wdrożony w środowisku produkcyjnym, ponieważ może to mieć wpływ na powitania aplikacji w tryb failover.</span><span class="sxs-lookup"><span data-stu-id="89b88-164">Never use hello console redirection policy in an application that is deployed in production because this can affect hello application failover.</span></span> <span data-ttu-id="89b88-165">*Tylko* użyć tej funkcji dla rozwoju lokalnych i debugowania.</span><span class="sxs-lookup"><span data-stu-id="89b88-165">*Only* use this for local development and debugging purposes.</span></span>  
> 
> 

<span data-ttu-id="89b88-166">Witaj poniższy przykład przedstawia przekierowywania konsoli hello ustawienie z wartością FileRetentionCount:</span><span class="sxs-lookup"><span data-stu-id="89b88-166">hello following example shows setting hello console redirection with a FileRetentionCount value:</span></span>

```xml
<SetupEntryPoint>
    <ExeHost>
    <Program>MySetup.bat</Program>
    <WorkingFolder>CodePackage</WorkingFolder>
    <ConsoleRedirection FileRetentionCount="10"/>
    </ExeHost>
</SetupEntryPoint>
```

<span data-ttu-id="89b88-167">Jeśli zmienisz teraz hello MySetup.ps1 pliku toowrite **Echo** polecenie to zapisze plik wyjściowy toohello na potrzeby debugowania:</span><span class="sxs-lookup"><span data-stu-id="89b88-167">If you now change hello MySetup.ps1 file toowrite an **Echo** command, this will write toohello output file for debugging purposes:</span></span>

```
Echo "Test console redirection which writes toohello application log folder on hello node that hello application is deployed to"
```

<span data-ttu-id="89b88-168">**Po debugowania skryptu, natychmiast usunąć te zasady przekierowania konsoli**.</span><span class="sxs-lookup"><span data-stu-id="89b88-168">**After you debug your script, immediately remove this console redirection policy**.</span></span>

## <a name="configure-a-policy-for-service-code-packages"></a><span data-ttu-id="89b88-169">Konfigurowanie zasad dla pakietów kodu usługi</span><span class="sxs-lookup"><span data-stu-id="89b88-169">Configure a policy for service code packages</span></span>
<span data-ttu-id="89b88-170">W poprzednich krokach hello, przedstawiono sposób tooapply tooSetupEntryPoint zasad RunAs.</span><span class="sxs-lookup"><span data-stu-id="89b88-170">In hello preceding steps, you saw how tooapply a RunAs policy tooSetupEntryPoint.</span></span> <span data-ttu-id="89b88-171">Oto bardziej szczegółowe w sposób toocreate różnych podmiotów zabezpieczeń, które mogą być stosowane jako usługi zasady.</span><span class="sxs-lookup"><span data-stu-id="89b88-171">Let's look a little deeper into how toocreate different principals that can be applied as service policies.</span></span>

### <a name="create-local-user-groups"></a><span data-ttu-id="89b88-172">Tworzenie grup użytkowników lokalnych</span><span class="sxs-lookup"><span data-stu-id="89b88-172">Create local user groups</span></span>
<span data-ttu-id="89b88-173">Można zdefiniować i Utwórz grupy użytkowników pozwalają na użycie jednego lub więcej użytkowników toobe dodano grupę tooa.</span><span class="sxs-lookup"><span data-stu-id="89b88-173">You can define and create user groups that allow one or more users toobe added tooa group.</span></span> <span data-ttu-id="89b88-174">Jest to przydatne, jeśli jest wielu użytkowników do innej usługi, punkty wejścia i muszą toohave niektórych typowych uprawnień, które są dostępne na poziomie grupy hello.</span><span class="sxs-lookup"><span data-stu-id="89b88-174">This is useful if there are multiple users for different service entry points and they need toohave certain common privileges that are available at hello group level.</span></span> <span data-ttu-id="89b88-175">Witaj poniższy przykład przedstawia grupy lokalnej o nazwie **LocalAdminGroup** z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="89b88-175">hello following example shows a local group called **LocalAdminGroup** that has administrator privileges.</span></span> <span data-ttu-id="89b88-176">Dwóch użytkowników, Customer1 i Customer2, zostają członkami tej grupy lokalnej.</span><span class="sxs-lookup"><span data-stu-id="89b88-176">Two users, Customer1 and Customer2, are made members of this local group.</span></span>

```xml
<Principals>
 <Groups>
   <Group Name="LocalAdminGroup">
     <Membership>
       <SystemGroup Name="Administrators"/>
     </Membership>
   </Group>
 </Groups>
  <Users>
     <User Name="Customer1">
        <MemberOf>
           <Group NameRef="LocalAdminGroup" />
        </MemberOf>
     </User>
    <User Name="Customer2">
      <MemberOf>
        <Group NameRef="LocalAdminGroup" />
      </MemberOf>
    </User>
  </Users>
</Principals>
```

### <a name="create-local-users"></a><span data-ttu-id="89b88-177">Tworzenie użytkowników lokalnych</span><span class="sxs-lookup"><span data-stu-id="89b88-177">Create local users</span></span>
<span data-ttu-id="89b88-178">Można utworzyć użytkownika lokalnego, które mogą być używane toohelp bezpiecznego usługi aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="89b88-178">You can create a local user that can be used toohelp secure a service within hello application.</span></span> <span data-ttu-id="89b88-179">Gdy **LocalUser** typ konta jest określone w sekcji podmiotów hello manifestu aplikacji hello, sieć szkieletowa usług tworzy lokalne konta użytkowników na komputerach, w której wdrażana jest aplikacja hello.</span><span class="sxs-lookup"><span data-stu-id="89b88-179">When a **LocalUser** account type is specified in hello principals section of hello application manifest, Service Fabric creates local user accounts on machines where hello application is deployed.</span></span> <span data-ttu-id="89b88-180">Domyślnie te konta nie mają hello tej samej nazwy jak określone w aplikacji hello manifestu (na przykład Customer3 w hello następujące przykładowe).</span><span class="sxs-lookup"><span data-stu-id="89b88-180">By default, these accounts do not have hello same names as those specified in hello application manifest (for example, Customer3 in hello following sample).</span></span> <span data-ttu-id="89b88-181">Zamiast tego są generowane dynamicznie i losowego hasła.</span><span class="sxs-lookup"><span data-stu-id="89b88-181">Instead, they are dynamically generated and have random passwords.</span></span>

```xml
<Principals>
  <Users>
     <User Name="Customer3" AccountType="LocalUser" />
  </Users>
</Principals>
```

<span data-ttu-id="89b88-182">Jeśli aplikacja wymaga czy hello konto użytkownika i hasło być taka sama na wszystkich komputerach (na przykład uwierzytelnianie NTLM tooenable), hello manifestu klastra musi ustawić NTLMAuthenticationEnabled tootrue.</span><span class="sxs-lookup"><span data-stu-id="89b88-182">If an application requires that hello user account and password be same on all machines (for example, tooenable NTLM authentication), hello cluster manifest must set NTLMAuthenticationEnabled tootrue.</span></span> <span data-ttu-id="89b88-183">Witaj manifestu klastra musi również określać NTLMAuthenticationPasswordSecret, który jest używany toogenerate hello tego samego hasła na wszystkich komputerach.</span><span class="sxs-lookup"><span data-stu-id="89b88-183">hello cluster manifest must also specify an NTLMAuthenticationPasswordSecret that is used toogenerate hello same password across all machines.</span></span>

```xml
<Section Name="Hosting">
      <Parameter Name="EndpointProviderEnabled" Value="true"/>
      <Parameter Name="NTLMAuthenticationEnabled" Value="true"/>
      <Parameter Name="NTLMAuthenticationPassworkSecret" Value="******" IsEncrypted="true"/>
 </Section>
```

### <a name="assign-policies-toohello-service-code-packages"></a><span data-ttu-id="89b88-184">Przypisz zasady toohello pakietów kodu usługi</span><span class="sxs-lookup"><span data-stu-id="89b88-184">Assign policies toohello service code packages</span></span>
<span data-ttu-id="89b88-185">Witaj **RunAsPolicy** sekcji **ServiceManifestImport** Określa konto hello z sekcji hello podmiotów zabezpieczeń, który ma być używane toorun pakiet kodu.</span><span class="sxs-lookup"><span data-stu-id="89b88-185">hello **RunAsPolicy** section for a **ServiceManifestImport** specifies hello account from hello principals section that should be used toorun a code package.</span></span> <span data-ttu-id="89b88-186">Kodu manifestu pakietów z usługi hello również kojarzy z kontami użytkowników w sekcji podmiotów hello.</span><span class="sxs-lookup"><span data-stu-id="89b88-186">It also associates code packages from hello service manifest with user accounts in hello principals section.</span></span> <span data-ttu-id="89b88-187">Można to określić dla ustawienia hello lub punkty wejścia głównego, lub możesz określić `All` tooapply on tooboth.</span><span class="sxs-lookup"><span data-stu-id="89b88-187">You can specify this for hello setup or main entry points, or you can specify `All` tooapply it tooboth.</span></span> <span data-ttu-id="89b88-188">Witaj poniższy przykład przedstawia różne zasady są stosowane:</span><span class="sxs-lookup"><span data-stu-id="89b88-188">hello following example shows different policies being applied:</span></span>

```xml
<Policies>
<RunAsPolicy CodePackageRef="Code" UserRef="LocalAdmin" EntryPointType="Setup"/>
<RunAsPolicy CodePackageRef="Code" UserRef="Customer3" EntryPointType="Main"/>
</Policies>
```

<span data-ttu-id="89b88-189">Jeśli **EntryPointType** nie zostanie określony, domyślnie hello jest zaznaczona tooEntryPointType = "Main".</span><span class="sxs-lookup"><span data-stu-id="89b88-189">If **EntryPointType** is not specified, hello default is set tooEntryPointType=”Main”.</span></span> <span data-ttu-id="89b88-190">Określanie **SetupEntryPoint** jest szczególnie przydatne, gdy trzeba toorun pewnych operacji ustawienia wysokiego poziomu przy użyciu konta system.</span><span class="sxs-lookup"><span data-stu-id="89b88-190">Specifying **SetupEntryPoint** is especially useful when you want toorun certain high-privilege setup operations under a system account.</span></span> <span data-ttu-id="89b88-191">Kod obsługi rzeczywistych Hello można uruchamiany na koncie dolna uprawnień.</span><span class="sxs-lookup"><span data-stu-id="89b88-191">hello actual service code can run under a lower-privilege account.</span></span>

### <a name="apply-a-default-policy-tooall-service-code-packages"></a><span data-ttu-id="89b88-192">Zastosowanie pakietów kodu usługi tooall domyślne zasady</span><span class="sxs-lookup"><span data-stu-id="89b88-192">Apply a default policy tooall service code packages</span></span>
<span data-ttu-id="89b88-193">Użyj hello **DefaultRunAsPolicy** toospecify sekcji domyślne konto użytkownika dla wszystkich pakietów kodu, które nie mają określonej **RunAsPolicy** zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="89b88-193">You use hello **DefaultRunAsPolicy** section toospecify a default user account for all code packages that don’t have a specific **RunAsPolicy** defined.</span></span> <span data-ttu-id="89b88-194">Jeśli większość hello pakiety kodu, które są określone w manifeście usługi hello używany przez aplikację muszą toorun w obszarze hello tego samego użytkownika, powitalne aplikacji można zdefiniować tylko domyślnych zasad RunAs przy użyciu tego konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="89b88-194">If most of hello code packages that are specified in hello service manifest used by an application need toorun under hello same user, hello application can just define a default RunAs policy with that user account.</span></span> <span data-ttu-id="89b88-195">Witaj poniższy przykład określa, że jeśli pakiet kodu nie ma **RunAsPolicy** określony pakiet kodu hello należy uruchamiać w ramach hello **MyDefaultAccount** określone w sekcji podmiotów hello.</span><span class="sxs-lookup"><span data-stu-id="89b88-195">hello following example specifies that if a code package does not have a **RunAsPolicy** specified, hello code package should run under hello **MyDefaultAccount** specified in hello principals section.</span></span>

```xml
<Policies>
  <DefaultRunAsPolicy UserRef="MyDefaultAccount"/>
</Policies>
```
### <a name="use-an-active-directory-domain-group-or-user"></a><span data-ttu-id="89b88-196">Użyj grupy domeny usługi Active Directory lub użytkownika</span><span class="sxs-lookup"><span data-stu-id="89b88-196">Use an Active Directory domain group or user</span></span>
<span data-ttu-id="89b88-197">W przypadku wystąpienia usługi Service Fabric, który został zainstalowany w systemie Windows Server przy użyciu hello Autonomiczny Instalator rozszerzenia można uruchomić usługi hello hello poświadczenia dla konta użytkownika lub grupy usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="89b88-197">For an instance of Service Fabric that was installed on Windows Server by using hello standalone installer, you can run hello service under hello credentials for an Active Directory user or group account.</span></span> <span data-ttu-id="89b88-198">To jest usługa Active Directory lokalnie w domenie, a nie z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="89b88-198">This is Active Directory on-premises within your domain and is not with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="89b88-199">Przy użyciu użytkownika domeny lub grupy, można następnie dostęp do innych zasobów w domenie hello (na przykład udziałów plików), które ma odpowiednie uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="89b88-199">By using a domain user or group, you can then access other resources in hello domain (for example, file shares) that have been granted permissions.</span></span>

<span data-ttu-id="89b88-200">Witaj poniższy przykład przedstawia użytkownika usługi Active Directory o nazwie *TestUser* z ich domeny o nazwie hasła szyfrowane przy użyciu certyfikatu *MyCert*.</span><span class="sxs-lookup"><span data-stu-id="89b88-200">hello following example shows an Active Directory user called *TestUser* with their domain password encrypted by using a certificate called *MyCert*.</span></span> <span data-ttu-id="89b88-201">Można użyć hello `Invoke-ServiceFabricEncryptText` PowerShell polecenie toocreate hello tajny szyfrowania tekstu.</span><span class="sxs-lookup"><span data-stu-id="89b88-201">You can use hello `Invoke-ServiceFabricEncryptText` PowerShell command toocreate hello secret cipher text.</span></span> <span data-ttu-id="89b88-202">Zobacz [Zarządzanie kluczy tajnych w aplikacji usługi Service Fabric](service-fabric-application-secret-management.md) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="89b88-202">See [Managing secrets in Service Fabric applications](service-fabric-application-secret-management.md) for details.</span></span>

<span data-ttu-id="89b88-203">Klucz prywatny hello hello certyfikatu toodecrypt hello hasła toohello komputer lokalny należy wdrożyć przy użyciu metody poza pasmem (na platformie Azure jest za pośrednictwem usługi Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="89b88-203">You must deploy hello private key of hello certificate toodecrypt hello password toohello local machine by using an out-of-band method (in Azure, this is via Azure Resource Manager).</span></span> <span data-ttu-id="89b88-204">Następnie gdy usługa sieć szkieletowa wdraża hello usługi pakietu toohello maszyny, jest klucz tajny hello stanie toodecrypt i (wraz z nazwy użytkownika hello) uwierzytelniania za pomocą usługi Active Directory toorun w ramach tych poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="89b88-204">Then, when Service Fabric deploys hello service package toohello machine, it is able toodecrypt hello secret and (along with hello user name) authenticate with Active Directory toorun under those credentials.</span></span>

```xml
<Principals>
  <Users>
    <User Name="TestUser" AccountType="DomainUser" AccountName="Domain\User" Password="[Put encrypted password here using MyCert certificate]" PasswordEncrypted="true" />
  </Users>
</Principals>
<Policies>
  <DefaultRunAsPolicy UserRef="TestUser" />
  <SecurityAccessPolicies>
    <SecurityAccessPolicy ResourceRef="MyCert" PrincipalRef="TestUser" GrantRights="Full" ResourceType="Certificate" />
  </SecurityAccessPolicies>
</Policies>
<Certificates>
```
### <a name="use-a-group-managed-service-account"></a><span data-ttu-id="89b88-205">Użyj grupy zarządzane konto usługi.</span><span class="sxs-lookup"><span data-stu-id="89b88-205">Use a Group Managed Service Account.</span></span>
<span data-ttu-id="89b88-206">W przypadku wystąpienia usługi Service Fabric, który został zainstalowany w systemie Windows Server przy użyciu hello Autonomiczny Instalator rozszerzenia można uruchomić usługi hello jako grupa kont usług zarządzanych (gMSA).</span><span class="sxs-lookup"><span data-stu-id="89b88-206">For an instance of Service Fabric that was installed on Windows Server by using hello standalone installer, you can run hello service as a group Managed Service Account (gMSA).</span></span> <span data-ttu-id="89b88-207">Należy pamiętać, że jest to usługi Active Directory lokalnie w domenie, a nie z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="89b88-207">Note that this is Active Directory on-premises within your domain and is not with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="89b88-208">Za pomocą grupę nie jest hasłem ani zaszyfrowane hasło przechowywane w hello `Application Manifest`.</span><span class="sxs-lookup"><span data-stu-id="89b88-208">By using a gMSA there is no password or encrypted password stored in hello `Application Manifest`.</span></span>

<span data-ttu-id="89b88-209">Witaj poniższy przykład przedstawia sposób toocreate konto usługi zarządzane przez grupę o nazwie *testu svc$*; sposób toodeploy zarządzania węzłów klastra toohello konta usługi; i jak tooconfigure hello głównej nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="89b88-209">hello following example shows how toocreate a gMSA account called *svc-Test$*; how toodeploy that managed service account toohello cluster nodes; and how tooconfigure hello user principal.</span></span>

##### <a name="prerequisites"></a><span data-ttu-id="89b88-210">Wymagania wstępne.</span><span class="sxs-lookup"><span data-stu-id="89b88-210">Prerequisites.</span></span>
- <span data-ttu-id="89b88-211">Witaj domeny musi mieć klucz główny KDS.</span><span class="sxs-lookup"><span data-stu-id="89b88-211">hello domain needs a KDS root key.</span></span>
- <span data-ttu-id="89b88-212">Witaj domeny musi toobe w systemie Windows Server 2012 lub nowszego poziomu funkcjonalności.</span><span class="sxs-lookup"><span data-stu-id="89b88-212">hello domain needs toobe at a Windows Server 2012 or later functional level.</span></span>

##### <a name="example"></a><span data-ttu-id="89b88-213">Przykład</span><span class="sxs-lookup"><span data-stu-id="89b88-213">Example</span></span>
1. <span data-ttu-id="89b88-214">Poproś administratora domeny usługi active directory Utwórz konto usługi zarządzane przez grupę przy użyciu hello `New-ADServiceAccount` apletu polecenia i upewnij się, że hello `PrincipalsAllowedToRetrieveManagedPassword` zawiera wszystkie węzły klastra sieci szkieletowej usług hello.</span><span class="sxs-lookup"><span data-stu-id="89b88-214">Have an active directory domain administrator create a group managed service account using hello `New-ADServiceAccount` commandlet and ensure that hello `PrincipalsAllowedToRetrieveManagedPassword` includes all of hello service fabric cluster nodes.</span></span> <span data-ttu-id="89b88-215">Należy pamiętać, że `AccountName`, `DnsHostName`, i `ServicePrincipalName` muszą być unikatowe.</span><span class="sxs-lookup"><span data-stu-id="89b88-215">Note that `AccountName`, `DnsHostName`, and `ServicePrincipalName` must be unique.</span></span>
```
New-ADServiceAccount -name svc-Test$ -DnsHostName svc-test.contoso.com  -ServicePrincipalNames http/svc-test.contoso.com -PrincipalsAllowedToRetrieveManagedPassword SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$
```
2. <span data-ttu-id="89b88-216">Na każdym z węzłów klastra sieci szkieletowej usług hello (na przykład `SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$`), zainstalować i przetestować hello gMSA.</span><span class="sxs-lookup"><span data-stu-id="89b88-216">On each of hello service fabric cluster nodes (for example, `SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$`), install and test hello gMSA.</span></span>
```
Add-WindowsFeature RSAT-AD-PowerShell
Install-AdServiceAccount svc-Test$
Test-AdServiceAccount svc-Test$
```
3. <span data-ttu-id="89b88-217">Skonfiguruj hello głównej nazwy użytkownika oraz hello RunAsPolicy tooreference hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="89b88-217">Configure hello User principal, and configure hello RunAsPolicy tooreference hello user.</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="MyApplicationType" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MyServiceTypePkg" ServiceManifestVersion="1.0.0" />
      <ConfigOverrides />
      <Policies>
         <RunAsPolicy CodePackageRef="Code" UserRef="DomaingMSA"/>
      </Policies>
   </ServiceManifestImport>
  <Principals>
    <Users>
      <User Name="DomaingMSA" AccountType="ManagedServiceAccount" AccountName="domain\svc-Test$"/>
    </Users>
  </Principals>
</ApplicationManifest>
```

## <a name="assign-a-security-access-policy-for-http-and-https-endpoints"></a><span data-ttu-id="89b88-218">Przypisać zasady zabezpieczeń dostępu dla punktów końcowych HTTP i HTTPS</span><span class="sxs-lookup"><span data-stu-id="89b88-218">Assign a security access policy for HTTP and HTTPS endpoints</span></span>
<span data-ttu-id="89b88-219">Jeśli stosujesz usługi tooa zasad RunAs i manifestu usługi hello deklaruje punktu końcowego zasobów przy użyciu protokołu hello HTTP, musisz określić **SecurityAccessPolicy** tooensure, że porty przydzielone toothese punkty końcowe są prawidłowo Kontrola dostępu wyświetlane hello konto użytkownika Uruchom jako, które jest uruchamiana usługa hello.</span><span class="sxs-lookup"><span data-stu-id="89b88-219">If you apply a RunAs policy tooa service and hello service manifest declares endpoint resources with hello HTTP protocol, you must specify a **SecurityAccessPolicy** tooensure that ports allocated toothese endpoints are correctly access-control listed for hello RunAs user account that hello service runs under.</span></span> <span data-ttu-id="89b88-220">W przeciwnym razie **http.sys** nie ma dostępu do usługi toohello i uzyskać awarii przy wywołaniach z powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="89b88-220">Otherwise, **http.sys** does not have access toohello service, and you get failures with calls from hello client.</span></span> <span data-ttu-id="89b88-221">Witaj następujący przykład dotyczy hello Customer1 tooan punkt końcowy konta o nazwie **EndpointName**, które zapewnia pełne prawa dostępu.</span><span class="sxs-lookup"><span data-stu-id="89b88-221">hello following example applies hello Customer1 account tooan endpoint called **EndpointName**, which gives it full access rights.</span></span>

```xml
<Policies>
   <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
   <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and hello Endpoint is http -->
   <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
</Policies>
```

<span data-ttu-id="89b88-222">Hello punktu końcowego protokołu HTTPS należy również mieć nazwę hello tooindicate hello certyfikatu tooreturn toohello klienta.</span><span class="sxs-lookup"><span data-stu-id="89b88-222">For hello HTTPS endpoint, you also have tooindicate hello name of hello certificate tooreturn toohello client.</span></span> <span data-ttu-id="89b88-223">Można to zrobić za pomocą **EndpointBindingPolicy**, z certyfikatem hello zdefiniowanej w sekcji certyfikaty w manifeście aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="89b88-223">You can do this by using **EndpointBindingPolicy**, with hello certificate defined in a certificates section in hello application manifest.</span></span>

```xml
<Policies>
   <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
  <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and hello Endpoint is http -->
   <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
  <!--EndpointBindingPolicy is needed if hello EndpointName is secured with https -->
  <EndpointBindingPolicy EndpointRef="EndpointName" CertificateRef="Cert1" />
</Policies
```
## <a name="upgrading-multiple-applications-with-https-endpoints"></a><span data-ttu-id="89b88-224">Uaktualnianie wielu aplikacji z punktów końcowych https</span><span class="sxs-lookup"><span data-stu-id="89b88-224">Upgrading multiple applications with https endpoints</span></span>
<span data-ttu-id="89b88-225">Toobe należy zachować ostrożność nie toouse hello **tego samego portu** dla różnych wystąpień hello tej samej aplikacji przy użyciu protokołu http**s**.</span><span class="sxs-lookup"><span data-stu-id="89b88-225">You need toobe careful not toouse hello **same port** for different instances of hello same application when using http**s**.</span></span> <span data-ttu-id="89b88-226">Przyczyna Hello jest, że sieć szkieletowa usług nie będzie możliwe tooupgrade hello certyfikatu dla jednego z wystąpień aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="89b88-226">hello reason is that Service Fabric won't be able tooupgrade hello cert for one of hello application instances.</span></span> <span data-ttu-id="89b88-227">Na przykład, aplikacja 1 lub aplikacji 2 zarówno tooupgrade ich toocert cert 1, 2.</span><span class="sxs-lookup"><span data-stu-id="89b88-227">For example, if application 1 or application 2 both want tooupgrade their cert 1 toocert 2.</span></span> <span data-ttu-id="89b88-228">W przypadku uaktualniania hello sieci szkieletowej usług może mieć wyczyścić rejestracji certyfikatu 1 hello przy użyciu składnika http.sys nawet hello jest nadal używa jej inna aplikacja.</span><span class="sxs-lookup"><span data-stu-id="89b88-228">When hello upgrade happens, Service Fabric might have cleaned up hello cert 1 registration with http.sys even though hello other application is still using it.</span></span> <span data-ttu-id="89b88-229">tooprevent, sieć szkieletowa usług wykryje, że istnieje już inne wystąpienie aplikacji zarejestrowanych na powitania portu z certyfikatem hello (z powodu toohttp.sys) i operacji hello kończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="89b88-229">tooprevent this, Service Fabric detects that there is already another application instance registered on hello port with hello certificate (due toohttp.sys) and fails hello operation.</span></span>

<span data-ttu-id="89b88-230">Dlatego usługi sieć szkieletowa nie obsługuje uaktualnienia z dwóch różnych usług za pomocą **hello tego samego portu** w innej aplikacji wystąpień.</span><span class="sxs-lookup"><span data-stu-id="89b88-230">Hence Service Fabric does not support upgrading two different services using **hello same port** in different application instances.</span></span> <span data-ttu-id="89b88-231">Innymi słowy, nie można użyć hello sam certyfikat na różnych usług na powitania tego samego portu.</span><span class="sxs-lookup"><span data-stu-id="89b88-231">In other words, you cannot use hello same certificate on different services on hello same port.</span></span> <span data-ttu-id="89b88-232">Jeśli potrzebujesz toohave udostępnionej certyfikatów na powitania sam port, należy tooensure tego hello usług są umieszczane na kilka różnych maszyn z ograniczeń umieszczania.</span><span class="sxs-lookup"><span data-stu-id="89b88-232">If you need toohave a shared certificate on hello same port, you need tooensure that hello services are placed on different machines with placement constraints.</span></span> <span data-ttu-id="89b88-233">Lub należy wziąć pod uwagę przy użyciu portów dynamicznych sieci szkieletowej usług, jeśli to możliwe dla każdej usługi w każdego wystąpienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="89b88-233">Or consider using Service Fabric dynamic ports if possible for each service in each application instance.</span></span> 

<span data-ttu-id="89b88-234">Jeśli widzisz uaktualnienia kończy się niepowodzeniem z protokołu https, błąd ostrzeżenie "hello interfejsu API serwera HTTP systemu Windows nie obsługuje wielu certyfikatów dla aplikacji, które współużytkują port".</span><span class="sxs-lookup"><span data-stu-id="89b88-234">If you see an upgrade fail with https, an error warning saying "hello Windows HTTP Server API does not support multiple certificates for applications that share a port.”</span></span>

## <a name="a-complete-application-manifest-example"></a><span data-ttu-id="89b88-235">W przykładzie manifestu kompletna aplikacja</span><span class="sxs-lookup"><span data-stu-id="89b88-235">A complete application manifest example</span></span>
<span data-ttu-id="89b88-236">powitania po manifest aplikacji zawiera wiele hello różne ustawienia:</span><span class="sxs-lookup"><span data-stu-id="89b88-236">hello following application manifest shows many of hello different settings:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="Application3Type" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <Parameters>
      <Parameter Name="Stateless1_InstanceCount" DefaultValue="-1" />
   </Parameters>
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="Stateless1Pkg" ServiceManifestVersion="1.0.0" />
      <ConfigOverrides />
      <Policies>
         <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
         <RunAsPolicy CodePackageRef="Code" UserRef="LocalAdmin" EntryPointType="Setup" />
        <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and hello Endpoint is http -->
         <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
        <!--EndpointBindingPolicy is needed hello EndpointName is secured with https -->
        <EndpointBindingPolicy EndpointRef="EndpointName" CertificateRef="Cert1" />
     </Policies>
   </ServiceManifestImport>
   <DefaultServices>
      <Service Name="Stateless1">
         <StatelessService ServiceTypeName="Stateless1Type" InstanceCount="[Stateless1_InstanceCount]">
            <SingletonPartition />
         </StatelessService>
      </Service>
   </DefaultServices>
   <Principals>
      <Groups>
         <Group Name="LocalAdminGroup">
            <Membership>
               <SystemGroup Name="Administrators" />
            </Membership>
         </Group>
      </Groups>
      <Users>
         <User Name="LocalAdmin">
            <MemberOf>
               <Group NameRef="LocalAdminGroup" />
            </MemberOf>
         </User>
         <!--Customer1 below create a local account that this service runs under -->
         <User Name="Customer1" />
         <User Name="MyDefaultAccount" AccountType="NetworkService" />
      </Users>
   </Principals>
   <Policies>
      <DefaultRunAsPolicy UserRef="LocalAdmin" />
   </Policies>
   <Certificates>
     <EndpointCertificate Name="Cert1" X509FindValue="FF EE E0 TT JJ DD JJ EE EE XX 23 4T 66 "/>
  </Certificates>
</ApplicationManifest>
```


<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="89b88-237">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="89b88-237">Next steps</span></span>
* [<span data-ttu-id="89b88-238">Zrozumienie modelu aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="89b88-238">Understand hello application model</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="89b88-239">Określ zasoby w manifeście usługi</span><span class="sxs-lookup"><span data-stu-id="89b88-239">Specify resources in a service manifest</span></span>](service-fabric-service-manifest-resources.md)
* [<span data-ttu-id="89b88-240">Wdrażanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="89b88-240">Deploy an application</span></span>](service-fabric-deploy-remove-applications.md)

[image1]: ./media/service-fabric-application-runas-security/copy-to-output.png
