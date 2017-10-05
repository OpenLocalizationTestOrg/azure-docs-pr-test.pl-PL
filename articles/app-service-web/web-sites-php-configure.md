---
title: "Skonfigurować PHP w aplikacjach sieci Web usługi aplikacji Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak skonfigurować domyślnej instalacji PHP lub Dodaj niestandardowy instalacji PHP dla aplikacji sieci Web w usłudze Azure App Service."
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
ms.openlocfilehash: 624dd416f37aacdb3d2f6e59afdc2efe646e610b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-php-in-azure-app-service-web-apps"></a><span data-ttu-id="a1682-103">Skonfigurować PHP w aplikacjach sieci Web usługi aplikacji Azure</span><span class="sxs-lookup"><span data-stu-id="a1682-103">Configure PHP in Azure App Service Web Apps</span></span>
## <a name="introduction"></a><span data-ttu-id="a1682-104">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="a1682-104">Introduction</span></span>
<span data-ttu-id="a1682-105">W tym przewodniku opisano sposób konfigurowania wbudowanych środowiska uruchomieniowego języka PHP dla aplikacji sieci Web w [usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714), podaj niestandardowego środowiska uruchomieniowego języka PHP i Włącz rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="a1682-105">This guide will show you how to configure the built-in PHP runtime for Web Apps in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714), provide a custom PHP runtime, and enable extensions.</span></span> <span data-ttu-id="a1682-106">Aby korzystać z usługi aplikacji, należy zarejestrować się w celu [bezpłatnej wersji próbnej].</span><span class="sxs-lookup"><span data-stu-id="a1682-106">To use App Service, sign up for the [free trial].</span></span> <span data-ttu-id="a1682-107">Aby uzyskać najbardziej z tego przewodnika, należy najpierw utworzyć aplikację sieci web PHP w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="a1682-107">To get the most from this guide, you should first create a PHP web app in App Service.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="how-to-change-the-built-in-php-version"></a><span data-ttu-id="a1682-108">Porady: zmiana wbudowanych wersji PHP</span><span class="sxs-lookup"><span data-stu-id="a1682-108">How to: Change the built-in PHP version</span></span>
<span data-ttu-id="a1682-109">Domyślnie program PHP w wersji 5.5 jest zainstalowana i natychmiast dostępnej do użycia podczas tworzenia aplikacji sieci web usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a1682-109">By default, PHP 5.5 is installed and immediately available for use when you create an App Service web app.</span></span> <span data-ttu-id="a1682-110">Najlepszym sposobem Zobacz poprawki dostępnych wersji domyślnej konfiguracji i włączone rozszerzenia jest wdrożenie skryptu, który wywołuje [phpinfo()] funkcji.</span><span class="sxs-lookup"><span data-stu-id="a1682-110">The best way to see the available release revision, its default configuration, and the enabled extensions is to deploy a script that calls the [phpinfo()] function.</span></span>

<span data-ttu-id="a1682-111">Wersje PHP 5.6 i PHP 7.0 są również dostępne, ale nie jest włączony domyślnie.</span><span class="sxs-lookup"><span data-stu-id="a1682-111">PHP 5.6 and PHP 7.0 versions are also available, but not enabled by default.</span></span> <span data-ttu-id="a1682-112">Aby zaktualizować wersję PHP, wykonaj jedną z następujących metod:</span><span class="sxs-lookup"><span data-stu-id="a1682-112">To update the PHP version, follow one of these methods:</span></span>

### <a name="azure-portal"></a><span data-ttu-id="a1682-113">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="a1682-113">Azure Portal</span></span>
1. <span data-ttu-id="a1682-114">Przejdź do aplikacji sieci web w [Azure Portal](https://portal.azure.com) i wybierz polecenie **ustawienia** przycisku.</span><span class="sxs-lookup"><span data-stu-id="a1682-114">Browse to your web app in the [Azure Portal](https://portal.azure.com) and click on the **Settings** button.</span></span>
   
    ![Ustawienia aplikacji sieci Web][settings-button]
2. <span data-ttu-id="a1682-116">Z **ustawienia** wybierz bloku **ustawienia aplikacji** i wybierz nową wersję PHP.</span><span class="sxs-lookup"><span data-stu-id="a1682-116">From the **Settings** blade select **Application Settings** and choose the new PHP version.</span></span>
   
    ![Ustawienia aplikacji][application-settings]
3. <span data-ttu-id="a1682-118">Kliknij przycisk **zapisać** przycisk w górnej części **ustawienia aplikacji w sieci Web** bloku.</span><span class="sxs-lookup"><span data-stu-id="a1682-118">Click the **Save** button at the top of the **Web app settings** blade.</span></span>
   
    ![Zapisanie ustawień konfiguracji][save-button]

### <a name="azure-powershell-windows"></a><span data-ttu-id="a1682-120">Program Azure PowerShell (system Windows)</span><span class="sxs-lookup"><span data-stu-id="a1682-120">Azure PowerShell (Windows)</span></span>
1. <span data-ttu-id="a1682-121">Otwórz programu Azure PowerShell, a następnie zaloguj się do swojego konta:</span><span class="sxs-lookup"><span data-stu-id="a1682-121">Open Azure PowerShell, and login to your account:</span></span>
   
        PS C:\> Login-AzureRmAccount
2. <span data-ttu-id="a1682-122">Ustaw wersję PHP dla aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="a1682-122">Set the PHP version for the web app.</span></span>
   
        PS C:\> Set-AzureWebsite -PhpVersion {5.5 | 5.6 | 7.0} -Name {app-name}
3. <span data-ttu-id="a1682-123">Wersja PHP ma teraz wartość.</span><span class="sxs-lookup"><span data-stu-id="a1682-123">The PHP version is now set.</span></span> <span data-ttu-id="a1682-124">Można potwierdzić te ustawienia:</span><span class="sxs-lookup"><span data-stu-id="a1682-124">You can confirm these settings:</span></span>
   
        PS C:\> Get-AzureWebsite -Name {app-name} | findstr PhpVersion

### <a name="azure-command-line-interface-linux-mac-windows"></a><span data-ttu-id="a1682-125">Interfejs wiersza polecenia platformy Azure (Linux, Mac, system Windows)</span><span class="sxs-lookup"><span data-stu-id="a1682-125">Azure Command-Line Interface (Linux, Mac, Windows)</span></span>
<span data-ttu-id="a1682-126">Aby korzystać z interfejsu wiersza polecenia platformy Azure, musi mieć **Node.js** zainstalowany na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="a1682-126">To use the Azure Command-Line Interface, you must have **Node.js** installed on your computer.</span></span>

1. <span data-ttu-id="a1682-127">Otwórz okno terminalu i logowania do konta.</span><span class="sxs-lookup"><span data-stu-id="a1682-127">Open Terminal, and login to your account.</span></span>
   
        azure login
2. <span data-ttu-id="a1682-128">Ustaw wersję PHP dla aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="a1682-128">Set the PHP version for the web app.</span></span>
   
        azure site set --php-version {5.5 | 5.6 | 7.0} {app-name}

3. <span data-ttu-id="a1682-129">Wersja PHP ma teraz wartość.</span><span class="sxs-lookup"><span data-stu-id="a1682-129">The PHP version is now set.</span></span> <span data-ttu-id="a1682-130">Można potwierdzić te ustawienia:</span><span class="sxs-lookup"><span data-stu-id="a1682-130">You can confirm these settings:</span></span>
   
        azure site show {app-name}

> [!NOTE] 
> <span data-ttu-id="a1682-131">[Azure CLI 2.0](https://github.com/Azure/azure-cli) polecenia, które są równoważne z powyższych są:</span><span class="sxs-lookup"><span data-stu-id="a1682-131">The [Azure CLI 2.0](https://github.com/Azure/azure-cli) commands that are equivalent to the above are:</span></span>
>
>

    az login
    az appservice web config update --php-version {5.5 | 5.6 | 7.0} -g {resource-group-name} -n {app-name}
    az appservice web config show -g {resource-group-name} -n {app-name}

## <a name="how-to-change-the-built-in-php-configurations"></a><span data-ttu-id="a1682-132">Porady: Zmienianie wbudowanych konfiguracji PHP</span><span class="sxs-lookup"><span data-stu-id="a1682-132">How to: Change the built-in PHP configurations</span></span>
<span data-ttu-id="a1682-133">Dla dowolnego wbudowanych środowiska uruchomieniowego języka PHP można zmienić opcje konfiguracji, wykonując poniższe kroki.</span><span class="sxs-lookup"><span data-stu-id="a1682-133">For any built-in PHP runtime, you can change any of the configuration options by following the steps below.</span></span> <span data-ttu-id="a1682-134">(Informacje o dyrektywy php.ini znajdują się w temacie [listy dyrektywy php.ini].)</span><span class="sxs-lookup"><span data-stu-id="a1682-134">(For information about php.ini directives, see [List of php.ini directives].)</span></span>

### <a name="changing-phpiniuser-phpiniperdir-phpiniall-configuration-settings"></a><span data-ttu-id="a1682-135">Zmiana PHP\_INI\_użytkownika, PHP\_INI\_PERDIR, PHP\_INI\_wszystkie ustawienia konfiguracji</span><span class="sxs-lookup"><span data-stu-id="a1682-135">Changing PHP\_INI\_USER, PHP\_INI\_PERDIR, PHP\_INI\_ALL configuration settings</span></span>
1. <span data-ttu-id="a1682-136">Dodaj [. user.ini] plik do katalogu głównego.</span><span class="sxs-lookup"><span data-stu-id="a1682-136">Add a [.user.ini] file to your root directory.</span></span>
2. <span data-ttu-id="a1682-137">Ustawienia konfiguracji w celu dodania `.user.ini` plików przy użyciu takiej samej składni, należy użyć w `php.ini` pliku.</span><span class="sxs-lookup"><span data-stu-id="a1682-137">Add configuration settings to the `.user.ini` file using the same syntax you would use in a `php.ini` file.</span></span> <span data-ttu-id="a1682-138">Na przykład, jeśli chcesz włączyć `display_errors` ustawienia i określ `upload_max_filesize` ustawienie 10M, Twoje `.user.ini` plik będzie zawierać ten tekst:</span><span class="sxs-lookup"><span data-stu-id="a1682-138">For example, if you wanted to turn the `display_errors` setting on and set `upload_max_filesize` setting to 10M, your `.user.ini` file would contain this text:</span></span>
   
        ; Example Settings
        display_errors=On
        upload_max_filesize=10M
   
        ; OPTIONAL: Turn this on to write errors to d:\home\LogFiles\php_errors.log
        ; log_errors=On
3. <span data-ttu-id="a1682-139">Wdrażanie aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="a1682-139">Deploy your web app.</span></span>
4. <span data-ttu-id="a1682-140">Uruchom ponownie aplikację sieci web.</span><span class="sxs-lookup"><span data-stu-id="a1682-140">Restart the web app.</span></span> <span data-ttu-id="a1682-141">(Ponowne uruchomienie jest konieczne, ponieważ odczytuje częstotliwość, z którym PHP `.user.ini` podlega pliki `user_ini.cache_ttl` ustawienie, które jest to ustawienie systemowe i jest domyślnie 300 sekund (5 minut).</span><span class="sxs-lookup"><span data-stu-id="a1682-141">(Restarting is necessary because the frequency with which PHP reads `.user.ini` files is governed by the `user_ini.cache_ttl` setting, which is a system level setting and is 300 seconds (5 minutes) by default.</span></span> <span data-ttu-id="a1682-142">Ponowne uruchamianie aplikacji sieci web wymusza PHP, aby odczytać nowe ustawienia w `.user.ini` pliku.)</span><span class="sxs-lookup"><span data-stu-id="a1682-142">Restarting the web app forces PHP to read the new settings in the `.user.ini` file.)</span></span>

<span data-ttu-id="a1682-143">Alternatywą wobec przy użyciu `.user.ini` plików, można użyć [ini_set()] funkcji w skryptach, aby ustawić opcje konfiguracji, które nie są dyrektywy na poziomie systemu.</span><span class="sxs-lookup"><span data-stu-id="a1682-143">As an alternative to using a `.user.ini` file, you can use the [ini_set()] function in scripts to set configuration options that are not system-level directives.</span></span>

### <a name="changing-phpinisystem-configuration-settings"></a><span data-ttu-id="a1682-144">Zmiana PHP\_INI\_ustawień konfiguracji systemu</span><span class="sxs-lookup"><span data-stu-id="a1682-144">Changing PHP\_INI\_SYSTEM configuration settings</span></span>
1. <span data-ttu-id="a1682-145">Dodaj ustawienie aplikacji do aplikacji sieci Web przy użyciu klucza `PHP_INI_SCAN_DIR` i wartości`d:\home\site\ini`</span><span class="sxs-lookup"><span data-stu-id="a1682-145">Add an App Setting to your Web App with the key `PHP_INI_SCAN_DIR` and value `d:\home\site\ini`</span></span>
2. <span data-ttu-id="a1682-146">Utwórz `settings.ini` plików przy użyciu konsoli Kudu (http://&lt;-Nazwa lokacji&gt;. scm.azurewebsite.net) w `d:\home\site\ini` katalogu.</span><span class="sxs-lookup"><span data-stu-id="a1682-146">Create an `settings.ini` file using Kudu Console (http://&lt;site-name&gt;.scm.azurewebsite.net) in the `d:\home\site\ini` directory.</span></span>
3. <span data-ttu-id="a1682-147">Ustawienia konfiguracji w celu dodania `settings.ini` plików przy użyciu takiej samej składni, które ma zostać użyty w pliku php.ini.</span><span class="sxs-lookup"><span data-stu-id="a1682-147">Add configuration settings to the `settings.ini` file using the same syntax you would use in a php.ini file.</span></span> <span data-ttu-id="a1682-148">Na przykład, jeśli chcesz punktu `curl.cainfo` ustawienie `*.crt` pliku i określ dla ustawienia "wincache.maxfilesize" 512 KB, Twoje `settings.ini` plik będzie zawierać ten tekst:</span><span class="sxs-lookup"><span data-stu-id="a1682-148">For example, if you wanted to point the `curl.cainfo` setting to a `*.crt` file and set 'wincache.maxfilesize' setting to 512K, your `settings.ini` file would contain this text:</span></span>
   
        ; Example Settings
        curl.cainfo="%ProgramFiles(x86)%\Git\bin\curl-ca-bundle.crt"
        wincache.maxfilesize=512
4. <span data-ttu-id="a1682-149">Ponownie uruchom aplikację sieci Web, aby załadować zmiany.</span><span class="sxs-lookup"><span data-stu-id="a1682-149">Restart your Web App to load the changes.</span></span>

## <a name="how-to-enable-extensions-in-the-default-php-runtime"></a><span data-ttu-id="a1682-150">Porady: Włącz rozszerzenia w środowisku wykonawczym PHP domyślne</span><span class="sxs-lookup"><span data-stu-id="a1682-150">How to: Enable extensions in the default PHP runtime</span></span>
<span data-ttu-id="a1682-151">Jak wspomniano w poprzedniej sekcji, najlepiej domyślnej wersji PHP, domyślnej konfiguracji i włączone rozszerzenia jest wdrożenie skrypt, który wywołuje [phpinfo()].</span><span class="sxs-lookup"><span data-stu-id="a1682-151">As noted in the previous section, the best way to see the default PHP version, its default configuration, and the enabled extensions is to deploy a script that calls [phpinfo()].</span></span> <span data-ttu-id="a1682-152">Aby włączyć dodatkowe rozszerzenia, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a1682-152">To enable additional extensions, follow the steps below:</span></span>

### <a name="configure-via-ini-settings"></a><span data-ttu-id="a1682-153">Konfigurowanie za pomocą ustawienia ini</span><span class="sxs-lookup"><span data-stu-id="a1682-153">Configure via ini settings</span></span>
1. <span data-ttu-id="a1682-154">Dodaj `ext` do katalogu `d:\home\site` katalogu.</span><span class="sxs-lookup"><span data-stu-id="a1682-154">Add a `ext` directory to the `d:\home\site` directory.</span></span>
2. <span data-ttu-id="a1682-155">Umieść `.dll` rozszerzenia plików `ext` katalog (na przykład `php_xdebug.dll`).</span><span class="sxs-lookup"><span data-stu-id="a1682-155">Put `.dll` extension files in the `ext` directory (for example, `php_xdebug.dll`).</span></span> <span data-ttu-id="a1682-156">Upewnij się, że rozszerzenia są zgodne z domyślną wersją PHP i są VC9 i zgodne z systemem innym niż wątkowo (nts).</span><span class="sxs-lookup"><span data-stu-id="a1682-156">Make sure that the extensions are compatible with default version of PHP and are VC9 and non-thread-safe (nts) compatible.</span></span>
3. <span data-ttu-id="a1682-157">Dodaj ustawienie aplikacji do aplikacji sieci Web przy użyciu klucza `PHP_INI_SCAN_DIR` i wartości`d:\home\site\ini`</span><span class="sxs-lookup"><span data-stu-id="a1682-157">Add an App Setting to your Web App with the key `PHP_INI_SCAN_DIR` and value `d:\home\site\ini`</span></span>
4. <span data-ttu-id="a1682-158">Utwórz `ini` w pliku `d:\home\site\ini` o nazwie `extensions.ini`.</span><span class="sxs-lookup"><span data-stu-id="a1682-158">Create an `ini` file in `d:\home\site\ini` called `extensions.ini`.</span></span>
5. <span data-ttu-id="a1682-159">Ustawienia konfiguracji w celu dodania `extensions.ini` plików przy użyciu takiej samej składni, które ma zostać użyty w pliku php.ini.</span><span class="sxs-lookup"><span data-stu-id="a1682-159">Add configuration settings to the `extensions.ini` file using the same syntax you would use in a php.ini file.</span></span> <span data-ttu-id="a1682-160">Na przykład, jeśli chcesz włączyć rozszerzenia bazy danych MongoDB i narzędzia XDebug Twoje `extensions.ini` plik będzie zawierać ten tekst:</span><span class="sxs-lookup"><span data-stu-id="a1682-160">For example, if you wanted to enable the MongoDB and XDebug extensions, your `extensions.ini` file would contain this text:</span></span>
   
        ; Enable Extensions
        extension=d:\home\site\ext\php_mongo.dll
        zend_extension=d:\home\site\ext\php_xdebug.dll
6. <span data-ttu-id="a1682-161">Ponownie uruchom aplikację sieci Web, aby załadować zmiany.</span><span class="sxs-lookup"><span data-stu-id="a1682-161">Restart your Web App to load the changes.</span></span>

### <a name="configure-via-app-setting"></a><span data-ttu-id="a1682-162">Konfigurowanie za pomocą ustawienia aplikacji</span><span class="sxs-lookup"><span data-stu-id="a1682-162">Configure via App Setting</span></span>
1. <span data-ttu-id="a1682-163">Dodaj `bin` do katalogu głównego katalogu.</span><span class="sxs-lookup"><span data-stu-id="a1682-163">Add a `bin` directory to the root directory.</span></span>
2. <span data-ttu-id="a1682-164">Umieść `.dll` rozszerzenia plików `bin` katalog (na przykład `php_xdebug.dll`).</span><span class="sxs-lookup"><span data-stu-id="a1682-164">Put `.dll` extension files in the `bin` directory (for example, `php_xdebug.dll`).</span></span> <span data-ttu-id="a1682-165">Upewnij się, że rozszerzenia są zgodne z domyślną wersją PHP i są VC9 i zgodne z systemem innym niż wątkowo (nts).</span><span class="sxs-lookup"><span data-stu-id="a1682-165">Make sure that the extensions are compatible with default version of PHP and are VC9 and non-thread-safe (nts) compatible.</span></span>
3. <span data-ttu-id="a1682-166">Wdrażanie aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="a1682-166">Deploy your web app.</span></span>
4. <span data-ttu-id="a1682-167">Przejdź do aplikacji sieci web w portalu Azure i wybierz polecenie **ustawienia** przycisku.</span><span class="sxs-lookup"><span data-stu-id="a1682-167">Browse to your web app in the Azure Portal and click on the **Settings** button.</span></span>
   
    ![Ustawienia aplikacji sieci Web][settings-button]
5. <span data-ttu-id="a1682-169">Z **ustawienia** wybierz bloku **ustawienia aplikacji** i przewiń do **ustawień aplikacji** sekcji.</span><span class="sxs-lookup"><span data-stu-id="a1682-169">From the **Settings** blade select **Application Settings** and scroll to the **App settings** section.</span></span>
6. <span data-ttu-id="a1682-170">W **ustawień aplikacji** sekcji, Utwórz **PHP_EXTENSIONS** klucza.</span><span class="sxs-lookup"><span data-stu-id="a1682-170">In the **App settings** section, create a **PHP_EXTENSIONS** key.</span></span> <span data-ttu-id="a1682-171">Wartość tego klucza będzie ścieżka względem katalogu głównego witryny sieci Web: **bin\your ext, rozszerzenie pliku**.</span><span class="sxs-lookup"><span data-stu-id="a1682-171">The value for this key would be a path relative to website root: **bin\your-ext-file**.</span></span>
   
    ![Włączanie rozszerzenia w ustawieniach aplikacji][php-extensions]
7. <span data-ttu-id="a1682-173">Kliknij przycisk **zapisać** przycisk w górnej części **ustawienia aplikacji w sieci Web** bloku.</span><span class="sxs-lookup"><span data-stu-id="a1682-173">Click the **Save** button at the top of the **Web app settings** blade.</span></span>
   
    ![Zapisanie ustawień konfiguracji][save-button]

<span data-ttu-id="a1682-175">Zend rozszerzenia również są obsługiwane przy użyciu **PHP_ZENDEXTENSIONS** klucza.</span><span class="sxs-lookup"><span data-stu-id="a1682-175">Zend extensions are also supported by using a **PHP_ZENDEXTENSIONS** key.</span></span> <span data-ttu-id="a1682-176">Aby włączyć wiele rozszerzeń, zawiera listę rozdzielaną przecinkami `.dll` pliki do wartości ustawienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a1682-176">To enable multiple extensions, include a comma-separated list of `.dll` files for the app setting value.</span></span>

## <a name="how-to-use-a-custom-php-runtime"></a><span data-ttu-id="a1682-177">Porady: Użyj niestandardowego środowiska uruchomieniowego języka PHP</span><span class="sxs-lookup"><span data-stu-id="a1682-177">How to: Use a custom PHP runtime</span></span>
<span data-ttu-id="a1682-178">Zamiast domyślnego środowiska uruchomieniowego języka PHP aplikacje sieci Web usługi aplikacji można użyć środowiska uruchomieniowego języka PHP, które umożliwiają wykonywanie skryptów PHP.</span><span class="sxs-lookup"><span data-stu-id="a1682-178">Instead of the default PHP runtime, App Service Web Apps can use a PHP runtime that you provide to execute PHP scripts.</span></span> <span data-ttu-id="a1682-179">Środowisko uruchomieniowe, które należy podać można skonfigurować przy `php.ini` pliku, który też podać.</span><span class="sxs-lookup"><span data-stu-id="a1682-179">The runtime that you provide can be configured by a `php.ini` file that you also provide.</span></span> <span data-ttu-id="a1682-180">Aby użyć niestandardowego środowiska uruchomieniowego języka PHP z aplikacjami sieci Web, wykonaj poniższe kroki.</span><span class="sxs-lookup"><span data-stu-id="a1682-180">To use a custom PHP runtime with Web Apps, follow the steps below.</span></span>

1. <span data-ttu-id="a1682-181">Uzyskaj z systemem innym niż wątkowo, VC9 lub VC11 zgodnej wersji programu PHP dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="a1682-181">Obtain a non-thread-safe, VC9 or VC11 compatible version of PHP for Windows.</span></span> <span data-ttu-id="a1682-182">Najnowsze wersje PHP dla systemu Windows można znaleźć tutaj: [http://windows.php.net/download/].</span><span class="sxs-lookup"><span data-stu-id="a1682-182">Recent releases of PHP for Windows can be found here: [http://windows.php.net/download/].</span></span> <span data-ttu-id="a1682-183">Starsze wersje można znaleźć w tym miejscu archiwum: [http://windows.php.net/downloads/releases/archives/].</span><span class="sxs-lookup"><span data-stu-id="a1682-183">Older releases can be found in the archive here: [http://windows.php.net/downloads/releases/archives/].</span></span>
2. <span data-ttu-id="a1682-184">Modyfikowanie `php.ini` Twojego środowiska uruchomieniowego w pliku.</span><span class="sxs-lookup"><span data-stu-id="a1682-184">Modify the `php.ini` file for your runtime.</span></span> <span data-ttu-id="a1682-185">Należy pamiętać, że wszystkie ustawienia konfiguracji, które są dyrektywy system poziom — tylko do będą ignorowane przez aplikacje sieci Web.</span><span class="sxs-lookup"><span data-stu-id="a1682-185">Note that any configuration settings that are system-level-only directives will be ignored by Web Apps.</span></span> <span data-ttu-id="a1682-186">(Informacje dyrektywy system poziom wyłącznie-, zobacz [listy dyrektywy php.ini]).</span><span class="sxs-lookup"><span data-stu-id="a1682-186">(For information about system-level-only directives, see [List of php.ini directives]).</span></span>
3. <span data-ttu-id="a1682-187">Opcjonalnie można dodać rozszerzenia do Twojego środowiska uruchomieniowego języka PHP i włączyć je w `php.ini` pliku.</span><span class="sxs-lookup"><span data-stu-id="a1682-187">Optionally, add extensions to your PHP runtime and enable them in the `php.ini` file.</span></span>
4. <span data-ttu-id="a1682-188">Dodaj `bin` do katalogu głównego i put katalog, który zawiera Twojego środowiska uruchomieniowego języka PHP w tym katalogu (na przykład `bin\php`).</span><span class="sxs-lookup"><span data-stu-id="a1682-188">Add a `bin` directory to your root directory, and put the directory that contains your PHP runtime in it (for example, `bin\php`).</span></span>
5. <span data-ttu-id="a1682-189">Wdrażanie aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="a1682-189">Deploy your web app.</span></span>
6. <span data-ttu-id="a1682-190">Przejdź do aplikacji sieci web w portalu Azure i wybierz polecenie **ustawienia** przycisku.</span><span class="sxs-lookup"><span data-stu-id="a1682-190">Browse to your web app in the Azure Portal and click on the **Settings** button.</span></span>
   
    ![Ustawienia aplikacji sieci Web][settings-button]
7. <span data-ttu-id="a1682-192">Z **ustawienia** wybierz bloku **ustawienia aplikacji** i przewiń do **mapowania obsługi** sekcji.</span><span class="sxs-lookup"><span data-stu-id="a1682-192">From the **Settings** blade select **Application Settings** and scroll to the **Handler mappings** section.</span></span> <span data-ttu-id="a1682-193">Dodaj `*.php` rozszerzenie pola i Dodaj ścieżkę do `php-cgi.exe` pliku wykonywalnego.</span><span class="sxs-lookup"><span data-stu-id="a1682-193">Add `*.php` to the Extension field and add the path to the `php-cgi.exe` executable.</span></span> <span data-ttu-id="a1682-194">Jeśli umieścisz Twojego środowiska uruchomieniowego języka PHP `bin` katalog w katalogu głównym aplikacji, ścieżka będzie `D:\home\site\wwwroot\bin\php\php-cgi.exe`.</span><span class="sxs-lookup"><span data-stu-id="a1682-194">If you put your PHP runtime in the `bin` directory in the root of you application, the path will be `D:\home\site\wwwroot\bin\php\php-cgi.exe`.</span></span>
   
    ![Określ w mapowania programu obsługi program obsługi][handler-mappings]
8. <span data-ttu-id="a1682-196">Kliknij przycisk **zapisać** przycisk w górnej części **ustawienia aplikacji w sieci Web** bloku.</span><span class="sxs-lookup"><span data-stu-id="a1682-196">Click the **Save** button at the top of the **Web app settings** blade.</span></span>
   
    ![Zapisanie ustawień konfiguracji][save-button]

<a name="composer" />

## <a name="how-to-enable-composer-automation-in-azure"></a><span data-ttu-id="a1682-198">Porady: Automatyzowanie Composer na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="a1682-198">How to: Enable Composer automation in Azure</span></span>
<span data-ttu-id="a1682-199">Domyślnie usługi aplikacji nie są wykonywane z composer.json, jeśli istnieje w projekcie PHP.</span><span class="sxs-lookup"><span data-stu-id="a1682-199">By default, App Service doesn't do anything with composer.json, if you have one in your PHP project.</span></span> <span data-ttu-id="a1682-200">Jeśli używasz [wdrożenia Git](app-service-deploy-local-git.md), można włączyć composer.json przetwarzania podczas `git push` , należy włączyć rozszerzenie Composer.</span><span class="sxs-lookup"><span data-stu-id="a1682-200">If you use [Git deployment](app-service-deploy-local-git.md), you can enable composer.json processing during `git push` by enabling the Composer extension.</span></span>

> [!NOTE]
> <span data-ttu-id="a1682-201">Możesz [głos najwyższej jakości Composer pomocy technicznej w usłudze App Service w tym miejscu](https://feedback.azure.com/forums/169385-web-apps-formerly-websites/suggestions/6477437-first-class-support-for-composer-and-pip)!</span><span class="sxs-lookup"><span data-stu-id="a1682-201">You can [vote for first-class Composer support in App Service here](https://feedback.azure.com/forums/169385-web-apps-formerly-websites/suggestions/6477437-first-class-support-for-composer-and-pip)!</span></span>
> 
> 

1. <span data-ttu-id="a1682-202">W przypadku programu PHP sieci web bloku aplikacji w [portalu Azure](https://portal.azure.com), kliknij przycisk **narzędzia** > **rozszerzenia**.</span><span class="sxs-lookup"><span data-stu-id="a1682-202">In your PHP web app's blade in the [Azure portal](https://portal.azure.com), click **Tools** > **Extensions**.</span></span>
   
    ![Azure bloku ustawienia portalu Automatyzowanie Composer na platformie Azure](./media/web-sites-php-configure/composer-extension-settings.png)
2. <span data-ttu-id="a1682-204">Kliknij przycisk **Dodaj**, następnie kliknij przycisk **Composer**.</span><span class="sxs-lookup"><span data-stu-id="a1682-204">Click **Add**, then click **Composer**.</span></span>
   
    ![Dodaj rozszerzenie Composer Automatyzowanie Composer na platformie Azure](./media/web-sites-php-configure/composer-extension-add.png)
3. <span data-ttu-id="a1682-206">Kliknij przycisk **OK** zaakceptować postanowienia prawne.</span><span class="sxs-lookup"><span data-stu-id="a1682-206">Click **OK** to accept legal terms.</span></span> <span data-ttu-id="a1682-207">Kliknij przycisk **OK** ponownie, aby dodać rozszerzenie.</span><span class="sxs-lookup"><span data-stu-id="a1682-207">Click **OK** again to add the extension.</span></span>
   
    <span data-ttu-id="a1682-208">**Zainstalowanych rozszerzeń** bloku będzie zawierać teraz rozszerzenie Composer.</span><span class="sxs-lookup"><span data-stu-id="a1682-208">The **Installed extensions** blade will now show the Composer extension.</span></span>  
    <span data-ttu-id="a1682-209">![Zaakceptuj postanowienia prawne Automatyzowanie Composer na platformie Azure](./media/web-sites-php-configure/composer-extension-view.png)</span><span class="sxs-lookup"><span data-stu-id="a1682-209">![Accept legal terms to enable Composer automation in Azure](./media/web-sites-php-configure/composer-extension-view.png)</span></span>
4. <span data-ttu-id="a1682-210">Teraz, wykonywać `git add`, `git commit`, i `git push` , takich jak w poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="a1682-210">Now, perform `git add`, `git commit`, and `git push` like in the previous section.</span></span> <span data-ttu-id="a1682-211">Pojawi się, czy Composer jest instalowany zdefiniowane w composer.json zależności.</span><span class="sxs-lookup"><span data-stu-id="a1682-211">You'll now see that Composer is installing dependencies defined in composer.json.</span></span>
   
    ![Wdrażanie Git za pomocą automatyzacji Composer na platformie Azure](./media/web-sites-php-configure/composer-extension-success.png)

## <a name="next-steps"></a><span data-ttu-id="a1682-213">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a1682-213">Next steps</span></span>
<span data-ttu-id="a1682-214">Aby uzyskać więcej informacji, zobacz [Centrum deweloperów języka PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="a1682-214">For more information, see the [PHP Developer Center](/develop/php/).</span></span>

> [!NOTE]
> <span data-ttu-id="a1682-215">Jeśli chcesz zacząć korzystać z usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź do artykułu [Try App Service](https://azure.microsoft.com/try/app-service/) (Wypróbuj usługę App Service), w którym wyjaśniono, jak od razu utworzyć początkową aplikację sieci Web o krótkim okresie istnienia w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="a1682-215">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="a1682-216">Bez kart kredytowych i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="a1682-216">No credit cards required; no commitments.</span></span>
> 
> 

<span data-ttu-id="a1682-217">[bezpłatnej wersji próbnej]: https://www.windowsazure.com/pricing/free-trial/</span><span class="sxs-lookup"><span data-stu-id="a1682-217">[free trial]: https://www.windowsazure.com/pricing/free-trial/</span></span>
<span data-ttu-id="a1682-218">[phpinfo()]: http://php.net/manual/en/function.phpinfo.php</span><span class="sxs-lookup"><span data-stu-id="a1682-218">[phpinfo()]: http://php.net/manual/en/function.phpinfo.php</span></span>
[select-php-version]: ./media/web-sites-php-configure/select-php-version.png
<span data-ttu-id="a1682-219">[listy dyrektywy php.ini]: http://www.php.net/manual/en/ini.list.php</span><span class="sxs-lookup"><span data-stu-id="a1682-219">[List of php.ini directives]: http://www.php.net/manual/en/ini.list.php</span></span>
<span data-ttu-id="a1682-220">[. user.ini]: http://www.php.net/manual/en/configuration.file.per-user.php</span><span class="sxs-lookup"><span data-stu-id="a1682-220">[.user.ini]: http://www.php.net/manual/en/configuration.file.per-user.php</span></span>
<span data-ttu-id="a1682-221">[ini_set()]: http://www.php.net/manual/en/function.ini-set.php</span><span class="sxs-lookup"><span data-stu-id="a1682-221">[ini_set()]: http://www.php.net/manual/en/function.ini-set.php</span></span>
[application-settings]: ./media/web-sites-php-configure/application-settings.png
[settings-button]: ./media/web-sites-php-configure/settings-button.png
[save-button]: ./media/web-sites-php-configure/save-button.png
[php-extensions]: ./media/web-sites-php-configure/php-extensions.png
[handler-mappings]: ./media/web-sites-php-configure/handler-mappings.png
<span data-ttu-id="a1682-222">[http://windows.php.net/download/]: http://windows.php.net/download/</span><span class="sxs-lookup"><span data-stu-id="a1682-222">[http://windows.php.net/download/]: http://windows.php.net/download/</span></span>
<span data-ttu-id="a1682-223">[http://windows.php.net/downloads/releases/archives/]: http://windows.php.net/downloads/releases/archives/</span><span class="sxs-lookup"><span data-stu-id="a1682-223">[http://windows.php.net/downloads/releases/archives/]: http://windows.php.net/downloads/releases/archives/</span></span>
[SETPHPVERCLI]: ./media/web-sites-php-configure/ChangePHPVersion-XPlatCLI.png
[GETPHPVERCLI]: ./media/web-sites-php-configure/ShowPHPVersion-XplatCLI.png
[SETPHPVERPS]: ./media/web-sites-php-configure/ChangePHPVersion-PS.png
[GETPHPVERPS]: ./media/web-sites-php-configure/ShowPHPVersion-PS.png

