---
title: "Wykorzystywać środowisk opracowywania oprogramowania dla aplikacji sieci web | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać miejsc wdrożenia do konfigurowania i zarządzania nią wiele środowisk deweloperskich dla aplikacji"
services: app-service\web
documentationcenter: 
author: sunbuild
manager: yochayk
editor: 
ms.assetid: 16a594dc-61f5-4984-b5ca-9d5abc39fb1e
ms.service: app-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 10/24/2016
ms.author: sumuth
ms.openlocfilehash: 25248411659f6c7b2e386e310428c365c44ea2e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-devops-environments-effectively-for-your-web-apps"></a><span data-ttu-id="e4493-103">Wykorzystywać środowisk opracowywania oprogramowania dla aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="e4493-103">Use DevOps environments effectively for your web apps</span></span>
<span data-ttu-id="e4493-104">W tym artykule przedstawiono sposób konfigurowania i zarządzania nią wdrożenia aplikacji sieci web, gdy wiele wersji aplikacji znajdują się w różnych środowiskach, takich jak projektowanie, przemieszczania jakości (QA) i produkcji.</span><span class="sxs-lookup"><span data-stu-id="e4493-104">This article shows you how to set up and manage web application deployments when multiple versions of your application are in various environments, such as development, staging, quality assurance (QA), and production.</span></span> <span data-ttu-id="e4493-105">Każda wersja aplikacji mogą być uważane Środowisko deweloperskie do określonego celu procesu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="e4493-105">Each version of your application can be considered as a development environment for the specific purpose of your deployment process.</span></span> <span data-ttu-id="e4493-106">Na przykład deweloperzy mogą używać środowiska pytań i odpowiedzi, aby przetestować jakość aplikacji przed ich Wypchnij zmiany do środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="e4493-106">For example, developers can use the QA environment to test the quality of the application before they push the changes to production.</span></span>
<span data-ttu-id="e4493-107">Wiele środowisk deweloperskich może być wyzwaniem, ponieważ należy do śledzenia kodu, zarządzanie zasobami (obliczeniowych, aplikacji sieci web, bazy danych, pamięci podręcznej, itp.) i wdrożyć kod w środowiskach.</span><span class="sxs-lookup"><span data-stu-id="e4493-107">Multiple development environments can be a challenge because you need to track code, manage resources (compute, web app, database, cache, etc.), and deploy code across environments.</span></span>

## <a name="set-up-a-non-production-environment-stage-dev-qa"></a><span data-ttu-id="e4493-108">Konfigurowanie środowiska nieprodukcyjnych (etap, deweloperów, pytań i odpowiedzi)</span><span class="sxs-lookup"><span data-stu-id="e4493-108">Set up a non-production environment (stage, dev, QA)</span></span>
<span data-ttu-id="e4493-109">Po skonfigurowaniu i uruchomieniu aplikacji sieci web produkcyjnej następnym krokiem jest utworzenie środowiskach nieprodukcyjnych.</span><span class="sxs-lookup"><span data-stu-id="e4493-109">After a production web app is up and running, the next step is to create a non-production environment.</span></span> <span data-ttu-id="e4493-110">Aby korzystać z miejsc wdrożenia, upewnij się, że działają w trybie planu Standard lub Premium usługi Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="e4493-110">To use deployment slots, make sure that you are running in the Standard or Premium Azure App Service plan mode.</span></span> <span data-ttu-id="e4493-111">Miejsca wdrożenia są aplikacje sieci web, które mają własne nazwy hosta.</span><span class="sxs-lookup"><span data-stu-id="e4493-111">Deployment slots are live web apps that have their own host names.</span></span> <span data-ttu-id="e4493-112">Elementy zawartości i konfiguracji aplikacji sieci Web może być zamieniona między dwóch miejsc wdrożenia, w tym miejsca produkcji.</span><span class="sxs-lookup"><span data-stu-id="e4493-112">Web app content and configuration elements can be swapped between two deployment slots, including the production slot.</span></span> <span data-ttu-id="e4493-113">Podczas wdrażania aplikacji w miejscu wdrożenia można uzyskać następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="e4493-113">When you deploy your application to a deployment slot, you get the following benefits:</span></span>

- <span data-ttu-id="e4493-114">Można sprawdzić poprawność zmiany w aplikacji sieci web w tymczasowej miejsce wdrożenia przed wymiany aplikacji z miejscem produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="e4493-114">You can validate changes to a web app in a staging deployment slot before you swap the app with the production slot.</span></span>
- <span data-ttu-id="e4493-115">Podczas wdrażania aplikacji sieci web na gnieździe najpierw i zamienić go w środowisku produkcyjnym, wszystkie wystąpienia gniazda są przygotowaniu miejsca przed wymieniane w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="e4493-115">When you deploy a web app to a slot first and swap it into production, all instances of the slot are warmed up before being swapped into production.</span></span> <span data-ttu-id="e4493-116">Ten proces eliminuje przestoju podczas wdrażania aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="e4493-116">This process eliminates downtime when you deploy your web app.</span></span> <span data-ttu-id="e4493-117">Przekierowywanie ruchu jest łatwego i żadne żądania są usuwane z powodu operacji wymiany.</span><span class="sxs-lookup"><span data-stu-id="e4493-117">The traffic redirection is seamless, and no requests are dropped due to swap operations.</span></span> <span data-ttu-id="e4493-118">Aby zautomatyzować ten całego przepływu pracy, należy skonfigurować [automatycznej wymiany](web-sites-staged-publishing.md#configure-auto-swap) podczas weryfikacji przed wymiany nie jest wymagana.</span><span class="sxs-lookup"><span data-stu-id="e4493-118">To automate this entire workflow, configure [Auto Swap](web-sites-staged-publishing.md#configure-auto-swap) when pre-swap validation is not needed.</span></span>
- <span data-ttu-id="e4493-119">Po wymiany miejsca, który ma teraz aplikacji sieci web wcześniej przygotowanych ma poprzedniej aplikacji sieci web produkcyjnej.</span><span class="sxs-lookup"><span data-stu-id="e4493-119">After a swap, the slot that has the previously staged web app now has the previous production web app.</span></span> <span data-ttu-id="e4493-120">W przypadku zmiany miejscami do miejsca produkcji są niezgodne z oczekiwaniami, można przeprowadzić wymiany tego samego natychmiast pobrać sieci web "Ostatnia znana dobra konfiguracja" aplikacji z powrotem.</span><span class="sxs-lookup"><span data-stu-id="e4493-120">If the changes swapped into the production slot are not as you expected, you can perform the same swap immediately to get your "last known good" web app back.</span></span>

<span data-ttu-id="e4493-121">Aby skonfigurować przemieszczania miejsce wdrożenia, zobacz [Konfigurowanie środowiska dla aplikacji sieci web w usłudze Azure App Service przejściowe](web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="e4493-121">To set up a staging deployment slot, see [Set up staging environments for web apps in Azure App Service](web-sites-staged-publishing.md).</span></span> <span data-ttu-id="e4493-122">Każde środowisko powinna zawierać własny zestaw zasobów.</span><span class="sxs-lookup"><span data-stu-id="e4493-122">Every environment should include its own set of resources.</span></span> <span data-ttu-id="e4493-123">Na przykład jeśli aplikacja sieci web korzysta z bazy danych, następnie zarówno produkcyjne i przejściowe aplikacji sieci web należy używać różnych baz danych.</span><span class="sxs-lookup"><span data-stu-id="e4493-123">For example, if your web app uses a database, then both production and staging web apps should use different databases.</span></span> <span data-ttu-id="e4493-124">Dodaj przemieszczania programowanie środowiska zasoby, takie jak bazy danych, magazynu lub pamięci podręcznej, aby ustawić przejściowego środowiska deweloperskiego.</span><span class="sxs-lookup"><span data-stu-id="e4493-124">Add staging development environment resources such as database, storage, or cache to set your staging development environment.</span></span>

## <a name="examples-of-using-multiple-development-environments"></a><span data-ttu-id="e4493-125">Przykłady użycia wielu środowisk deweloperskich</span><span class="sxs-lookup"><span data-stu-id="e4493-125">Examples of using multiple development environments</span></span>
<span data-ttu-id="e4493-126">Żadnego projektu należy stosować zarządzania kodem źródłowym z co najmniej dwóch środowisk: Programowanie i produkcji.</span><span class="sxs-lookup"><span data-stu-id="e4493-126">Any project should follow source code management with at least two environments: development and production.</span></span> <span data-ttu-id="e4493-127">Korzystając z systemów zarządzania zawartością (CMSs), platformy aplikacji, itp., aplikacja może nie obsługiwać ten scenariusz bez dostosowania.</span><span class="sxs-lookup"><span data-stu-id="e4493-127">If you use content management systems (CMSs), application frameworks, etc., the application might not support this scenario without customization.</span></span> <span data-ttu-id="e4493-128">Tej możliwości ma wartość true dla kilku popularnych platformach, które opisano w poniższych sekcjach.</span><span class="sxs-lookup"><span data-stu-id="e4493-128">This eventuality is true for some of the popular frameworks that are discussed in the following sections.</span></span> <span data-ttu-id="e4493-129">Wiele pytań wyniknąć podczas pracy z CMS/platform, takich jak:</span><span class="sxs-lookup"><span data-stu-id="e4493-129">Lots of questions come to mind when you work with CMS/frameworks, such as:</span></span>

- <span data-ttu-id="e4493-130">Jak możesz rozbicie zawartość w różnych środowiskach?</span><span class="sxs-lookup"><span data-stu-id="e4493-130">How do you break the content out into different environments?</span></span>
- <span data-ttu-id="e4493-131">Jakie pliki można zmienić bez wpływu na aktualizacje wersji framework?</span><span class="sxs-lookup"><span data-stu-id="e4493-131">What files can you change without affecting framework version updates?</span></span>
- <span data-ttu-id="e4493-132">Sposób zarządzania konfiguracjami na środowisko</span><span class="sxs-lookup"><span data-stu-id="e4493-132">How do you manage configurations per environment?</span></span>
- <span data-ttu-id="e4493-133">Jak zarządzać wersji aktualizacji dla modułów, dodatki plug-in i core framework?</span><span class="sxs-lookup"><span data-stu-id="e4493-133">How do you manage version updates for modules, plugins, and the core framework?</span></span>

<span data-ttu-id="e4493-134">Istnieje wiele sposobów, aby skonfigurować wiele środowisk dla projektu.</span><span class="sxs-lookup"><span data-stu-id="e4493-134">There are many ways to set up multiple environments for your project.</span></span> <span data-ttu-id="e4493-135">W poniższych przykładach pokazano jedną metodę dla każdej odpowiedniej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e4493-135">The following examples show one method for each respective application.</span></span>

### <a name="wordpress"></a><span data-ttu-id="e4493-136">WordPress</span><span class="sxs-lookup"><span data-stu-id="e4493-136">WordPress</span></span>
<span data-ttu-id="e4493-137">W tej sekcji dowiesz się, jak skonfigurować przepływ pracy wdrażania przy użyciu miejsc WordPress.</span><span class="sxs-lookup"><span data-stu-id="e4493-137">In this section, you will learn how to set up a deployment workflow by using slots for WordPress.</span></span> <span data-ttu-id="e4493-138">WordPress, na przykład większość rozwiązań CMS, nie obsługuje wiele środowisk deweloperskich bez dostosowania.</span><span class="sxs-lookup"><span data-stu-id="e4493-138">WordPress, like most CMS solutions, does not support multiple development environments without customization.</span></span> <span data-ttu-id="e4493-139">Funkcja Web Apps w usłudze Azure App Service ma kilka funkcji, które ułatwiają do przechowywania ustawień konfiguracji poza swój kod.</span><span class="sxs-lookup"><span data-stu-id="e4493-139">The Web Apps feature of Azure App Service has a few features that make it easy to store configuration settings outside your code.</span></span>

1. <span data-ttu-id="e4493-140">Przed utworzeniem miejsca przemieszczania, należy skonfigurować kod aplikacji do obsługi wielu środowisk.</span><span class="sxs-lookup"><span data-stu-id="e4493-140">Before you create a staging slot, set up your application code to support multiple environments.</span></span> <span data-ttu-id="e4493-141">Aby obsługiwać wiele środowisk w WordPress, należy edytować `wp-config.php` na komputerze lokalnym sieci web app i Dodaj następujący kod na początku pliku.</span><span class="sxs-lookup"><span data-stu-id="e4493-141">To support multiple environments in WordPress, you need to edit `wp-config.php` on your local development web app and add the following code at the beginning of the file.</span></span> <span data-ttu-id="e4493-142">Ten proces spowoduje włączenie aplikacji do pobrania prawidłowej konfiguracji na podstawie wybranego środowiska.</span><span class="sxs-lookup"><span data-stu-id="e4493-142">This process will enable your application to pick the correct configuration based on the selected environment.</span></span>

    ```
    // Support multiple environments
    // set the config file based on current environment
    if (strpos($_SERVER['HTTP_HOST'],'localhost') !== false) {
    // local development
     $config_file = 'config/wp-config.local.php';
    }
    elseif ((strpos(getenv('WP_ENV'),'stage') !== false) || (strpos(getenv('WP_ENV'),'prod' )!== false ))
    //single file for all azure development environments
     $config_file = 'config/wp-config.azure.php';
    }
    $path = dirname(__FILE__). '/';
    if (file_exists($path. $config_file)) {
    // include the config file if it exists, otherwise WP is going to fail
    require_once $path. $config_file;
    ```

2. <span data-ttu-id="e4493-143">Utwórz folder w katalogu głównym aplikacji sieci web o nazwie `config`i Dodaj `wp-config.azure.php` i `wp-config.local.php` pliki, które zawierają odpowiednio Twojego środowiska platformy Azure i lokalnego środowiska.</span><span class="sxs-lookup"><span data-stu-id="e4493-143">Create a folder under web app root called `config`, and add the `wp-config.azure.php` and `wp-config.local.php` files, which represent your Azure environment and local environment respectively.</span></span>

3. <span data-ttu-id="e4493-144">Skopiuj następujące w `wp-config.local.php`:</span><span class="sxs-lookup"><span data-stu-id="e4493-144">Copy the following in `wp-config.local.php`:</span></span>

    ```
    <?php
    // MySQL settings
    /** The name of the database for WordPress */

    define('DB_NAME', 'yourdatabasename');

    /** MySQL database username */
    define('DB_USER', 'yourdbuser');

    /** MySQL database password */
    define('DB_PASSWORD', 'yourpassword');

    /** MySQL hostname */
    define('DB_HOST', 'localhost');
    /**
     * For developers: WordPress debugging mode.
     * * Change this to true to enable the display of notices during development.
     * It is strongly recommended that plugin and theme developers use WP_DEBUG
     * in their development environments.
     */
    define('WP_DEBUG', true);

    //Security key settings
    define('AUTH_KEY', 'put your unique phrase here');
    define('SECURE_AUTH_KEY','put your unique phrase here');
    define('LOGGED_IN_KEY','put your unique phrase here');
    define('NONCE_KEY', 'put your unique phrase here');
    define('AUTH_SALT', 'put your unique phrase here');
    define('SECURE_AUTH_SALT', 'put your unique phrase here');
    define('LOGGED_IN_SALT', 'put your unique phrase here');
    define('NONCE_SALT', 'put your unique phrase here');

    /**
     * WordPress Database Table prefix.
     *
     * You can have multiple installations in one database if you give each a unique
     * prefix. Only numbers, letters, and underscores please!
     */
    $table_prefix = 'wp_';
    ```

    <span data-ttu-id="e4493-145">To ustawienie zabezpieczeń kluczy zgodnie z opisami w poprzednich kod może pomóc zapobiec trwa zaatakowane aplikacji sieci web, użyj unikatowe wartości.</span><span class="sxs-lookup"><span data-stu-id="e4493-145">Setting the security keys as illustrated in the previous code can help to prevent your web app from being hacked, so use unique values.</span></span> <span data-ttu-id="e4493-146">Jeśli chcesz wygenerować ciąg dla wymienionych kluczy zabezpieczeń w kodzie można [przejdź do automatycznego generatora](https://api.wordpress.org/secret-key/1.1/salt) można utworzyć nowej pary klucz wartość.</span><span class="sxs-lookup"><span data-stu-id="e4493-146">If you need to generate the string for security keys mentioned in the code, you can [go to the automatic generator](https://api.wordpress.org/secret-key/1.1/salt) to create new key/value pairs.</span></span>

4. <span data-ttu-id="e4493-147">Skopiuj następujący kod w `wp-config.azure.php`:</span><span class="sxs-lookup"><span data-stu-id="e4493-147">Copy the following code in `wp-config.azure.php`:</span></span>

    ```    
    <?php
    // MySQL settings
    /** The name of the database for WordPress */

    define('DB_NAME', getenv('DB_NAME'));

    /** MySQL database username */
    define('DB_USER', getenv('DB_USER'));

    /** MySQL database password */
    define('DB_PASSWORD', getenv('DB_PASSWORD'));

    /** MySQL hostname */
    define('DB_HOST', getenv('DB_HOST'));

    /**
    * For developers: WordPress debugging mode.
    *
    * Change this to true to enable the display of notices during development.
    * It is strongly recommended that plugin and theme developers use WP_DEBUG
    * in their development environments.
    * Turn on debug logging to investigate issues without displaying to end user. For WP_DEBUG_LOG to
    * do anything, WP_DEBUG must be enabled (true). WP_DEBUG_DISPLAY should be used in conjunction
    * with WP_DEBUG_LOG so that errors are not displayed on the page */

    */
    define('WP_DEBUG', getenv('WP_DEBUG'));
    define('WP_DEBUG_LOG', getenv('TURN_ON_DEBUG_LOG'));
    define('WP_DEBUG_DISPLAY',false);

    //Security key settings
    /** If you need to generate the string for security keys mentioned above, you can go the automatic generator to create new keys/values: https://api.wordpress.org/secret-key/1.1/salt **/
    define('AUTH_KEY',getenv('DB_AUTH_KEY'));
    define('SECURE_AUTH_KEY', getenv('DB_SECURE_AUTH_KEY'));
    define('LOGGED_IN_KEY', getenv('DB_LOGGED_IN_KEY'));
    define('NONCE_KEY', getenv('DB_NONCE_KEY'));
    define('AUTH_SALT', getenv('DB_AUTH_SALT'));
    define('SECURE_AUTH_SALT', getenv('DB_SECURE_AUTH_SALT'));
    define('LOGGED_IN_SALT',  getenv('DB_LOGGED_IN_SALT'));
    define('NONCE_SALT',  getenv('DB_NONCE_SALT'));

    /**
    * WordPress Database Table prefix.
    *
    * You can have multiple installations in one database if you give each a unique
    * prefix. Only numbers, letters, and underscores please!
    */
    $table_prefix = getenv('DB_PREFIX');
    ```

#### <a name="use-relative-paths"></a><span data-ttu-id="e4493-148">Użycie ścieżek względnych</span><span class="sxs-lookup"><span data-stu-id="e4493-148">Use relative paths</span></span>
<span data-ttu-id="e4493-149">Ostatnia rzecz do skonfigurowania w aplikacji WordPress jest ścieżek względnych.</span><span class="sxs-lookup"><span data-stu-id="e4493-149">One last thing to configure in the WordPress app is relative paths.</span></span> <span data-ttu-id="e4493-150">WordPress przechowują adres URL w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="e4493-150">WordPress stores URL information in the database.</span></span> <span data-ttu-id="e4493-151">Ten magazyn umożliwia przenoszenie zawartości z jednego środowiska do innego trudniejsze.</span><span class="sxs-lookup"><span data-stu-id="e4493-151">This storage makes moving content from one environment to another more difficult.</span></span> <span data-ttu-id="e4493-152">Musisz zaktualizować bazę danych, za każdym razem, gdy przenoszenia danych z lokalnego do etapu lub etap w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="e4493-152">You need to update the database every time you move from local to stage or stage to production environments.</span></span> <span data-ttu-id="e4493-153">Aby zmniejszyć ryzyko problemów, które może być spowodowany z wdrażania bazy danych, za każdym razem, gdy wdrażanie z jednego środowiska do innego, należy użyć [względną głównego łączy wtyczki](https://wordpress.org/plugins/root-relative-urls/), które można zainstalować za pomocą pulpitu nawigacyjnego WordPress administratora.</span><span class="sxs-lookup"><span data-stu-id="e4493-153">To reduce the risk of issues that can be caused with deploying a database every time you deploy from one environment to another, use the [Relative Root links plugin](https://wordpress.org/plugins/root-relative-urls/), which you can install by using the WordPress administrator dashboard.</span></span>

<span data-ttu-id="e4493-154">Dodaj następujące wpisy do Twojej `wp-config.php` pliku przed `That's all, stop editing!` komentarza:</span><span class="sxs-lookup"><span data-stu-id="e4493-154">Add the following entries to your `wp-config.php` file before the `That's all, stop editing!` comment:</span></span>

```

  define('WP_HOME', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_SITEURL', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_CONTENT_URL', '/wp-content');
    define('DOMAIN_CURRENT_SITE', filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
```

<span data-ttu-id="e4493-155">Aktywowanie wtyczki za pomocą `Plugins` menu w pulpitu nawigacyjnego WordPress administratora.</span><span class="sxs-lookup"><span data-stu-id="e4493-155">Activate the plugin through the `Plugins` menu in WordPress administrator dashboard.</span></span> <span data-ttu-id="e4493-156">Zapisz ustawienia łącze stałe dla aplikacji WordPress.</span><span class="sxs-lookup"><span data-stu-id="e4493-156">Save your permalink settings for WordPress app.</span></span>

#### <a name="the-final-wp-configphp-file"></a><span data-ttu-id="e4493-157">Ostatni `wp-config.php` pliku</span><span class="sxs-lookup"><span data-stu-id="e4493-157">The final `wp-config.php` file</span></span>
<span data-ttu-id="e4493-158">Nie wpłynie na wszystkie aktualizacje core WordPress z `wp-config.php`, `wp-config.azure.php`, i `wp-config.local.php` plików.</span><span class="sxs-lookup"><span data-stu-id="e4493-158">Any WordPress core updates will not affect your `wp-config.php`, `wp-config.azure.php`, and `wp-config.local.php` files.</span></span> <span data-ttu-id="e4493-159">Oto ostateczną wersją `wp-config.php` pliku:</span><span class="sxs-lookup"><span data-stu-id="e4493-159">Here's a final version of the `wp-config.php` file:</span></span>

```
<?php
/**
 * The base configurations of the WordPress.
 *
 * This file has the following configurations: MySQL settings, Table Prefix,
 * Secret Keys, and ABSPATH. You can find more information by visiting
 *
 * Codex page. You can get the MySQL settings from your web host.
 *
 * This file is used by the wp-config.php creation script during the
 * installation. You don't have to use the web web app, you can just copy this file
 * to "wp-config.php" and fill in the values.
 *
 * @package WordPress
 */

// Support multiple environments
// set the config file based on current environment
if (strpos($_SERVER['HTTP_HOST'],'localhost') !== false) { // local development
  $config_file = 'config/wp-config.local.php';
}
elseif ((strpos(getenv('WP_ENV'),'stage') !== false) ||(strpos(getenv('WP_ENV'),'prod' )!== false )){
  $config_file = 'config/wp-config.azure.php';
}


$path = dirname(__FILE__). '/';
if (file_exists($path. $config_file)) {
  // include the config file if it exists, otherwise WP is going to fail
  require_once $path. $config_file;
}

/** Database Charset to use in creating database tables. */
define('DB_CHARSET', 'utf8');

/** The Database Collate type. Don't change this if in doubt. */
define('DB_COLLATE', '');


/* That's all, stop editing! Happy blogging. */

define('WP_HOME', 'http://'. $_SERVER['HTTP_HOST']);
define('WP_SITEURL', 'http://'. $_SERVER['HTTP_HOST']);
define('WP_CONTENT_URL', '/wp-content');
define('DOMAIN_CURRENT_SITE', $_SERVER['HTTP_HOST']);

/** Absolute path to the WordPress directory. */
if ( !defined('ABSPATH') )
    define('ABSPATH', dirname(__FILE__). '/');

/** Sets up WordPress vars and included files. */
require_once(ABSPATH. 'wp-settings.php');
```

#### <a name="set-up-a-staging-environment"></a><span data-ttu-id="e4493-160">Konfigurowanie środowiska przemieszczania</span><span class="sxs-lookup"><span data-stu-id="e4493-160">Set up a staging environment</span></span>
1. <span data-ttu-id="e4493-161">Jeśli masz już aplikację sieci web WordPress z subskrypcją platformy Azure, zaloguj się do [portalu Azure](http://portal.azure.com), a następnie przejdź do aplikacji sieci web WordPress.</span><span class="sxs-lookup"><span data-stu-id="e4493-161">If you already have a WordPress web app running on your Azure subscription, sign in to the [Azure portal](http://portal.azure.com), and then go to your WordPress web app.</span></span> <span data-ttu-id="e4493-162">Jeśli nie masz aplikacji sieci web WordPress, można utworzyć z poziomu portalu Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="e4493-162">If you don't have a WordPress web app, you can create one from the Azure Marketplace.</span></span> <span data-ttu-id="e4493-163">Aby dowiedzieć się więcej, zobacz [tworzenie aplikacji sieci web WordPress w usłudze Azure App Service](web-sites-php-web-site-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="e4493-163">To learn more, see [Create a WordPress web app in Azure App Service](web-sites-php-web-site-gallery.md).</span></span>
<span data-ttu-id="e4493-164">Kliknij przycisk **ustawienia** > **miejsc wdrożenia** > **Dodaj** można utworzyć miejsca wdrożenia o nazwie *etapu*.</span><span class="sxs-lookup"><span data-stu-id="e4493-164">Click **Settings** > **Deployment slots** > **Add** to create a deployment slot with the name *stage*.</span></span> <span data-ttu-id="e4493-165">Miejsce wdrożenia jest inna aplikacja sieci web udostępniającej tyle samo zasobów co aplikacji głównej sieci web utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="e4493-165">A deployment slot is another web application that shares the same resources as the primary web app that you created previously.</span></span>

    ![Tworzenie miejsca wdrożenia etapu](./media/app-service-web-staged-publishing-realworld-scenarios/1setupstage.png)

2. <span data-ttu-id="e4493-167">Dodaj inny baza danych MySQL, powiedz `wordpress-stage-db`, w danej grupie zasobów `wordpressapp-group`.</span><span class="sxs-lookup"><span data-stu-id="e4493-167">Add another MySQL database, say `wordpress-stage-db`, to your resource group, `wordpressapp-group`.</span></span>

    ![Dodaj bazę danych MySQL do grupy zasobów](./media/app-service-web-staged-publishing-realworld-scenarios/2addmysql.png)

3. <span data-ttu-id="e4493-169">Zaktualizuj parametry połączenia dla Twojego miejsca wdrożenia etapu wskazywał nową bazę danych, `wordpress-stage-db`.</span><span class="sxs-lookup"><span data-stu-id="e4493-169">Update the connection strings for your stage deployment slot to point to the new database, `wordpress-stage-db`.</span></span> <span data-ttu-id="e4493-170">Aplikacja sieci web produkcji `wordpressprodapp`i aplikacji sieci web na potrzeby przemieszczania `wordpressprodapp-stage`, musi wskazywać różnych baz danych.</span><span class="sxs-lookup"><span data-stu-id="e4493-170">Your production web app, `wordpressprodapp`, and staging web app, `wordpressprodapp-stage`, must point to different databases.</span></span>

#### <a name="configure-environment-specific-app-settings"></a><span data-ttu-id="e4493-171">Konfiguruj ustawienia specyficzne dla środowiska aplikacji</span><span class="sxs-lookup"><span data-stu-id="e4493-171">Configure environment-specific app settings</span></span>
<span data-ttu-id="e4493-172">Deweloperzy mogą przechowywać pary klucz wartość ciągu na platformie Azure jako część dane konfiguracyjne o nazwie **ustawień aplikacji**, który jest skojarzony z aplikacją sieci web.</span><span class="sxs-lookup"><span data-stu-id="e4493-172">Developers can store key/value string pairs in Azure as part of the configuration information, called **App Settings**, that's associated with a web app.</span></span> <span data-ttu-id="e4493-173">W czasie wykonywania aplikacje sieci web pobierania tych wartości i automatycznie udostępnić kodu uruchamianego w aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="e4493-173">At runtime, web apps automatically retrieve these values and make them available to code that's running in your web app.</span></span> <span data-ttu-id="e4493-174">Z punktu widzenia zabezpieczeń, który jest korzyści nieuprzywilejowany po stronie, ponieważ poufne informacje, takie jak parametry połączenia bazy danych, które obejmują hasła, nigdy nie wyświetlane jako zwykły tekst w pliku takich jak `wp-config.php`.</span><span class="sxs-lookup"><span data-stu-id="e4493-174">From a security perspective, that is a nice side benefit because sensitive information, such as database connection strings that include passwords, never show up as clear text in a file such as `wp-config.php`.</span></span>

<span data-ttu-id="e4493-175">Ten proces, który znajduje się w sekcjach, jest przydatne, ponieważ obejmuje ona zarówno pliku zmiany i bazy danych dla aplikacji WordPress:</span><span class="sxs-lookup"><span data-stu-id="e4493-175">This process, which is explained in the following paragraphs, is useful because it includes both file changes and database changes for the WordPress app:</span></span>

* <span data-ttu-id="e4493-176">Uaktualnienie wersji WordPress</span><span class="sxs-lookup"><span data-stu-id="e4493-176">WordPress version upgrade</span></span>
* <span data-ttu-id="e4493-177">Dodawanie nowych lub edytowanie lub uaktualnić wtyczek</span><span class="sxs-lookup"><span data-stu-id="e4493-177">Add new or edit or upgrade plugins</span></span>
* <span data-ttu-id="e4493-178">Dodawanie nowych lub edytowanie lub uaktualnić motywów</span><span class="sxs-lookup"><span data-stu-id="e4493-178">Add new or edit or upgrade themes</span></span>

<span data-ttu-id="e4493-179">Konfiguruj ustawienia aplikacji dla:</span><span class="sxs-lookup"><span data-stu-id="e4493-179">Configure app settings for:</span></span>

* <span data-ttu-id="e4493-180">Informacje o bazie danych</span><span class="sxs-lookup"><span data-stu-id="e4493-180">Database information</span></span>
* <span data-ttu-id="e4493-181">Włączenie/wyłączenie rejestrowania WordPress</span><span class="sxs-lookup"><span data-stu-id="e4493-181">Turning on/off WordPress logging</span></span>
* <span data-ttu-id="e4493-182">Ustawienia zabezpieczeń WordPress</span><span class="sxs-lookup"><span data-stu-id="e4493-182">WordPress security settings</span></span>

![Ustawienia aplikacji dla aplikacji sieci web Wordpress](./media/app-service-web-staged-publishing-realworld-scenarios/3configure.png)

<span data-ttu-id="e4493-184">Upewnij się, Dodaj poniższe ustawienia aplikacji dla gniazda sieci produkcyjnych w sieci web aplikacji i etap.</span><span class="sxs-lookup"><span data-stu-id="e4493-184">Make sure that you add the following app settings for your production web app and stage slot.</span></span> <span data-ttu-id="e4493-185">Należy pamiętać, że aplikacja sieci web w środowisku produkcyjnym i przemieszczania aplikacji sieci web różnych baz danych.</span><span class="sxs-lookup"><span data-stu-id="e4493-185">Note that the production web app and staging web app use different databases.</span></span>

1. <span data-ttu-id="e4493-186">Wyczyść **ustawienie miejsca** pola wyboru dla wszystkich parametrów ustawień, z wyjątkiem WP_ENV.</span><span class="sxs-lookup"><span data-stu-id="e4493-186">Clear the **Slot Setting** checkbox for all the settings parameters except WP_ENV.</span></span> <span data-ttu-id="e4493-187">Ten proces będzie wymiany konfiguracji dla aplikacji sieci web, zawartość pliku i bazy danych.</span><span class="sxs-lookup"><span data-stu-id="e4493-187">This process will swap the configuration for your web app, file content, and database.</span></span> <span data-ttu-id="e4493-188">Jeśli **ustawienie miejsca** jest zaznaczone, ustawienia aplikacji i połączenia aplikacji sieci web w ciągu konfiguracji będzie *nie* przenieść w środowiskach, w trakcie **wymiany** operacji.</span><span class="sxs-lookup"><span data-stu-id="e4493-188">If **Slot Setting** is checked, the web app’s app settings and connection string configuration will *not* move across environments when doing a **Swap** operation.</span></span> <span data-ttu-id="e4493-189">Wszelkie zmiany bazy danych, które znajdują się nie będę powodować utraty aplikacji sieci web w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="e4493-189">Any database changes that are present will not break your production web app.</span></span>

2. <span data-ttu-id="e4493-190">Wdrażanie aplikacji sieci web środowisko rozwoju lokalnego do etapu aplikacji sieci web i bazy danych za pomocą programu WebMatrix lub narzędzia wybranych przez użytkownika, takie jak FTP, Git lub PhpMyAdmin.</span><span class="sxs-lookup"><span data-stu-id="e4493-190">Deploy the local development environment web app to the stage web app and database by using WebMatrix or tools of your choice, such as FTP, Git, or PhpMyAdmin.</span></span>

    ![Okno dialogowe publikowania macierzy sieci Web dla aplikacji sieci web WordPress](./media/app-service-web-staged-publishing-realworld-scenarios/4wmpublish.png)

3. <span data-ttu-id="e4493-192">Przeglądanie i testowanie przemieszczania aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="e4493-192">Browse and test your staging web app.</span></span> <span data-ttu-id="e4493-193">Biorąc pod uwagę scenariusz, w której ma zostać zaktualizowany motywu aplikacji sieci web w tym miejscu jest przemieszczania aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="e4493-193">Considering a scenario where the theme of the web app is to be updated, here is the staging web app.</span></span>

    ![Przeglądaj przemieszczania aplikacji sieci web przed wymiany gniazd](./media/app-service-web-staged-publishing-realworld-scenarios/5wpstage.png)

4. <span data-ttu-id="e4493-195">Jeśli wszystko wygląda dobrze, kliknij przycisk **wymiany** przycisk tymczasową aplikację sieci web w taki sposób, aby przenieść zawartość do środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="e4493-195">If all looks good, click the **Swap** button on your staging web app to move your content to the production environment.</span></span> <span data-ttu-id="e4493-196">W takim przypadku zamienić aplikacji sieci web i bazy danych w środowiskach podczas każdego **wymiany** operacji.</span><span class="sxs-lookup"><span data-stu-id="e4493-196">In this case, you swap the web app and the database across environments during every **Swap** operation.</span></span>

    ![Zamień podgląd zmian dla środowiska WordPress](./media/app-service-web-staged-publishing-realworld-scenarios/6swaps1.png)

    > [!NOTE]
    > <span data-ttu-id="e4493-198">Jeśli scenariusz wymaga tylko push plików (Brak aktualizacji bazy danych), następnie sprawdź **ustawienie miejsca** dla wszystkich bazy danych związanych z *ustawień aplikacji* i *ustawienia parametry połączenia z* w **ustawień aplikacji sieci Web** bloku w portalu Azure, zanim spowoduje **wymiany**.</span><span class="sxs-lookup"><span data-stu-id="e4493-198">If your scenario needs to only push files (no database updates), then check **Slot Setting** for all the database-related *app settings* and *connection strings settings* in the **Web App Settings** blade within the Azure portal before doing the **Swap**.</span></span> <span data-ttu-id="e4493-199">W takim przypadku DB_NAME, DB_HOST DB_PASSWORD, DB_USER i domyślnych ustawień połączenia w ciągu powinna nie pojawiają się w podgląd zmian po wykonaniu **wymiany**.</span><span class="sxs-lookup"><span data-stu-id="e4493-199">In this case, DB_NAME, DB_HOST, DB_PASSWORD, DB_USER, and default connection string settings should not show up in preview changes when you do a **Swap**.</span></span> <span data-ttu-id="e4493-200">W tej chwili po zakończeniu **wymiany** operacji, aplikacji sieci web WordPress będzie mieć tylko pliki aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="e4493-200">At this time, when you complete the **Swap** operation, the WordPress web app will have the updates files only.</span></span>
    >
    >

    <span data-ttu-id="e4493-201">Przed to **wymiany**, w tym miejscu jest aplikacja sieci web WordPress produkcji.</span><span class="sxs-lookup"><span data-stu-id="e4493-201">Before doing a **Swap**, here is the production WordPress web app.</span></span>
    <span data-ttu-id="e4493-202">![Aplikacja sieci web produkcyjnym przed wymiany gniazd](./media/app-service-web-staged-publishing-realworld-scenarios/7bfswap.png)</span><span class="sxs-lookup"><span data-stu-id="e4493-202">![Production web app before swapping slots](./media/app-service-web-staged-publishing-realworld-scenarios/7bfswap.png)</span></span>

    <span data-ttu-id="e4493-203">Po **wymiany** operacji motywu została zaktualizowana na aplikację sieci web w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="e4493-203">After the **Swap** operation, the theme has been updated on your production web app.</span></span>

    ![Aplikacja sieci web produkcji po wymiany gniazd](./media/app-service-web-staged-publishing-realworld-scenarios/8afswap.png)

5. <span data-ttu-id="e4493-205">Gdy potrzebne do przywrócenia, można przejść do produkcji w sieci web **ustawień aplikacji**i kliknij przycisk **wymiany** przycisk, aby zamienić aplikację sieci web i bazy danych z produkcji na miejsce wystawiania.</span><span class="sxs-lookup"><span data-stu-id="e4493-205">When you need to roll back, you can go to the production web **App Settings**, and click the **Swap** button to swap the web app and database from production to staging slot.</span></span> <span data-ttu-id="e4493-206">Pamiętaj, że jeśli zmian w bazie danych są dołączone **wymiany** operacji, a następnie wdrożyć do tymczasowej aplikacji sieci web, następnym razem należy wdrożyć zmian w bazie danych do bieżącej bazy danych przemieszczania aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="e4493-206">Remember that if database changes are included with a **Swap** operation, then the next time you deploy to your staging web app, you need to deploy the database changes to the current database for your staging web app.</span></span> <span data-ttu-id="e4493-207">Bieżąca baza danych może być poprzedniej produkcyjną bazę danych lub baza danych etapu.</span><span class="sxs-lookup"><span data-stu-id="e4493-207">The current database might be the previous production database or the stage database.</span></span>

#### <a name="summary"></a><span data-ttu-id="e4493-208">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="e4493-208">Summary</span></span>
<span data-ttu-id="e4493-209">Poniżej znajduje się uogólniony procesu dla dowolnej aplikacji, która ma bazy danych:</span><span class="sxs-lookup"><span data-stu-id="e4493-209">Following is a generalized process for any application that has a database:</span></span>

1. <span data-ttu-id="e4493-210">Zainstaluj aplikację w środowisku lokalnym.</span><span class="sxs-lookup"><span data-stu-id="e4493-210">Install the application on your local environment.</span></span>
2. <span data-ttu-id="e4493-211">Zawiera konfiguracje specyficzne dla środowiska (lokalne i Azure Web Apps).</span><span class="sxs-lookup"><span data-stu-id="e4493-211">Include environment-specific configurations (local and Azure Web Apps).</span></span>
3. <span data-ttu-id="e4493-212">Konfigurowanie środowiska przemieszczania i produkcji dla aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="e4493-212">Set up your staging and production environments for Web Apps.</span></span>
4. <span data-ttu-id="e4493-213">Jeśli masz już uruchomione na platformie Azure aplikacji produkcyjnych, synchronizować produkcji zawartość (pliki/kod i bazy danych) do środowiska lokalnego i tymczasowej.</span><span class="sxs-lookup"><span data-stu-id="e4493-213">If you have a production application already running on Azure, sync your production content (files/code and database) to local and staging environments.</span></span>
5. <span data-ttu-id="e4493-214">Tworzenie aplikacji w środowisku lokalnym.</span><span class="sxs-lookup"><span data-stu-id="e4493-214">Develop your application on your local environment.</span></span>
6. <span data-ttu-id="e4493-215">Ustaw aplikację sieci web produkcji konserwacja lub tryb zablokowane, a następnie zsynchronizować bazy danych zawartości z produkcji do środowisk przemieszczania i deweloperów.</span><span class="sxs-lookup"><span data-stu-id="e4493-215">Place your production web app under maintenance or locked mode, and sync database content from production to staging and dev environments.</span></span>
7. <span data-ttu-id="e4493-216">Wdróż środowisko przejściowe i testowania.</span><span class="sxs-lookup"><span data-stu-id="e4493-216">Deploy to the staging environment and test.</span></span>
8. <span data-ttu-id="e4493-217">Wdróż do środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="e4493-217">Deploy to production environment.</span></span>
9. <span data-ttu-id="e4493-218">Powtórz kroki od 4 do 6.</span><span class="sxs-lookup"><span data-stu-id="e4493-218">Repeat steps 4 through 6.</span></span>

### <a name="umbraco"></a><span data-ttu-id="e4493-219">Umbraco</span><span class="sxs-lookup"><span data-stu-id="e4493-219">Umbraco</span></span>
<span data-ttu-id="e4493-220">W tej sekcji dowiesz się, jak Umbraco CMS używa niestandardowego modułu do wdrożenia w wielu środowiskach DevOps.</span><span class="sxs-lookup"><span data-stu-id="e4493-220">In this section, you will learn how the Umbraco CMS uses a custom module to deploy across multiple DevOps environments.</span></span> <span data-ttu-id="e4493-221">W poniższym przykładzie przedstawiono różne podejścia do zarządzania wieloma środowisk deweloperskich.</span><span class="sxs-lookup"><span data-stu-id="e4493-221">This example provides a different approach to managing multiple development environments.</span></span>

<span data-ttu-id="e4493-222">[Umbraco CMS](http://umbraco.com/) jest rozwiązaniem .NET CMS popularnych, która jest używana przez wielu deweloperów.</span><span class="sxs-lookup"><span data-stu-id="e4493-222">[Umbraco CMS](http://umbraco.com/) is a popular .NET CMS solution that's used by many developers.</span></span> <span data-ttu-id="e4493-223">Zapewnia [Courier2](http://umbraco.com/products/more-add-ons/courier-2) modułu wdrażania od projektowania do etapu przemieszczania w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="e4493-223">It provides the [Courier2](http://umbraco.com/products/more-add-ons/courier-2) module to deploy from development to staging to production environments.</span></span> <span data-ttu-id="e4493-224">Środowisko deweloperskie lokalnej dla aplikacji sieci web Umbraco CMS można łatwo utworzyć za pomocą programu Visual Studio lub programu WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="e4493-224">You can easily create a local development environment for an Umbraco CMS web app by using Visual Studio or WebMatrix.</span></span>

- [<span data-ttu-id="e4493-225">Tworzenie aplikacji sieci web Umbraco z programem Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e4493-225">Create an Umbraco web app with Visual Studio</span></span>](https://our.umbraco.org/documentation/Installation/install-umbraco-with-nuget)
- [<span data-ttu-id="e4493-226">Tworzenie aplikacji sieci web Umbraco za pomocą programu WebMatrix</span><span class="sxs-lookup"><span data-stu-id="e4493-226">Create an Umbraco web app with WebMatrix</span></span>](http://umbraco.tv/videos/umbraco-v7/implementor/fundamentals/installation/creating-umbraco-site-from-webmatrix-web-gallery/)

<span data-ttu-id="e4493-227">Zawsze pamiętaj, aby usunąć `install` folder aplikacji i nigdy nie przekazuj do etapu lub produkcji aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="e4493-227">Always remember to remove the `install` folder under your application, and never upload it to stage or production web apps.</span></span> <span data-ttu-id="e4493-228">W tym samouczku korzysta z programu WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="e4493-228">This tutorial uses WebMatrix.</span></span>

#### <a name="set-up-a-staging-environment"></a><span data-ttu-id="e4493-229">Konfigurowanie środowiska przemieszczania</span><span class="sxs-lookup"><span data-stu-id="e4493-229">Set up a staging environment</span></span>
1. <span data-ttu-id="e4493-230">Tworzenie miejsca wdrożenia, jak wspomniano wcześniej, Umbraco CMS aplikacji sieci web, przy założeniu, że masz już aplikację sieci web Umbraco CMS i uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="e4493-230">Create a deployment slot as mentioned previously for the Umbraco CMS web app, assuming you already have an Umbraco CMS web app up and running.</span></span> <span data-ttu-id="e4493-231">Jeśli nie chcesz, możesz utworzyć jedną z witryny Marketplace.</span><span class="sxs-lookup"><span data-stu-id="e4493-231">If you do not, you can create one from the Marketplace.</span></span>
2. <span data-ttu-id="e4493-232">Zaktualizuj parametry połączenia dla Twojego miejsca wdrożenia etapu wskaż nowy **umbraco etap db** bazy danych.</span><span class="sxs-lookup"><span data-stu-id="e4493-232">Update the connection string for your stage deployment slot to point to the new **umbraco-stage-db** database.</span></span> <span data-ttu-id="e4493-233">Produkcji aplikacji sieci web (umbraositecms-1) i przemieszczania aplikacji sieci web (umbracositecms-1-etap) *musi* punktu do różnych baz danych.</span><span class="sxs-lookup"><span data-stu-id="e4493-233">Your production web app (umbraositecms-1) and staging web app (umbracositecms-1-stage) *must* point to different databases.</span></span>

    ![Zaktualizuj parametry połączenia dla aplikacji sieci web za pomocą nowej tymczasowej bazy danych przemieszczania](./media/app-service-web-staged-publishing-realworld-scenarios/9umbconnstr.png)

3. <span data-ttu-id="e4493-235">Kliknij przycisk **ustawień publikowania pobrać** dla miejsca wdrożenia **etapu**.</span><span class="sxs-lookup"><span data-stu-id="e4493-235">Click **Get Publish settings** for the deployment slot **stage**.</span></span> <span data-ttu-id="e4493-236">Ten proces pobierze plik ustawień publikowania, który przechowuje wszystkie informacje, które Visual Studio lub WebMatrix wymaga, aby opublikować aplikację z lokalnej aplikacji sieci web do aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e4493-236">This process will download a publish settings file that stores all the information that Visual Studio or WebMatrix requires to publish your application from the local development web app to the Azure web app.</span></span>

    ![Ustawienie aplikacji sieci web przemieszczania publikowania Get](./media/app-service-web-staged-publishing-realworld-scenarios/10getpsetting.png)
4. <span data-ttu-id="e4493-238">Otwórz aplikację sieci web lokalne działania projektowe w programie WebMatrix lub Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e4493-238">Open your local development web app in WebMatrix or Visual Studio.</span></span> <span data-ttu-id="e4493-239">W tym samouczku korzysta z programu WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="e4493-239">This tutorial uses WebMatrix.</span></span> <span data-ttu-id="e4493-240">Najpierw należy zaimportować plik ustawień publikowania dla aplikacji sieci web tymczasowej.</span><span class="sxs-lookup"><span data-stu-id="e4493-240">First, you need to import the publish settings file for your staging web app.</span></span>

    ![Importowanie ustawień publikowania dla Umbraco przy użyciu macierzy sieci Web](./media/app-service-web-staged-publishing-realworld-scenarios/11import.png)

5. <span data-ttu-id="e4493-242">Przegląd zmian dokonanych w oknie dialogowym i wdrażanie aplikacji sieci web lokalnego do aplikacji sieci web platformy Azure, *umbracositecms-1-etap*.</span><span class="sxs-lookup"><span data-stu-id="e4493-242">Review changes in the dialog box, and deploy your local web app to your Azure web app, *umbracositecms-1-stage*.</span></span> <span data-ttu-id="e4493-243">Podczas wdrażania plików bezpośrednio do aplikacji sieci web przemieszczania, zostaną pominięte pliki w `~/app_data/TEMP/` folderu, ponieważ te pliki zostaną ponownie wygenerowane przy pierwszym etapie aplikacji sieci web uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="e4493-243">When you deploy files directly to your staging web app, you will omit files in the `~/app_data/TEMP/` folder because these files will be regenerated when the stage web app is first started.</span></span> <span data-ttu-id="e4493-244">Należy również pominąć `~/app_data/umbraco.config` pliku, który również zostanie ponownie wygenerowany.</span><span class="sxs-lookup"><span data-stu-id="e4493-244">You should also omit the `~/app_data/umbraco.config` file, which will also be regenerated.</span></span>

    ![Przejrzyj zmiany publikowania w sieci web macierzy.](./media/app-service-web-staged-publishing-realworld-scenarios/12umbpublish.png)

6. <span data-ttu-id="e4493-246">Po opublikowaniu pomyślnie aplikacji sieci web w lokalnej Umbraco przemieszczania aplikacji sieci web, przejdź do aplikacji sieci web przemieszczania, a następnie uruchom kilka testów w celu wykluczenia problemów.</span><span class="sxs-lookup"><span data-stu-id="e4493-246">After you successfully publish the Umbraco local web app to the staging web app, browse to your staging web app, and run a few tests to rule out any issues.</span></span>

#### <a name="set-up-the-courier2-deployment-module"></a><span data-ttu-id="e4493-247">Konfigurowanie modułu wdrażania Courier2</span><span class="sxs-lookup"><span data-stu-id="e4493-247">Set up the Courier2 deployment module</span></span>
<span data-ttu-id="e4493-248">Z [Courier2](http://umbraco.com/products/more-add-ons/courier-2) modułu, można po prostu prawym przyciskiem myszy do wypychania zawartości, arkusze stylów i moduły programowanie z przemieszczania aplikacji sieci web w aplikacji sieci web w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="e4493-248">With the [Courier2](http://umbraco.com/products/more-add-ons/courier-2) module, you can simply right-click to push content, style sheets, and development modules from a staging web app to a production web app.</span></span> <span data-ttu-id="e4493-249">Ten proces zmniejsza ryzyko przerwanie aplikacji sieci web w środowisku produkcyjnym, podczas wdrażania aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="e4493-249">This process reduces the risk of breaking your production web app when you deploy an update.</span></span>
<span data-ttu-id="e4493-250">Zakupu licencję na Courier2 dla `*.azurewebsites.net` domeny i domeny niestandardowej (Powiedz http://abc.com).</span><span class="sxs-lookup"><span data-stu-id="e4493-250">Purchase a license for Courier2 for the `*.azurewebsites.net` domain and your custom domain (say http://abc.com).</span></span> <span data-ttu-id="e4493-251">Po zakupie licencji, umieść pobranej licencji (. Plik — Umowa Licencyjna) w `bin` folderu.</span><span class="sxs-lookup"><span data-stu-id="e4493-251">After you purchase the license, place the downloaded license (.LIC file) in the `bin` folder.</span></span>

![Upuść plik licencji w obszarze bin folder](./media/app-service-web-staged-publishing-realworld-scenarios/13droplic.png)

1. <span data-ttu-id="e4493-253">[Pobierz pakiet Courier2](https://our.umbraco.org/projects/umbraco-pro/umbraco-courier-2/).</span><span class="sxs-lookup"><span data-stu-id="e4493-253">[Download the Courier2 package](https://our.umbraco.org/projects/umbraco-pro/umbraco-courier-2/).</span></span> <span data-ttu-id="e4493-254">Kliknij przycisk Zaloguj się na etapie aplikacji sieci web, powiedz http://umbracocms-site-stage.azurewebsites.net/umbraco **Developer** menu, a następnie kliknij przycisk **pakiety** > **zainstaluj pakiet lokalny**.</span><span class="sxs-lookup"><span data-stu-id="e4493-254">Sign in to your stage web app, say http://umbracocms-site-stage.azurewebsites.net/umbraco, click the **Developer** menu, and then click **Packages** > **Install local package**.</span></span>

    ![Instalator pakietu Umbraco](./media/app-service-web-staged-publishing-realworld-scenarios/14umbpkg.png)

2. <span data-ttu-id="e4493-256">Przekaż pakiet Courier2 za pomocą Instalatora.</span><span class="sxs-lookup"><span data-stu-id="e4493-256">Upload the Courier2 package by using the installer.</span></span>

    ![Przekaż pakiet courier modułu](./media/app-service-web-staged-publishing-realworld-scenarios/15umbloadpkg.png)

3. <span data-ttu-id="e4493-258">Aby skonfigurować pakiet, należy zaktualizować plik courier.config pod **Config** folderu aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="e4493-258">To configure the package, you need to update the courier.config file under the **Config** folder of your web app.</span></span>

    ```xml
    <!-- Repository connection settings -->
     <!-- For each site, a custom repository must be configured, so Courier knows how to connect and authenticate-->
     <repositories>
        <!-- If a custom Umbraco Membership provider is used, specify login & password + set the passwordEncoding to clear: -->
        <repository name="production web app" alias="stage" type="CourierWebserviceRepositoryProvider" visible="true">
          <url>http://umbracositecms-1.azurewebsites.net</url>
          <user>0</user>
          <!--<login>user@email.com</login> -->
          <!-- <password>user_password</password>-->
          <!-- <passwordEncoding>Clear</passwordEncoding>-->
          </repository>
     </repositories>
     ```

4. <span data-ttu-id="e4493-259">W obszarze `<repositories>`, wprowadź produkcyjnym adres URL i użytkownika informacje o lokacji.</span><span class="sxs-lookup"><span data-stu-id="e4493-259">Under `<repositories>`, enter the production site URL and user information.</span></span>
    <span data-ttu-id="e4493-260">Jeśli korzystasz z domyślnego dostawcę członkostwa Umbraco, Dodaj identyfikator użytkownika administracji w &lt;użytkownika&gt; sekcji.</span><span class="sxs-lookup"><span data-stu-id="e4493-260">If you are using the default Umbraco membership provider, then add the ID for the Administration user in the &lt;user&gt; section.</span></span>
    <span data-ttu-id="e4493-261">Jeśli używasz niestandardowego dostawcy członkostwa Umbraco, użyj `<login>`,`<password>` w module Courier2 nawiązać do miejsca produkcji.</span><span class="sxs-lookup"><span data-stu-id="e4493-261">If you are using a custom Umbraco membership provider, use `<login>`,`<password>` in the Courier2 module to connect to the production site.</span></span>
    <span data-ttu-id="e4493-262">Aby uzyskać więcej informacji [zapoznaj się z dokumentacją modułu Courier2](http://umbraco.com/help-and-support/customer-area/courier-2-support-and-download/developer-documentation).</span><span class="sxs-lookup"><span data-stu-id="e4493-262">For more details, [review the documentation for the Courier2 module](http://umbraco.com/help-and-support/customer-area/courier-2-support-and-download/developer-documentation).</span></span>

5. <span data-ttu-id="e4493-263">Podobnie zainstalować moduł Courier2 w swojej witrynie produkcji i skonfigurować go, aby wskazywała aplikację sieci web etap w jego pliku odpowiednich courier.config, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="e4493-263">Similarly, install the Courier2 module on your production site, and configure it to point to the stage web app in its respective courier.config file as shown here.</span></span>

    ```xml
     <!-- Repository connection settings -->
     <!-- For each site, a custom repository must be configured, so Courier knows how to connect and authenticate-->
     <repositories>
        <!-- If a custom Umbraco Membership provider is used, specify login & password + set the passwordEncoding to clear: -->
        <repository name="Stage web app" alias="stage" type="CourierWebserviceRepositoryProvider" visible="true">
          <url>http://umbracositecms-1-stage.azurewebsites.net</url>
          <user>0</user>
          </repository>
     </repositories>
    ```

6. <span data-ttu-id="e4493-264">Kliknij przycisk **Courier2** na pulpicie nawigacyjnym aplikacji sieci web Umbraco CMS, a następnie kliknij **lokalizacje**.</span><span class="sxs-lookup"><span data-stu-id="e4493-264">Click the **Courier2** tab in the Umbraco CMS web app dashboard, and then click **Locations**.</span></span> <span data-ttu-id="e4493-265">Jak wspomniano w powinna zostać wyświetlona nazwa repozytorium `courier.config`.</span><span class="sxs-lookup"><span data-stu-id="e4493-265">You should see the repository name as mentioned in `courier.config`.</span></span> <span data-ttu-id="e4493-266">Czy ten proces w środowisku produkcyjnym i tymczasowej aplikacjami sieci web.</span><span class="sxs-lookup"><span data-stu-id="e4493-266">Do this process on both your production and staging web apps.</span></span>

    ![Repozytorium aplikacji sieci web docelowego widoku](./media/app-service-web-staged-publishing-realworld-scenarios/16courierloc.png)

7. <span data-ttu-id="e4493-268">Aby wdrożyć zawartość z witryny przemieszczania do miejsca produkcji, przejdź do **zawartości**i wybierz istniejącą stronę lub Utwórz nową stronę.</span><span class="sxs-lookup"><span data-stu-id="e4493-268">To deploy content from the staging site to the production site, go to **Content**, and select an existing page or create a new page.</span></span> <span data-ttu-id="e4493-269">Wybiorę istniejącej strony z mojej aplikacji sieci web, gdzie jest tytuł strony **wprowadzenie — nowy**, a następnie kliknij przycisk **Zapisz i opublikuj**.</span><span class="sxs-lookup"><span data-stu-id="e4493-269">I will select an existing page from my web app where the title of the page is **Getting Started – new**, and then click **Save and Publish**.</span></span>

    ![Zmień tytuł strony i publikowanie](./media/app-service-web-staged-publishing-realworld-scenarios/17changepg.png)

8. <span data-ttu-id="e4493-271">Kliknij prawym przyciskiem myszy zmodyfikowane strony, aby wyświetlić wszystkie opcje.</span><span class="sxs-lookup"><span data-stu-id="e4493-271">Right-click the modified page to view all the options.</span></span> <span data-ttu-id="e4493-272">Kliknij przycisk **Courier** otworzyć **wdrożenia** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="e4493-272">Click **Courier** to open the **Deployment** dialog box.</span></span> <span data-ttu-id="e4493-273">Kliknij przycisk **Wdróż** do inicjowania wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="e4493-273">Click **Deploy** to initiate deployment.</span></span>

    ![Okno dialogowe wdrożenia modułu Courier](./media/app-service-web-staged-publishing-realworld-scenarios/18dialog1.png)

9. <span data-ttu-id="e4493-275">Przejrzyj zmiany, a następnie kliknij przycisk **Kontynuuj**.</span><span class="sxs-lookup"><span data-stu-id="e4493-275">Review the changes, and then click **Continue**.</span></span>

    ![Courier modułu wdrażania okna dialogowego przejrzyj zmiany](./media/app-service-web-staged-publishing-realworld-scenarios/19dialog2.png)

    <span data-ttu-id="e4493-277">Dziennik wdrażania pokazuje, czy wdrażanie zakończyło się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="e4493-277">The deployment log shows if the deployment was successful.</span></span>

     ![Wyświetl dzienniki wdrożenia z modułu Courier](./media/app-service-web-staged-publishing-realworld-scenarios/20successdlg.png)

10. <span data-ttu-id="e4493-279">Przeglądanie aplikacji sieci web produkcji, jeśli zmiany są uwzględniane.</span><span class="sxs-lookup"><span data-stu-id="e4493-279">Browse your production web app to see if the changes are reflected.</span></span>

     ![Przeglądanie aplikacji sieci web w środowisku produkcyjnym](./media/app-service-web-staged-publishing-realworld-scenarios/21umbpg.png)

<span data-ttu-id="e4493-281">Aby dowiedzieć się więcej o sposobie używania Courier, zapoznaj się z dokumentacją.</span><span class="sxs-lookup"><span data-stu-id="e4493-281">To learn more about how to use Courier, review the documentation.</span></span>

#### <a name="how-to-upgrade-the-umbraco-cms-version"></a><span data-ttu-id="e4493-282">Jak uaktualnić wersję Umbraco CMS</span><span class="sxs-lookup"><span data-stu-id="e4493-282">How to upgrade the Umbraco CMS version</span></span>
<span data-ttu-id="e4493-283">Zostanie Courier nie pomocy uaktualnienia z jednej wersji systemu Umbraco CMS do innego.</span><span class="sxs-lookup"><span data-stu-id="e4493-283">Courier will not help you upgrade from one version of Umbraco CMS to another.</span></span> <span data-ttu-id="e4493-284">Po uaktualnieniu z wersji Umbraco CMS, musisz sprawdzić dla niezgodności z niestandardowych modułów lub modułów z partnerami i Umbraco podstawowe biblioteki.</span><span class="sxs-lookup"><span data-stu-id="e4493-284">When you upgrade an Umbraco CMS version, you must check for incompatibilities with your custom modules or modules from partners and the Umbraco Core libraries.</span></span> <span data-ttu-id="e4493-285">Poniżej przedstawiono najlepsze rozwiązania:</span><span class="sxs-lookup"><span data-stu-id="e4493-285">Here are best practices:</span></span>

* <span data-ttu-id="e4493-286">Zawsze tworzyć kopie zapasowe aplikacji sieci web i bazy danych przed uaktualnieniem.</span><span class="sxs-lookup"><span data-stu-id="e4493-286">Always back up your web app and database before you upgrade.</span></span> <span data-ttu-id="e4493-287">Aplikacji sieci web na platformie Azure możesz Konfigurowanie automatycznego tworzenia kopii zapasowych dla witryny sieci Web za pomocą funkcji Kopia zapasowa i przywracanie witryny, w razie potrzeby, używając funkcji przywracania.</span><span class="sxs-lookup"><span data-stu-id="e4493-287">On web apps in Azure, you can set up automatic backups for your websites by using the backup feature and restore your site if needed by using the restore feature.</span></span> <span data-ttu-id="e4493-288">Aby uzyskać więcej informacji, zobacz [sposób wykonywania kopii zapasowej aplikacji sieci web](web-sites-backup.md) i [Przywracanie aplikacji sieci web](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="e4493-288">For more details, see [How to back up your web app](web-sites-backup.md) and [How to restore your web app](web-sites-restore.md).</span></span>
* <span data-ttu-id="e4493-289">Sprawdź, czy pakiety partnerów są zgodne z wersją, które w przypadku uaktualniania.</span><span class="sxs-lookup"><span data-stu-id="e4493-289">Check if packages from partners are compatible with the version you're upgrading to.</span></span> <span data-ttu-id="e4493-290">Przejrzyj zgodność projektu z wersją Umbraco CMS, pakietu strony pobierania.</span><span class="sxs-lookup"><span data-stu-id="e4493-290">On the package's download page, review the project compatibility with Umbraco CMS version.</span></span>

<span data-ttu-id="e4493-291">Aby uzyskać więcej informacji o sposobie uaktualniania aplikacji sieci web lokalnie [Zobacz ogólne wskazówki uaktualnienia](https://our.umbraco.org/documentation/getting-started/setup/upgrading/general).</span><span class="sxs-lookup"><span data-stu-id="e4493-291">For more details about how to upgrade your web app locally, [see the general upgrade guidance](https://our.umbraco.org/documentation/getting-started/setup/upgrading/general).</span></span>

<span data-ttu-id="e4493-292">Po uaktualnieniu witrynie lokalnej opublikować zmiany tymczasową aplikację sieci web.</span><span class="sxs-lookup"><span data-stu-id="e4493-292">After your local development site is upgraded, publish the changes to the staging web app.</span></span> <span data-ttu-id="e4493-293">Testowanie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e4493-293">Test your application.</span></span> <span data-ttu-id="e4493-294">Jeśli wszystko wygląda dobrze, użyj **wymiany** przycisk, aby zamienić przemieszczania witryny aplikacji sieci web w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="e4493-294">If all looks good, use the **Swap** button to swap your staging site to the production web app.</span></span> <span data-ttu-id="e4493-295">Jeśli używasz **wymiany** operacji, można wyświetlić zmiany, które zostaną zmodyfikowane w konfiguracji aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="e4493-295">When you use the **Swap** operation, you can view the changes that will be affected in your web app's configuration.</span></span> <span data-ttu-id="e4493-296">To **wymiany** operacji zamienia aplikacji sieci web i baz danych.</span><span class="sxs-lookup"><span data-stu-id="e4493-296">This **Swap** operation swaps the web apps and databases.</span></span> <span data-ttu-id="e4493-297">Po **wymiany**, aplikacji sieci web w środowisku produkcyjnym wskaże umbraco — etap db bazy danych i przemieszczania aplikacji sieci web będzie wskazywać umbraco produkcyjną db bazy danych.</span><span class="sxs-lookup"><span data-stu-id="e4493-297">After the **Swap**, the production web app will point to the umbraco-stage-db database, and the staging web app will point to umbraco-prod-db database.</span></span>

![Do wdrażania Umbraco CMS w wersji zapoznawczej wymiany](./media/app-service-web-staged-publishing-realworld-scenarios/22umbswap.png)

<span data-ttu-id="e4493-299">Poniżej przedstawiono zalety wymiany zarówno aplikacji sieci web i bazy danych:</span><span class="sxs-lookup"><span data-stu-id="e4493-299">Here are advantages of swapping both the web app and the database:</span></span>

* <span data-ttu-id="e4493-300">Możesz przywrócić poprzedniej wersji aplikacji sieci web z inną **wymiany** Jeśli występują problemy z aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e4493-300">You can roll back to the previous version of your web app with another **Swap** if there are any application issues.</span></span>
* <span data-ttu-id="e4493-301">W przypadku uaktualnienia należy wdrożyć plików i baz danych z tymczasowej aplikacji sieci web w środowisku produkcyjnym aplikacji sieci web i bazy danych.</span><span class="sxs-lookup"><span data-stu-id="e4493-301">For an upgrade, you need to deploy files and databases from the staging web app to the production web app and database.</span></span> <span data-ttu-id="e4493-302">Wiele można wystąpienia problemów podczas wdrażania plików i baz danych.</span><span class="sxs-lookup"><span data-stu-id="e4493-302">Many things can go wrong when you deploy files and databases.</span></span> <span data-ttu-id="e4493-303">Za pomocą **wymiany** funkcji gniazd, możemy skrócenie czasu przestoju podczas uaktualniania i zmniejszyć ryzyko błędów, które mogą wystąpić podczas wdrażania zmian.</span><span class="sxs-lookup"><span data-stu-id="e4493-303">By using the **Swap** feature of slots, we can reduce downtime during an upgrade and reduce the risk of failures that can occur when you deploy changes.</span></span>
* <span data-ttu-id="e4493-304">Możesz zrobić **A / B, testowanie** za pomocą [testowanie w produkcji](https://azure.microsoft.com/documentation/videos/introduction-to-azure-websites-testing-in-production-with-galin-iliev/) funkcji.</span><span class="sxs-lookup"><span data-stu-id="e4493-304">You can do **A/B testing** by using the [Testing in production](https://azure.microsoft.com/documentation/videos/introduction-to-azure-websites-testing-in-production-with-galin-iliev/) feature.</span></span>

<span data-ttu-id="e4493-305">W tym przykładzie przedstawiono elastyczność platformy których można tworzyć niestandardowe moduły podobne do modułu Umbraco Courier, aby zarządzać wdrażaniem środowiskach.</span><span class="sxs-lookup"><span data-stu-id="e4493-305">This example shows you the flexibility of the platform where you can build custom modules similar to Umbraco Courier module to manage deployment across environments.</span></span>

## <a name="references"></a><span data-ttu-id="e4493-306">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="e4493-306">References</span></span>
[<span data-ttu-id="e4493-307">Programowanie zwinne oprogramowania z usługi aplikacji Azure</span><span class="sxs-lookup"><span data-stu-id="e4493-307">Agile software development with Azure App Service</span></span>](app-service-agile-software-development.md)

[<span data-ttu-id="e4493-308">Konfigurowanie środowisk dla aplikacji sieci web w usłudze Azure App Service przejściowych</span><span class="sxs-lookup"><span data-stu-id="e4493-308">Set up staging environments for web apps in Azure App Service</span></span>](web-sites-staged-publishing.md)

[<span data-ttu-id="e4493-309">Jak zablokować dostęp do miejsc wdrożenia nieprodukcyjnych w sieci web</span><span class="sxs-lookup"><span data-stu-id="e4493-309">How to block web access to non-production deployment slots</span></span>](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
