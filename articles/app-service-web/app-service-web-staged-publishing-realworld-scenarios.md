---
title: "aaaUse DevOps środowisk skutecznie dla aplikacji sieci web | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak wdrożenia toouse gniazd tooset się i zarządzanie nimi wiele środowisk deweloperskich dla aplikacji"
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
ms.openlocfilehash: 61a552e735a4ad9769b661d7c988744074ba2962
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-devops-environments-effectively-for-your-web-apps"></a><span data-ttu-id="1e493-103">Wykorzystywać środowisk opracowywania oprogramowania dla aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="1e493-103">Use DevOps environments effectively for your web apps</span></span>
<span data-ttu-id="1e493-104">W tym artykule opisano sposób tooset Konfigurowanie i zarządzanie wdrożenia aplikacji sieci web, gdy wiele wersji aplikacji znajdują się w różnych środowiskach, takich jak projektowanie, przemieszczania jakości (QA) i produkcji.</span><span class="sxs-lookup"><span data-stu-id="1e493-104">This article shows you how tooset up and manage web application deployments when multiple versions of your application are in various environments, such as development, staging, quality assurance (QA), and production.</span></span> <span data-ttu-id="1e493-105">Każdej wersji aplikacji mogą być uważane Środowisko deweloperskie do określonego celu hello procesu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="1e493-105">Each version of your application can be considered as a development environment for hello specific purpose of your deployment process.</span></span> <span data-ttu-id="1e493-106">Na przykład deweloperzy mogą używać hello jakości hello tootest środowiska w odpowiedzi na pytania aplikacji hello przed ich push hello tooproduction zmiany.</span><span class="sxs-lookup"><span data-stu-id="1e493-106">For example, developers can use hello QA environment tootest hello quality of hello application before they push hello changes tooproduction.</span></span>
<span data-ttu-id="1e493-107">Wiele środowisk deweloperskich można wyzwanie, ponieważ należy tootrack kodu, zarządzanie zasobami (obliczeniowych, aplikacji sieci web, bazy danych, pamięci podręcznej, itp.) i wdrożyć kod w środowiskach.</span><span class="sxs-lookup"><span data-stu-id="1e493-107">Multiple development environments can be a challenge because you need tootrack code, manage resources (compute, web app, database, cache, etc.), and deploy code across environments.</span></span>

## <a name="set-up-a-non-production-environment-stage-dev-qa"></a><span data-ttu-id="1e493-108">Konfigurowanie środowiska nieprodukcyjnych (etap, deweloperów, pytań i odpowiedzi)</span><span class="sxs-lookup"><span data-stu-id="1e493-108">Set up a non-production environment (stage, dev, QA)</span></span>
<span data-ttu-id="1e493-109">Po skonfigurowaniu i uruchomieniu aplikacji sieci web produkcyjnej hello następnym krokiem jest toocreate środowiskach nieprodukcyjnych.</span><span class="sxs-lookup"><span data-stu-id="1e493-109">After a production web app is up and running, hello next step is toocreate a non-production environment.</span></span> <span data-ttu-id="1e493-110">miejsca wdrożenia toouse, upewnij się, że działają w trybie planu Standard lub Premium usługi Azure App Service hello.</span><span class="sxs-lookup"><span data-stu-id="1e493-110">toouse deployment slots, make sure that you are running in hello Standard or Premium Azure App Service plan mode.</span></span> <span data-ttu-id="1e493-111">Miejsca wdrożenia są aplikacje sieci web, które mają własne nazwy hosta.</span><span class="sxs-lookup"><span data-stu-id="1e493-111">Deployment slots are live web apps that have their own host names.</span></span> <span data-ttu-id="1e493-112">Elementy zawartości i konfiguracji aplikacji sieci Web może być zamieniona między dwóch miejsc wdrożenia, w tym hello miejsca produkcji.</span><span class="sxs-lookup"><span data-stu-id="1e493-112">Web app content and configuration elements can be swapped between two deployment slots, including hello production slot.</span></span> <span data-ttu-id="1e493-113">Podczas wdrażania przedział czasu wdrożenia tooa aplikacji można uzyskać hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="1e493-113">When you deploy your application tooa deployment slot, you get hello following benefits:</span></span>

- <span data-ttu-id="1e493-114">Aplikacja sieci web tooa zmian w tymczasowych miejsce wdrożenia można sprawdzić przed wymiany aplikacji hello z miejscem produkcyjnym hello.</span><span class="sxs-lookup"><span data-stu-id="1e493-114">You can validate changes tooa web app in a staging deployment slot before you swap hello app with hello production slot.</span></span>
- <span data-ttu-id="1e493-115">Gdy najpierw wdrożyć miejsca tooa aplikacji sieci web i zamienić go w środowisku produkcyjnym, wszystkie wystąpienia miejsca hello są przygotowaniu miejsca przed wymieniane w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="1e493-115">When you deploy a web app tooa slot first and swap it into production, all instances of hello slot are warmed up before being swapped into production.</span></span> <span data-ttu-id="1e493-116">Ten proces eliminuje przestoju podczas wdrażania aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="1e493-116">This process eliminates downtime when you deploy your web app.</span></span> <span data-ttu-id="1e493-117">przekierowywanie ruchu Hello jest łatwego i żadne żądania są usuwane z powodu operacji tooswap.</span><span class="sxs-lookup"><span data-stu-id="1e493-117">hello traffic redirection is seamless, and no requests are dropped due tooswap operations.</span></span> <span data-ttu-id="1e493-118">tooautomate całego przepływu pracy, skonfiguruj [automatycznej wymiany](web-sites-staged-publishing.md#configure-auto-swap) podczas weryfikacji przed wymiany nie jest wymagana.</span><span class="sxs-lookup"><span data-stu-id="1e493-118">tooautomate this entire workflow, configure [Auto Swap](web-sites-staged-publishing.md#configure-auto-swap) when pre-swap validation is not needed.</span></span>
- <span data-ttu-id="1e493-119">Po wymiany gniazdo hello, który ma teraz hello wcześniej przygotowanych aplikacji sieci web ma hello poprzedniej aplikacji sieci web produkcyjnej.</span><span class="sxs-lookup"><span data-stu-id="1e493-119">After a swap, hello slot that has hello previously staged web app now has hello previous production web app.</span></span> <span data-ttu-id="1e493-120">Jeśli zmiany hello miejscami do miejsca produkcji hello są niezgodne z oczekiwaniami, można wykonać hello sam zamiana natychmiast tooget Twojego "ostatniej znanej dobrej" kopii aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="1e493-120">If hello changes swapped into hello production slot are not as you expected, you can perform hello same swap immediately tooget your "last known good" web app back.</span></span>

<span data-ttu-id="1e493-121">tooset się przemieszczania miejsce wdrożenia, zobacz [Konfigurowanie środowiska dla aplikacji sieci web w usłudze Azure App Service przejściowe](web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="1e493-121">tooset up a staging deployment slot, see [Set up staging environments for web apps in Azure App Service](web-sites-staged-publishing.md).</span></span> <span data-ttu-id="1e493-122">Każde środowisko powinna zawierać własny zestaw zasobów.</span><span class="sxs-lookup"><span data-stu-id="1e493-122">Every environment should include its own set of resources.</span></span> <span data-ttu-id="1e493-123">Na przykład jeśli aplikacja sieci web korzysta z bazy danych, następnie zarówno produkcyjne i przejściowe aplikacji sieci web należy używać różnych baz danych.</span><span class="sxs-lookup"><span data-stu-id="1e493-123">For example, if your web app uses a database, then both production and staging web apps should use different databases.</span></span> <span data-ttu-id="1e493-124">Dodaj przemieszczania zasobów środowisko rozwoju, takich jak bazy danych, magazynu lub tooset pamięci podręcznej środowiska deweloperskiego tymczasowej.</span><span class="sxs-lookup"><span data-stu-id="1e493-124">Add staging development environment resources such as database, storage, or cache tooset your staging development environment.</span></span>

## <a name="examples-of-using-multiple-development-environments"></a><span data-ttu-id="1e493-125">Przykłady użycia wielu środowisk deweloperskich</span><span class="sxs-lookup"><span data-stu-id="1e493-125">Examples of using multiple development environments</span></span>
<span data-ttu-id="1e493-126">Żadnego projektu należy stosować zarządzania kodem źródłowym z co najmniej dwóch środowisk: Programowanie i produkcji.</span><span class="sxs-lookup"><span data-stu-id="1e493-126">Any project should follow source code management with at least two environments: development and production.</span></span> <span data-ttu-id="1e493-127">Jeśli używasz systemów zarządzania zawartością (CMSs), platformy aplikacji, itp., aplikacji hello mogą nie obsługiwać ten scenariusz bez dostosowania.</span><span class="sxs-lookup"><span data-stu-id="1e493-127">If you use content management systems (CMSs), application frameworks, etc., hello application might not support this scenario without customization.</span></span> <span data-ttu-id="1e493-128">Tej możliwości ma wartość true dla niektórych hello popularnych środowisk omówionych w hello następujące sekcje.</span><span class="sxs-lookup"><span data-stu-id="1e493-128">This eventuality is true for some of hello popular frameworks that are discussed in hello following sections.</span></span> <span data-ttu-id="1e493-129">Wiele pytań pochodzą toomind podczas pracy z CMS/platform, takich jak:</span><span class="sxs-lookup"><span data-stu-id="1e493-129">Lots of questions come toomind when you work with CMS/frameworks, such as:</span></span>

- <span data-ttu-id="1e493-130">Jak możesz rozbicie hello zawartości w różnych środowiskach?</span><span class="sxs-lookup"><span data-stu-id="1e493-130">How do you break hello content out into different environments?</span></span>
- <span data-ttu-id="1e493-131">Jakie pliki można zmienić bez wpływu na aktualizacje wersji framework?</span><span class="sxs-lookup"><span data-stu-id="1e493-131">What files can you change without affecting framework version updates?</span></span>
- <span data-ttu-id="1e493-132">Sposób zarządzania konfiguracjami na środowisko</span><span class="sxs-lookup"><span data-stu-id="1e493-132">How do you manage configurations per environment?</span></span>
- <span data-ttu-id="1e493-133">Jak zarządzać wersji aktualizacji dla modułów, dodatki plug-in i hello core framework?</span><span class="sxs-lookup"><span data-stu-id="1e493-133">How do you manage version updates for modules, plugins, and hello core framework?</span></span>

<span data-ttu-id="1e493-134">Istnieje wiele sposobów tooset się wiele środowisk dla projektu.</span><span class="sxs-lookup"><span data-stu-id="1e493-134">There are many ways tooset up multiple environments for your project.</span></span> <span data-ttu-id="1e493-135">Witaj poniższe przykłady przedstawiają jedną metodę dla każdej odpowiedniej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1e493-135">hello following examples show one method for each respective application.</span></span>

### <a name="wordpress"></a><span data-ttu-id="1e493-136">WordPress</span><span class="sxs-lookup"><span data-stu-id="1e493-136">WordPress</span></span>
<span data-ttu-id="1e493-137">W tej sekcji dowiesz się, jak gniazd tooset się przepływ pracy wdrażania przy użyciu platformy WordPress.</span><span class="sxs-lookup"><span data-stu-id="1e493-137">In this section, you will learn how tooset up a deployment workflow by using slots for WordPress.</span></span> <span data-ttu-id="1e493-138">WordPress, na przykład większość rozwiązań CMS, nie obsługuje wiele środowisk deweloperskich bez dostosowania.</span><span class="sxs-lookup"><span data-stu-id="1e493-138">WordPress, like most CMS solutions, does not support multiple development environments without customization.</span></span> <span data-ttu-id="1e493-139">Funkcja Web Apps Hello Azure App Service ma kilka funkcji, dzięki któremu można łatwo toostore ustawienia konfiguracji poza swój kod.</span><span class="sxs-lookup"><span data-stu-id="1e493-139">hello Web Apps feature of Azure App Service has a few features that make it easy toostore configuration settings outside your code.</span></span>

1. <span data-ttu-id="1e493-140">Przed utworzeniem miejsca przemieszczania, skonfiguruj toosupport kod z aplikacji wiele środowisk.</span><span class="sxs-lookup"><span data-stu-id="1e493-140">Before you create a staging slot, set up your application code toosupport multiple environments.</span></span> <span data-ttu-id="1e493-141">toosupport wiele środowisk w WordPress, potrzebujesz tooedit `wp-config.php` na komputerze lokalnym sieci web app i Dodaj hello następującego kodu na początku hello hello pliku.</span><span class="sxs-lookup"><span data-stu-id="1e493-141">toosupport multiple environments in WordPress, you need tooedit `wp-config.php` on your local development web app and add hello following code at hello beginning of hello file.</span></span> <span data-ttu-id="1e493-142">Ten proces umożliwi toopick hello poprawne konfigurację aplikacji na podstawie hello wybranego środowiska.</span><span class="sxs-lookup"><span data-stu-id="1e493-142">This process will enable your application toopick hello correct configuration based on hello selected environment.</span></span>

    ```
    // Support multiple environments
    // set hello config file based on current environment
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
    // include hello config file if it exists, otherwise WP is going toofail
    require_once $path. $config_file;
    ```

2. <span data-ttu-id="1e493-143">Utwórz folder w katalogu głównym aplikacji sieci web o nazwie `config`i Dodaj hello `wp-config.azure.php` i `wp-config.local.php` pliki, które zawierają odpowiednio Twojego środowiska platformy Azure i lokalnego środowiska.</span><span class="sxs-lookup"><span data-stu-id="1e493-143">Create a folder under web app root called `config`, and add hello `wp-config.azure.php` and `wp-config.local.php` files, which represent your Azure environment and local environment respectively.</span></span>

3. <span data-ttu-id="1e493-144">Skopiuj następujące hello w `wp-config.local.php`:</span><span class="sxs-lookup"><span data-stu-id="1e493-144">Copy hello following in `wp-config.local.php`:</span></span>

    ```
    <?php
    // MySQL settings
    /** hello name of hello database for WordPress */

    define('DB_NAME', 'yourdatabasename');

    /** MySQL database username */
    define('DB_USER', 'yourdbuser');

    /** MySQL database password */
    define('DB_PASSWORD', 'yourpassword');

    /** MySQL hostname */
    define('DB_HOST', 'localhost');
    /**
     * For developers: WordPress debugging mode.
     * * Change this tootrue tooenable hello display of notices during development.
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

    <span data-ttu-id="1e493-145">Ustawienia kluczy zabezpieczeń hello zgodnie z opisami w poprzednim kodzie hello może pomóc tooprevent aplikacji sieci web z trwa zaatakowane, należy więc unikatowe wartości.</span><span class="sxs-lookup"><span data-stu-id="1e493-145">Setting hello security keys as illustrated in hello previous code can help tooprevent your web app from being hacked, so use unique values.</span></span> <span data-ttu-id="1e493-146">Jeśli potrzebujesz ciąg hello toogenerate wymienionych w kodzie hello kluczy zabezpieczeń, możesz [generator automatyczne przejście toohello](https://api.wordpress.org/secret-key/1.1/salt) toocreate nowy klucz/wartość pary.</span><span class="sxs-lookup"><span data-stu-id="1e493-146">If you need toogenerate hello string for security keys mentioned in hello code, you can [go toohello automatic generator](https://api.wordpress.org/secret-key/1.1/salt) toocreate new key/value pairs.</span></span>

4. <span data-ttu-id="1e493-147">Kopiuj hello poniższy kod w `wp-config.azure.php`:</span><span class="sxs-lookup"><span data-stu-id="1e493-147">Copy hello following code in `wp-config.azure.php`:</span></span>

    ```    
    <?php
    // MySQL settings
    /** hello name of hello database for WordPress */

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
    * Change this tootrue tooenable hello display of notices during development.
    * It is strongly recommended that plugin and theme developers use WP_DEBUG
    * in their development environments.
    * Turn on debug logging tooinvestigate issues without displaying tooend user. For WP_DEBUG_LOG to
    * do anything, WP_DEBUG must be enabled (true). WP_DEBUG_DISPLAY should be used in conjunction
    * with WP_DEBUG_LOG so that errors are not displayed on hello page */

    */
    define('WP_DEBUG', getenv('WP_DEBUG'));
    define('WP_DEBUG_LOG', getenv('TURN_ON_DEBUG_LOG'));
    define('WP_DEBUG_DISPLAY',false);

    //Security key settings
    /** If you need toogenerate hello string for security keys mentioned above, you can go hello automatic generator toocreate new keys/values: https://api.wordpress.org/secret-key/1.1/salt **/
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

#### <a name="use-relative-paths"></a><span data-ttu-id="1e493-148">Użycie ścieżek względnych</span><span class="sxs-lookup"><span data-stu-id="1e493-148">Use relative paths</span></span>
<span data-ttu-id="1e493-149">Jeden ostatniego tooconfigure operacją w aplikacji WordPress hello jest ścieżek względnych.</span><span class="sxs-lookup"><span data-stu-id="1e493-149">One last thing tooconfigure in hello WordPress app is relative paths.</span></span> <span data-ttu-id="1e493-150">WordPress przechowują adres URL w hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="1e493-150">WordPress stores URL information in hello database.</span></span> <span data-ttu-id="1e493-151">Ta pamięć masowa utrudnia przenoszenia zawartości z jednego środowiska tooanother.</span><span class="sxs-lookup"><span data-stu-id="1e493-151">This storage makes moving content from one environment tooanother more difficult.</span></span> <span data-ttu-id="1e493-152">Należy bazy danych hello tooupdate każdorazowego przenoszenia danych z toostage lokalnej lub środowisk tooproduction etapu.</span><span class="sxs-lookup"><span data-stu-id="1e493-152">You need tooupdate hello database every time you move from local toostage or stage tooproduction environments.</span></span> <span data-ttu-id="1e493-153">ryzyko hello tooreduce problemów, które może być spowodowany z wdrażania bazy danych, za każdym razem, gdy wdrażanie z jednego środowiska tooanother, użyj hello [względną głównego łączy wtyczki](https://wordpress.org/plugins/root-relative-urls/), które można zainstalować przy użyciu hello WordPress administratora pulpit nawigacyjny.</span><span class="sxs-lookup"><span data-stu-id="1e493-153">tooreduce hello risk of issues that can be caused with deploying a database every time you deploy from one environment tooanother, use hello [Relative Root links plugin](https://wordpress.org/plugins/root-relative-urls/), which you can install by using hello WordPress administrator dashboard.</span></span>

<span data-ttu-id="1e493-154">Dodaj następujące wpisy tooyour hello `wp-config.php` pliku przed hello `That's all, stop editing!` komentarza:</span><span class="sxs-lookup"><span data-stu-id="1e493-154">Add hello following entries tooyour `wp-config.php` file before hello `That's all, stop editing!` comment:</span></span>

```

  define('WP_HOME', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_SITEURL', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_CONTENT_URL', '/wp-content');
    define('DOMAIN_CURRENT_SITE', filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
```

<span data-ttu-id="1e493-155">Aktywowanie wtyczki hello za pośrednictwem hello `Plugins` menu w pulpitu nawigacyjnego WordPress administratora.</span><span class="sxs-lookup"><span data-stu-id="1e493-155">Activate hello plugin through hello `Plugins` menu in WordPress administrator dashboard.</span></span> <span data-ttu-id="1e493-156">Zapisz ustawienia łącze stałe dla aplikacji WordPress.</span><span class="sxs-lookup"><span data-stu-id="1e493-156">Save your permalink settings for WordPress app.</span></span>

#### <a name="hello-final-wp-configphp-file"></a><span data-ttu-id="1e493-157">Witaj końcowego `wp-config.php` pliku</span><span class="sxs-lookup"><span data-stu-id="1e493-157">hello final `wp-config.php` file</span></span>
<span data-ttu-id="1e493-158">Nie wpłynie na wszystkie aktualizacje core WordPress z `wp-config.php`, `wp-config.azure.php`, i `wp-config.local.php` plików.</span><span class="sxs-lookup"><span data-stu-id="1e493-158">Any WordPress core updates will not affect your `wp-config.php`, `wp-config.azure.php`, and `wp-config.local.php` files.</span></span> <span data-ttu-id="1e493-159">Oto ostateczną wersją hello `wp-config.php` pliku:</span><span class="sxs-lookup"><span data-stu-id="1e493-159">Here's a final version of hello `wp-config.php` file:</span></span>

```
<?php
/**
 * hello base configurations of hello WordPress.
 *
 * This file has hello following configurations: MySQL settings, Table Prefix,
 * Secret Keys, and ABSPATH. You can find more information by visiting
 *
 * Codex page. You can get hello MySQL settings from your web host.
 *
 * This file is used by hello wp-config.php creation script during the
 * installation. You don't have toouse hello web web app, you can just copy this file
 * too"wp-config.php" and fill in hello values.
 *
 * @package WordPress
 */

// Support multiple environments
// set hello config file based on current environment
if (strpos($_SERVER['HTTP_HOST'],'localhost') !== false) { // local development
  $config_file = 'config/wp-config.local.php';
}
elseif ((strpos(getenv('WP_ENV'),'stage') !== false) ||(strpos(getenv('WP_ENV'),'prod' )!== false )){
  $config_file = 'config/wp-config.azure.php';
}


$path = dirname(__FILE__). '/';
if (file_exists($path. $config_file)) {
  // include hello config file if it exists, otherwise WP is going toofail
  require_once $path. $config_file;
}

/** Database Charset toouse in creating database tables. */
define('DB_CHARSET', 'utf8');

/** hello Database Collate type. Don't change this if in doubt. */
define('DB_COLLATE', '');


/* That's all, stop editing! Happy blogging. */

define('WP_HOME', 'http://'. $_SERVER['HTTP_HOST']);
define('WP_SITEURL', 'http://'. $_SERVER['HTTP_HOST']);
define('WP_CONTENT_URL', '/wp-content');
define('DOMAIN_CURRENT_SITE', $_SERVER['HTTP_HOST']);

/** Absolute path toohello WordPress directory. */
if ( !defined('ABSPATH') )
    define('ABSPATH', dirname(__FILE__). '/');

/** Sets up WordPress vars and included files. */
require_once(ABSPATH. 'wp-settings.php');
```

#### <a name="set-up-a-staging-environment"></a><span data-ttu-id="1e493-160">Konfigurowanie środowiska przemieszczania</span><span class="sxs-lookup"><span data-stu-id="1e493-160">Set up a staging environment</span></span>
1. <span data-ttu-id="1e493-161">Jeśli masz już aplikację sieci web WordPress z subskrypcją platformy Azure, zaloguj się w toohello [portalu Azure](http://portal.azure.com), a następnie przejdź aplikacji sieci web WordPress tooyour.</span><span class="sxs-lookup"><span data-stu-id="1e493-161">If you already have a WordPress web app running on your Azure subscription, sign in toohello [Azure portal](http://portal.azure.com), and then go tooyour WordPress web app.</span></span> <span data-ttu-id="1e493-162">Jeśli nie masz aplikacji sieci web WordPress, można utworzyć jedną z hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="1e493-162">If you don't have a WordPress web app, you can create one from hello Azure Marketplace.</span></span> <span data-ttu-id="1e493-163">toolearn więcej, zobacz [tworzenie aplikacji sieci web WordPress w usłudze Azure App Service](web-sites-php-web-site-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="1e493-163">toolearn more, see [Create a WordPress web app in Azure App Service](web-sites-php-web-site-gallery.md).</span></span>
<span data-ttu-id="1e493-164">Kliknij przycisk **ustawienia** > **miejsc wdrożenia** > **Dodaj** toocreate miejsca wdrożenia o nazwie hello *etap*.</span><span class="sxs-lookup"><span data-stu-id="1e493-164">Click **Settings** > **Deployment slots** > **Add** toocreate a deployment slot with hello name *stage*.</span></span> <span data-ttu-id="1e493-165">Miejsce wdrożenia jest inną aplikację sieci web, która udziałów hello tyle samo zasobów co hello aplikacji głównej sieci web, utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="1e493-165">A deployment slot is another web application that shares hello same resources as hello primary web app that you created previously.</span></span>

    ![Tworzenie miejsca wdrożenia etapu](./media/app-service-web-staged-publishing-realworld-scenarios/1setupstage.png)

2. <span data-ttu-id="1e493-167">Dodaj inny baza danych MySQL, powiedz `wordpress-stage-db`, grupy zasobów tooyour `wordpressapp-group`.</span><span class="sxs-lookup"><span data-stu-id="1e493-167">Add another MySQL database, say `wordpress-stage-db`, tooyour resource group, `wordpressapp-group`.</span></span>

    ![Dodaj grupę tooresource bazy danych MySQL](./media/app-service-web-staged-publishing-realworld-scenarios/2addmysql.png)

3. <span data-ttu-id="1e493-169">Aktualizowanie parametrów połączenia hello etap wdrażania miejsca toopoint toohello nowej bazy danych, `wordpress-stage-db`.</span><span class="sxs-lookup"><span data-stu-id="1e493-169">Update hello connection strings for your stage deployment slot toopoint toohello new database, `wordpress-stage-db`.</span></span> <span data-ttu-id="1e493-170">Aplikacja sieci web produkcji `wordpressprodapp`i aplikacji sieci web na potrzeby przemieszczania `wordpressprodapp-stage`, bazy danych punktu toodifferent musi.</span><span class="sxs-lookup"><span data-stu-id="1e493-170">Your production web app, `wordpressprodapp`, and staging web app, `wordpressprodapp-stage`, must point toodifferent databases.</span></span>

#### <a name="configure-environment-specific-app-settings"></a><span data-ttu-id="1e493-171">Konfiguruj ustawienia specyficzne dla środowiska aplikacji</span><span class="sxs-lookup"><span data-stu-id="1e493-171">Configure environment-specific app settings</span></span>
<span data-ttu-id="1e493-172">Deweloperzy mogą przechowywać pary klucz wartość ciągu na platformie Azure w ramach hello informacji o konfiguracji, o nazwie **ustawień aplikacji**, który jest skojarzony z aplikacją sieci web.</span><span class="sxs-lookup"><span data-stu-id="1e493-172">Developers can store key/value string pairs in Azure as part of hello configuration information, called **App Settings**, that's associated with a web app.</span></span> <span data-ttu-id="1e493-173">W czasie wykonywania aplikacje sieci web automatycznie pobierania tych wartości i były dostępne toocode, działającej w aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="1e493-173">At runtime, web apps automatically retrieve these values and make them available toocode that's running in your web app.</span></span> <span data-ttu-id="1e493-174">Z punktu widzenia zabezpieczeń, który jest korzyści nieuprzywilejowany po stronie, ponieważ poufne informacje, takie jak parametry połączenia bazy danych, które obejmują hasła, nigdy nie wyświetlane jako zwykły tekst w pliku takich jak `wp-config.php`.</span><span class="sxs-lookup"><span data-stu-id="1e493-174">From a security perspective, that is a nice side benefit because sensitive information, such as database connection strings that include passwords, never show up as clear text in a file such as `wp-config.php`.</span></span>

<span data-ttu-id="1e493-175">Ten proces, który znajduje się w powitania po akapitów, jest przydatne, ponieważ obejmuje ona zarówno pliku zmiany i bazy danych dla aplikacji WordPress hello:</span><span class="sxs-lookup"><span data-stu-id="1e493-175">This process, which is explained in hello following paragraphs, is useful because it includes both file changes and database changes for hello WordPress app:</span></span>

* <span data-ttu-id="1e493-176">Uaktualnienie wersji WordPress</span><span class="sxs-lookup"><span data-stu-id="1e493-176">WordPress version upgrade</span></span>
* <span data-ttu-id="1e493-177">Dodawanie nowych lub edytowanie lub uaktualnić wtyczek</span><span class="sxs-lookup"><span data-stu-id="1e493-177">Add new or edit or upgrade plugins</span></span>
* <span data-ttu-id="1e493-178">Dodawanie nowych lub edytowanie lub uaktualnić motywów</span><span class="sxs-lookup"><span data-stu-id="1e493-178">Add new or edit or upgrade themes</span></span>

<span data-ttu-id="1e493-179">Konfiguruj ustawienia aplikacji dla:</span><span class="sxs-lookup"><span data-stu-id="1e493-179">Configure app settings for:</span></span>

* <span data-ttu-id="1e493-180">Informacje o bazie danych</span><span class="sxs-lookup"><span data-stu-id="1e493-180">Database information</span></span>
* <span data-ttu-id="1e493-181">Włączenie/wyłączenie rejestrowania WordPress</span><span class="sxs-lookup"><span data-stu-id="1e493-181">Turning on/off WordPress logging</span></span>
* <span data-ttu-id="1e493-182">Ustawienia zabezpieczeń WordPress</span><span class="sxs-lookup"><span data-stu-id="1e493-182">WordPress security settings</span></span>

![Ustawienia aplikacji dla aplikacji sieci web Wordpress](./media/app-service-web-staged-publishing-realworld-scenarios/3configure.png)

<span data-ttu-id="1e493-184">Upewnij się, że dodane hello następujące ustawienia aplikacji dla miejsca z produkcji w sieci web app i etap.</span><span class="sxs-lookup"><span data-stu-id="1e493-184">Make sure that you add hello following app settings for your production web app and stage slot.</span></span> <span data-ttu-id="1e493-185">Należy pamiętać, że aplikacja sieci web produkcji hello i przemieszczania aplikacji sieci web korzystają z różnych baz danych.</span><span class="sxs-lookup"><span data-stu-id="1e493-185">Note that hello production web app and staging web app use different databases.</span></span>

1. <span data-ttu-id="1e493-186">Wyczyść hello **ustawienie miejsca** pola wyboru dla wszystkich parametrów hello ustawienia, z wyjątkiem WP_ENV.</span><span class="sxs-lookup"><span data-stu-id="1e493-186">Clear hello **Slot Setting** checkbox for all hello settings parameters except WP_ENV.</span></span> <span data-ttu-id="1e493-187">Ten proces będzie wymiany hello konfiguracji dla aplikacji sieci web, zawartość pliku i bazy danych.</span><span class="sxs-lookup"><span data-stu-id="1e493-187">This process will swap hello configuration for your web app, file content, and database.</span></span> <span data-ttu-id="1e493-188">Jeśli **ustawienie miejsca** jest zaznaczone, ustawienia aplikacji i konfiguracja ciąg połączenia aplikacji sieci web hello będzie *nie* przenieść w środowiskach, w trakcie **wymiany** operacji.</span><span class="sxs-lookup"><span data-stu-id="1e493-188">If **Slot Setting** is checked, hello web app’s app settings and connection string configuration will *not* move across environments when doing a **Swap** operation.</span></span> <span data-ttu-id="1e493-189">Wszelkie zmiany bazy danych, które znajdują się nie będę powodować utraty aplikacji sieci web w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="1e493-189">Any database changes that are present will not break your production web app.</span></span>

2. <span data-ttu-id="1e493-190">Wdróż hello rozwoju lokalnego środowiska sieci web aplikacji toohello etap web app i bazy danych za pomocą programu WebMatrix lub narzędzia wybranych przez użytkownika, takie jak FTP, Git lub PhpMyAdmin.</span><span class="sxs-lookup"><span data-stu-id="1e493-190">Deploy hello local development environment web app toohello stage web app and database by using WebMatrix or tools of your choice, such as FTP, Git, or PhpMyAdmin.</span></span>

    ![Okno dialogowe publikowania macierzy sieci Web dla aplikacji sieci web WordPress](./media/app-service-web-staged-publishing-realworld-scenarios/4wmpublish.png)

3. <span data-ttu-id="1e493-192">Przeglądanie i testowanie przemieszczania aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="1e493-192">Browse and test your staging web app.</span></span> <span data-ttu-id="1e493-193">Biorąc pod uwagę scenariusz, w przypadku toobe zaktualizowane motywu hello hello aplikacji sieci web w tym miejscu jest hello przemieszczania aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="1e493-193">Considering a scenario where hello theme of hello web app is toobe updated, here is hello staging web app.</span></span>

    ![Przeglądaj przemieszczania aplikacji sieci web przed wymiany gniazd](./media/app-service-web-staged-publishing-realworld-scenarios/5wpstage.png)

4. <span data-ttu-id="1e493-195">Jeśli wszystko wygląda dobrze, kliknij przycisk hello **wymiany** znajdującego się na Twoje przemieszczania toomove aplikacji sieci web środowiska produkcyjnego toohello zawartości.</span><span class="sxs-lookup"><span data-stu-id="1e493-195">If all looks good, click hello **Swap** button on your staging web app toomove your content toohello production environment.</span></span> <span data-ttu-id="1e493-196">W takim przypadku zamienić hello aplikacji sieci web i bazy danych hello w środowiskach podczas każdego **wymiany** operacji.</span><span class="sxs-lookup"><span data-stu-id="1e493-196">In this case, you swap hello web app and hello database across environments during every **Swap** operation.</span></span>

    ![Zamień podgląd zmian dla środowiska WordPress](./media/app-service-web-staged-publishing-realworld-scenarios/6swaps1.png)

    > [!NOTE]
    > <span data-ttu-id="1e493-198">Jeżeli dany scenariusz wymaga tooonly wypychania plików (Brak aktualizacji bazy danych), sprawdź **ustawienie miejsca** dla wszystkich hello związanych z bazy danych *ustawień aplikacji* i *ustawieniaParametrypołączeniaz*w hello **ustawień aplikacji sieci Web** bloku w portalu Azure, przed wykonaniem hello hello **wymiany**.</span><span class="sxs-lookup"><span data-stu-id="1e493-198">If your scenario needs tooonly push files (no database updates), then check **Slot Setting** for all hello database-related *app settings* and *connection strings settings* in hello **Web App Settings** blade within hello Azure portal before doing hello **Swap**.</span></span> <span data-ttu-id="1e493-199">W takim przypadku DB_NAME, DB_HOST DB_PASSWORD, DB_USER i domyślnych ustawień połączenia w ciągu powinna nie pojawiają się w podgląd zmian po wykonaniu **wymiany**.</span><span class="sxs-lookup"><span data-stu-id="1e493-199">In this case, DB_NAME, DB_HOST, DB_PASSWORD, DB_USER, and default connection string settings should not show up in preview changes when you do a **Swap**.</span></span> <span data-ttu-id="1e493-200">W tej chwili po zakończeniu hello **wymiany** operacji hello aplikacji sieci web WordPress będzie mieć hello aktualizacji tylko pliki.</span><span class="sxs-lookup"><span data-stu-id="1e493-200">At this time, when you complete hello **Swap** operation, hello WordPress web app will have hello updates files only.</span></span>
    >
    >

    <span data-ttu-id="1e493-201">Przed to **wymiany**, Oto aplikacji sieci web WordPress hello w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="1e493-201">Before doing a **Swap**, here is hello production WordPress web app.</span></span>
    <span data-ttu-id="1e493-202">![Aplikacja sieci web produkcyjnym przed wymiany gniazd](./media/app-service-web-staged-publishing-realworld-scenarios/7bfswap.png)</span><span class="sxs-lookup"><span data-stu-id="1e493-202">![Production web app before swapping slots](./media/app-service-web-staged-publishing-realworld-scenarios/7bfswap.png)</span></span>

    <span data-ttu-id="1e493-203">Po hello **wymiany** operacji motywu hello została zaktualizowana na aplikację sieci web w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="1e493-203">After hello **Swap** operation, hello theme has been updated on your production web app.</span></span>

    ![Aplikacja sieci web produkcji po wymiany gniazd](./media/app-service-web-staged-publishing-realworld-scenarios/8afswap.png)

5. <span data-ttu-id="1e493-205">Jeśli potrzebujesz ponownie tooroll toohello produkcji w sieci web można przejść **ustawień aplikacji**i kliknij przycisk hello **wymiany** przycisk tooswap hello web app i bazy danych z poziomu gniazda produkcyjnego toostaging.</span><span class="sxs-lookup"><span data-stu-id="1e493-205">When you need tooroll back, you can go toohello production web **App Settings**, and click hello **Swap** button tooswap hello web app and database from production toostaging slot.</span></span> <span data-ttu-id="1e493-206">Pamiętaj, że jeśli zmian w bazie danych są dołączone **wymiany** operacji, a następnie hello następnym wdrażanie aplikacji sieci web na potrzeby przemieszczania tooyour toodeploy hello zmiany toohello bieżąca baza danych jest wymagane dla tymczasową aplikację sieci web.</span><span class="sxs-lookup"><span data-stu-id="1e493-206">Remember that if database changes are included with a **Swap** operation, then hello next time you deploy tooyour staging web app, you need toodeploy hello database changes toohello current database for your staging web app.</span></span> <span data-ttu-id="1e493-207">Hello bieżąca baza danych może być hello poprzedniej produkcyjną bazę danych lub hello etap w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="1e493-207">hello current database might be hello previous production database or hello stage database.</span></span>

#### <a name="summary"></a><span data-ttu-id="1e493-208">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="1e493-208">Summary</span></span>
<span data-ttu-id="1e493-209">Poniżej znajduje się uogólniony procesu dla dowolnej aplikacji, która ma bazy danych:</span><span class="sxs-lookup"><span data-stu-id="1e493-209">Following is a generalized process for any application that has a database:</span></span>

1. <span data-ttu-id="1e493-210">Instalacji aplikacji hello w środowisku lokalnym.</span><span class="sxs-lookup"><span data-stu-id="1e493-210">Install hello application on your local environment.</span></span>
2. <span data-ttu-id="1e493-211">Zawiera konfiguracje specyficzne dla środowiska (lokalne i Azure Web Apps).</span><span class="sxs-lookup"><span data-stu-id="1e493-211">Include environment-specific configurations (local and Azure Web Apps).</span></span>
3. <span data-ttu-id="1e493-212">Konfigurowanie środowiska przemieszczania i produkcji dla aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="1e493-212">Set up your staging and production environments for Web Apps.</span></span>
4. <span data-ttu-id="1e493-213">Jeśli masz już uruchomione na platformie Azure aplikacji produkcyjnych, synchronizować produkcji zawartości (pliki/kod i bazy danych) toolocal przemieszczania środowiska i.</span><span class="sxs-lookup"><span data-stu-id="1e493-213">If you have a production application already running on Azure, sync your production content (files/code and database) toolocal and staging environments.</span></span>
5. <span data-ttu-id="1e493-214">Tworzenie aplikacji w środowisku lokalnym.</span><span class="sxs-lookup"><span data-stu-id="1e493-214">Develop your application on your local environment.</span></span>
6. <span data-ttu-id="1e493-215">Ustaw aplikację sieci web produkcji konserwacja lub tryb zablokowane, a zsynchronizować bazy danych zawartości z toostaging i deweloperów środowisk produkcyjnych.</span><span class="sxs-lookup"><span data-stu-id="1e493-215">Place your production web app under maintenance or locked mode, and sync database content from production toostaging and dev environments.</span></span>
7. <span data-ttu-id="1e493-216">Wdróż toohello przemieszczania środowiska i testowania.</span><span class="sxs-lookup"><span data-stu-id="1e493-216">Deploy toohello staging environment and test.</span></span>
8. <span data-ttu-id="1e493-217">Wdróż tooproduction środowiska.</span><span class="sxs-lookup"><span data-stu-id="1e493-217">Deploy tooproduction environment.</span></span>
9. <span data-ttu-id="1e493-218">Powtórz kroki od 4 do 6.</span><span class="sxs-lookup"><span data-stu-id="1e493-218">Repeat steps 4 through 6.</span></span>

### <a name="umbraco"></a><span data-ttu-id="1e493-219">Umbraco</span><span class="sxs-lookup"><span data-stu-id="1e493-219">Umbraco</span></span>
<span data-ttu-id="1e493-220">W tej sekcji dowiesz się, jak hello Umbraco CMS w wielu środowiskach DevOps używa toodeploy niestandardowego modułu.</span><span class="sxs-lookup"><span data-stu-id="1e493-220">In this section, you will learn how hello Umbraco CMS uses a custom module toodeploy across multiple DevOps environments.</span></span> <span data-ttu-id="1e493-221">W poniższym przykładzie przedstawiono toomanaging różne podejścia wiele środowisk deweloperskich.</span><span class="sxs-lookup"><span data-stu-id="1e493-221">This example provides a different approach toomanaging multiple development environments.</span></span>

<span data-ttu-id="1e493-222">[Umbraco CMS](http://umbraco.com/) jest rozwiązaniem .NET CMS popularnych, która jest używana przez wielu deweloperów.</span><span class="sxs-lookup"><span data-stu-id="1e493-222">[Umbraco CMS](http://umbraco.com/) is a popular .NET CMS solution that's used by many developers.</span></span> <span data-ttu-id="1e493-223">Zapewnia hello [Courier2](http://umbraco.com/products/more-add-ons/courier-2) toodeploy modułu ze środowisk tooproduction toostaging programowanie.</span><span class="sxs-lookup"><span data-stu-id="1e493-223">It provides hello [Courier2](http://umbraco.com/products/more-add-ons/courier-2) module toodeploy from development toostaging tooproduction environments.</span></span> <span data-ttu-id="1e493-224">Środowisko deweloperskie lokalnej dla aplikacji sieci web Umbraco CMS można łatwo utworzyć za pomocą programu Visual Studio lub programu WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="1e493-224">You can easily create a local development environment for an Umbraco CMS web app by using Visual Studio or WebMatrix.</span></span>

- [<span data-ttu-id="1e493-225">Tworzenie aplikacji sieci web Umbraco z programem Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1e493-225">Create an Umbraco web app with Visual Studio</span></span>](https://our.umbraco.org/documentation/Installation/install-umbraco-with-nuget)
- [<span data-ttu-id="1e493-226">Tworzenie aplikacji sieci web Umbraco za pomocą programu WebMatrix</span><span class="sxs-lookup"><span data-stu-id="1e493-226">Create an Umbraco web app with WebMatrix</span></span>](http://umbraco.tv/videos/umbraco-v7/implementor/fundamentals/installation/creating-umbraco-site-from-webmatrix-web-gallery/)

<span data-ttu-id="1e493-227">Zawsze pamiętaj tooremove hello `install` folder aplikacji i nigdy nie przesłania go toostage lub produkcyjnych aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="1e493-227">Always remember tooremove hello `install` folder under your application, and never upload it toostage or production web apps.</span></span> <span data-ttu-id="1e493-228">W tym samouczku korzysta z programu WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="1e493-228">This tutorial uses WebMatrix.</span></span>

#### <a name="set-up-a-staging-environment"></a><span data-ttu-id="1e493-229">Konfigurowanie środowiska przemieszczania</span><span class="sxs-lookup"><span data-stu-id="1e493-229">Set up a staging environment</span></span>
1. <span data-ttu-id="1e493-230">Tworzenie miejsca wdrożenia, jak już wspomniano hello Umbraco CMS aplikacji sieci web, przy założeniu, że masz już aplikację sieci web Umbraco CMS i uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="1e493-230">Create a deployment slot as mentioned previously for hello Umbraco CMS web app, assuming you already have an Umbraco CMS web app up and running.</span></span> <span data-ttu-id="1e493-231">Jeśli nie chcesz, możesz utworzyć jedną z hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="1e493-231">If you do not, you can create one from hello Marketplace.</span></span>
2. <span data-ttu-id="1e493-232">Zaktualizować hello parametry połączenia dla Twojego etap wdrażania miejsca toopoint toohello nowe **umbraco etap db** bazy danych.</span><span class="sxs-lookup"><span data-stu-id="1e493-232">Update hello connection string for your stage deployment slot toopoint toohello new **umbraco-stage-db** database.</span></span> <span data-ttu-id="1e493-233">Produkcji aplikacji sieci web (umbraositecms-1) i przemieszczania aplikacji sieci web (umbracositecms-1-etap) *musi* toodifferent punktu baz danych.</span><span class="sxs-lookup"><span data-stu-id="1e493-233">Your production web app (umbraositecms-1) and staging web app (umbracositecms-1-stage) *must* point toodifferent databases.</span></span>

    ![Zaktualizuj parametry połączenia dla aplikacji sieci web za pomocą nowej tymczasowej bazy danych przemieszczania](./media/app-service-web-staged-publishing-realworld-scenarios/9umbconnstr.png)

3. <span data-ttu-id="1e493-235">Kliknij przycisk **ustawień publikowania pobrać** dla miejsca wdrożenia hello **etapu**.</span><span class="sxs-lookup"><span data-stu-id="1e493-235">Click **Get Publish settings** for hello deployment slot **stage**.</span></span> <span data-ttu-id="1e493-236">Ten proces pobierze plik ustawień publikowania, który przechowuje wszystkie informacje hello, że program Visual Studio lub programu WebMatrix wymaga toopublish aplikacji hello lokalnej sieci web aplikacji toohello aplikacji sieci web Azure.</span><span class="sxs-lookup"><span data-stu-id="1e493-236">This process will download a publish settings file that stores all hello information that Visual Studio or WebMatrix requires toopublish your application from hello local development web app toohello Azure web app.</span></span>

    ![Ustawienie aplikacji sieci web na potrzeby przemieszczania hello publikowania Get](./media/app-service-web-staged-publishing-realworld-scenarios/10getpsetting.png)
4. <span data-ttu-id="1e493-238">Otwórz aplikację sieci web lokalne działania projektowe w programie WebMatrix lub Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1e493-238">Open your local development web app in WebMatrix or Visual Studio.</span></span> <span data-ttu-id="1e493-239">W tym samouczku korzysta z programu WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="1e493-239">This tutorial uses WebMatrix.</span></span> <span data-ttu-id="1e493-240">Najpierw należy tooimport hello pliku ustawień aplikacji sieci web przemieszczania publikowania.</span><span class="sxs-lookup"><span data-stu-id="1e493-240">First, you need tooimport hello publish settings file for your staging web app.</span></span>

    ![Importowanie ustawień publikowania dla Umbraco przy użyciu macierzy sieci Web](./media/app-service-web-staged-publishing-realworld-scenarios/11import.png)

5. <span data-ttu-id="1e493-242">Przegląd zmian dokonanych w oknie dialogowym hello i wdrażania aplikacji sieci web platformy Azure tooyour aplikacji lokalnej sieci web, *umbracositecms-1-etap*.</span><span class="sxs-lookup"><span data-stu-id="1e493-242">Review changes in hello dialog box, and deploy your local web app tooyour Azure web app, *umbracositecms-1-stage*.</span></span> <span data-ttu-id="1e493-243">Podczas wdrażania plików bezpośrednio z aplikacji sieci web tooyour przemieszczania, zostaną pominięte pliki w hello `~/app_data/TEMP/` folderu, ponieważ te pliki zostaną ponownie wygenerowane po pierwszej aplikacji sieci web etap hello uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="1e493-243">When you deploy files directly tooyour staging web app, you will omit files in hello `~/app_data/TEMP/` folder because these files will be regenerated when hello stage web app is first started.</span></span> <span data-ttu-id="1e493-244">Należy również pominąć hello `~/app_data/umbraco.config` pliku, który również zostanie ponownie wygenerowany.</span><span class="sxs-lookup"><span data-stu-id="1e493-244">You should also omit hello `~/app_data/umbraco.config` file, which will also be regenerated.</span></span>

    ![Przejrzyj zmiany publikowania w sieci web macierzy.](./media/app-service-web-staged-publishing-realworld-scenarios/12umbpublish.png)

6. <span data-ttu-id="1e493-246">Po opublikowaniu pomyślnie hello Umbraco lokalnych aplikacji sieci web aplikacji toohello przemieszczania sieci web, przejdź tooyour przemieszczania aplikacji sieci web, a następnie uruchom kilka toorule testy ewentualnych problemów.</span><span class="sxs-lookup"><span data-stu-id="1e493-246">After you successfully publish hello Umbraco local web app toohello staging web app, browse tooyour staging web app, and run a few tests toorule out any issues.</span></span>

#### <a name="set-up-hello-courier2-deployment-module"></a><span data-ttu-id="1e493-247">Konfigurowanie modułu wdrażania Courier2 hello</span><span class="sxs-lookup"><span data-stu-id="1e493-247">Set up hello Courier2 deployment module</span></span>
<span data-ttu-id="1e493-248">Z hello [Courier2](http://umbraco.com/products/more-add-ons/courier-2) moduł, możesz można po prostu kliknij prawym przyciskiem myszy toopush zawartość, arkusze stylów i modułów programowanie z tymczasową aplikację sieci web aplikacji tooa produkcji sieci web.</span><span class="sxs-lookup"><span data-stu-id="1e493-248">With hello [Courier2](http://umbraco.com/products/more-add-ons/courier-2) module, you can simply right-click toopush content, style sheets, and development modules from a staging web app tooa production web app.</span></span> <span data-ttu-id="1e493-249">Ten proces zmniejsza ryzyko hello przerwanie aplikacji sieci web w środowisku produkcyjnym, podczas wdrażania aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="1e493-249">This process reduces hello risk of breaking your production web app when you deploy an update.</span></span>
<span data-ttu-id="1e493-250">Zakupu licencję dla Courier2 na powitania `*.azurewebsites.net` domeny i domeny niestandardowej (Powiedz http://abc.com).</span><span class="sxs-lookup"><span data-stu-id="1e493-250">Purchase a license for Courier2 for hello `*.azurewebsites.net` domain and your custom domain (say http://abc.com).</span></span> <span data-ttu-id="1e493-251">Po zakupie licencji hello hello miejscu pobrane licencji (. Plik — Umowa Licencyjna) w hello `bin` folderu.</span><span class="sxs-lookup"><span data-stu-id="1e493-251">After you purchase hello license, place hello downloaded license (.LIC file) in hello `bin` folder.</span></span>

![Upuść plik licencji w obszarze bin folder](./media/app-service-web-staged-publishing-realworld-scenarios/13droplic.png)

1. <span data-ttu-id="1e493-253">[Pobierz pakiet hello Courier2](https://our.umbraco.org/projects/umbraco-pro/umbraco-courier-2/).</span><span class="sxs-lookup"><span data-stu-id="1e493-253">[Download hello Courier2 package](https://our.umbraco.org/projects/umbraco-pro/umbraco-courier-2/).</span></span> <span data-ttu-id="1e493-254">Hello kliknij przycisk Zaloguj w aplikacji sieci web etap tooyour, powiedz http://umbracocms-site-stage.azurewebsites.net/umbraco **Developer** menu, a następnie kliknij przycisk **pakiety** > **instalacji Pakiet lokalny**.</span><span class="sxs-lookup"><span data-stu-id="1e493-254">Sign in tooyour stage web app, say http://umbracocms-site-stage.azurewebsites.net/umbraco, click hello **Developer** menu, and then click **Packages** > **Install local package**.</span></span>

    ![Instalator pakietu Umbraco](./media/app-service-web-staged-publishing-realworld-scenarios/14umbpkg.png)

2. <span data-ttu-id="1e493-256">Przekaż pakiet hello Courier2 przy użyciu Instalatora hello.</span><span class="sxs-lookup"><span data-stu-id="1e493-256">Upload hello Courier2 package by using hello installer.</span></span>

    ![Przekaż pakiet courier modułu](./media/app-service-web-staged-publishing-realworld-scenarios/15umbloadpkg.png)

3. <span data-ttu-id="1e493-258">tooconfigure hello pakietu, należy tooupdate hello courier.config plik pod hello **Config** folderu aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="1e493-258">tooconfigure hello package, you need tooupdate hello courier.config file under hello **Config** folder of your web app.</span></span>

    ```xml
    <!-- Repository connection settings -->
     <!-- For each site, a custom repository must be configured, so Courier knows how tooconnect and authenticate-->
     <repositories>
        <!-- If a custom Umbraco Membership provider is used, specify login & password + set hello passwordEncoding tooclear: -->
        <repository name="production web app" alias="stage" type="CourierWebserviceRepositoryProvider" visible="true">
          <url>http://umbracositecms-1.azurewebsites.net</url>
          <user>0</user>
          <!--<login>user@email.com</login> -->
          <!-- <password>user_password</password>-->
          <!-- <passwordEncoding>Clear</passwordEncoding>-->
          </repository>
     </repositories>
     ```

4. <span data-ttu-id="1e493-259">W obszarze `<repositories>`, wprowadź hello produkcji lokacji adres URL i informacji o użytkownikach.</span><span class="sxs-lookup"><span data-stu-id="1e493-259">Under `<repositories>`, enter hello production site URL and user information.</span></span>
    <span data-ttu-id="1e493-260">Jeśli używasz hello domyślnego dostawcę członkostwa Umbraco, Dodaj hello identyfikator użytkownika administracji hello w hello &lt;użytkownika&gt; sekcji.</span><span class="sxs-lookup"><span data-stu-id="1e493-260">If you are using hello default Umbraco membership provider, then add hello ID for hello Administration user in hello &lt;user&gt; section.</span></span>
    <span data-ttu-id="1e493-261">Jeśli używasz niestandardowego dostawcy członkostwa Umbraco, użyj `<login>`,`<password>` w lokacji hello Courier2 modułu tooconnect toohello produkcyjnej.</span><span class="sxs-lookup"><span data-stu-id="1e493-261">If you are using a custom Umbraco membership provider, use `<login>`,`<password>` in hello Courier2 module tooconnect toohello production site.</span></span>
    <span data-ttu-id="1e493-262">Aby uzyskać więcej informacji [hello dokumentacji modułu hello Courier2](http://umbraco.com/help-and-support/customer-area/courier-2-support-and-download/developer-documentation).</span><span class="sxs-lookup"><span data-stu-id="1e493-262">For more details, [review hello documentation for hello Courier2 module](http://umbraco.com/help-and-support/customer-area/courier-2-support-and-download/developer-documentation).</span></span>

5. <span data-ttu-id="1e493-263">Podobnie zainstalować moduł Courier2 hello w swojej witrynie produkcji, a następnie ją skonfigurować aplikację sieci web etap toohello toopoint w jego pliku odpowiednich courier.config, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="1e493-263">Similarly, install hello Courier2 module on your production site, and configure it toopoint toohello stage web app in its respective courier.config file as shown here.</span></span>

    ```xml
     <!-- Repository connection settings -->
     <!-- For each site, a custom repository must be configured, so Courier knows how tooconnect and authenticate-->
     <repositories>
        <!-- If a custom Umbraco Membership provider is used, specify login & password + set hello passwordEncoding tooclear: -->
        <repository name="Stage web app" alias="stage" type="CourierWebserviceRepositoryProvider" visible="true">
          <url>http://umbracositecms-1-stage.azurewebsites.net</url>
          <user>0</user>
          </repository>
     </repositories>
    ```

6. <span data-ttu-id="1e493-264">Kliknij przycisk hello **Courier2** w hello pulpitu nawigacyjnego aplikacji sieci web Umbraco CMS, a następnie kliknij **lokalizacje**.</span><span class="sxs-lookup"><span data-stu-id="1e493-264">Click hello **Courier2** tab in hello Umbraco CMS web app dashboard, and then click **Locations**.</span></span> <span data-ttu-id="1e493-265">Jak wspomniano w powinna zostać wyświetlona nazwa repozytorium hello `courier.config`.</span><span class="sxs-lookup"><span data-stu-id="1e493-265">You should see hello repository name as mentioned in `courier.config`.</span></span> <span data-ttu-id="1e493-266">Czy ten proces w środowisku produkcyjnym i tymczasowej aplikacjami sieci web.</span><span class="sxs-lookup"><span data-stu-id="1e493-266">Do this process on both your production and staging web apps.</span></span>

    ![Repozytorium aplikacji sieci web docelowego widoku](./media/app-service-web-staged-publishing-realworld-scenarios/16courierloc.png)

7. <span data-ttu-id="1e493-268">zawartość toodeploy z hello przemieszczania lokacji toohello produkcji, przejdź zbyt**zawartości**i wybierz istniejącą stronę lub Utwórz nową stronę.</span><span class="sxs-lookup"><span data-stu-id="1e493-268">toodeploy content from hello staging site toohello production site, go too**Content**, and select an existing page or create a new page.</span></span> <span data-ttu-id="1e493-269">Wybiorę istniejącej strony z mojej aplikacji sieci web, gdzie jest hello tytuł strony hello **wprowadzenie — nowy**, a następnie kliknij przycisk **Zapisz i opublikuj**.</span><span class="sxs-lookup"><span data-stu-id="1e493-269">I will select an existing page from my web app where hello title of hello page is **Getting Started – new**, and then click **Save and Publish**.</span></span>

    ![Zmień tytuł strony i publikowanie](./media/app-service-web-staged-publishing-realworld-scenarios/17changepg.png)

8. <span data-ttu-id="1e493-271">Kliknij prawym przyciskiem myszy hello zmodyfikować tooview strony wszystkie opcje hello.</span><span class="sxs-lookup"><span data-stu-id="1e493-271">Right-click hello modified page tooview all hello options.</span></span> <span data-ttu-id="1e493-272">Kliknij przycisk **Courier** tooopen hello **wdrożenia** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="1e493-272">Click **Courier** tooopen hello **Deployment** dialog box.</span></span> <span data-ttu-id="1e493-273">Kliknij przycisk **Wdróż** tooinitiate wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="1e493-273">Click **Deploy** tooinitiate deployment.</span></span>

    ![Okno dialogowe wdrożenia modułu Courier](./media/app-service-web-staged-publishing-realworld-scenarios/18dialog1.png)

9. <span data-ttu-id="1e493-275">Przejrzyj zmiany hello, a następnie kliknij przycisk **Kontynuuj**.</span><span class="sxs-lookup"><span data-stu-id="1e493-275">Review hello changes, and then click **Continue**.</span></span>

    ![Courier modułu wdrażania okna dialogowego przejrzyj zmiany](./media/app-service-web-staged-publishing-realworld-scenarios/19dialog2.png)

    <span data-ttu-id="1e493-277">dziennika wdrażania Hello pokazuje, jeśli wdrożenie hello powiodło się.</span><span class="sxs-lookup"><span data-stu-id="1e493-277">hello deployment log shows if hello deployment was successful.</span></span>

     ![Wyświetl dzienniki wdrożenia z modułu Courier](./media/app-service-web-staged-publishing-realworld-scenarios/20successdlg.png)

10. <span data-ttu-id="1e493-279">Przeglądaj toosee aplikacji sieci web z produkcji, jeśli hello zmiany są uwzględniane.</span><span class="sxs-lookup"><span data-stu-id="1e493-279">Browse your production web app toosee if hello changes are reflected.</span></span>

     ![Przeglądanie aplikacji sieci web w środowisku produkcyjnym](./media/app-service-web-staged-publishing-realworld-scenarios/21umbpg.png)

<span data-ttu-id="1e493-281">więcej informacji na temat sposobu toouse Courier, przejrzyj hello dokumentacji toolearn.</span><span class="sxs-lookup"><span data-stu-id="1e493-281">toolearn more about how toouse Courier, review hello documentation.</span></span>

#### <a name="how-tooupgrade-hello-umbraco-cms-version"></a><span data-ttu-id="1e493-282">Jak tooupgrade hello Umbraco CMS w wersji</span><span class="sxs-lookup"><span data-stu-id="1e493-282">How tooupgrade hello Umbraco CMS version</span></span>
<span data-ttu-id="1e493-283">Zostanie Courier nie pomocy uaktualnienia z jednej wersji tooanother Umbraco CMS.</span><span class="sxs-lookup"><span data-stu-id="1e493-283">Courier will not help you upgrade from one version of Umbraco CMS tooanother.</span></span> <span data-ttu-id="1e493-284">Po uaktualnieniu z wersji Umbraco CMS należy sprawdź, czy niezgodności z niestandardowych modułów lub modułów z partnerami i hello Umbraco podstawowe biblioteki.</span><span class="sxs-lookup"><span data-stu-id="1e493-284">When you upgrade an Umbraco CMS version, you must check for incompatibilities with your custom modules or modules from partners and hello Umbraco Core libraries.</span></span> <span data-ttu-id="1e493-285">Poniżej przedstawiono najlepsze rozwiązania:</span><span class="sxs-lookup"><span data-stu-id="1e493-285">Here are best practices:</span></span>

* <span data-ttu-id="1e493-286">Zawsze tworzyć kopie zapasowe aplikacji sieci web i bazy danych przed uaktualnieniem.</span><span class="sxs-lookup"><span data-stu-id="1e493-286">Always back up your web app and database before you upgrade.</span></span> <span data-ttu-id="1e493-287">Aplikacji sieci web na platformie Azure można skonfigurować automatycznego tworzenia kopii zapasowych dla witryny sieci Web za pomocą funkcji Kopia zapasowa hello i przywrócić witryny, w razie potrzeby, używając funkcji przywracania hello.</span><span class="sxs-lookup"><span data-stu-id="1e493-287">On web apps in Azure, you can set up automatic backups for your websites by using hello backup feature and restore your site if needed by using hello restore feature.</span></span> <span data-ttu-id="1e493-288">Aby uzyskać więcej informacji, zobacz [jak tooback zapasowej swojej aplikacji sieci web](web-sites-backup.md) i [jak toorestore aplikacji sieci web](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="1e493-288">For more details, see [How tooback up your web app](web-sites-backup.md) and [How toorestore your web app](web-sites-restore.md).</span></span>
* <span data-ttu-id="1e493-289">Sprawdź, czy pakiety partnerów są zgodne z wersją hello, które w przypadku uaktualniania.</span><span class="sxs-lookup"><span data-stu-id="1e493-289">Check if packages from partners are compatible with hello version you're upgrading to.</span></span> <span data-ttu-id="1e493-290">Przejrzyj hello projektu zgodności z wersją Umbraco CMS, pakietów hello strony pobierania.</span><span class="sxs-lookup"><span data-stu-id="1e493-290">On hello package's download page, review hello project compatibility with Umbraco CMS version.</span></span>

<span data-ttu-id="1e493-291">Aby uzyskać więcej informacji o tym, jak tooupgrade aplikację sieci web lokalnie, [Zobacz hello ogólne wskazówki uaktualnienia](https://our.umbraco.org/documentation/getting-started/setup/upgrading/general).</span><span class="sxs-lookup"><span data-stu-id="1e493-291">For more details about how tooupgrade your web app locally, [see hello general upgrade guidance](https://our.umbraco.org/documentation/getting-started/setup/upgrading/general).</span></span>

<span data-ttu-id="1e493-292">Po uaktualnieniu witrynie lokalnej publikowania toohello zmiany hello przemieszczania aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="1e493-292">After your local development site is upgraded, publish hello changes toohello staging web app.</span></span> <span data-ttu-id="1e493-293">Testowanie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1e493-293">Test your application.</span></span> <span data-ttu-id="1e493-294">Jeśli wszystko wygląda dobrze, użyj hello **wymiany** przycisk tooswap przemieszczania lokacji toohello produkcji aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="1e493-294">If all looks good, use hello **Swap** button tooswap your staging site toohello production web app.</span></span> <span data-ttu-id="1e493-295">Jeśli używasz hello **wymiany** operacji, można wyświetlić hello zmiany, które zostaną zmodyfikowane w konfiguracji aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="1e493-295">When you use hello **Swap** operation, you can view hello changes that will be affected in your web app's configuration.</span></span> <span data-ttu-id="1e493-296">To **wymiany** operacji zamienia hello aplikacji sieci web i baz danych.</span><span class="sxs-lookup"><span data-stu-id="1e493-296">This **Swap** operation swaps hello web apps and databases.</span></span> <span data-ttu-id="1e493-297">Po hello **wymiany**hello produkcyjnej sieci web aplikacji będzie toohello punktu umbraco — etap db z bazy danych i hello tymczasowej bazie tooumbraco punkt-produkcyjną db zostanie aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="1e493-297">After hello **Swap**, hello production web app will point toohello umbraco-stage-db database, and hello staging web app will point tooumbraco-prod-db database.</span></span>

![Do wdrażania Umbraco CMS w wersji zapoznawczej wymiany](./media/app-service-web-staged-publishing-realworld-scenarios/22umbswap.png)

<span data-ttu-id="1e493-299">Poniżej przedstawiono zalety wymiany zarówno hello aplikacji sieci web i bazy danych hello:</span><span class="sxs-lookup"><span data-stu-id="1e493-299">Here are advantages of swapping both hello web app and hello database:</span></span>

* <span data-ttu-id="1e493-300">Możesz je wycofać toohello poprzedniej wersji aplikacji sieci web z inną **wymiany** Jeśli występują problemy z aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1e493-300">You can roll back toohello previous version of your web app with another **Swap** if there are any application issues.</span></span>
* <span data-ttu-id="1e493-301">W przypadku uaktualnienia należy toodeploy plików i baz danych z hello przemieszczania aplikacji sieci web produkcyjnej toohello aplikacji sieci web i bazy danych.</span><span class="sxs-lookup"><span data-stu-id="1e493-301">For an upgrade, you need toodeploy files and databases from hello staging web app toohello production web app and database.</span></span> <span data-ttu-id="1e493-302">Wiele można wystąpienia problemów podczas wdrażania plików i baz danych.</span><span class="sxs-lookup"><span data-stu-id="1e493-302">Many things can go wrong when you deploy files and databases.</span></span> <span data-ttu-id="1e493-303">Za pomocą hello **wymiany** funkcji gniazd, firma Microsoft może skrócić czas przestojów podczas uaktualniania i zmniejszyć hello ryzyko błędów, które mogą wystąpić podczas wdrażania zmian.</span><span class="sxs-lookup"><span data-stu-id="1e493-303">By using hello **Swap** feature of slots, we can reduce downtime during an upgrade and reduce hello risk of failures that can occur when you deploy changes.</span></span>
* <span data-ttu-id="1e493-304">Możesz zrobić **A / B, testowanie** przy użyciu hello [testowanie w produkcji](https://azure.microsoft.com/documentation/videos/introduction-to-azure-websites-testing-in-production-with-galin-iliev/) funkcji.</span><span class="sxs-lookup"><span data-stu-id="1e493-304">You can do **A/B testing** by using hello [Testing in production](https://azure.microsoft.com/documentation/videos/introduction-to-azure-websites-testing-in-production-with-galin-iliev/) feature.</span></span>

<span data-ttu-id="1e493-305">Ten przedstawia przykład hello elastyczność platformy hello, których można tworzyć niestandardowe moduły podobne tooUmbraco Courier modułu toomanage wdrożenia w środowiskach.</span><span class="sxs-lookup"><span data-stu-id="1e493-305">This example shows you hello flexibility of hello platform where you can build custom modules similar tooUmbraco Courier module toomanage deployment across environments.</span></span>

## <a name="references"></a><span data-ttu-id="1e493-306">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="1e493-306">References</span></span>
[<span data-ttu-id="1e493-307">Programowanie zwinne oprogramowania z usługi aplikacji Azure</span><span class="sxs-lookup"><span data-stu-id="1e493-307">Agile software development with Azure App Service</span></span>](app-service-agile-software-development.md)

[<span data-ttu-id="1e493-308">Konfigurowanie środowisk dla aplikacji sieci web w usłudze Azure App Service przejściowych</span><span class="sxs-lookup"><span data-stu-id="1e493-308">Set up staging environments for web apps in Azure App Service</span></span>](web-sites-staged-publishing.md)

[<span data-ttu-id="1e493-309">Jak tooblock web uzyskują dostęp do miejsc wdrożenia produkcyjnego toonon</span><span class="sxs-lookup"><span data-stu-id="1e493-309">How tooblock web access toonon-production deployment slots</span></span>](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
