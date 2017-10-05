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
# <a name="use-devops-environments-effectively-for-your-web-apps"></a>Wykorzystywać środowisk opracowywania oprogramowania dla aplikacji sieci web
W tym artykule przedstawiono sposób konfigurowania i zarządzania nią wdrożenia aplikacji sieci web, gdy wiele wersji aplikacji znajdują się w różnych środowiskach, takich jak projektowanie, przemieszczania jakości (QA) i produkcji. Każda wersja aplikacji mogą być uważane Środowisko deweloperskie do określonego celu procesu wdrażania. Na przykład deweloperzy mogą używać środowiska pytań i odpowiedzi, aby przetestować jakość aplikacji przed ich Wypchnij zmiany do środowiska produkcyjnego.
Wiele środowisk deweloperskich może być wyzwaniem, ponieważ należy do śledzenia kodu, zarządzanie zasobami (obliczeniowych, aplikacji sieci web, bazy danych, pamięci podręcznej, itp.) i wdrożyć kod w środowiskach.

## <a name="set-up-a-non-production-environment-stage-dev-qa"></a>Konfigurowanie środowiska nieprodukcyjnych (etap, deweloperów, pytań i odpowiedzi)
Po skonfigurowaniu i uruchomieniu aplikacji sieci web produkcyjnej następnym krokiem jest utworzenie środowiskach nieprodukcyjnych. Aby korzystać z miejsc wdrożenia, upewnij się, że działają w trybie planu Standard lub Premium usługi Azure App Service. Miejsca wdrożenia są aplikacje sieci web, które mają własne nazwy hosta. Elementy zawartości i konfiguracji aplikacji sieci Web może być zamieniona między dwóch miejsc wdrożenia, w tym miejsca produkcji. Podczas wdrażania aplikacji w miejscu wdrożenia można uzyskać następujące korzyści:

- Można sprawdzić poprawność zmiany w aplikacji sieci web w tymczasowej miejsce wdrożenia przed wymiany aplikacji z miejscem produkcyjnym.
- Podczas wdrażania aplikacji sieci web na gnieździe najpierw i zamienić go w środowisku produkcyjnym, wszystkie wystąpienia gniazda są przygotowaniu miejsca przed wymieniane w środowisku produkcyjnym. Ten proces eliminuje przestoju podczas wdrażania aplikacji sieci web. Przekierowywanie ruchu jest łatwego i żadne żądania są usuwane z powodu operacji wymiany. Aby zautomatyzować ten całego przepływu pracy, należy skonfigurować [automatycznej wymiany](web-sites-staged-publishing.md#configure-auto-swap) podczas weryfikacji przed wymiany nie jest wymagana.
- Po wymiany miejsca, który ma teraz aplikacji sieci web wcześniej przygotowanych ma poprzedniej aplikacji sieci web produkcyjnej. W przypadku zmiany miejscami do miejsca produkcji są niezgodne z oczekiwaniami, można przeprowadzić wymiany tego samego natychmiast pobrać sieci web "Ostatnia znana dobra konfiguracja" aplikacji z powrotem.

Aby skonfigurować przemieszczania miejsce wdrożenia, zobacz [Konfigurowanie środowiska dla aplikacji sieci web w usłudze Azure App Service przejściowe](web-sites-staged-publishing.md). Każde środowisko powinna zawierać własny zestaw zasobów. Na przykład jeśli aplikacja sieci web korzysta z bazy danych, następnie zarówno produkcyjne i przejściowe aplikacji sieci web należy używać różnych baz danych. Dodaj przemieszczania programowanie środowiska zasoby, takie jak bazy danych, magazynu lub pamięci podręcznej, aby ustawić przejściowego środowiska deweloperskiego.

## <a name="examples-of-using-multiple-development-environments"></a>Przykłady użycia wielu środowisk deweloperskich
Żadnego projektu należy stosować zarządzania kodem źródłowym z co najmniej dwóch środowisk: Programowanie i produkcji. Korzystając z systemów zarządzania zawartością (CMSs), platformy aplikacji, itp., aplikacja może nie obsługiwać ten scenariusz bez dostosowania. Tej możliwości ma wartość true dla kilku popularnych platformach, które opisano w poniższych sekcjach. Wiele pytań wyniknąć podczas pracy z CMS/platform, takich jak:

- Jak możesz rozbicie zawartość w różnych środowiskach?
- Jakie pliki można zmienić bez wpływu na aktualizacje wersji framework?
- Sposób zarządzania konfiguracjami na środowisko
- Jak zarządzać wersji aktualizacji dla modułów, dodatki plug-in i core framework?

Istnieje wiele sposobów, aby skonfigurować wiele środowisk dla projektu. W poniższych przykładach pokazano jedną metodę dla każdej odpowiedniej aplikacji.

### <a name="wordpress"></a>WordPress
W tej sekcji dowiesz się, jak skonfigurować przepływ pracy wdrażania przy użyciu miejsc WordPress. WordPress, na przykład większość rozwiązań CMS, nie obsługuje wiele środowisk deweloperskich bez dostosowania. Funkcja Web Apps w usłudze Azure App Service ma kilka funkcji, które ułatwiają do przechowywania ustawień konfiguracji poza swój kod.

1. Przed utworzeniem miejsca przemieszczania, należy skonfigurować kod aplikacji do obsługi wielu środowisk. Aby obsługiwać wiele środowisk w WordPress, należy edytować `wp-config.php` na komputerze lokalnym sieci web app i Dodaj następujący kod na początku pliku. Ten proces spowoduje włączenie aplikacji do pobrania prawidłowej konfiguracji na podstawie wybranego środowiska.

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

2. Utwórz folder w katalogu głównym aplikacji sieci web o nazwie `config`i Dodaj `wp-config.azure.php` i `wp-config.local.php` pliki, które zawierają odpowiednio Twojego środowiska platformy Azure i lokalnego środowiska.

3. Skopiuj następujące w `wp-config.local.php`:

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

    To ustawienie zabezpieczeń kluczy zgodnie z opisami w poprzednich kod może pomóc zapobiec trwa zaatakowane aplikacji sieci web, użyj unikatowe wartości. Jeśli chcesz wygenerować ciąg dla wymienionych kluczy zabezpieczeń w kodzie można [przejdź do automatycznego generatora](https://api.wordpress.org/secret-key/1.1/salt) można utworzyć nowej pary klucz wartość.

4. Skopiuj następujący kod w `wp-config.azure.php`:

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

#### <a name="use-relative-paths"></a>Użycie ścieżek względnych
Ostatnia rzecz do skonfigurowania w aplikacji WordPress jest ścieżek względnych. WordPress przechowują adres URL w bazie danych. Ten magazyn umożliwia przenoszenie zawartości z jednego środowiska do innego trudniejsze. Musisz zaktualizować bazę danych, za każdym razem, gdy przenoszenia danych z lokalnego do etapu lub etap w środowisku produkcyjnym. Aby zmniejszyć ryzyko problemów, które może być spowodowany z wdrażania bazy danych, za każdym razem, gdy wdrażanie z jednego środowiska do innego, należy użyć [względną głównego łączy wtyczki](https://wordpress.org/plugins/root-relative-urls/), które można zainstalować za pomocą pulpitu nawigacyjnego WordPress administratora.

Dodaj następujące wpisy do Twojej `wp-config.php` pliku przed `That's all, stop editing!` komentarza:

```

  define('WP_HOME', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_SITEURL', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_CONTENT_URL', '/wp-content');
    define('DOMAIN_CURRENT_SITE', filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
```

Aktywowanie wtyczki za pomocą `Plugins` menu w pulpitu nawigacyjnego WordPress administratora. Zapisz ustawienia łącze stałe dla aplikacji WordPress.

#### <a name="the-final-wp-configphp-file"></a>Ostatni `wp-config.php` pliku
Nie wpłynie na wszystkie aktualizacje core WordPress z `wp-config.php`, `wp-config.azure.php`, i `wp-config.local.php` plików. Oto ostateczną wersją `wp-config.php` pliku:

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

#### <a name="set-up-a-staging-environment"></a>Konfigurowanie środowiska przemieszczania
1. Jeśli masz już aplikację sieci web WordPress z subskrypcją platformy Azure, zaloguj się do [portalu Azure](http://portal.azure.com), a następnie przejdź do aplikacji sieci web WordPress. Jeśli nie masz aplikacji sieci web WordPress, można utworzyć z poziomu portalu Azure Marketplace. Aby dowiedzieć się więcej, zobacz [tworzenie aplikacji sieci web WordPress w usłudze Azure App Service](web-sites-php-web-site-gallery.md).
Kliknij przycisk **ustawienia** > **miejsc wdrożenia** > **Dodaj** można utworzyć miejsca wdrożenia o nazwie *etapu*. Miejsce wdrożenia jest inna aplikacja sieci web udostępniającej tyle samo zasobów co aplikacji głównej sieci web utworzony wcześniej.

    ![Tworzenie miejsca wdrożenia etapu](./media/app-service-web-staged-publishing-realworld-scenarios/1setupstage.png)

2. Dodaj inny baza danych MySQL, powiedz `wordpress-stage-db`, w danej grupie zasobów `wordpressapp-group`.

    ![Dodaj bazę danych MySQL do grupy zasobów](./media/app-service-web-staged-publishing-realworld-scenarios/2addmysql.png)

3. Zaktualizuj parametry połączenia dla Twojego miejsca wdrożenia etapu wskazywał nową bazę danych, `wordpress-stage-db`. Aplikacja sieci web produkcji `wordpressprodapp`i aplikacji sieci web na potrzeby przemieszczania `wordpressprodapp-stage`, musi wskazywać różnych baz danych.

#### <a name="configure-environment-specific-app-settings"></a>Konfiguruj ustawienia specyficzne dla środowiska aplikacji
Deweloperzy mogą przechowywać pary klucz wartość ciągu na platformie Azure jako część dane konfiguracyjne o nazwie **ustawień aplikacji**, który jest skojarzony z aplikacją sieci web. W czasie wykonywania aplikacje sieci web pobierania tych wartości i automatycznie udostępnić kodu uruchamianego w aplikacji sieci web. Z punktu widzenia zabezpieczeń, który jest korzyści nieuprzywilejowany po stronie, ponieważ poufne informacje, takie jak parametry połączenia bazy danych, które obejmują hasła, nigdy nie wyświetlane jako zwykły tekst w pliku takich jak `wp-config.php`.

Ten proces, który znajduje się w sekcjach, jest przydatne, ponieważ obejmuje ona zarówno pliku zmiany i bazy danych dla aplikacji WordPress:

* Uaktualnienie wersji WordPress
* Dodawanie nowych lub edytowanie lub uaktualnić wtyczek
* Dodawanie nowych lub edytowanie lub uaktualnić motywów

Konfiguruj ustawienia aplikacji dla:

* Informacje o bazie danych
* Włączenie/wyłączenie rejestrowania WordPress
* Ustawienia zabezpieczeń WordPress

![Ustawienia aplikacji dla aplikacji sieci web Wordpress](./media/app-service-web-staged-publishing-realworld-scenarios/3configure.png)

Upewnij się, Dodaj poniższe ustawienia aplikacji dla gniazda sieci produkcyjnych w sieci web aplikacji i etap. Należy pamiętać, że aplikacja sieci web w środowisku produkcyjnym i przemieszczania aplikacji sieci web różnych baz danych.

1. Wyczyść **ustawienie miejsca** pola wyboru dla wszystkich parametrów ustawień, z wyjątkiem WP_ENV. Ten proces będzie wymiany konfiguracji dla aplikacji sieci web, zawartość pliku i bazy danych. Jeśli **ustawienie miejsca** jest zaznaczone, ustawienia aplikacji i połączenia aplikacji sieci web w ciągu konfiguracji będzie *nie* przenieść w środowiskach, w trakcie **wymiany** operacji. Wszelkie zmiany bazy danych, które znajdują się nie będę powodować utraty aplikacji sieci web w środowisku produkcyjnym.

2. Wdrażanie aplikacji sieci web środowisko rozwoju lokalnego do etapu aplikacji sieci web i bazy danych za pomocą programu WebMatrix lub narzędzia wybranych przez użytkownika, takie jak FTP, Git lub PhpMyAdmin.

    ![Okno dialogowe publikowania macierzy sieci Web dla aplikacji sieci web WordPress](./media/app-service-web-staged-publishing-realworld-scenarios/4wmpublish.png)

3. Przeglądanie i testowanie przemieszczania aplikacji sieci web. Biorąc pod uwagę scenariusz, w której ma zostać zaktualizowany motywu aplikacji sieci web w tym miejscu jest przemieszczania aplikacji sieci web.

    ![Przeglądaj przemieszczania aplikacji sieci web przed wymiany gniazd](./media/app-service-web-staged-publishing-realworld-scenarios/5wpstage.png)

4. Jeśli wszystko wygląda dobrze, kliknij przycisk **wymiany** przycisk tymczasową aplikację sieci web w taki sposób, aby przenieść zawartość do środowiska produkcyjnego. W takim przypadku zamienić aplikacji sieci web i bazy danych w środowiskach podczas każdego **wymiany** operacji.

    ![Zamień podgląd zmian dla środowiska WordPress](./media/app-service-web-staged-publishing-realworld-scenarios/6swaps1.png)

    > [!NOTE]
    > Jeśli scenariusz wymaga tylko push plików (Brak aktualizacji bazy danych), następnie sprawdź **ustawienie miejsca** dla wszystkich bazy danych związanych z *ustawień aplikacji* i *ustawienia parametry połączenia z* w **ustawień aplikacji sieci Web** bloku w portalu Azure, zanim spowoduje **wymiany**. W takim przypadku DB_NAME, DB_HOST DB_PASSWORD, DB_USER i domyślnych ustawień połączenia w ciągu powinna nie pojawiają się w podgląd zmian po wykonaniu **wymiany**. W tej chwili po zakończeniu **wymiany** operacji, aplikacji sieci web WordPress będzie mieć tylko pliki aktualizacji.
    >
    >

    Przed to **wymiany**, w tym miejscu jest aplikacja sieci web WordPress produkcji.
    ![Aplikacja sieci web produkcyjnym przed wymiany gniazd](./media/app-service-web-staged-publishing-realworld-scenarios/7bfswap.png)

    Po **wymiany** operacji motywu została zaktualizowana na aplikację sieci web w środowisku produkcyjnym.

    ![Aplikacja sieci web produkcji po wymiany gniazd](./media/app-service-web-staged-publishing-realworld-scenarios/8afswap.png)

5. Gdy potrzebne do przywrócenia, można przejść do produkcji w sieci web **ustawień aplikacji**i kliknij przycisk **wymiany** przycisk, aby zamienić aplikację sieci web i bazy danych z produkcji na miejsce wystawiania. Pamiętaj, że jeśli zmian w bazie danych są dołączone **wymiany** operacji, a następnie wdrożyć do tymczasowej aplikacji sieci web, następnym razem należy wdrożyć zmian w bazie danych do bieżącej bazy danych przemieszczania aplikacji sieci web. Bieżąca baza danych może być poprzedniej produkcyjną bazę danych lub baza danych etapu.

#### <a name="summary"></a>Podsumowanie
Poniżej znajduje się uogólniony procesu dla dowolnej aplikacji, która ma bazy danych:

1. Zainstaluj aplikację w środowisku lokalnym.
2. Zawiera konfiguracje specyficzne dla środowiska (lokalne i Azure Web Apps).
3. Konfigurowanie środowiska przemieszczania i produkcji dla aplikacji sieci Web.
4. Jeśli masz już uruchomione na platformie Azure aplikacji produkcyjnych, synchronizować produkcji zawartość (pliki/kod i bazy danych) do środowiska lokalnego i tymczasowej.
5. Tworzenie aplikacji w środowisku lokalnym.
6. Ustaw aplikację sieci web produkcji konserwacja lub tryb zablokowane, a następnie zsynchronizować bazy danych zawartości z produkcji do środowisk przemieszczania i deweloperów.
7. Wdróż środowisko przejściowe i testowania.
8. Wdróż do środowiska produkcyjnego.
9. Powtórz kroki od 4 do 6.

### <a name="umbraco"></a>Umbraco
W tej sekcji dowiesz się, jak Umbraco CMS używa niestandardowego modułu do wdrożenia w wielu środowiskach DevOps. W poniższym przykładzie przedstawiono różne podejścia do zarządzania wieloma środowisk deweloperskich.

[Umbraco CMS](http://umbraco.com/) jest rozwiązaniem .NET CMS popularnych, która jest używana przez wielu deweloperów. Zapewnia [Courier2](http://umbraco.com/products/more-add-ons/courier-2) modułu wdrażania od projektowania do etapu przemieszczania w środowisku produkcyjnym. Środowisko deweloperskie lokalnej dla aplikacji sieci web Umbraco CMS można łatwo utworzyć za pomocą programu Visual Studio lub programu WebMatrix.

- [Tworzenie aplikacji sieci web Umbraco z programem Visual Studio](https://our.umbraco.org/documentation/Installation/install-umbraco-with-nuget)
- [Tworzenie aplikacji sieci web Umbraco za pomocą programu WebMatrix](http://umbraco.tv/videos/umbraco-v7/implementor/fundamentals/installation/creating-umbraco-site-from-webmatrix-web-gallery/)

Zawsze pamiętaj, aby usunąć `install` folder aplikacji i nigdy nie przekazuj do etapu lub produkcji aplikacji sieci web. W tym samouczku korzysta z programu WebMatrix.

#### <a name="set-up-a-staging-environment"></a>Konfigurowanie środowiska przemieszczania
1. Tworzenie miejsca wdrożenia, jak wspomniano wcześniej, Umbraco CMS aplikacji sieci web, przy założeniu, że masz już aplikację sieci web Umbraco CMS i uruchamiania. Jeśli nie chcesz, możesz utworzyć jedną z witryny Marketplace.
2. Zaktualizuj parametry połączenia dla Twojego miejsca wdrożenia etapu wskaż nowy **umbraco etap db** bazy danych. Produkcji aplikacji sieci web (umbraositecms-1) i przemieszczania aplikacji sieci web (umbracositecms-1-etap) *musi* punktu do różnych baz danych.

    ![Zaktualizuj parametry połączenia dla aplikacji sieci web za pomocą nowej tymczasowej bazy danych przemieszczania](./media/app-service-web-staged-publishing-realworld-scenarios/9umbconnstr.png)

3. Kliknij przycisk **ustawień publikowania pobrać** dla miejsca wdrożenia **etapu**. Ten proces pobierze plik ustawień publikowania, który przechowuje wszystkie informacje, które Visual Studio lub WebMatrix wymaga, aby opublikować aplikację z lokalnej aplikacji sieci web do aplikacji sieci web platformy Azure.

    ![Ustawienie aplikacji sieci web przemieszczania publikowania Get](./media/app-service-web-staged-publishing-realworld-scenarios/10getpsetting.png)
4. Otwórz aplikację sieci web lokalne działania projektowe w programie WebMatrix lub Visual Studio. W tym samouczku korzysta z programu WebMatrix. Najpierw należy zaimportować plik ustawień publikowania dla aplikacji sieci web tymczasowej.

    ![Importowanie ustawień publikowania dla Umbraco przy użyciu macierzy sieci Web](./media/app-service-web-staged-publishing-realworld-scenarios/11import.png)

5. Przegląd zmian dokonanych w oknie dialogowym i wdrażanie aplikacji sieci web lokalnego do aplikacji sieci web platformy Azure, *umbracositecms-1-etap*. Podczas wdrażania plików bezpośrednio do aplikacji sieci web przemieszczania, zostaną pominięte pliki w `~/app_data/TEMP/` folderu, ponieważ te pliki zostaną ponownie wygenerowane przy pierwszym etapie aplikacji sieci web uruchomiona. Należy również pominąć `~/app_data/umbraco.config` pliku, który również zostanie ponownie wygenerowany.

    ![Przejrzyj zmiany publikowania w sieci web macierzy.](./media/app-service-web-staged-publishing-realworld-scenarios/12umbpublish.png)

6. Po opublikowaniu pomyślnie aplikacji sieci web w lokalnej Umbraco przemieszczania aplikacji sieci web, przejdź do aplikacji sieci web przemieszczania, a następnie uruchom kilka testów w celu wykluczenia problemów.

#### <a name="set-up-the-courier2-deployment-module"></a>Konfigurowanie modułu wdrażania Courier2
Z [Courier2](http://umbraco.com/products/more-add-ons/courier-2) modułu, można po prostu prawym przyciskiem myszy do wypychania zawartości, arkusze stylów i moduły programowanie z przemieszczania aplikacji sieci web w aplikacji sieci web w środowisku produkcyjnym. Ten proces zmniejsza ryzyko przerwanie aplikacji sieci web w środowisku produkcyjnym, podczas wdrażania aktualizacji.
Zakupu licencję na Courier2 dla `*.azurewebsites.net` domeny i domeny niestandardowej (Powiedz http://abc.com). Po zakupie licencji, umieść pobranej licencji (. Plik — Umowa Licencyjna) w `bin` folderu.

![Upuść plik licencji w obszarze bin folder](./media/app-service-web-staged-publishing-realworld-scenarios/13droplic.png)

1. [Pobierz pakiet Courier2](https://our.umbraco.org/projects/umbraco-pro/umbraco-courier-2/). Kliknij przycisk Zaloguj się na etapie aplikacji sieci web, powiedz http://umbracocms-site-stage.azurewebsites.net/umbraco **Developer** menu, a następnie kliknij przycisk **pakiety** > **zainstaluj pakiet lokalny**.

    ![Instalator pakietu Umbraco](./media/app-service-web-staged-publishing-realworld-scenarios/14umbpkg.png)

2. Przekaż pakiet Courier2 za pomocą Instalatora.

    ![Przekaż pakiet courier modułu](./media/app-service-web-staged-publishing-realworld-scenarios/15umbloadpkg.png)

3. Aby skonfigurować pakiet, należy zaktualizować plik courier.config pod **Config** folderu aplikacji sieci web.

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

4. W obszarze `<repositories>`, wprowadź produkcyjnym adres URL i użytkownika informacje o lokacji.
    Jeśli korzystasz z domyślnego dostawcę członkostwa Umbraco, Dodaj identyfikator użytkownika administracji w &lt;użytkownika&gt; sekcji.
    Jeśli używasz niestandardowego dostawcy członkostwa Umbraco, użyj `<login>`,`<password>` w module Courier2 nawiązać do miejsca produkcji.
    Aby uzyskać więcej informacji [zapoznaj się z dokumentacją modułu Courier2](http://umbraco.com/help-and-support/customer-area/courier-2-support-and-download/developer-documentation).

5. Podobnie zainstalować moduł Courier2 w swojej witrynie produkcji i skonfigurować go, aby wskazywała aplikację sieci web etap w jego pliku odpowiednich courier.config, jak pokazano poniżej.

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

6. Kliknij przycisk **Courier2** na pulpicie nawigacyjnym aplikacji sieci web Umbraco CMS, a następnie kliknij **lokalizacje**. Jak wspomniano w powinna zostać wyświetlona nazwa repozytorium `courier.config`. Czy ten proces w środowisku produkcyjnym i tymczasowej aplikacjami sieci web.

    ![Repozytorium aplikacji sieci web docelowego widoku](./media/app-service-web-staged-publishing-realworld-scenarios/16courierloc.png)

7. Aby wdrożyć zawartość z witryny przemieszczania do miejsca produkcji, przejdź do **zawartości**i wybierz istniejącą stronę lub Utwórz nową stronę. Wybiorę istniejącej strony z mojej aplikacji sieci web, gdzie jest tytuł strony **wprowadzenie — nowy**, a następnie kliknij przycisk **Zapisz i opublikuj**.

    ![Zmień tytuł strony i publikowanie](./media/app-service-web-staged-publishing-realworld-scenarios/17changepg.png)

8. Kliknij prawym przyciskiem myszy zmodyfikowane strony, aby wyświetlić wszystkie opcje. Kliknij przycisk **Courier** otworzyć **wdrożenia** okno dialogowe. Kliknij przycisk **Wdróż** do inicjowania wdrożenia.

    ![Okno dialogowe wdrożenia modułu Courier](./media/app-service-web-staged-publishing-realworld-scenarios/18dialog1.png)

9. Przejrzyj zmiany, a następnie kliknij przycisk **Kontynuuj**.

    ![Courier modułu wdrażania okna dialogowego przejrzyj zmiany](./media/app-service-web-staged-publishing-realworld-scenarios/19dialog2.png)

    Dziennik wdrażania pokazuje, czy wdrażanie zakończyło się niepowodzeniem.

     ![Wyświetl dzienniki wdrożenia z modułu Courier](./media/app-service-web-staged-publishing-realworld-scenarios/20successdlg.png)

10. Przeglądanie aplikacji sieci web produkcji, jeśli zmiany są uwzględniane.

     ![Przeglądanie aplikacji sieci web w środowisku produkcyjnym](./media/app-service-web-staged-publishing-realworld-scenarios/21umbpg.png)

Aby dowiedzieć się więcej o sposobie używania Courier, zapoznaj się z dokumentacją.

#### <a name="how-to-upgrade-the-umbraco-cms-version"></a>Jak uaktualnić wersję Umbraco CMS
Zostanie Courier nie pomocy uaktualnienia z jednej wersji systemu Umbraco CMS do innego. Po uaktualnieniu z wersji Umbraco CMS, musisz sprawdzić dla niezgodności z niestandardowych modułów lub modułów z partnerami i Umbraco podstawowe biblioteki. Poniżej przedstawiono najlepsze rozwiązania:

* Zawsze tworzyć kopie zapasowe aplikacji sieci web i bazy danych przed uaktualnieniem. Aplikacji sieci web na platformie Azure możesz Konfigurowanie automatycznego tworzenia kopii zapasowych dla witryny sieci Web za pomocą funkcji Kopia zapasowa i przywracanie witryny, w razie potrzeby, używając funkcji przywracania. Aby uzyskać więcej informacji, zobacz [sposób wykonywania kopii zapasowej aplikacji sieci web](web-sites-backup.md) i [Przywracanie aplikacji sieci web](web-sites-restore.md).
* Sprawdź, czy pakiety partnerów są zgodne z wersją, które w przypadku uaktualniania. Przejrzyj zgodność projektu z wersją Umbraco CMS, pakietu strony pobierania.

Aby uzyskać więcej informacji o sposobie uaktualniania aplikacji sieci web lokalnie [Zobacz ogólne wskazówki uaktualnienia](https://our.umbraco.org/documentation/getting-started/setup/upgrading/general).

Po uaktualnieniu witrynie lokalnej opublikować zmiany tymczasową aplikację sieci web. Testowanie aplikacji. Jeśli wszystko wygląda dobrze, użyj **wymiany** przycisk, aby zamienić przemieszczania witryny aplikacji sieci web w środowisku produkcyjnym. Jeśli używasz **wymiany** operacji, można wyświetlić zmiany, które zostaną zmodyfikowane w konfiguracji aplikacji sieci web. To **wymiany** operacji zamienia aplikacji sieci web i baz danych. Po **wymiany**, aplikacji sieci web w środowisku produkcyjnym wskaże umbraco — etap db bazy danych i przemieszczania aplikacji sieci web będzie wskazywać umbraco produkcyjną db bazy danych.

![Do wdrażania Umbraco CMS w wersji zapoznawczej wymiany](./media/app-service-web-staged-publishing-realworld-scenarios/22umbswap.png)

Poniżej przedstawiono zalety wymiany zarówno aplikacji sieci web i bazy danych:

* Możesz przywrócić poprzedniej wersji aplikacji sieci web z inną **wymiany** Jeśli występują problemy z aplikacji.
* W przypadku uaktualnienia należy wdrożyć plików i baz danych z tymczasowej aplikacji sieci web w środowisku produkcyjnym aplikacji sieci web i bazy danych. Wiele można wystąpienia problemów podczas wdrażania plików i baz danych. Za pomocą **wymiany** funkcji gniazd, możemy skrócenie czasu przestoju podczas uaktualniania i zmniejszyć ryzyko błędów, które mogą wystąpić podczas wdrażania zmian.
* Możesz zrobić **A / B, testowanie** za pomocą [testowanie w produkcji](https://azure.microsoft.com/documentation/videos/introduction-to-azure-websites-testing-in-production-with-galin-iliev/) funkcji.

W tym przykładzie przedstawiono elastyczność platformy których można tworzyć niestandardowe moduły podobne do modułu Umbraco Courier, aby zarządzać wdrażaniem środowiskach.

## <a name="references"></a>Dokumentacja
[Programowanie zwinne oprogramowania z usługi aplikacji Azure](app-service-agile-software-development.md)

[Konfigurowanie środowisk dla aplikacji sieci web w usłudze Azure App Service przejściowych](web-sites-staged-publishing.md)

[Jak zablokować dostęp do miejsc wdrożenia nieprodukcyjnych w sieci web](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
