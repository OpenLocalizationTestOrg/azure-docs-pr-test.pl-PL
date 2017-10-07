---
title: "aaaConfigure PHP w aplikacjach sieci Web usługi aplikacji Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure hello domyślnej instalacji PHP lub Dodaj niestandardowy instalacji PHP dla aplikacji sieci Web w usłudze Azure App Service."
services: app-service
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 95c4072b-8570-496b-9c48-ee21a223fb60
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 2e461e4a269a4ce5614f5f05560f38bc53066251
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-php-in-azure-app-service-web-apps"></a><span data-ttu-id="89fb6-103">Skonfigurować PHP w aplikacjach sieci Web usługi aplikacji Azure</span><span class="sxs-lookup"><span data-stu-id="89fb6-103">Configure PHP in Azure App Service Web Apps</span></span>
## <a name="introduction"></a><span data-ttu-id="89fb6-104">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="89fb6-104">Introduction</span></span>
<span data-ttu-id="89fb6-105">W tym przewodniku opisano, jak tooconfigure hello wbudowanych środowiska uruchomieniowego języka PHP dla aplikacji sieci Web w [usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714), podaj niestandardowego środowiska uruchomieniowego języka PHP i Włącz rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="89fb6-105">This guide will show you how tooconfigure hello built-in PHP runtime for Web Apps in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714), provide a custom PHP runtime, and enable extensions.</span></span> <span data-ttu-id="89fb6-106">toouse App Service, zarejestruj się, aby hello [bezpłatnej wersji próbnej].</span><span class="sxs-lookup"><span data-stu-id="89fb6-106">toouse App Service, sign up for hello [free trial].</span></span> <span data-ttu-id="89fb6-107">Witaj tooget najbardziej z tego podręcznika, należy najpierw utworzyć aplikację sieci web PHP w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="89fb6-107">tooget hello most from this guide, you should first create a PHP web app in App Service.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="how-to-change-hello-built-in-php-version"></a><span data-ttu-id="89fb6-108">Porady: zmiana hello wbudowanych wersji PHP</span><span class="sxs-lookup"><span data-stu-id="89fb6-108">How to: Change hello built-in PHP version</span></span>
<span data-ttu-id="89fb6-109">Domyślnie program PHP w wersji 5.5 jest zainstalowana i natychmiast dostępnej do użycia podczas tworzenia aplikacji sieci web usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="89fb6-109">By default, PHP 5.5 is installed and immediately available for use when you create an App Service web app.</span></span> <span data-ttu-id="89fb6-110">Witaj najlepsze sposób toosee hello dostępnych wersji zmian w, konfiguracji domyślnej i hello włączonego rozszerzenia jest toodeploy skrypt, który wywołuje hello [phpinfo()] funkcji.</span><span class="sxs-lookup"><span data-stu-id="89fb6-110">hello best way toosee hello available release revision, its default configuration, and hello enabled extensions is toodeploy a script that calls hello [phpinfo()] function.</span></span>

<span data-ttu-id="89fb6-111">Wersje PHP 5.6 i PHP 7.0 są również dostępne, ale nie jest włączony domyślnie.</span><span class="sxs-lookup"><span data-stu-id="89fb6-111">PHP 5.6 and PHP 7.0 versions are also available, but not enabled by default.</span></span> <span data-ttu-id="89fb6-112">tooupdate hello wersji PHP, wykonaj jedną z następujących metod:</span><span class="sxs-lookup"><span data-stu-id="89fb6-112">tooupdate hello PHP version, follow one of these methods:</span></span>

### <a name="azure-portal"></a><span data-ttu-id="89fb6-113">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="89fb6-113">Azure Portal</span></span>
1. <span data-ttu-id="89fb6-114">Przeglądaj tooyour aplikacji sieci web w hello [Azure Portal](https://portal.azure.com) i kliknij na powitania **ustawienia** przycisku.</span><span class="sxs-lookup"><span data-stu-id="89fb6-114">Browse tooyour web app in hello [Azure Portal](https://portal.azure.com) and click on hello **Settings** button.</span></span>
   
    ![Ustawienia aplikacji sieci Web][settings-button]
2. <span data-ttu-id="89fb6-116">Z hello **ustawienia** wybierz bloku **ustawienia aplikacji** i wybierz nową wersję PHP hello.</span><span class="sxs-lookup"><span data-stu-id="89fb6-116">From hello **Settings** blade select **Application Settings** and choose hello new PHP version.</span></span>
   
    ![Ustawienia aplikacji][application-settings]
3. <span data-ttu-id="89fb6-118">Kliknij przycisk hello **zapisać** u góry hello hello **ustawienia aplikacji w sieci Web** bloku.</span><span class="sxs-lookup"><span data-stu-id="89fb6-118">Click hello **Save** button at hello top of hello **Web app settings** blade.</span></span>
   
    ![Zapisanie ustawień konfiguracji][save-button]

### <a name="azure-powershell-windows"></a><span data-ttu-id="89fb6-120">Program Azure PowerShell (system Windows)</span><span class="sxs-lookup"><span data-stu-id="89fb6-120">Azure PowerShell (Windows)</span></span>
1. <span data-ttu-id="89fb6-121">Otwórz program Azure PowerShell i konta logowania tooyour:</span><span class="sxs-lookup"><span data-stu-id="89fb6-121">Open Azure PowerShell, and login tooyour account:</span></span>
   
        PS C:\> Login-AzureRmAccount
2. <span data-ttu-id="89fb6-122">Ustaw wersję PHP hello hello aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="89fb6-122">Set hello PHP version for hello web app.</span></span>
   
        PS C:\> Set-AzureWebsite -PhpVersion {5.5 | 5.6 | 7.0} -Name {app-name}
3. <span data-ttu-id="89fb6-123">Wersja PHP Hello ma teraz wartość.</span><span class="sxs-lookup"><span data-stu-id="89fb6-123">hello PHP version is now set.</span></span> <span data-ttu-id="89fb6-124">Można potwierdzić te ustawienia:</span><span class="sxs-lookup"><span data-stu-id="89fb6-124">You can confirm these settings:</span></span>
   
        PS C:\> Get-AzureWebsite -Name {app-name} | findstr PhpVersion

### <a name="azure-command-line-interface-linux-mac-windows"></a><span data-ttu-id="89fb6-125">Interfejs wiersza polecenia platformy Azure (Linux, Mac, system Windows)</span><span class="sxs-lookup"><span data-stu-id="89fb6-125">Azure Command-Line Interface (Linux, Mac, Windows)</span></span>
<span data-ttu-id="89fb6-126">toouse hello interfejsu wiersza polecenia platformy Azure, musisz mieć **Node.js** zainstalowany na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="89fb6-126">toouse hello Azure Command-Line Interface, you must have **Node.js** installed on your computer.</span></span>

1. <span data-ttu-id="89fb6-127">Otwórz Terminal i konta logowania tooyour.</span><span class="sxs-lookup"><span data-stu-id="89fb6-127">Open Terminal, and login tooyour account.</span></span>
   
        azure login
2. <span data-ttu-id="89fb6-128">Ustaw wersję PHP hello hello aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="89fb6-128">Set hello PHP version for hello web app.</span></span>
   
        azure site set --php-version {5.5 | 5.6 | 7.0} {app-name}

3. <span data-ttu-id="89fb6-129">Wersja PHP Hello ma teraz wartość.</span><span class="sxs-lookup"><span data-stu-id="89fb6-129">hello PHP version is now set.</span></span> <span data-ttu-id="89fb6-130">Można potwierdzić te ustawienia:</span><span class="sxs-lookup"><span data-stu-id="89fb6-130">You can confirm these settings:</span></span>
   
        azure site show {app-name}

> [!NOTE] 
> <span data-ttu-id="89fb6-131">Witaj [Azure CLI 2.0](https://github.com/Azure/azure-cli) są poleceń, które są równoważne toohello powyżej:</span><span class="sxs-lookup"><span data-stu-id="89fb6-131">hello [Azure CLI 2.0](https://github.com/Azure/azure-cli) commands that are equivalent toohello above are:</span></span>
>
>

    az login
    az appservice web config update --php-version {5.5 | 5.6 | 7.0} -g {resource-group-name} -n {app-name}
    az appservice web config show -g {resource-group-name} -n {app-name}

## <a name="how-to-change-hello-built-in-php-configurations"></a><span data-ttu-id="89fb6-132">Porady: Zmienianie hello wbudowanych konfiguracji PHP</span><span class="sxs-lookup"><span data-stu-id="89fb6-132">How to: Change hello built-in PHP configurations</span></span>
<span data-ttu-id="89fb6-133">Dla dowolnego wbudowanych środowiska uruchomieniowego języka PHP można zmienić hello opcje konfiguracji, wykonując poniższe kroki hello.</span><span class="sxs-lookup"><span data-stu-id="89fb6-133">For any built-in PHP runtime, you can change any of hello configuration options by following hello steps below.</span></span> <span data-ttu-id="89fb6-134">(Informacje o dyrektywy php.ini znajdują się w temacie [listy dyrektywy php.ini].)</span><span class="sxs-lookup"><span data-stu-id="89fb6-134">(For information about php.ini directives, see [List of php.ini directives].)</span></span>

### <a name="changing-phpiniuser-phpiniperdir-phpiniall-configuration-settings"></a><span data-ttu-id="89fb6-135">Zmiana PHP\_INI\_użytkownika, PHP\_INI\_PERDIR, PHP\_INI\_wszystkie ustawienia konfiguracji</span><span class="sxs-lookup"><span data-stu-id="89fb6-135">Changing PHP\_INI\_USER, PHP\_INI\_PERDIR, PHP\_INI\_ALL configuration settings</span></span>
1. <span data-ttu-id="89fb6-136">Dodaj [. user.ini] katalog główny tooyour pliku.</span><span class="sxs-lookup"><span data-stu-id="89fb6-136">Add a [.user.ini] file tooyour root directory.</span></span>
2. <span data-ttu-id="89fb6-137">Dodaj toohello ustawienia konfiguracji `.user.ini` plik za pomocą hello samej składni, należy użyć w `php.ini` pliku.</span><span class="sxs-lookup"><span data-stu-id="89fb6-137">Add configuration settings toohello `.user.ini` file using hello same syntax you would use in a `php.ini` file.</span></span> <span data-ttu-id="89fb6-138">Na przykład, jeśli potrzebujesz tooturn hello `display_errors` ustawienia i określ `upload_max_filesize` ustawienie too10M, Twoje `.user.ini` plik będzie zawierać ten tekst:</span><span class="sxs-lookup"><span data-stu-id="89fb6-138">For example, if you wanted tooturn hello `display_errors` setting on and set `upload_max_filesize` setting too10M, your `.user.ini` file would contain this text:</span></span>
   
        ; Example Settings
        display_errors=On
        upload_max_filesize=10M
   
        ; OPTIONAL: Turn this on toowrite errors tood:\home\LogFiles\php_errors.log
        ; log_errors=On
3. <span data-ttu-id="89fb6-139">Wdrażanie aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="89fb6-139">Deploy your web app.</span></span>
4. <span data-ttu-id="89fb6-140">Uruchom ponownie hello aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="89fb6-140">Restart hello web app.</span></span> <span data-ttu-id="89fb6-141">(Ponowne uruchomienie jest konieczne, ponieważ odczytuje hello częstotliwość, z którym PHP `.user.ini` plików podlega hello `user_ini.cache_ttl` ustawienie, które jest to ustawienie systemowe i jest domyślnie 300 sekund (5 minut).</span><span class="sxs-lookup"><span data-stu-id="89fb6-141">(Restarting is necessary because hello frequency with which PHP reads `.user.ini` files is governed by hello `user_ini.cache_ttl` setting, which is a system level setting and is 300 seconds (5 minutes) by default.</span></span> <span data-ttu-id="89fb6-142">Nowe ustawienia hello tooread PHP w hello wymusza ponownie uruchomić aplikacji sieci web hello `.user.ini` pliku.)</span><span class="sxs-lookup"><span data-stu-id="89fb6-142">Restarting hello web app forces PHP tooread hello new settings in hello `.user.ini` file.)</span></span>

<span data-ttu-id="89fb6-143">Jako alternatywne toousing `.user.ini` plików, można użyć hello [ini_set()] funkcji w opcje konfiguracji tooset skrypty, które nie są dyrektywy na poziomie systemu.</span><span class="sxs-lookup"><span data-stu-id="89fb6-143">As an alternative toousing a `.user.ini` file, you can use hello [ini_set()] function in scripts tooset configuration options that are not system-level directives.</span></span>

### <a name="changing-phpinisystem-configuration-settings"></a><span data-ttu-id="89fb6-144">Zmiana PHP\_INI\_ustawień konfiguracji systemu</span><span class="sxs-lookup"><span data-stu-id="89fb6-144">Changing PHP\_INI\_SYSTEM configuration settings</span></span>
1. <span data-ttu-id="89fb6-145">Dodaj ustawienie aplikacji tooyour aplikacji sieci Web z kluczem hello `PHP_INI_SCAN_DIR` i wartości`d:\home\site\ini`</span><span class="sxs-lookup"><span data-stu-id="89fb6-145">Add an App Setting tooyour Web App with hello key `PHP_INI_SCAN_DIR` and value `d:\home\site\ini`</span></span>
2. <span data-ttu-id="89fb6-146">Utwórz `settings.ini` plików przy użyciu konsoli Kudu (http://&lt;-Nazwa lokacji&gt;. scm.azurewebsite.net) w hello `d:\home\site\ini` katalogu.</span><span class="sxs-lookup"><span data-stu-id="89fb6-146">Create an `settings.ini` file using Kudu Console (http://&lt;site-name&gt;.scm.azurewebsite.net) in hello `d:\home\site\ini` directory.</span></span>
3. <span data-ttu-id="89fb6-147">Dodaj toohello ustawienia konfiguracji `settings.ini` plik za pomocą hello samej składni, należy użyć w pliku php.ini.</span><span class="sxs-lookup"><span data-stu-id="89fb6-147">Add configuration settings toohello `settings.ini` file using hello same syntax you would use in a php.ini file.</span></span> <span data-ttu-id="89fb6-148">Na przykład, jeśli potrzebujesz toopoint hello `curl.cainfo` ustawienie tooa `*.crt` pliku i ustaw "wincache.maxfilesize" ustawienie too512K, Twoje `settings.ini` plik będzie zawierać ten tekst:</span><span class="sxs-lookup"><span data-stu-id="89fb6-148">For example, if you wanted toopoint hello `curl.cainfo` setting tooa `*.crt` file and set 'wincache.maxfilesize' setting too512K, your `settings.ini` file would contain this text:</span></span>
   
        ; Example Settings
        curl.cainfo="%ProgramFiles(x86)%\Git\bin\curl-ca-bundle.crt"
        wincache.maxfilesize=512
4. <span data-ttu-id="89fb6-149">Uruchom ponownie zmiany hello tooload aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="89fb6-149">Restart your Web App tooload hello changes.</span></span>

## <a name="how-to-enable-extensions-in-hello-default-php-runtime"></a><span data-ttu-id="89fb6-150">Porady: Włączanie rozszerzenia w środowisku uruchomieniowym PHP domyślne hello</span><span class="sxs-lookup"><span data-stu-id="89fb6-150">How to: Enable extensions in hello default PHP runtime</span></span>
<span data-ttu-id="89fb6-151">Zgodnie z opisem w poprzedniej sekcji hello, hello najlepsze sposób toosee hello domyślną wersję PHP jego domyślna konfiguracja i hello włączone rozszerzenia jest toodeploy skrypt, który wywołuje [phpinfo()].</span><span class="sxs-lookup"><span data-stu-id="89fb6-151">As noted in hello previous section, hello best way toosee hello default PHP version, its default configuration, and hello enabled extensions is toodeploy a script that calls [phpinfo()].</span></span> <span data-ttu-id="89fb6-152">tooenable dodatkowe rozszerzenia, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="89fb6-152">tooenable additional extensions, follow hello steps below:</span></span>

### <a name="configure-via-ini-settings"></a><span data-ttu-id="89fb6-153">Konfigurowanie za pomocą ustawienia ini</span><span class="sxs-lookup"><span data-stu-id="89fb6-153">Configure via ini settings</span></span>
1. <span data-ttu-id="89fb6-154">Dodaj `ext` toohello katalogu `d:\home\site` katalogu.</span><span class="sxs-lookup"><span data-stu-id="89fb6-154">Add a `ext` directory toohello `d:\home\site` directory.</span></span>
2. <span data-ttu-id="89fb6-155">Umieść `.dll` pliki rozszerzeń w hello `ext` katalog (na przykład `php_xdebug.dll`).</span><span class="sxs-lookup"><span data-stu-id="89fb6-155">Put `.dll` extension files in hello `ext` directory (for example, `php_xdebug.dll`).</span></span> <span data-ttu-id="89fb6-156">Upewnij się, że rozszerzenia hello są zgodne z domyślną wersją PHP i są VC9 i zgodne z systemem innym niż wątkowo (nts).</span><span class="sxs-lookup"><span data-stu-id="89fb6-156">Make sure that hello extensions are compatible with default version of PHP and are VC9 and non-thread-safe (nts) compatible.</span></span>
3. <span data-ttu-id="89fb6-157">Dodaj ustawienie aplikacji tooyour aplikacji sieci Web z kluczem hello `PHP_INI_SCAN_DIR` i wartości`d:\home\site\ini`</span><span class="sxs-lookup"><span data-stu-id="89fb6-157">Add an App Setting tooyour Web App with hello key `PHP_INI_SCAN_DIR` and value `d:\home\site\ini`</span></span>
4. <span data-ttu-id="89fb6-158">Utwórz `ini` w pliku `d:\home\site\ini` o nazwie `extensions.ini`.</span><span class="sxs-lookup"><span data-stu-id="89fb6-158">Create an `ini` file in `d:\home\site\ini` called `extensions.ini`.</span></span>
5. <span data-ttu-id="89fb6-159">Dodaj toohello ustawienia konfiguracji `extensions.ini` plik za pomocą hello samej składni, należy użyć w pliku php.ini.</span><span class="sxs-lookup"><span data-stu-id="89fb6-159">Add configuration settings toohello `extensions.ini` file using hello same syntax you would use in a php.ini file.</span></span> <span data-ttu-id="89fb6-160">Na przykład, jeśli potrzebujesz rozszerzenia bazy danych MongoDB i narzędzia XDebug tooenable hello Twoje `extensions.ini` plik będzie zawierać ten tekst:</span><span class="sxs-lookup"><span data-stu-id="89fb6-160">For example, if you wanted tooenable hello MongoDB and XDebug extensions, your `extensions.ini` file would contain this text:</span></span>
   
        ; Enable Extensions
        extension=d:\home\site\ext\php_mongo.dll
        zend_extension=d:\home\site\ext\php_xdebug.dll
6. <span data-ttu-id="89fb6-161">Uruchom ponownie zmiany hello tooload aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="89fb6-161">Restart your Web App tooload hello changes.</span></span>

### <a name="configure-via-app-setting"></a><span data-ttu-id="89fb6-162">Konfigurowanie za pomocą ustawienia aplikacji</span><span class="sxs-lookup"><span data-stu-id="89fb6-162">Configure via App Setting</span></span>
1. <span data-ttu-id="89fb6-163">Dodaj `bin` katalog główny toohello katalogu.</span><span class="sxs-lookup"><span data-stu-id="89fb6-163">Add a `bin` directory toohello root directory.</span></span>
2. <span data-ttu-id="89fb6-164">Umieść `.dll` pliki rozszerzeń w hello `bin` katalog (na przykład `php_xdebug.dll`).</span><span class="sxs-lookup"><span data-stu-id="89fb6-164">Put `.dll` extension files in hello `bin` directory (for example, `php_xdebug.dll`).</span></span> <span data-ttu-id="89fb6-165">Upewnij się, że rozszerzenia hello są zgodne z domyślną wersją PHP i są VC9 i zgodne z systemem innym niż wątkowo (nts).</span><span class="sxs-lookup"><span data-stu-id="89fb6-165">Make sure that hello extensions are compatible with default version of PHP and are VC9 and non-thread-safe (nts) compatible.</span></span>
3. <span data-ttu-id="89fb6-166">Wdrażanie aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="89fb6-166">Deploy your web app.</span></span>
4. <span data-ttu-id="89fb6-167">Przeglądaj tooyour aplikacji sieci web w portalu Azure hello i kliknij na powitania **ustawienia** przycisku.</span><span class="sxs-lookup"><span data-stu-id="89fb6-167">Browse tooyour web app in hello Azure Portal and click on hello **Settings** button.</span></span>
   
    ![Ustawienia aplikacji sieci Web][settings-button]
5. <span data-ttu-id="89fb6-169">Z hello **ustawienia** wybierz bloku **ustawienia aplikacji** i przewiń toohello **ustawień aplikacji** sekcji.</span><span class="sxs-lookup"><span data-stu-id="89fb6-169">From hello **Settings** blade select **Application Settings** and scroll toohello **App settings** section.</span></span>
6. <span data-ttu-id="89fb6-170">W hello **ustawień aplikacji** sekcji, Utwórz **PHP_EXTENSIONS** klucza.</span><span class="sxs-lookup"><span data-stu-id="89fb6-170">In hello **App settings** section, create a **PHP_EXTENSIONS** key.</span></span> <span data-ttu-id="89fb6-171">Witaj wartość tego klucza będzie głównego toowebsite względną ścieżkę: **bin\your ext, rozszerzenie pliku**.</span><span class="sxs-lookup"><span data-stu-id="89fb6-171">hello value for this key would be a path relative toowebsite root: **bin\your-ext-file**.</span></span>
   
    ![Włączanie rozszerzenia w ustawieniach aplikacji][php-extensions]
7. <span data-ttu-id="89fb6-173">Kliknij przycisk hello **zapisać** u góry hello hello **ustawienia aplikacji w sieci Web** bloku.</span><span class="sxs-lookup"><span data-stu-id="89fb6-173">Click hello **Save** button at hello top of hello **Web app settings** blade.</span></span>
   
    ![Zapisanie ustawień konfiguracji][save-button]

<span data-ttu-id="89fb6-175">Zend rozszerzenia również są obsługiwane przy użyciu **PHP_ZENDEXTENSIONS** klucza.</span><span class="sxs-lookup"><span data-stu-id="89fb6-175">Zend extensions are also supported by using a **PHP_ZENDEXTENSIONS** key.</span></span> <span data-ttu-id="89fb6-176">tooenable obejmują wiele rozszerzeń rozdzielaną przecinkami listę `.dll` pliki do wartości ustawienia aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="89fb6-176">tooenable multiple extensions, include a comma-separated list of `.dll` files for hello app setting value.</span></span>

## <a name="how-to-use-a-custom-php-runtime"></a><span data-ttu-id="89fb6-177">Porady: Użyj niestandardowego środowiska uruchomieniowego języka PHP</span><span class="sxs-lookup"><span data-stu-id="89fb6-177">How to: Use a custom PHP runtime</span></span>
<span data-ttu-id="89fb6-178">Zamiast hello środowiska uruchomieniowego języka PHP domyślne aplikacje sieci Web usługi aplikacji można użyć środowiska uruchomieniowego języka PHP Podaj tooexecute skrypty PHP.</span><span class="sxs-lookup"><span data-stu-id="89fb6-178">Instead of hello default PHP runtime, App Service Web Apps can use a PHP runtime that you provide tooexecute PHP scripts.</span></span> <span data-ttu-id="89fb6-179">środowisko uruchomieniowe Hello, które należy podać można skonfigurować przy `php.ini` pliku, który też podać.</span><span class="sxs-lookup"><span data-stu-id="89fb6-179">hello runtime that you provide can be configured by a `php.ini` file that you also provide.</span></span> <span data-ttu-id="89fb6-180">toouse niestandardowego środowiska uruchomieniowego języka PHP z aplikacjami sieci Web, wykonaj kroki hello poniżej.</span><span class="sxs-lookup"><span data-stu-id="89fb6-180">toouse a custom PHP runtime with Web Apps, follow hello steps below.</span></span>

1. <span data-ttu-id="89fb6-181">Uzyskaj z systemem innym niż wątkowo, VC9 lub VC11 zgodnej wersji programu PHP dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="89fb6-181">Obtain a non-thread-safe, VC9 or VC11 compatible version of PHP for Windows.</span></span> <span data-ttu-id="89fb6-182">Najnowsze wersje PHP dla systemu Windows można znaleźć tutaj: [http://windows.php.net/download/].</span><span class="sxs-lookup"><span data-stu-id="89fb6-182">Recent releases of PHP for Windows can be found here: [http://windows.php.net/download/].</span></span> <span data-ttu-id="89fb6-183">Starsze wersje można znaleźć w tym miejscu archiwum hello: [http://windows.php.net/downloads/releases/archives/].</span><span class="sxs-lookup"><span data-stu-id="89fb6-183">Older releases can be found in hello archive here: [http://windows.php.net/downloads/releases/archives/].</span></span>
2. <span data-ttu-id="89fb6-184">Modyfikowanie hello `php.ini` Twojego środowiska uruchomieniowego w pliku.</span><span class="sxs-lookup"><span data-stu-id="89fb6-184">Modify hello `php.ini` file for your runtime.</span></span> <span data-ttu-id="89fb6-185">Należy pamiętać, że wszystkie ustawienia konfiguracji, które są dyrektywy system poziom — tylko do będą ignorowane przez aplikacje sieci Web.</span><span class="sxs-lookup"><span data-stu-id="89fb6-185">Note that any configuration settings that are system-level-only directives will be ignored by Web Apps.</span></span> <span data-ttu-id="89fb6-186">(Informacje dyrektywy system poziom wyłącznie-, zobacz [listy dyrektywy php.ini]).</span><span class="sxs-lookup"><span data-stu-id="89fb6-186">(For information about system-level-only directives, see [List of php.ini directives]).</span></span>
3. <span data-ttu-id="89fb6-187">Opcjonalnie dodaj środowiska uruchomieniowego języka PHP tooyour rozszerzenia i włączyć je w hello `php.ini` pliku.</span><span class="sxs-lookup"><span data-stu-id="89fb6-187">Optionally, add extensions tooyour PHP runtime and enable them in hello `php.ini` file.</span></span>
4. <span data-ttu-id="89fb6-188">Dodaj `bin` katalog główny tooyour katalog i umieść hello katalog, który zawiera Twojego środowiska uruchomieniowego języka PHP w nim (na przykład `bin\php`).</span><span class="sxs-lookup"><span data-stu-id="89fb6-188">Add a `bin` directory tooyour root directory, and put hello directory that contains your PHP runtime in it (for example, `bin\php`).</span></span>
5. <span data-ttu-id="89fb6-189">Wdrażanie aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="89fb6-189">Deploy your web app.</span></span>
6. <span data-ttu-id="89fb6-190">Przeglądaj tooyour aplikacji sieci web w portalu Azure hello i kliknij na powitania **ustawienia** przycisku.</span><span class="sxs-lookup"><span data-stu-id="89fb6-190">Browse tooyour web app in hello Azure Portal and click on hello **Settings** button.</span></span>
   
    ![Ustawienia aplikacji sieci Web][settings-button]
7. <span data-ttu-id="89fb6-192">Z hello **ustawienia** wybierz bloku **ustawienia aplikacji** i przewiń toohello **mapowania obsługi** sekcji.</span><span class="sxs-lookup"><span data-stu-id="89fb6-192">From hello **Settings** blade select **Application Settings** and scroll toohello **Handler mappings** section.</span></span> <span data-ttu-id="89fb6-193">Dodaj `*.php` toohello rozszerzenie pola i Dodaj hello ścieżki toohello `php-cgi.exe` pliku wykonywalnego.</span><span class="sxs-lookup"><span data-stu-id="89fb6-193">Add `*.php` toohello Extension field and add hello path toohello `php-cgi.exe` executable.</span></span> <span data-ttu-id="89fb6-194">Jeśli umieścisz Twojego środowiska uruchomieniowego języka PHP w hello `bin` katalog w katalogu głównym aplikacji hello, ścieżka hello będzie `D:\home\site\wwwroot\bin\php\php-cgi.exe`.</span><span class="sxs-lookup"><span data-stu-id="89fb6-194">If you put your PHP runtime in hello `bin` directory in hello root of you application, hello path will be `D:\home\site\wwwroot\bin\php\php-cgi.exe`.</span></span>
   
    ![Określ w mapowania programu obsługi program obsługi][handler-mappings]
8. <span data-ttu-id="89fb6-196">Kliknij przycisk hello **zapisać** u góry hello hello **ustawienia aplikacji w sieci Web** bloku.</span><span class="sxs-lookup"><span data-stu-id="89fb6-196">Click hello **Save** button at hello top of hello **Web app settings** blade.</span></span>
   
    ![Zapisanie ustawień konfiguracji][save-button]

<a name="composer" />

## <a name="how-to-enable-composer-automation-in-azure"></a><span data-ttu-id="89fb6-198">Porady: Automatyzowanie Composer na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="89fb6-198">How to: Enable Composer automation in Azure</span></span>
<span data-ttu-id="89fb6-199">Domyślnie usługi aplikacji nie są wykonywane z composer.json, jeśli istnieje w projekcie PHP.</span><span class="sxs-lookup"><span data-stu-id="89fb6-199">By default, App Service doesn't do anything with composer.json, if you have one in your PHP project.</span></span> <span data-ttu-id="89fb6-200">Jeśli używasz [wdrożenia Git](app-service-deploy-local-git.md), można włączyć composer.json przetwarzania podczas `git push` , należy włączyć rozszerzenie Composer hello.</span><span class="sxs-lookup"><span data-stu-id="89fb6-200">If you use [Git deployment](app-service-deploy-local-git.md), you can enable composer.json processing during `git push` by enabling hello Composer extension.</span></span>

> [!NOTE]
> <span data-ttu-id="89fb6-201">Możesz [głos najwyższej jakości Composer pomocy technicznej w usłudze App Service w tym miejscu](https://feedback.azure.com/forums/169385-web-apps-formerly-websites/suggestions/6477437-first-class-support-for-composer-and-pip)!</span><span class="sxs-lookup"><span data-stu-id="89fb6-201">You can [vote for first-class Composer support in App Service here](https://feedback.azure.com/forums/169385-web-apps-formerly-websites/suggestions/6477437-first-class-support-for-composer-and-pip)!</span></span>
> 
> 

1. <span data-ttu-id="89fb6-202">W przypadku programu PHP sieci web bloku aplikacji w hello [portalu Azure](https://portal.azure.com), kliknij przycisk **narzędzia** > **rozszerzenia**.</span><span class="sxs-lookup"><span data-stu-id="89fb6-202">In your PHP web app's blade in hello [Azure portal](https://portal.azure.com), click **Tools** > **Extensions**.</span></span>
   
    ![Azure Portal ustawienia bloku tooenable Composer Automatyzacja na platformie Azure](./media/web-sites-php-configure/composer-extension-settings.png)
2. <span data-ttu-id="89fb6-204">Kliknij przycisk **Dodaj**, następnie kliknij przycisk **Composer**.</span><span class="sxs-lookup"><span data-stu-id="89fb6-204">Click **Add**, then click **Composer**.</span></span>
   
    ![Dodaj automatyzacji Composer tooenable rozszerzenie Composer na platformie Azure](./media/web-sites-php-configure/composer-extension-add.png)
3. <span data-ttu-id="89fb6-206">Kliknij przycisk **OK** tooaccept postanowienia prawne.</span><span class="sxs-lookup"><span data-stu-id="89fb6-206">Click **OK** tooaccept legal terms.</span></span> <span data-ttu-id="89fb6-207">Kliknij przycisk **OK** ponownie tooadd hello rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="89fb6-207">Click **OK** again tooadd hello extension.</span></span>
   
    <span data-ttu-id="89fb6-208">Witaj **zainstalowanych rozszerzeń** bloku będzie zawierać teraz rozszerzenie Composer hello.</span><span class="sxs-lookup"><span data-stu-id="89fb6-208">hello **Installed extensions** blade will now show hello Composer extension.</span></span>  
    <span data-ttu-id="89fb6-209">![Zaakceptuj postanowienia prawne tooenable Composer Automatyzacja na platformie Azure](./media/web-sites-php-configure/composer-extension-view.png)</span><span class="sxs-lookup"><span data-stu-id="89fb6-209">![Accept legal terms tooenable Composer automation in Azure](./media/web-sites-php-configure/composer-extension-view.png)</span></span>
4. <span data-ttu-id="89fb6-210">Teraz, wykonywać `git add`, `git commit`, i `git push` podobnie jak w poprzedniej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="89fb6-210">Now, perform `git add`, `git commit`, and `git push` like in hello previous section.</span></span> <span data-ttu-id="89fb6-211">Pojawi się, czy Composer jest instalowany zdefiniowane w composer.json zależności.</span><span class="sxs-lookup"><span data-stu-id="89fb6-211">You'll now see that Composer is installing dependencies defined in composer.json.</span></span>
   
    ![Wdrażanie Git za pomocą automatyzacji Composer na platformie Azure](./media/web-sites-php-configure/composer-extension-success.png)

## <a name="next-steps"></a><span data-ttu-id="89fb6-213">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="89fb6-213">Next steps</span></span>
<span data-ttu-id="89fb6-214">Aby uzyskać więcej informacji, zobacz hello [Centrum deweloperów języka PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="89fb6-214">For more information, see hello [PHP Developer Center](/develop/php/).</span></span>

> [!NOTE]
> <span data-ttu-id="89fb6-215">Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="89fb6-215">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="89fb6-216">Bez kart kredytowych i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="89fb6-216">No credit cards required; no commitments.</span></span>
> 
> 

[bezpłatna wersja próbna]: https://www.windowsazure.com/pricing/free-trial/
[phpinfo()]: http://php.net/manual/en/function.phpinfo.php
[select-php-version]: ./media/web-sites-php-configure/select-php-version.png
[Lista php.ini dyrektywy]: http://www.php.net/manual/en/ini.list.php
[. user.ini]: http://www.php.net/manual/en/configuration.file.per-user.php
[ini_set()]: http://www.php.net/manual/en/function.ini-set.php
[application-settings]: ./media/web-sites-php-configure/application-settings.png
[settings-button]: ./media/web-sites-php-configure/settings-button.png
[save-button]: ./media/web-sites-php-configure/save-button.png
[php-extensions]: ./media/web-sites-php-configure/php-extensions.png
[handler-mappings]: ./media/web-sites-php-configure/handler-mappings.png
[http://Windows.php.NET/Download/]: http://windows.php.net/download/
[http://Windows.php.NET/downloads/Releases/Archives/]: http://windows.php.net/downloads/releases/archives/
[SETPHPVERCLI]: ./media/web-sites-php-configure/ChangePHPVersion-XPlatCLI.png
[GETPHPVERCLI]: ./media/web-sites-php-configure/ShowPHPVersion-XplatCLI.png
[SETPHPVERPS]: ./media/web-sites-php-configure/ChangePHPVersion-PS.png
[GETPHPVERPS]: ./media/web-sites-php-configure/ShowPHPVersion-PS.png

