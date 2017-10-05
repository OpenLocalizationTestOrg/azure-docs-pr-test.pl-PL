---
title: Tworzenie Azure role sieci web i proces roboczy dla PHP | Dokumentacja firmy Microsoft
description: "Przewodnik dotyczący tworzenia ról sieci web i proces roboczy PHP w usłudze w chmurze platformy Azure i konfigurowania środowiska uruchomieniowego języka PHP."
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
ms.openlocfilehash: 214fdcfe20f3fa4ebcbe41308404f8b7e7d15310
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-create-php-web-and-worker-roles"></a><span data-ttu-id="65d31-103">Jak utworzyć role sieci web i proces roboczy języka PHP</span><span class="sxs-lookup"><span data-stu-id="65d31-103">How to create PHP web and worker roles</span></span>
## <a name="overview"></a><span data-ttu-id="65d31-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="65d31-104">Overview</span></span>
<span data-ttu-id="65d31-105">W tym przewodniku opisano sposób tworzyć role sieci web lub procesu roboczego PHP w środowisku projektowym systemu Windows, wybierz określonej wersji programu PHP w wersjach "wbudowanych" dostępne zmiany konfiguracji PHP, Włącz rozszerzenia i na koniec wdrażanie na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="65d31-105">This guide will show you how to create PHP web or worker roles in a Windows development environment, choose a specific version of PHP from the "built-in" versions available, change the PHP configuration, enable extensions, and finally, deploy to Azure.</span></span> <span data-ttu-id="65d31-106">Zawiera również opis sposobu konfigurowania roli sieci web lub procesu roboczego do używania środowiska uruchomieniowego języka PHP (z konfiguracji niestandardowej i rozszerzenia) podane.</span><span class="sxs-lookup"><span data-stu-id="65d31-106">It also describes how to configure a web or worker role to use a PHP runtime (with custom configuration and extensions) that you provide.</span></span>

## <a name="what-are-php-web-and-worker-roles"></a><span data-ttu-id="65d31-107">Co to są role sieć web i proces roboczy PHP?</span><span class="sxs-lookup"><span data-stu-id="65d31-107">What are PHP web and worker roles?</span></span>
<span data-ttu-id="65d31-108">Platforma Azure udostępnia trzy modele obliczeniowe na potrzeby uruchamiania aplikacji: Azure App Service, maszynach wirtualnych platformy Azure i usługi w chmurze Azure.</span><span class="sxs-lookup"><span data-stu-id="65d31-108">Azure provides three compute models for running applications: Azure App Service, Azure Virtual Machines, and Azure Cloud Services.</span></span> <span data-ttu-id="65d31-109">Wszystkie trzy modele obsługują PHP.</span><span class="sxs-lookup"><span data-stu-id="65d31-109">All three models support PHP.</span></span> <span data-ttu-id="65d31-110">Usługi w chmurze, które obejmują role sieć web i proces roboczy, zapewnia *platforma jako usługa (PaaS)*.</span><span class="sxs-lookup"><span data-stu-id="65d31-110">Cloud Services, which includes web and worker roles, provides *platform as a service (PaaS)*.</span></span> <span data-ttu-id="65d31-111">W ramach usługi w chmurze rola sieci web zapewnia dedykowany serwer sieci web usług Internet Information Services (IIS) umożliwia obsługę aplikacji frontonu sieci web.</span><span class="sxs-lookup"><span data-stu-id="65d31-111">Within a cloud service, a web role provides a dedicated Internet Information Services (IIS) web server to host front-end web applications.</span></span> <span data-ttu-id="65d31-112">Rola proces roboczy można uruchamiać asynchroniczne, długotrwałe lub ciągłe zadania niezależne interakcji z użytkownikiem lub danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="65d31-112">A worker role can run asynchronous, long-running or perpetual tasks independent of user interaction or input.</span></span>

<span data-ttu-id="65d31-113">Aby uzyskać więcej informacji o tych opcjach, zobacz [obliczeniowe hosting opcji dostarczanych przez platformę Azure](cloud-services/cloud-services-choose-me.md).</span><span class="sxs-lookup"><span data-stu-id="65d31-113">For more information about these options, see [Compute hosting options provided by Azure](cloud-services/cloud-services-choose-me.md).</span></span>

## <a name="download-the-azure-sdk-for-php"></a><span data-ttu-id="65d31-114">Pobierz zestaw Azure SDK dla języka PHP</span><span class="sxs-lookup"><span data-stu-id="65d31-114">Download the Azure SDK for PHP</span></span>
<span data-ttu-id="65d31-115">[Zestaw Azure SDK for PHP] składa się z kilku składników.</span><span class="sxs-lookup"><span data-stu-id="65d31-115">The [Azure SDK for PHP] consists of several components.</span></span> <span data-ttu-id="65d31-116">W tym artykule będzie korzystać z dwóch z nich: Azure PowerShell i emulatory platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="65d31-116">This article will use two of them: Azure PowerShell and the Azure emulators.</span></span> <span data-ttu-id="65d31-117">Te dwa składniki można zainstalować za pomocą Instalatora platformy sieci Web firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="65d31-117">These two components can be installed via the Microsoft Web Platform Installer.</span></span> <span data-ttu-id="65d31-118">Aby uzyskać więcej informacji, zobacz [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="65d31-118">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="create-a-cloud-services-project"></a><span data-ttu-id="65d31-119">Tworzenie projektu usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="65d31-119">Create a Cloud Services project</span></span>
<span data-ttu-id="65d31-120">Pierwszym krokiem tworzenia roli sieci web lub procesu roboczego PHP jest tworzenie projektu usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="65d31-120">The first step in creating a PHP web or worker role is to create an Azure Service project.</span></span> <span data-ttu-id="65d31-121">projekt usługi Azure służy jako kontener logicznej dla sieci web i proces roboczy ról i zawiera projektu [definicji (csdef) usługi] i [konfiguracji usługi (cscfg)] plików.</span><span class="sxs-lookup"><span data-stu-id="65d31-121">an Azure Service project serves as a logical container for web and worker roles, and it contains the project's [service definition (.csdef)] and [service configuration (.cscfg)] files.</span></span>

<span data-ttu-id="65d31-122">Aby utworzyć nowy projekt usługi Azure, uruchomienie programu Azure PowerShell jako administrator i uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="65d31-122">To create a new Azure Service project, run Azure PowerShell as an administrator, and execute the following command:</span></span>

    PS C:\>New-AzureServiceProject myProject

<span data-ttu-id="65d31-123">To polecenie spowoduje utworzenie nowego katalogu (`myProject`) do której można dodać role sieci web i proces roboczy.</span><span class="sxs-lookup"><span data-stu-id="65d31-123">This command will create a new directory (`myProject`) to which you can add web and worker roles.</span></span>

## <a name="add-php-web-or-worker-roles"></a><span data-ttu-id="65d31-124">Dodawanie ról PHP sieci web lub procesu roboczego</span><span class="sxs-lookup"><span data-stu-id="65d31-124">Add PHP web or worker roles</span></span>
<span data-ttu-id="65d31-125">Aby dodać rolę sieci web PHP na projekt, uruchom następujące polecenie w katalogu głównym projektu:</span><span class="sxs-lookup"><span data-stu-id="65d31-125">To add a PHP web role to a project, run the following command from within the project's root directory:</span></span>

    PS C:\myProject> Add-AzurePHPWebRole roleName

<span data-ttu-id="65d31-126">Dla roli proces roboczy Użyj tego polecenia:</span><span class="sxs-lookup"><span data-stu-id="65d31-126">For a worker role, use this command:</span></span>

    PS C:\myProject> Add-AzurePHPWorkerRole roleName

> [!NOTE]
> <span data-ttu-id="65d31-127">`roleName` Parametr jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="65d31-127">The `roleName` parameter is optional.</span></span> <span data-ttu-id="65d31-128">Jeśli zostanie pominięty, zostanie automatycznie wygenerowana nazwa roli.</span><span class="sxs-lookup"><span data-stu-id="65d31-128">If it is omitted, the role name will be automatically generated.</span></span> <span data-ttu-id="65d31-129">Pierwszy rola sieci web utworzony będzie `WebRole1`, drugi będzie `WebRole2`i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="65d31-129">The first web role created will be `WebRole1`, the second will be `WebRole2`, and so on.</span></span> <span data-ttu-id="65d31-130">Pierwszy roli procesu roboczego, utworzony zostanie `WorkerRole1`, drugi będzie `WorkerRole2`i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="65d31-130">The first worker role created will be `WorkerRole1`, the second will be `WorkerRole2`, and so on.</span></span>
>
>

## <a name="specify-the-built-in-php-version"></a><span data-ttu-id="65d31-131">Określ wbudowane wersję PHP</span><span class="sxs-lookup"><span data-stu-id="65d31-131">Specify the built-in PHP version</span></span>
<span data-ttu-id="65d31-132">Po dodaniu roli PHP sieci web lub procesu roboczego do projektu pliki konfiguracji projektu są modyfikowane, dzięki czemu PHP zostanie zainstalowana na każde wystąpienie w sieci web lub procesu roboczego aplikacji po jej wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="65d31-132">When you add a PHP web or worker role to a project, the project's configuration files are modified so that PHP will be installed on each web or worker instance of your application when it is deployed.</span></span> <span data-ttu-id="65d31-133">Aby wyświetlić wersję PHP, które będą instalowane domyślnie, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="65d31-133">To see the version of PHP that will be installed by default, run the following command:</span></span>

    PS C:\myProject> Get-AzureServiceProjectRoleRuntime

<span data-ttu-id="65d31-134">Dane wyjściowe polecenia powyżej będzie wyglądać podobnie do co przedstawiono poniżej.</span><span class="sxs-lookup"><span data-stu-id="65d31-134">The output from the command above will look similar to what is shown below.</span></span> <span data-ttu-id="65d31-135">W tym przykładzie `IsDefault` flaga jest ustawiona na `true` dla programów PHP 5.3.17, i wskazujący, że będzie domyślna wersja PHP zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="65d31-135">In this example, the `IsDefault` flag is set to `true` for PHP 5.3.17, indicating that it will be the default PHP version installed.</span></span>

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

<span data-ttu-id="65d31-136">Wersja środowiska uruchomieniowego PHP można ustawić na dowolnej wersji PHP, które są wymienione.</span><span class="sxs-lookup"><span data-stu-id="65d31-136">You can set the PHP runtime version to any of the PHP versions that are listed.</span></span> <span data-ttu-id="65d31-137">Na przykład, aby ustawić wersję PHP (dla roli o nazwie `roleName`) do 5.4.0, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="65d31-137">For example, to set the PHP version (for a role with the name `roleName`) to 5.4.0, use the following command:</span></span>

    PS C:\myProject> Set-AzureServiceProjectRole roleName php 5.4.0

> [!NOTE]
> <span data-ttu-id="65d31-138">Dostępne wersje PHP mogą ulec zmianie w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="65d31-138">Available PHP versions may change in the future.</span></span>
>
>

## <a name="customize-the-built-in-php-runtime"></a><span data-ttu-id="65d31-139">Dostosowywanie wbudowanej środowiska uruchomieniowego języka PHP</span><span class="sxs-lookup"><span data-stu-id="65d31-139">Customize the built-in PHP runtime</span></span>
<span data-ttu-id="65d31-140">Masz pełną kontrolę nad konfiguracji środowiska uruchomieniowego języka PHP, instalowanego podczas wykonaj kroki opisane powyżej, w tym modyfikowanie `php.ini` ustawienia i włączania rozszerzeń.</span><span class="sxs-lookup"><span data-stu-id="65d31-140">You have complete control over the configuration of the PHP runtime that is installed when you follow the steps above, including modification of `php.ini` settings and enabling of extensions.</span></span>

<span data-ttu-id="65d31-141">Aby dostosować wbudowanych środowiska uruchomieniowego języka PHP, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="65d31-141">To customize the built-in PHP runtime, follow these steps:</span></span>

1. <span data-ttu-id="65d31-142">Dodaj nowy folder o nazwie `php`, do `bin` katalogu swojej roli sieci web.</span><span class="sxs-lookup"><span data-stu-id="65d31-142">Add a new folder, named `php`, to the `bin` directory of your web role.</span></span> <span data-ttu-id="65d31-143">Dla roli proces roboczy Dodaj go do katalogu głównego roli.</span><span class="sxs-lookup"><span data-stu-id="65d31-143">For a worker role, add it to the role's root directory.</span></span>
2. <span data-ttu-id="65d31-144">W `php` folderu, utworzyć inny folder o nazwie `ext`.</span><span class="sxs-lookup"><span data-stu-id="65d31-144">In the `php` folder, create another folder called `ext`.</span></span> <span data-ttu-id="65d31-145">Umieszczaj żadnego `.dll` rozszerzenia plików (np. `php_mongo.dll`), który chcesz włączyć w tym folderze.</span><span class="sxs-lookup"><span data-stu-id="65d31-145">Put any `.dll` extension files (e.g., `php_mongo.dll`) that you want to enable in this folder.</span></span>
3. <span data-ttu-id="65d31-146">Dodaj `php.ini` pliku `php` folderu.</span><span class="sxs-lookup"><span data-stu-id="65d31-146">Add a `php.ini` file to the `php` folder.</span></span> <span data-ttu-id="65d31-147">Włącz wszystkie rozszerzenia niestandardowe i ustaw wszystkie dyrektywy PHP w tym pliku.</span><span class="sxs-lookup"><span data-stu-id="65d31-147">Enable any custom extensions and set any PHP directives in this file.</span></span> <span data-ttu-id="65d31-148">Na przykład, jeśli chcesz włączyć `display_errors` na i Włącz `php_mongo.dll` rozszerzenia, zawartość z `php.ini` pliku będzie następujące:</span><span class="sxs-lookup"><span data-stu-id="65d31-148">For example, if you wanted to turn `display_errors` on and enable the `php_mongo.dll` extension, the contents of your `php.ini` file would be as follows:</span></span>

        display_errors=On
        extension=php_mongo.dll

> [!NOTE]
> <span data-ttu-id="65d31-149">Wszystkie ustawienia, które nie zostanie jawnie ustawiona `php.ini` pliku Podaj zostanie automatycznie można ustawić wartości domyślne.</span><span class="sxs-lookup"><span data-stu-id="65d31-149">Any settings that you don't explicitly set in the `php.ini` file that you provide will automatically be set to their default values.</span></span> <span data-ttu-id="65d31-150">Jednak należy pamiętać, że można dodać pełnego `php.ini` pliku.</span><span class="sxs-lookup"><span data-stu-id="65d31-150">However, keep in mind that you can add a complete `php.ini` file.</span></span>
>
>

## <a name="use-your-own-php-runtime"></a><span data-ttu-id="65d31-151">Użyć własnego środowiska uruchomieniowego języka PHP</span><span class="sxs-lookup"><span data-stu-id="65d31-151">Use your own PHP runtime</span></span>
<span data-ttu-id="65d31-152">W niektórych przypadkach, zamiast wybierania wbudowanych środowiska uruchomieniowego języka PHP i konfigurowania go jak opisano powyżej możesz podać własne środowiska uruchomieniowego języka PHP.</span><span class="sxs-lookup"><span data-stu-id="65d31-152">In some cases, instead of selecting a built-in PHP runtime and configuring it as described above, you may want to provide your own PHP runtime.</span></span> <span data-ttu-id="65d31-153">Na przykład można użyć tego samego środowiska uruchomieniowego języka PHP w roli sieci web lub procesu roboczego używanego w środowisku projektowania.</span><span class="sxs-lookup"><span data-stu-id="65d31-153">For example, you can use the same PHP runtime in a web or worker role that you use in your development environment.</span></span> <span data-ttu-id="65d31-154">Ułatwia to upewnij się, że aplikacja nie spowoduje zmiany zachowania w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="65d31-154">This makes it easier to ensure that the application will not change behavior in your production environment.</span></span>

### <a name="configure-a-web-role-to-use-your-own-php-runtime"></a><span data-ttu-id="65d31-155">Skonfiguruj rolę sieci web do używania własnego środowiska uruchomieniowego języka PHP</span><span class="sxs-lookup"><span data-stu-id="65d31-155">Configure a web role to use your own PHP runtime</span></span>
<span data-ttu-id="65d31-156">Aby skonfigurować rolę sieci web do używania środowiska uruchomieniowego języka PHP, który podasz, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="65d31-156">To configure a web role to use a PHP runtime that you provide, follow these steps:</span></span>

1. <span data-ttu-id="65d31-157">Tworzenie projektu usługi Azure i Dodaj rolę sieci web PHP, jak opisano wcześniej w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="65d31-157">Create an Azure Service project and add a PHP web role as described previously in this topic.</span></span>
2. <span data-ttu-id="65d31-158">Utwórz `php` folderu w `bin` folderu, który znajduje się w katalogu głównym roli sieci web, a następnie dodać do Twojego środowiska uruchomieniowego języka PHP (wszystkie pliki binarne, pliki konfiguracji, podfoldery itp.) `php` folderu.</span><span class="sxs-lookup"><span data-stu-id="65d31-158">Create a `php` folder in the `bin` folder that is in your web role's root directory, and then add your PHP runtime (all binaries, configuration files, subfolders, etc.) to the `php` folder.</span></span>
3. <span data-ttu-id="65d31-159">(OPCJONALNIE) Jeśli korzysta z Twojego środowiska uruchomieniowego języka PHP [Drivers firmy Microsoft dla programów PHP i SQL Server][sqlsrv drivers], będzie konieczne skonfigurowanie roli sieci web do zainstalowania [programu SQL Server Native Client 2012] [ sql native client] po zainicjowaniu obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="65d31-159">(OPTIONAL) If your PHP runtime uses the [Microsoft Drivers for PHP for SQL Server][sqlsrv drivers], you will need to configure your web role to install [SQL Server Native Client 2012][sql native client] when it is provisioned.</span></span> <span data-ttu-id="65d31-160">Aby to zrobić, należy dodać [Instalator sqlncli.msi x64] do `bin` folderu w katalogu głównym roli sieci web.</span><span class="sxs-lookup"><span data-stu-id="65d31-160">To do this, add the [sqlncli.msi x64 installer] to the `bin` folder in your web role's root directory.</span></span> <span data-ttu-id="65d31-161">Po udostępnieniu roli, skryptu uruchomieniowego opisany w następnym kroku zostanie dyskretnie uruchom Instalatora.</span><span class="sxs-lookup"><span data-stu-id="65d31-161">The startup script described in the next step will silently run the installer when the role is provisioned.</span></span> <span data-ttu-id="65d31-162">Jeśli Twojego środowiska uruchomieniowego języka PHP nie używa Drivers firmy Microsoft dla programów PHP i SQL Server, należy usunąć następujący wiersz w skrypcie pokazano w następnym kroku:</span><span class="sxs-lookup"><span data-stu-id="65d31-162">If your PHP runtime does not use the Microsoft Drivers for PHP for SQL Server, you can remove the following line from the script shown in the next step:</span></span>

        msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES
4. <span data-ttu-id="65d31-163">Zdefiniuj zadanie uruchamiania, który konfiguruje [Internet Information Services (IIS)] [ iis.net] na potrzeby obsługi żądań dla Twojego środowiska uruchomieniowego języka PHP `.php` stron.</span><span class="sxs-lookup"><span data-stu-id="65d31-163">Define a startup task that configures [Internet Information Services (IIS)][iis.net] to use your PHP runtime to handle requests for `.php` pages.</span></span> <span data-ttu-id="65d31-164">Aby to zrobić, otwórz `setup_web.cmd` pliku (w `bin` pliku katalog główny roli sieci web) w edytorze tekstów i zastąp jego zawartość następujący skrypt:</span><span class="sxs-lookup"><span data-stu-id="65d31-164">To do this, open the `setup_web.cmd` file (in the `bin` file of your web role's root directory) in a text editor and replace its contents with the following script:</span></span>

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
5. <span data-ttu-id="65d31-165">Dodawania plików aplikacji do katalogu głównego roli sieci web.</span><span class="sxs-lookup"><span data-stu-id="65d31-165">Add your application files to your web role's root directory.</span></span> <span data-ttu-id="65d31-166">Jest to katalog główny serwera sieci web.</span><span class="sxs-lookup"><span data-stu-id="65d31-166">This will be the web server's root directory.</span></span>
6. <span data-ttu-id="65d31-167">Publikowanie aplikacji, zgodnie z opisem w [opublikować aplikację](#publish-your-application) poniższej sekcji.</span><span class="sxs-lookup"><span data-stu-id="65d31-167">Publish your application as described in the [Publish your application](#publish-your-application) section below.</span></span>

> [!NOTE]
> <span data-ttu-id="65d31-168">`download.ps1` Skryptu (w `bin` folder katalogu głównego roli sieci web) mogą być usuwane po wykonaj kroki opisane powyżej, aby przy użyciu własnego środowiska uruchomieniowego języka PHP.</span><span class="sxs-lookup"><span data-stu-id="65d31-168">The `download.ps1` script (in the `bin` folder of the web role's root directory) can be deleted after you follow the steps described above for using your own PHP runtime.</span></span>
>
>

### <a name="configure-a-worker-role-to-use-your-own-php-runtime"></a><span data-ttu-id="65d31-169">Konfigurowanie roli proces roboczy, aby użyć własnego środowiska uruchomieniowego języka PHP</span><span class="sxs-lookup"><span data-stu-id="65d31-169">Configure a worker role to use your own PHP runtime</span></span>
<span data-ttu-id="65d31-170">Aby skonfigurować rolę procesu roboczego, aby użyć środowiska uruchomieniowego języka PHP, który podasz, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="65d31-170">To configure a worker role to use a PHP runtime that you provide, follow these steps:</span></span>

1. <span data-ttu-id="65d31-171">Tworzenie projektu usługi Azure i Dodaj rolę procesu roboczego PHP, jak opisano wcześniej w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="65d31-171">Create an Azure Service project and add a PHP worker role as described previously in this topic.</span></span>
2. <span data-ttu-id="65d31-172">Utwórz `php` folderu w katalogu głównym roli procesu roboczego, a następnie dodać do Twojego środowiska uruchomieniowego języka PHP (wszystkie pliki binarne, pliki konfiguracji, podfoldery itp.) `php` folderu.</span><span class="sxs-lookup"><span data-stu-id="65d31-172">Create a `php` folder in the worker role's root directory, and then add your PHP runtime (all binaries, configuration files, subfolders, etc.) to the `php` folder.</span></span>
3. <span data-ttu-id="65d31-173">(OPCJONALNIE) Jeśli korzysta z Twojego środowiska uruchomieniowego języka PHP [Drivers firmy Microsoft dla programów PHP i SQL Server][sqlsrv drivers], musisz skonfigurować swojej roli procesu roboczego, aby zainstalować [programu SQL Server Native Client 2012] [ sql native client] po zainicjowaniu obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="65d31-173">(OPTIONAL) If your PHP runtime uses [Microsoft Drivers for PHP for SQL Server][sqlsrv drivers], you will need to configure your worker role to install [SQL Server Native Client 2012][sql native client] when it is provisioned.</span></span> <span data-ttu-id="65d31-174">Aby to zrobić, należy dodać [Instalator sqlncli.msi x64] do katalogu głównego roli procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="65d31-174">To do this, add the [sqlncli.msi x64 installer] to the worker role's root directory.</span></span> <span data-ttu-id="65d31-175">Po udostępnieniu roli, skryptu uruchomieniowego opisany w następnym kroku zostanie dyskretnie uruchom Instalatora.</span><span class="sxs-lookup"><span data-stu-id="65d31-175">The startup script described in the next step will silently run the installer when the role is provisioned.</span></span> <span data-ttu-id="65d31-176">Jeśli Twojego środowiska uruchomieniowego języka PHP nie używa Drivers firmy Microsoft dla programów PHP i SQL Server, należy usunąć następujący wiersz w skrypcie pokazano w następnym kroku:</span><span class="sxs-lookup"><span data-stu-id="65d31-176">If your PHP runtime does not use the Microsoft Drivers for PHP for SQL Server, you can remove the following line from the script shown in the next step:</span></span>

        msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES
4. <span data-ttu-id="65d31-177">Zdefiniuj zadanie uruchamiania, który dodaje użytkownika `php.exe` pliku wykonywalnego do zmiennej środowiskowej PATH roli procesu roboczego po udostępnieniu roli.</span><span class="sxs-lookup"><span data-stu-id="65d31-177">Define a startup task that adds your `php.exe` executable to the worker role's PATH environment variable when the role is provisioned.</span></span> <span data-ttu-id="65d31-178">Aby to zrobić, otwórz `setup_worker.cmd` plików (w katalogu głównym roli procesu roboczego) w edytorze tekstów i zastąp jego zawartość następujący skrypt:</span><span class="sxs-lookup"><span data-stu-id="65d31-178">To do this, open the `setup_worker.cmd` file (in the worker role's root directory) in a text editor and replace its contents with the following script:</span></span>

    ```cmd
    @echo on

    cd "%~dp0"

    echo Granting permissions for Network Service to the web root directory...
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
5. <span data-ttu-id="65d31-179">Dodawania plików aplikacji do katalogu głównego swojej roli procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="65d31-179">Add your application files to your worker role's root directory.</span></span>
6. <span data-ttu-id="65d31-180">Publikowanie aplikacji, zgodnie z opisem w [opublikować aplikację](#publish-your-application) poniższej sekcji.</span><span class="sxs-lookup"><span data-stu-id="65d31-180">Publish your application as described in the [Publish your application](#publish-your-application) section below.</span></span>

## <a name="run-your-application-in-the-compute-and-storage-emulators"></a><span data-ttu-id="65d31-181">Uruchom aplikację w emulatory zasobów obliczeniowych i magazynu</span><span class="sxs-lookup"><span data-stu-id="65d31-181">Run your application in the compute and storage emulators</span></span>
<span data-ttu-id="65d31-182">Emulatory Azure zapewniają lokalnego środowiska można przetestować aplikację Azure, przed wdrożeniem w chmurze.</span><span class="sxs-lookup"><span data-stu-id="65d31-182">The Azure emulators provide a local environment in which you can test your Azure application before you deploy it to the cloud.</span></span> <span data-ttu-id="65d31-183">Istnieją pewne różnice między emulatorów i środowiska platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="65d31-183">There are some differences between the emulators and the Azure environment.</span></span> <span data-ttu-id="65d31-184">Aby lepiej zrozumieć to, zobacz [użyć emulatora magazynu Azure do programowania i testowania](storage/common/storage-use-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="65d31-184">To understand this better, see [Use the Azure storage emulator for development and testing](storage/common/storage-use-emulator.md).</span></span>

<span data-ttu-id="65d31-185">Należy pamiętać, że użytkownik musi mieć zainstalowane lokalnie, aby użyć emulatora obliczeń PHP.</span><span class="sxs-lookup"><span data-stu-id="65d31-185">Note that you must have PHP installed locally to use the compute emulator.</span></span> <span data-ttu-id="65d31-186">Emulator obliczeń użyje lokalnej instalacji PHP do uruchamiania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="65d31-186">The compute emulator will use your local PHP installation to run your application.</span></span>

<span data-ttu-id="65d31-187">Aby uruchomić projekt w emulatorów, uruchom następujące polecenie z katalogu głównego projektu:</span><span class="sxs-lookup"><span data-stu-id="65d31-187">To run your project in the emulators, execute the following command from your project's root directory:</span></span>

    PS C:\MyProject> Start-AzureEmulator

<span data-ttu-id="65d31-188">Zostaną wyświetlone dane wyjściowe podobne do poniższego:</span><span class="sxs-lookup"><span data-stu-id="65d31-188">You will see output similar to this:</span></span>

    Creating local package...
    Starting Emulator...
    Role is running at http://127.0.0.1:81
    Started

<span data-ttu-id="65d31-189">Widać działanie aplikacji w emulatorze przez otwarcie przeglądarki sieci web i przeglądania lokalny adres wyświetlany w danych wyjściowych (`http://127.0.0.1:81` w powyższym przykładowe dane wyjściowe).</span><span class="sxs-lookup"><span data-stu-id="65d31-189">You can see your application running in the emulator by opening a web browser and browsing to the local address shown in the output (`http://127.0.0.1:81` in the example output above).</span></span>

<span data-ttu-id="65d31-190">Aby zatrzymać emulatorów, wykonanie tego polecenia:</span><span class="sxs-lookup"><span data-stu-id="65d31-190">To stop the emulators, execute this command:</span></span>

    PS C:\MyProject> Stop-AzureEmulator

## <a name="publish-your-application"></a><span data-ttu-id="65d31-191">Publikowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="65d31-191">Publish your application</span></span>
<span data-ttu-id="65d31-192">Aby opublikować aplikację, należy najpierw zaimportować Twoje ustawienia publikowania za pomocą [AzurePublishSettingsFile importu](https://msdn.microsoft.com/library/azure/dn790370.aspx) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="65d31-192">To publish your application, you need to first import your publish settings by using the [Import-AzurePublishSettingsFile](https://msdn.microsoft.com/library/azure/dn790370.aspx) cmdlet.</span></span> <span data-ttu-id="65d31-193">Następnie można opublikować aplikację przy użyciu [Publish-AzureServiceProject](https://msdn.microsoft.com/library/azure/dn495166.aspx) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="65d31-193">Then you can publish your application by using the [Publish-AzureServiceProject](https://msdn.microsoft.com/library/azure/dn495166.aspx) cmdlet.</span></span> <span data-ttu-id="65d31-194">Informacje logowania, zobacz [jak instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="65d31-194">For information about signing in, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="next-steps"></a><span data-ttu-id="65d31-195">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="65d31-195">Next steps</span></span>
<span data-ttu-id="65d31-196">Aby uzyskać więcej informacji, zobacz [Centrum deweloperów języka PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="65d31-196">For more information, see the [PHP Developer Center](/develop/php/).</span></span>

[Zestaw Azure SDK for PHP]: /develop/php/common-tasks/download-php-sdk/
[install ps and emulators]: http://go.microsoft.com/fwlink/p/?linkid=320376&clcid=0x409
[definicji (csdef) usługi]: http://msdn.microsoft.com/library/windowsazure/ee758711.aspx
[konfiguracji usługi (cscfg)]: http://msdn.microsoft.com/library/windowsazure/ee758710.aspx
[iis.net]: http://www.iis.net/
[sql native client]: http://msdn.microsoft.com/sqlserver/aa937733.aspx
[sqlsrv drivers]: http://php.net/sqlsrv
[Instalator sqlncli.msi x64]: http://go.microsoft.com/fwlink/?LinkID=239648
