---
title: "aaaCreate Azure role sieć web i procesu roboczego dla programu PHP | Dokumentacja firmy Microsoft"
description: "Przewodnik toocreating PHP sieci web i proces roboczy role usługi w chmurze Azure i konfigurowanie hello środowiska uruchomieniowego języka PHP."
services: 
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9f7ccda0-bd96-4f7b-a7af-fb279a9e975b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 04a6e8c9c379cb0f854645941b6bc7d614bb91f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-php-web-and-worker-roles"></a><span data-ttu-id="f875a-103">Jak toocreate role sieć web i proces roboczy języka PHP</span><span class="sxs-lookup"><span data-stu-id="f875a-103">How toocreate PHP web and worker roles</span></span>
## <a name="overview"></a><span data-ttu-id="f875a-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="f875a-104">Overview</span></span>
<span data-ttu-id="f875a-105">W tym przewodniku opisano sposób toocreate role sieci web lub procesu roboczego PHP w środowisku programowania Windows wybierz określonej wersji programu PHP z hello "wbudowanych" wersje dostępne, zmienić konfigurację PHP hello Włącz rozszerzenia i ponadto wdrożyć tooAzure.</span><span class="sxs-lookup"><span data-stu-id="f875a-105">This guide will show you how toocreate PHP web or worker roles in a Windows development environment, choose a specific version of PHP from hello "built-in" versions available, change hello PHP configuration, enable extensions, and finally, deploy tooAzure.</span></span> <span data-ttu-id="f875a-106">Opisano również sposób tooconfigure sieci web lub procesu roboczego roli toouse środowiska uruchomieniowego języka PHP (z konfiguracji niestandardowej i rozszerzenia) podane.</span><span class="sxs-lookup"><span data-stu-id="f875a-106">It also describes how tooconfigure a web or worker role toouse a PHP runtime (with custom configuration and extensions) that you provide.</span></span>

## <a name="what-are-php-web-and-worker-roles"></a><span data-ttu-id="f875a-107">Co to są role sieć web i proces roboczy PHP?</span><span class="sxs-lookup"><span data-stu-id="f875a-107">What are PHP web and worker roles?</span></span>
<span data-ttu-id="f875a-108">Platforma Azure udostępnia trzy modele obliczeniowe na potrzeby uruchamiania aplikacji: Azure App Service, maszynach wirtualnych platformy Azure i usługi w chmurze Azure.</span><span class="sxs-lookup"><span data-stu-id="f875a-108">Azure provides three compute models for running applications: Azure App Service, Azure Virtual Machines, and Azure Cloud Services.</span></span> <span data-ttu-id="f875a-109">Wszystkie trzy modele obsługują PHP.</span><span class="sxs-lookup"><span data-stu-id="f875a-109">All three models support PHP.</span></span> <span data-ttu-id="f875a-110">Usługi w chmurze, które obejmują role sieć web i proces roboczy, zapewnia *platforma jako usługa (PaaS)*.</span><span class="sxs-lookup"><span data-stu-id="f875a-110">Cloud Services, which includes web and worker roles, provides *platform as a service (PaaS)*.</span></span> <span data-ttu-id="f875a-111">W ramach usługi w chmurze rola sieć web zapewnia dedykowanych sieci web usług Internet Information Services (IIS) aplikacji frontonu sieci web toohost serwera.</span><span class="sxs-lookup"><span data-stu-id="f875a-111">Within a cloud service, a web role provides a dedicated Internet Information Services (IIS) web server toohost front-end web applications.</span></span> <span data-ttu-id="f875a-112">Rola proces roboczy można uruchamiać asynchroniczne, długotrwałe lub ciągłe zadania niezależne interakcji z użytkownikiem lub danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="f875a-112">A worker role can run asynchronous, long-running or perpetual tasks independent of user interaction or input.</span></span>

<span data-ttu-id="f875a-113">Aby uzyskać więcej informacji o tych opcjach, zobacz [obliczeniowe hosting opcji dostarczanych przez platformę Azure](cloud-services/cloud-services-choose-me.md).</span><span class="sxs-lookup"><span data-stu-id="f875a-113">For more information about these options, see [Compute hosting options provided by Azure](cloud-services/cloud-services-choose-me.md).</span></span>

## <a name="download-hello-azure-sdk-for-php"></a><span data-ttu-id="f875a-114">Pobierz hello Azure SDK dla języka PHP</span><span class="sxs-lookup"><span data-stu-id="f875a-114">Download hello Azure SDK for PHP</span></span>
<span data-ttu-id="f875a-115">Witaj [zestaw Azure SDK for PHP] składa się z kilku składników.</span><span class="sxs-lookup"><span data-stu-id="f875a-115">hello [Azure SDK for PHP] consists of several components.</span></span> <span data-ttu-id="f875a-116">W tym artykule będzie korzystać z dwóch z nich: programu Azure PowerShell i hello emulatory platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f875a-116">This article will use two of them: Azure PowerShell and hello Azure emulators.</span></span> <span data-ttu-id="f875a-117">Te dwa składniki można zainstalować za pomocą Instalatora platformy sieci Web firmy Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="f875a-117">These two components can be installed via hello Microsoft Web Platform Installer.</span></span> <span data-ttu-id="f875a-118">Aby uzyskać więcej informacji, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f875a-118">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="create-a-cloud-services-project"></a><span data-ttu-id="f875a-119">Tworzenie projektu usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="f875a-119">Create a Cloud Services project</span></span>
<span data-ttu-id="f875a-120">pierwszym krokiem Hello tworzenie roli sieci web lub procesu roboczego PHP jest toocreate projektu usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="f875a-120">hello first step in creating a PHP web or worker role is toocreate an Azure Service project.</span></span> <span data-ttu-id="f875a-121">projekt usługi Azure służy jako kontener logicznej dla sieci web i proces roboczy ról i zawiera projekt hello [definicji (csdef) usługi] i [konfiguracji usługi (cscfg)] plików.</span><span class="sxs-lookup"><span data-stu-id="f875a-121">an Azure Service project serves as a logical container for web and worker roles, and it contains hello project's [service definition (.csdef)] and [service configuration (.cscfg)] files.</span></span>

<span data-ttu-id="f875a-122">toocreate nowego projektu usługi Azure, uruchom program Azure PowerShell jako administrator i wykonaj hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="f875a-122">toocreate a new Azure Service project, run Azure PowerShell as an administrator, and execute hello following command:</span></span>

    PS C:\>New-AzureServiceProject myProject

<span data-ttu-id="f875a-123">To polecenie spowoduje utworzenie nowego katalogu (`myProject`) toowhich można dodać role sieci web i proces roboczy.</span><span class="sxs-lookup"><span data-stu-id="f875a-123">This command will create a new directory (`myProject`) toowhich you can add web and worker roles.</span></span>

## <a name="add-php-web-or-worker-roles"></a><span data-ttu-id="f875a-124">Dodawanie ról PHP sieci web lub procesu roboczego</span><span class="sxs-lookup"><span data-stu-id="f875a-124">Add PHP web or worker roles</span></span>
<span data-ttu-id="f875a-125">tooadd projektu tooa roli sieci web PHP, uruchom następujące polecenia w katalogu głównym projektu hello hello:</span><span class="sxs-lookup"><span data-stu-id="f875a-125">tooadd a PHP web role tooa project, run hello following command from within hello project's root directory:</span></span>

    PS C:\myProject> Add-AzurePHPWebRole roleName

<span data-ttu-id="f875a-126">Dla roli proces roboczy Użyj tego polecenia:</span><span class="sxs-lookup"><span data-stu-id="f875a-126">For a worker role, use this command:</span></span>

    PS C:\myProject> Add-AzurePHPWorkerRole roleName

> [!NOTE]
> <span data-ttu-id="f875a-127">Witaj `roleName` parametr jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="f875a-127">hello `roleName` parameter is optional.</span></span> <span data-ttu-id="f875a-128">Jeśli zostanie pominięty, będą automatycznie generowane hello nazwy roli.</span><span class="sxs-lookup"><span data-stu-id="f875a-128">If it is omitted, hello role name will be automatically generated.</span></span> <span data-ttu-id="f875a-129">Hello utworzone pierwszego rola sieci web będzie `WebRole1`, hello drugi będzie `WebRole2`i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="f875a-129">hello first web role created will be `WebRole1`, hello second will be `WebRole2`, and so on.</span></span> <span data-ttu-id="f875a-130">będzie Hello pierwszy roli proces roboczy utworzony `WorkerRole1`, hello drugi będzie `WorkerRole2`i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="f875a-130">hello first worker role created will be `WorkerRole1`, hello second will be `WorkerRole2`, and so on.</span></span>
>
>

## <a name="specify-hello-built-in-php-version"></a><span data-ttu-id="f875a-131">Określ hello wbudowanych wersji PHP</span><span class="sxs-lookup"><span data-stu-id="f875a-131">Specify hello built-in PHP version</span></span>
<span data-ttu-id="f875a-132">Po dodaniu PHP sieci web lub procesu roboczego roli tooa projektu pliki konfiguracji projektu hello są modyfikowane tak, aby PHP zostanie zainstalowana na każde wystąpienie w sieci web lub procesu roboczego aplikacji po jej wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="f875a-132">When you add a PHP web or worker role tooa project, hello project's configuration files are modified so that PHP will be installed on each web or worker instance of your application when it is deployed.</span></span> <span data-ttu-id="f875a-133">Wersja hello toosee PHP instalowanego domyślnie, uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="f875a-133">toosee hello version of PHP that will be installed by default, run hello following command:</span></span>

    PS C:\myProject> Get-AzureServiceProjectRoleRuntime

<span data-ttu-id="f875a-134">Witaj dane wyjściowe polecenia hello powyżej będzie wyglądała podobnie toowhat są wyświetlane poniżej.</span><span class="sxs-lookup"><span data-stu-id="f875a-134">hello output from hello command above will look similar toowhat is shown below.</span></span> <span data-ttu-id="f875a-135">W tym przykładzie hello `IsDefault` flaga jest ustawiona zbyt`true` dla programów PHP 5.3.17, i wskazujący będzie hello domyślne PHP wersji.</span><span class="sxs-lookup"><span data-stu-id="f875a-135">In this example, hello `IsDefault` flag is set too`true` for PHP 5.3.17, indicating that it will be hello default PHP version installed.</span></span>

```
Runtime Version     PackageUri                      IsDefault
------- -------     ----------                      ---------
Node 0.6.17         http://nodertncu.blob.core...   False
Node 0.6.20         http://nodertncu.blob.core...   True
Node 0.8.4          http://nodertncu.blob.core...   False
IISNode 0.1.21      http://nodertncu.blob.core...   True
Cache 1.8.0         http://nodertncu.blob.core...   True
PHP 5.3.17          http://nodertncu.blob.core...   True
PHP 5.4.0           http://nodertncu.blob.core...   False
```

<span data-ttu-id="f875a-136">Można ustawić hello PHP środowiska wykonawczego w wersji tooany hello wersji PHP, które są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="f875a-136">You can set hello PHP runtime version tooany of hello PHP versions that are listed.</span></span> <span data-ttu-id="f875a-137">Na przykład tooset wersji PHP hello (dla roli o nazwie hello `roleName`) too5.4.0, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="f875a-137">For example, tooset hello PHP version (for a role with hello name `roleName`) too5.4.0, use hello following command:</span></span>

    PS C:\myProject> Set-AzureServiceProjectRole roleName php 5.4.0

> [!NOTE]
> <span data-ttu-id="f875a-138">Dostępne wersje PHP mogą ulec zmianie w przyszłych hello.</span><span class="sxs-lookup"><span data-stu-id="f875a-138">Available PHP versions may change in hello future.</span></span>
>
>

## <a name="customize-hello-built-in-php-runtime"></a><span data-ttu-id="f875a-139">Dostosowywanie hello wbudowanych środowiska uruchomieniowego języka PHP</span><span class="sxs-lookup"><span data-stu-id="f875a-139">Customize hello built-in PHP runtime</span></span>
<span data-ttu-id="f875a-140">Masz pełną kontrolę nad hello konfigurację środowiska uruchomieniowego języka PHP hello zainstalowanego wykonanie kroków hello powyżej, w tym modyfikowanie `php.ini` ustawienia i włączania rozszerzeń.</span><span class="sxs-lookup"><span data-stu-id="f875a-140">You have complete control over hello configuration of hello PHP runtime that is installed when you follow hello steps above, including modification of `php.ini` settings and enabling of extensions.</span></span>

<span data-ttu-id="f875a-141">toocustomize hello wbudowanych środowiska uruchomieniowego języka PHP, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="f875a-141">toocustomize hello built-in PHP runtime, follow these steps:</span></span>

1. <span data-ttu-id="f875a-142">Dodaj nowy folder o nazwie `php`, toohello `bin` katalogu swojej roli sieci web.</span><span class="sxs-lookup"><span data-stu-id="f875a-142">Add a new folder, named `php`, toohello `bin` directory of your web role.</span></span> <span data-ttu-id="f875a-143">Dla roli proces roboczy Dodaj ją toohello roli katalogu głównego.</span><span class="sxs-lookup"><span data-stu-id="f875a-143">For a worker role, add it toohello role's root directory.</span></span>
2. <span data-ttu-id="f875a-144">W hello `php` folderu, utworzyć inny folder o nazwie `ext`.</span><span class="sxs-lookup"><span data-stu-id="f875a-144">In hello `php` folder, create another folder called `ext`.</span></span> <span data-ttu-id="f875a-145">Umieszczaj żadnego `.dll` rozszerzenia plików (np. `php_mongo.dll`), które mają tooenable w tym folderze.</span><span class="sxs-lookup"><span data-stu-id="f875a-145">Put any `.dll` extension files (e.g., `php_mongo.dll`) that you want tooenable in this folder.</span></span>
3. <span data-ttu-id="f875a-146">Dodaj `php.ini` pliku toohello `php` folderu.</span><span class="sxs-lookup"><span data-stu-id="f875a-146">Add a `php.ini` file toohello `php` folder.</span></span> <span data-ttu-id="f875a-147">Włącz wszystkie rozszerzenia niestandardowe i ustaw wszystkie dyrektywy PHP w tym pliku.</span><span class="sxs-lookup"><span data-stu-id="f875a-147">Enable any custom extensions and set any PHP directives in this file.</span></span> <span data-ttu-id="f875a-148">Na przykład, jeśli potrzebujesz tooturn `display_errors` na i Włącz hello `php_mongo.dll` rozszerzenia, zawartość hello Twojej `php.ini` pliku będzie następujące:</span><span class="sxs-lookup"><span data-stu-id="f875a-148">For example, if you wanted tooturn `display_errors` on and enable hello `php_mongo.dll` extension, hello contents of your `php.ini` file would be as follows:</span></span>

        display_errors=On
        extension=php_mongo.dll

> [!NOTE]
> <span data-ttu-id="f875a-149">Wszystkie ustawienia, które nie zostanie jawnie ustawiona w hello `php.ini` pliku Podaj zostanie automatycznie można ustawić wartości domyślne tootheir.</span><span class="sxs-lookup"><span data-stu-id="f875a-149">Any settings that you don't explicitly set in hello `php.ini` file that you provide will automatically be set tootheir default values.</span></span> <span data-ttu-id="f875a-150">Jednak należy pamiętać, że można dodać pełnego `php.ini` pliku.</span><span class="sxs-lookup"><span data-stu-id="f875a-150">However, keep in mind that you can add a complete `php.ini` file.</span></span>
>
>

## <a name="use-your-own-php-runtime"></a><span data-ttu-id="f875a-151">Użyć własnego środowiska uruchomieniowego języka PHP</span><span class="sxs-lookup"><span data-stu-id="f875a-151">Use your own PHP runtime</span></span>
<span data-ttu-id="f875a-152">W niektórych przypadkach, zamiast wybrać wbudowanych środowiska uruchomieniowego języka PHP i skonfigurować go, jak opisano powyżej może być tooprovide własnego środowiska uruchomieniowego języka PHP.</span><span class="sxs-lookup"><span data-stu-id="f875a-152">In some cases, instead of selecting a built-in PHP runtime and configuring it as described above, you may want tooprovide your own PHP runtime.</span></span> <span data-ttu-id="f875a-153">Na przykład można użyć tego samego środowiska uruchomieniowego języka PHP w roli sieci web lub procesu roboczego używanego w środowisku projektowania hello.</span><span class="sxs-lookup"><span data-stu-id="f875a-153">For example, you can use hello same PHP runtime in a web or worker role that you use in your development environment.</span></span> <span data-ttu-id="f875a-154">Dzięki temu można łatwiej tooensure aplikacji hello nie spowoduje zmiany zachowania w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="f875a-154">This makes it easier tooensure that hello application will not change behavior in your production environment.</span></span>

### <a name="configure-a-web-role-toouse-your-own-php-runtime"></a><span data-ttu-id="f875a-155">Skonfiguruj toouse roli sieci web z własnego środowiska uruchomieniowego języka PHP</span><span class="sxs-lookup"><span data-stu-id="f875a-155">Configure a web role toouse your own PHP runtime</span></span>
<span data-ttu-id="f875a-156">tooconfigure toouse roli sieci web środowiska uruchomieniowego języka PHP, które zapewniają, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="f875a-156">tooconfigure a web role toouse a PHP runtime that you provide, follow these steps:</span></span>

1. <span data-ttu-id="f875a-157">Tworzenie projektu usługi Azure i Dodaj rolę sieci web PHP, jak opisano wcześniej w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="f875a-157">Create an Azure Service project and add a PHP web role as described previously in this topic.</span></span>
2. <span data-ttu-id="f875a-158">Utwórz `php` folderu w hello `bin` folderu, który znajduje się w katalogu głównym roli sieci web, a następnie dodaj toohello środowiska uruchomieniowego (wszystkie pliki binarne, pliki konfiguracji, podfoldery itp.) z PHP `php` folderu.</span><span class="sxs-lookup"><span data-stu-id="f875a-158">Create a `php` folder in hello `bin` folder that is in your web role's root directory, and then add your PHP runtime (all binaries, configuration files, subfolders, etc.) toohello `php` folder.</span></span>
3. <span data-ttu-id="f875a-159">(OPCJONALNIE) Jeśli Twojego środowiska uruchomieniowego języka PHP używa hello [Drivers firmy Microsoft dla programów PHP i SQL Server][sqlsrv drivers], konieczne będzie tooconfigure tooinstall roli sieci web [programu SQL Server Native Client 2012] [ sql native client] po zainicjowaniu obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="f875a-159">(OPTIONAL) If your PHP runtime uses hello [Microsoft Drivers for PHP for SQL Server][sqlsrv drivers], you will need tooconfigure your web role tooinstall [SQL Server Native Client 2012][sql native client] when it is provisioned.</span></span> <span data-ttu-id="f875a-160">toodo, Dodaj hello [Instalator sqlncli.msi x64] toohello `bin` folderu w katalogu głównym roli sieci web.</span><span class="sxs-lookup"><span data-stu-id="f875a-160">toodo this, add hello [sqlncli.msi x64 installer] toohello `bin` folder in your web role's root directory.</span></span> <span data-ttu-id="f875a-161">skryptu uruchomieniowego Hello opisany w następnym kroku hello uruchomi dyskretnej Instalatora hello po udostępnieniu hello roli.</span><span class="sxs-lookup"><span data-stu-id="f875a-161">hello startup script described in hello next step will silently run hello installer when hello role is provisioned.</span></span> <span data-ttu-id="f875a-162">Jeśli Twojego środowiska uruchomieniowego języka PHP nie używa hello Drivers firmy Microsoft dla programu PHP dla programu SQL Server, należy usunąć hello następującego wiersza ze skryptu hello pokazano w następnym kroku hello:</span><span class="sxs-lookup"><span data-stu-id="f875a-162">If your PHP runtime does not use hello Microsoft Drivers for PHP for SQL Server, you can remove hello following line from hello script shown in hello next step:</span></span>

        msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES
4. <span data-ttu-id="f875a-163">Zdefiniuj zadanie uruchamiania, który konfiguruje [Internet Information Services (IIS)] [ iis.net] toouse Twojego toohandle środowiska uruchomieniowego PHP żądań dotyczących `.php` stron.</span><span class="sxs-lookup"><span data-stu-id="f875a-163">Define a startup task that configures [Internet Information Services (IIS)][iis.net] toouse your PHP runtime toohandle requests for `.php` pages.</span></span> <span data-ttu-id="f875a-164">toodo, otwórz hello `setup_web.cmd` pliku (w hello `bin` pliku katalog główny roli sieci web) w edytorze tekstów i zastąp jego zawartość z hello następujący skrypt:</span><span class="sxs-lookup"><span data-stu-id="f875a-164">toodo this, open hello `setup_web.cmd` file (in hello `bin` file of your web role's root directory) in a text editor and replace its contents with hello following script:</span></span>

    ```cmd
    @ECHO ON
    cd "%~dp0"

    if "%EMULATED%"=="true" exit /b 0

    msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES

    SET PHP_FULL_PATH=%~dp0php\php-cgi.exe
    SET NEW_PATH=%PATH%;%RoleRoot%\base\x86

    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /+"[fullPath='%PHP_FULL_PATH%',maxInstances='12',idleTimeout='60000',activityTimeout='3600',requestTimeout='60000',instanceMaxRequests='10000',protocol='NamedPipe',flushNamedPipe='False']" /commit:apphost
    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /+"[fullPath='%PHP_FULL_PATH%'].environmentVariables.[name='PATH',value='%NEW_PATH%']" /commit:apphost
    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /+"[fullPath='%PHP_FULL_PATH%'].environmentVariables.[name='PHP_FCGI_MAX_REQUESTS',value='10000']" /commit:apphost
    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/handlers /+"[name='PHP',path='*.php',verb='GET,HEAD,POST',modules='FastCgiModule',scriptProcessor='%PHP_FULL_PATH%',resourceType='Either',requireAccess='Script']" /commit:apphost
    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /"[fullPath='%PHP_FULL_PATH%'].queueLength:50000"
    ```
5. <span data-ttu-id="f875a-165">Dodaj katalog główny aplikacji pliki tooyour roli sieci web firmy.</span><span class="sxs-lookup"><span data-stu-id="f875a-165">Add your application files tooyour web role's root directory.</span></span> <span data-ttu-id="f875a-166">Jest to katalog główny serwera sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="f875a-166">This will be hello web server's root directory.</span></span>
6. <span data-ttu-id="f875a-167">Publikowanie aplikacji, zgodnie z opisem w hello [opublikować aplikację](#publish-your-application) poniższej sekcji.</span><span class="sxs-lookup"><span data-stu-id="f875a-167">Publish your application as described in hello [Publish your application](#publish-your-application) section below.</span></span>

> [!NOTE]
> <span data-ttu-id="f875a-168">Witaj `download.ps1` skryptu (w hello `bin` folder katalogu głównego roli sieci web hello) można usunąć po wykonaniu kroków hello opisane powyżej, aby przy użyciu własnego środowiska uruchomieniowego języka PHP.</span><span class="sxs-lookup"><span data-stu-id="f875a-168">hello `download.ps1` script (in hello `bin` folder of hello web role's root directory) can be deleted after you follow hello steps described above for using your own PHP runtime.</span></span>
>
>

### <a name="configure-a-worker-role-toouse-your-own-php-runtime"></a><span data-ttu-id="f875a-169">Skonfiguruj toouse roli procesu roboczego własnego środowiska uruchomieniowego języka PHP</span><span class="sxs-lookup"><span data-stu-id="f875a-169">Configure a worker role toouse your own PHP runtime</span></span>
<span data-ttu-id="f875a-170">tooconfigure toouse roli procesu roboczego środowiska wykonawczego PHP, które zapewniają, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="f875a-170">tooconfigure a worker role toouse a PHP runtime that you provide, follow these steps:</span></span>

1. <span data-ttu-id="f875a-171">Tworzenie projektu usługi Azure i Dodaj rolę procesu roboczego PHP, jak opisano wcześniej w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="f875a-171">Create an Azure Service project and add a PHP worker role as described previously in this topic.</span></span>
2. <span data-ttu-id="f875a-172">Utwórz `php` folderu w katalogu głównym roli procesu roboczego hello, a następnie dodaj programu PHP toohello środowiska uruchomieniowego (wszystkie pliki binarne, pliki konfiguracji, podfoldery itp.) `php` folderu.</span><span class="sxs-lookup"><span data-stu-id="f875a-172">Create a `php` folder in hello worker role's root directory, and then add your PHP runtime (all binaries, configuration files, subfolders, etc.) toohello `php` folder.</span></span>
3. <span data-ttu-id="f875a-173">(OPCJONALNIE) Jeśli korzysta z Twojego środowiska uruchomieniowego języka PHP [Drivers firmy Microsoft dla programów PHP i SQL Server][sqlsrv drivers], konieczne będzie tooconfigure Twojego tooinstall roli procesu roboczego [programu SQL Server Native Client 2012] [ sql native client] po zainicjowaniu obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="f875a-173">(OPTIONAL) If your PHP runtime uses [Microsoft Drivers for PHP for SQL Server][sqlsrv drivers], you will need tooconfigure your worker role tooinstall [SQL Server Native Client 2012][sql native client] when it is provisioned.</span></span> <span data-ttu-id="f875a-174">toodo, Dodaj hello [Instalator sqlncli.msi x64] roli procesu roboczego toohello katalogu głównego.</span><span class="sxs-lookup"><span data-stu-id="f875a-174">toodo this, add hello [sqlncli.msi x64 installer] toohello worker role's root directory.</span></span> <span data-ttu-id="f875a-175">skryptu uruchomieniowego Hello opisany w następnym kroku hello uruchomi dyskretnej Instalatora hello po udostępnieniu hello roli.</span><span class="sxs-lookup"><span data-stu-id="f875a-175">hello startup script described in hello next step will silently run hello installer when hello role is provisioned.</span></span> <span data-ttu-id="f875a-176">Jeśli Twojego środowiska uruchomieniowego języka PHP nie używa hello Drivers firmy Microsoft dla programu PHP dla programu SQL Server, należy usunąć hello następującego wiersza ze skryptu hello pokazano w następnym kroku hello:</span><span class="sxs-lookup"><span data-stu-id="f875a-176">If your PHP runtime does not use hello Microsoft Drivers for PHP for SQL Server, you can remove hello following line from hello script shown in hello next step:</span></span>

        msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES
4. <span data-ttu-id="f875a-177">Zdefiniuj zadanie uruchamiania, który dodaje użytkownika `php.exe` zmiennej środowiskowej PATH roli toohello pliku wykonywalnego procesu roboczego po udostępnieniu hello roli.</span><span class="sxs-lookup"><span data-stu-id="f875a-177">Define a startup task that adds your `php.exe` executable toohello worker role's PATH environment variable when hello role is provisioned.</span></span> <span data-ttu-id="f875a-178">toodo, otwórz hello `setup_worker.cmd` plików (w katalogu głównym roli procesu roboczego hello) w edytorze tekstów i zastąp jego zawartość hello następującego skryptu:</span><span class="sxs-lookup"><span data-stu-id="f875a-178">toodo this, open hello `setup_worker.cmd` file (in hello worker role's root directory) in a text editor and replace its contents with hello following script:</span></span>

    ```cmd
    @echo on

    cd "%~dp0"

    echo Granting permissions for Network Service toohello web root directory...
    icacls ..\ /grant "Network Service":(OI)(CI)W
    if %ERRORLEVEL% neq 0 goto error
    echo OK

    if "%EMULATED%"=="true" exit /b 0

    msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES

    setx Path "%PATH%;%~dp0php" /M

    if %ERRORLEVEL% neq 0 goto error

    echo SUCCESS
    exit /b 0

    :error

    echo FAILED
    exit /b -1
    ```
5. <span data-ttu-id="f875a-179">Dodaj katalog główny roli użytkownika aplikacji pliki tooyour procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="f875a-179">Add your application files tooyour worker role's root directory.</span></span>
6. <span data-ttu-id="f875a-180">Publikowanie aplikacji, zgodnie z opisem w hello [opublikować aplikację](#publish-your-application) poniższej sekcji.</span><span class="sxs-lookup"><span data-stu-id="f875a-180">Publish your application as described in hello [Publish your application](#publish-your-application) section below.</span></span>

## <a name="run-your-application-in-hello-compute-and-storage-emulators"></a><span data-ttu-id="f875a-181">Uruchom aplikację w hello emulatory zasobów obliczeniowych i magazynu</span><span class="sxs-lookup"><span data-stu-id="f875a-181">Run your application in hello compute and storage emulators</span></span>
<span data-ttu-id="f875a-182">Hello Azure emulatory Podaj lokalnego środowiska można przetestować aplikację Azure, przed wdrożeniem toohello chmury.</span><span class="sxs-lookup"><span data-stu-id="f875a-182">hello Azure emulators provide a local environment in which you can test your Azure application before you deploy it toohello cloud.</span></span> <span data-ttu-id="f875a-183">Istnieją pewne różnice między hello emulatorów i hello środowiska platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f875a-183">There are some differences between hello emulators and hello Azure environment.</span></span> <span data-ttu-id="f875a-184">toounderstand to lepsze, zobacz [użyć emulatora magazynu Azure hello do projektowania i testowania](storage/common/storage-use-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="f875a-184">toounderstand this better, see [Use hello Azure storage emulator for development and testing](storage/common/storage-use-emulator.md).</span></span>

<span data-ttu-id="f875a-185">Należy pamiętać, że użytkownik musi mieć PHP zainstalowane lokalnie emulatora obliczeń hello toouse.</span><span class="sxs-lookup"><span data-stu-id="f875a-185">Note that you must have PHP installed locally toouse hello compute emulator.</span></span> <span data-ttu-id="f875a-186">emulator obliczeń Hello będzie używać sieci lokalnej toorun instalacji PHP aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f875a-186">hello compute emulator will use your local PHP installation toorun your application.</span></span>

<span data-ttu-id="f875a-187">wykonanie projektu w emulatory hello toorun hello następujące polecenie z katalogu głównego projektu:</span><span class="sxs-lookup"><span data-stu-id="f875a-187">toorun your project in hello emulators, execute hello following command from your project's root directory:</span></span>

    PS C:\MyProject> Start-AzureEmulator

<span data-ttu-id="f875a-188">Zostaną wyświetlone dane wyjściowe podobne toothis:</span><span class="sxs-lookup"><span data-stu-id="f875a-188">You will see output similar toothis:</span></span>

    Creating local package...
    Starting Emulator...
    Role is running at http://127.0.0.1:81
    Started

<span data-ttu-id="f875a-189">Widać działanie aplikacji w emulatorze hello przez otwarcie przeglądarki sieci web i przeglądanie toohello lokalny adres wyświetlany w danych wyjściowych hello (`http://127.0.0.1:81` hello przykład danych wyjściowych powyżej).</span><span class="sxs-lookup"><span data-stu-id="f875a-189">You can see your application running in hello emulator by opening a web browser and browsing toohello local address shown in hello output (`http://127.0.0.1:81` in hello example output above).</span></span>

<span data-ttu-id="f875a-190">emulatory hello toostop, wykonanie tego polecenia:</span><span class="sxs-lookup"><span data-stu-id="f875a-190">toostop hello emulators, execute this command:</span></span>

    PS C:\MyProject> Stop-AzureEmulator

## <a name="publish-your-application"></a><span data-ttu-id="f875a-191">Publikowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="f875a-191">Publish your application</span></span>
<span data-ttu-id="f875a-192">toopublish aplikacji, należy importu toofirst Twojego ustawień publikowania za pomocą hello [AzurePublishSettingsFile importu](https://msdn.microsoft.com/library/azure/dn790370.aspx) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f875a-192">toopublish your application, you need toofirst import your publish settings by using hello [Import-AzurePublishSettingsFile](https://msdn.microsoft.com/library/azure/dn790370.aspx) cmdlet.</span></span> <span data-ttu-id="f875a-193">Następnie można opublikować aplikację przy użyciu hello [Publish-AzureServiceProject](https://msdn.microsoft.com/library/azure/dn495166.aspx) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f875a-193">Then you can publish your application by using hello [Publish-AzureServiceProject](https://msdn.microsoft.com/library/azure/dn495166.aspx) cmdlet.</span></span> <span data-ttu-id="f875a-194">Informacje logowania, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f875a-194">For information about signing in, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f875a-195">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f875a-195">Next steps</span></span>
<span data-ttu-id="f875a-196">Aby uzyskać więcej informacji, zobacz hello [Centrum deweloperów języka PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="f875a-196">For more information, see hello [PHP Developer Center](/develop/php/).</span></span>

[zestaw Azure SDK for PHP]: /develop/php/common-tasks/download-php-sdk/
[install ps and emulators]: http://go.microsoft.com/fwlink/p/?linkid=320376&clcid=0x409
[definicji (csdef) usługi]: http://msdn.microsoft.com/library/windowsazure/ee758711.aspx
[konfiguracji usługi (cscfg)]: http://msdn.microsoft.com/library/windowsazure/ee758710.aspx
[iis.net]: http://www.iis.net/
[sql native client]: http://msdn.microsoft.com/sqlserver/aa937733.aspx
[sqlsrv drivers]: http://php.net/sqlsrv
[Instalator sqlncli.msi x64]: http://go.microsoft.com/fwlink/?LinkID=239648
