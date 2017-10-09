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
# <a name="use-devops-environments-effectively-for-your-web-apps"></a>Wykorzystywać środowisk opracowywania oprogramowania dla aplikacji sieci web
W tym artykule opisano sposób tooset Konfigurowanie i zarządzanie wdrożenia aplikacji sieci web, gdy wiele wersji aplikacji znajdują się w różnych środowiskach, takich jak projektowanie, przemieszczania jakości (QA) i produkcji. Każdej wersji aplikacji mogą być uważane Środowisko deweloperskie do określonego celu hello procesu wdrażania. Na przykład deweloperzy mogą używać hello jakości hello tootest środowiska w odpowiedzi na pytania aplikacji hello przed ich push hello tooproduction zmiany.
Wiele środowisk deweloperskich można wyzwanie, ponieważ należy tootrack kodu, zarządzanie zasobami (obliczeniowych, aplikacji sieci web, bazy danych, pamięci podręcznej, itp.) i wdrożyć kod w środowiskach.

## <a name="set-up-a-non-production-environment-stage-dev-qa"></a>Konfigurowanie środowiska nieprodukcyjnych (etap, deweloperów, pytań i odpowiedzi)
Po skonfigurowaniu i uruchomieniu aplikacji sieci web produkcyjnej hello następnym krokiem jest toocreate środowiskach nieprodukcyjnych. miejsca wdrożenia toouse, upewnij się, że działają w trybie planu Standard lub Premium usługi Azure App Service hello. Miejsca wdrożenia są aplikacje sieci web, które mają własne nazwy hosta. Elementy zawartości i konfiguracji aplikacji sieci Web może być zamieniona między dwóch miejsc wdrożenia, w tym hello miejsca produkcji. Podczas wdrażania przedział czasu wdrożenia tooa aplikacji można uzyskać hello następujące korzyści:

- Aplikacja sieci web tooa zmian w tymczasowych miejsce wdrożenia można sprawdzić przed wymiany aplikacji hello z miejscem produkcyjnym hello.
- Gdy najpierw wdrożyć miejsca tooa aplikacji sieci web i zamienić go w środowisku produkcyjnym, wszystkie wystąpienia miejsca hello są przygotowaniu miejsca przed wymieniane w środowisku produkcyjnym. Ten proces eliminuje przestoju podczas wdrażania aplikacji sieci web. przekierowywanie ruchu Hello jest łatwego i żadne żądania są usuwane z powodu operacji tooswap. tooautomate całego przepływu pracy, skonfiguruj [automatycznej wymiany](web-sites-staged-publishing.md#configure-auto-swap) podczas weryfikacji przed wymiany nie jest wymagana.
- Po wymiany gniazdo hello, który ma teraz hello wcześniej przygotowanych aplikacji sieci web ma hello poprzedniej aplikacji sieci web produkcyjnej. Jeśli zmiany hello miejscami do miejsca produkcji hello są niezgodne z oczekiwaniami, można wykonać hello sam zamiana natychmiast tooget Twojego "ostatniej znanej dobrej" kopii aplikacji sieci web.

tooset się przemieszczania miejsce wdrożenia, zobacz [Konfigurowanie środowiska dla aplikacji sieci web w usłudze Azure App Service przejściowe](web-sites-staged-publishing.md). Każde środowisko powinna zawierać własny zestaw zasobów. Na przykład jeśli aplikacja sieci web korzysta z bazy danych, następnie zarówno produkcyjne i przejściowe aplikacji sieci web należy używać różnych baz danych. Dodaj przemieszczania zasobów środowisko rozwoju, takich jak bazy danych, magazynu lub tooset pamięci podręcznej środowiska deweloperskiego tymczasowej.

## <a name="examples-of-using-multiple-development-environments"></a>Przykłady użycia wielu środowisk deweloperskich
Żadnego projektu należy stosować zarządzania kodem źródłowym z co najmniej dwóch środowisk: Programowanie i produkcji. Jeśli używasz systemów zarządzania zawartością (CMSs), platformy aplikacji, itp., aplikacji hello mogą nie obsługiwać ten scenariusz bez dostosowania. Tej możliwości ma wartość true dla niektórych hello popularnych środowisk omówionych w hello następujące sekcje. Wiele pytań pochodzą toomind podczas pracy z CMS/platform, takich jak:

- Jak możesz rozbicie hello zawartości w różnych środowiskach?
- Jakie pliki można zmienić bez wpływu na aktualizacje wersji framework?
- Sposób zarządzania konfiguracjami na środowisko
- Jak zarządzać wersji aktualizacji dla modułów, dodatki plug-in i hello core framework?

Istnieje wiele sposobów tooset się wiele środowisk dla projektu. Witaj poniższe przykłady przedstawiają jedną metodę dla każdej odpowiedniej aplikacji.

### <a name="wordpress"></a>WordPress
W tej sekcji dowiesz się, jak gniazd tooset się przepływ pracy wdrażania przy użyciu platformy WordPress. WordPress, na przykład większość rozwiązań CMS, nie obsługuje wiele środowisk deweloperskich bez dostosowania. Funkcja Web Apps Hello Azure App Service ma kilka funkcji, dzięki któremu można łatwo toostore ustawienia konfiguracji poza swój kod.

1. Przed utworzeniem miejsca przemieszczania, skonfiguruj toosupport kod z aplikacji wiele środowisk. toosupport wiele środowisk w WordPress, potrzebujesz tooedit `wp-config.php` na komputerze lokalnym sieci web app i Dodaj hello następującego kodu na początku hello hello pliku. Ten proces umożliwi toopick hello poprawne konfigurację aplikacji na podstawie hello wybranego środowiska.

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

2. Utwórz folder w katalogu głównym aplikacji sieci web o nazwie `config`i Dodaj hello `wp-config.azure.php` i `wp-config.local.php` pliki, które zawierają odpowiednio Twojego środowiska platformy Azure i lokalnego środowiska.

3. Skopiuj następujące hello w `wp-config.local.php`:

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

    Ustawienia kluczy zabezpieczeń hello zgodnie z opisami w poprzednim kodzie hello może pomóc tooprevent aplikacji sieci web z trwa zaatakowane, należy więc unikatowe wartości. Jeśli potrzebujesz ciąg hello toogenerate wymienionych w kodzie hello kluczy zabezpieczeń, możesz [generator automatyczne przejście toohello](https://api.wordpress.org/secret-key/1.1/salt) toocreate nowy klucz/wartość pary.

4. Kopiuj hello poniższy kod w `wp-config.azure.php`:

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

#### <a name="use-relative-paths"></a>Użycie ścieżek względnych
Jeden ostatniego tooconfigure operacją w aplikacji WordPress hello jest ścieżek względnych. WordPress przechowują adres URL w hello bazy danych. Ta pamięć masowa utrudnia przenoszenia zawartości z jednego środowiska tooanother. Należy bazy danych hello tooupdate każdorazowego przenoszenia danych z toostage lokalnej lub środowisk tooproduction etapu. ryzyko hello tooreduce problemów, które może być spowodowany z wdrażania bazy danych, za każdym razem, gdy wdrażanie z jednego środowiska tooanother, użyj hello [względną głównego łączy wtyczki](https://wordpress.org/plugins/root-relative-urls/), które można zainstalować przy użyciu hello WordPress administratora pulpit nawigacyjny.

Dodaj następujące wpisy tooyour hello `wp-config.php` pliku przed hello `That's all, stop editing!` komentarza:

```

  define('WP_HOME', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_SITEURL', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_CONTENT_URL', '/wp-content');
    define('DOMAIN_CURRENT_SITE', filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
```

Aktywowanie wtyczki hello za pośrednictwem hello `Plugins` menu w pulpitu nawigacyjnego WordPress administratora. Zapisz ustawienia łącze stałe dla aplikacji WordPress.

#### <a name="hello-final-wp-configphp-file"></a>Witaj końcowego `wp-config.php` pliku
Nie wpłynie na wszystkie aktualizacje core WordPress z `wp-config.php`, `wp-config.azure.php`, i `wp-config.local.php` plików. Oto ostateczną wersją hello `wp-config.php` pliku:

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

#### <a name="set-up-a-staging-environment"></a>Konfigurowanie środowiska przemieszczania
1. Jeśli masz już aplikację sieci web WordPress z subskrypcją platformy Azure, zaloguj się w toohello [portalu Azure](http://portal.azure.com), a następnie przejdź aplikacji sieci web WordPress tooyour. Jeśli nie masz aplikacji sieci web WordPress, można utworzyć jedną z hello Azure Marketplace. toolearn więcej, zobacz [tworzenie aplikacji sieci web WordPress w usłudze Azure App Service](web-sites-php-web-site-gallery.md).
Kliknij przycisk **ustawienia** > **miejsc wdrożenia** > **Dodaj** toocreate miejsca wdrożenia o nazwie hello *etap*. Miejsce wdrożenia jest inną aplikację sieci web, która udziałów hello tyle samo zasobów co hello aplikacji głównej sieci web, utworzony wcześniej.

    ![Tworzenie miejsca wdrożenia etapu](./media/app-service-web-staged-publishing-realworld-scenarios/1setupstage.png)

2. Dodaj inny baza danych MySQL, powiedz `wordpress-stage-db`, grupy zasobów tooyour `wordpressapp-group`.

    ![Dodaj grupę tooresource bazy danych MySQL](./media/app-service-web-staged-publishing-realworld-scenarios/2addmysql.png)

3. Aktualizowanie parametrów połączenia hello etap wdrażania miejsca toopoint toohello nowej bazy danych, `wordpress-stage-db`. Aplikacja sieci web produkcji `wordpressprodapp`i aplikacji sieci web na potrzeby przemieszczania `wordpressprodapp-stage`, bazy danych punktu toodifferent musi.

#### <a name="configure-environment-specific-app-settings"></a>Konfiguruj ustawienia specyficzne dla środowiska aplikacji
Deweloperzy mogą przechowywać pary klucz wartość ciągu na platformie Azure w ramach hello informacji o konfiguracji, o nazwie **ustawień aplikacji**, który jest skojarzony z aplikacją sieci web. W czasie wykonywania aplikacje sieci web automatycznie pobierania tych wartości i były dostępne toocode, działającej w aplikacji sieci web. Z punktu widzenia zabezpieczeń, który jest korzyści nieuprzywilejowany po stronie, ponieważ poufne informacje, takie jak parametry połączenia bazy danych, które obejmują hasła, nigdy nie wyświetlane jako zwykły tekst w pliku takich jak `wp-config.php`.

Ten proces, który znajduje się w powitania po akapitów, jest przydatne, ponieważ obejmuje ona zarówno pliku zmiany i bazy danych dla aplikacji WordPress hello:

* Uaktualnienie wersji WordPress
* Dodawanie nowych lub edytowanie lub uaktualnić wtyczek
* Dodawanie nowych lub edytowanie lub uaktualnić motywów

Konfiguruj ustawienia aplikacji dla:

* Informacje o bazie danych
* Włączenie/wyłączenie rejestrowania WordPress
* Ustawienia zabezpieczeń WordPress

![Ustawienia aplikacji dla aplikacji sieci web Wordpress](./media/app-service-web-staged-publishing-realworld-scenarios/3configure.png)

Upewnij się, że dodane hello następujące ustawienia aplikacji dla miejsca z produkcji w sieci web app i etap. Należy pamiętać, że aplikacja sieci web produkcji hello i przemieszczania aplikacji sieci web korzystają z różnych baz danych.

1. Wyczyść hello **ustawienie miejsca** pola wyboru dla wszystkich parametrów hello ustawienia, z wyjątkiem WP_ENV. Ten proces będzie wymiany hello konfiguracji dla aplikacji sieci web, zawartość pliku i bazy danych. Jeśli **ustawienie miejsca** jest zaznaczone, ustawienia aplikacji i konfiguracja ciąg połączenia aplikacji sieci web hello będzie *nie* przenieść w środowiskach, w trakcie **wymiany** operacji. Wszelkie zmiany bazy danych, które znajdują się nie będę powodować utraty aplikacji sieci web w środowisku produkcyjnym.

2. Wdróż hello rozwoju lokalnego środowiska sieci web aplikacji toohello etap web app i bazy danych za pomocą programu WebMatrix lub narzędzia wybranych przez użytkownika, takie jak FTP, Git lub PhpMyAdmin.

    ![Okno dialogowe publikowania macierzy sieci Web dla aplikacji sieci web WordPress](./media/app-service-web-staged-publishing-realworld-scenarios/4wmpublish.png)

3. Przeglądanie i testowanie przemieszczania aplikacji sieci web. Biorąc pod uwagę scenariusz, w przypadku toobe zaktualizowane motywu hello hello aplikacji sieci web w tym miejscu jest hello przemieszczania aplikacji sieci web.

    ![Przeglądaj przemieszczania aplikacji sieci web przed wymiany gniazd](./media/app-service-web-staged-publishing-realworld-scenarios/5wpstage.png)

4. Jeśli wszystko wygląda dobrze, kliknij przycisk hello **wymiany** znajdującego się na Twoje przemieszczania toomove aplikacji sieci web środowiska produkcyjnego toohello zawartości. W takim przypadku zamienić hello aplikacji sieci web i bazy danych hello w środowiskach podczas każdego **wymiany** operacji.

    ![Zamień podgląd zmian dla środowiska WordPress](./media/app-service-web-staged-publishing-realworld-scenarios/6swaps1.png)

    > [!NOTE]
    > Jeżeli dany scenariusz wymaga tooonly wypychania plików (Brak aktualizacji bazy danych), sprawdź **ustawienie miejsca** dla wszystkich hello związanych z bazy danych *ustawień aplikacji* i *ustawieniaParametrypołączeniaz*w hello **ustawień aplikacji sieci Web** bloku w portalu Azure, przed wykonaniem hello hello **wymiany**. W takim przypadku DB_NAME, DB_HOST DB_PASSWORD, DB_USER i domyślnych ustawień połączenia w ciągu powinna nie pojawiają się w podgląd zmian po wykonaniu **wymiany**. W tej chwili po zakończeniu hello **wymiany** operacji hello aplikacji sieci web WordPress będzie mieć hello aktualizacji tylko pliki.
    >
    >

    Przed to **wymiany**, Oto aplikacji sieci web WordPress hello w środowisku produkcyjnym.
    ![Aplikacja sieci web produkcyjnym przed wymiany gniazd](./media/app-service-web-staged-publishing-realworld-scenarios/7bfswap.png)

    Po hello **wymiany** operacji motywu hello została zaktualizowana na aplikację sieci web w środowisku produkcyjnym.

    ![Aplikacja sieci web produkcji po wymiany gniazd](./media/app-service-web-staged-publishing-realworld-scenarios/8afswap.png)

5. Jeśli potrzebujesz ponownie tooroll toohello produkcji w sieci web można przejść **ustawień aplikacji**i kliknij przycisk hello **wymiany** przycisk tooswap hello web app i bazy danych z poziomu gniazda produkcyjnego toostaging. Pamiętaj, że jeśli zmian w bazie danych są dołączone **wymiany** operacji, a następnie hello następnym wdrażanie aplikacji sieci web na potrzeby przemieszczania tooyour toodeploy hello zmiany toohello bieżąca baza danych jest wymagane dla tymczasową aplikację sieci web. Hello bieżąca baza danych może być hello poprzedniej produkcyjną bazę danych lub hello etap w bazie danych.

#### <a name="summary"></a>Podsumowanie
Poniżej znajduje się uogólniony procesu dla dowolnej aplikacji, która ma bazy danych:

1. Instalacji aplikacji hello w środowisku lokalnym.
2. Zawiera konfiguracje specyficzne dla środowiska (lokalne i Azure Web Apps).
3. Konfigurowanie środowiska przemieszczania i produkcji dla aplikacji sieci Web.
4. Jeśli masz już uruchomione na platformie Azure aplikacji produkcyjnych, synchronizować produkcji zawartości (pliki/kod i bazy danych) toolocal przemieszczania środowiska i.
5. Tworzenie aplikacji w środowisku lokalnym.
6. Ustaw aplikację sieci web produkcji konserwacja lub tryb zablokowane, a zsynchronizować bazy danych zawartości z toostaging i deweloperów środowisk produkcyjnych.
7. Wdróż toohello przemieszczania środowiska i testowania.
8. Wdróż tooproduction środowiska.
9. Powtórz kroki od 4 do 6.

### <a name="umbraco"></a>Umbraco
W tej sekcji dowiesz się, jak hello Umbraco CMS w wielu środowiskach DevOps używa toodeploy niestandardowego modułu. W poniższym przykładzie przedstawiono toomanaging różne podejścia wiele środowisk deweloperskich.

[Umbraco CMS](http://umbraco.com/) jest rozwiązaniem .NET CMS popularnych, która jest używana przez wielu deweloperów. Zapewnia hello [Courier2](http://umbraco.com/products/more-add-ons/courier-2) toodeploy modułu ze środowisk tooproduction toostaging programowanie. Środowisko deweloperskie lokalnej dla aplikacji sieci web Umbraco CMS można łatwo utworzyć za pomocą programu Visual Studio lub programu WebMatrix.

- [Tworzenie aplikacji sieci web Umbraco z programem Visual Studio](https://our.umbraco.org/documentation/Installation/install-umbraco-with-nuget)
- [Tworzenie aplikacji sieci web Umbraco za pomocą programu WebMatrix](http://umbraco.tv/videos/umbraco-v7/implementor/fundamentals/installation/creating-umbraco-site-from-webmatrix-web-gallery/)

Zawsze pamiętaj tooremove hello `install` folder aplikacji i nigdy nie przesłania go toostage lub produkcyjnych aplikacji sieci web. W tym samouczku korzysta z programu WebMatrix.

#### <a name="set-up-a-staging-environment"></a>Konfigurowanie środowiska przemieszczania
1. Tworzenie miejsca wdrożenia, jak już wspomniano hello Umbraco CMS aplikacji sieci web, przy założeniu, że masz już aplikację sieci web Umbraco CMS i uruchamiania. Jeśli nie chcesz, możesz utworzyć jedną z hello Marketplace.
2. Zaktualizować hello parametry połączenia dla Twojego etap wdrażania miejsca toopoint toohello nowe **umbraco etap db** bazy danych. Produkcji aplikacji sieci web (umbraositecms-1) i przemieszczania aplikacji sieci web (umbracositecms-1-etap) *musi* toodifferent punktu baz danych.

    ![Zaktualizuj parametry połączenia dla aplikacji sieci web za pomocą nowej tymczasowej bazy danych przemieszczania](./media/app-service-web-staged-publishing-realworld-scenarios/9umbconnstr.png)

3. Kliknij przycisk **ustawień publikowania pobrać** dla miejsca wdrożenia hello **etapu**. Ten proces pobierze plik ustawień publikowania, który przechowuje wszystkie informacje hello, że program Visual Studio lub programu WebMatrix wymaga toopublish aplikacji hello lokalnej sieci web aplikacji toohello aplikacji sieci web Azure.

    ![Ustawienie aplikacji sieci web na potrzeby przemieszczania hello publikowania Get](./media/app-service-web-staged-publishing-realworld-scenarios/10getpsetting.png)
4. Otwórz aplikację sieci web lokalne działania projektowe w programie WebMatrix lub Visual Studio. W tym samouczku korzysta z programu WebMatrix. Najpierw należy tooimport hello pliku ustawień aplikacji sieci web przemieszczania publikowania.

    ![Importowanie ustawień publikowania dla Umbraco przy użyciu macierzy sieci Web](./media/app-service-web-staged-publishing-realworld-scenarios/11import.png)

5. Przegląd zmian dokonanych w oknie dialogowym hello i wdrażania aplikacji sieci web platformy Azure tooyour aplikacji lokalnej sieci web, *umbracositecms-1-etap*. Podczas wdrażania plików bezpośrednio z aplikacji sieci web tooyour przemieszczania, zostaną pominięte pliki w hello `~/app_data/TEMP/` folderu, ponieważ te pliki zostaną ponownie wygenerowane po pierwszej aplikacji sieci web etap hello uruchomiona. Należy również pominąć hello `~/app_data/umbraco.config` pliku, który również zostanie ponownie wygenerowany.

    ![Przejrzyj zmiany publikowania w sieci web macierzy.](./media/app-service-web-staged-publishing-realworld-scenarios/12umbpublish.png)

6. Po opublikowaniu pomyślnie hello Umbraco lokalnych aplikacji sieci web aplikacji toohello przemieszczania sieci web, przejdź tooyour przemieszczania aplikacji sieci web, a następnie uruchom kilka toorule testy ewentualnych problemów.

#### <a name="set-up-hello-courier2-deployment-module"></a>Konfigurowanie modułu wdrażania Courier2 hello
Z hello [Courier2](http://umbraco.com/products/more-add-ons/courier-2) moduł, możesz można po prostu kliknij prawym przyciskiem myszy toopush zawartość, arkusze stylów i modułów programowanie z tymczasową aplikację sieci web aplikacji tooa produkcji sieci web. Ten proces zmniejsza ryzyko hello przerwanie aplikacji sieci web w środowisku produkcyjnym, podczas wdrażania aktualizacji.
Zakupu licencję dla Courier2 na powitania `*.azurewebsites.net` domeny i domeny niestandardowej (Powiedz http://abc.com). Po zakupie licencji hello hello miejscu pobrane licencji (. Plik — Umowa Licencyjna) w hello `bin` folderu.

![Upuść plik licencji w obszarze bin folder](./media/app-service-web-staged-publishing-realworld-scenarios/13droplic.png)

1. [Pobierz pakiet hello Courier2](https://our.umbraco.org/projects/umbraco-pro/umbraco-courier-2/). Hello kliknij przycisk Zaloguj w aplikacji sieci web etap tooyour, powiedz http://umbracocms-site-stage.azurewebsites.net/umbraco **Developer** menu, a następnie kliknij przycisk **pakiety** > **instalacji Pakiet lokalny**.

    ![Instalator pakietu Umbraco](./media/app-service-web-staged-publishing-realworld-scenarios/14umbpkg.png)

2. Przekaż pakiet hello Courier2 przy użyciu Instalatora hello.

    ![Przekaż pakiet courier modułu](./media/app-service-web-staged-publishing-realworld-scenarios/15umbloadpkg.png)

3. tooconfigure hello pakietu, należy tooupdate hello courier.config plik pod hello **Config** folderu aplikacji sieci web.

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

4. W obszarze `<repositories>`, wprowadź hello produkcji lokacji adres URL i informacji o użytkownikach.
    Jeśli używasz hello domyślnego dostawcę członkostwa Umbraco, Dodaj hello identyfikator użytkownika administracji hello w hello &lt;użytkownika&gt; sekcji.
    Jeśli używasz niestandardowego dostawcy członkostwa Umbraco, użyj `<login>`,`<password>` w lokacji hello Courier2 modułu tooconnect toohello produkcyjnej.
    Aby uzyskać więcej informacji [hello dokumentacji modułu hello Courier2](http://umbraco.com/help-and-support/customer-area/courier-2-support-and-download/developer-documentation).

5. Podobnie zainstalować moduł Courier2 hello w swojej witrynie produkcji, a następnie ją skonfigurować aplikację sieci web etap toohello toopoint w jego pliku odpowiednich courier.config, jak pokazano poniżej.

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

6. Kliknij przycisk hello **Courier2** w hello pulpitu nawigacyjnego aplikacji sieci web Umbraco CMS, a następnie kliknij **lokalizacje**. Jak wspomniano w powinna zostać wyświetlona nazwa repozytorium hello `courier.config`. Czy ten proces w środowisku produkcyjnym i tymczasowej aplikacjami sieci web.

    ![Repozytorium aplikacji sieci web docelowego widoku](./media/app-service-web-staged-publishing-realworld-scenarios/16courierloc.png)

7. zawartość toodeploy z hello przemieszczania lokacji toohello produkcji, przejdź zbyt**zawartości**i wybierz istniejącą stronę lub Utwórz nową stronę. Wybiorę istniejącej strony z mojej aplikacji sieci web, gdzie jest hello tytuł strony hello **wprowadzenie — nowy**, a następnie kliknij przycisk **Zapisz i opublikuj**.

    ![Zmień tytuł strony i publikowanie](./media/app-service-web-staged-publishing-realworld-scenarios/17changepg.png)

8. Kliknij prawym przyciskiem myszy hello zmodyfikować tooview strony wszystkie opcje hello. Kliknij przycisk **Courier** tooopen hello **wdrożenia** okno dialogowe. Kliknij przycisk **Wdróż** tooinitiate wdrożenia.

    ![Okno dialogowe wdrożenia modułu Courier](./media/app-service-web-staged-publishing-realworld-scenarios/18dialog1.png)

9. Przejrzyj zmiany hello, a następnie kliknij przycisk **Kontynuuj**.

    ![Courier modułu wdrażania okna dialogowego przejrzyj zmiany](./media/app-service-web-staged-publishing-realworld-scenarios/19dialog2.png)

    dziennika wdrażania Hello pokazuje, jeśli wdrożenie hello powiodło się.

     ![Wyświetl dzienniki wdrożenia z modułu Courier](./media/app-service-web-staged-publishing-realworld-scenarios/20successdlg.png)

10. Przeglądaj toosee aplikacji sieci web z produkcji, jeśli hello zmiany są uwzględniane.

     ![Przeglądanie aplikacji sieci web w środowisku produkcyjnym](./media/app-service-web-staged-publishing-realworld-scenarios/21umbpg.png)

więcej informacji na temat sposobu toouse Courier, przejrzyj hello dokumentacji toolearn.

#### <a name="how-tooupgrade-hello-umbraco-cms-version"></a>Jak tooupgrade hello Umbraco CMS w wersji
Zostanie Courier nie pomocy uaktualnienia z jednej wersji tooanother Umbraco CMS. Po uaktualnieniu z wersji Umbraco CMS należy sprawdź, czy niezgodności z niestandardowych modułów lub modułów z partnerami i hello Umbraco podstawowe biblioteki. Poniżej przedstawiono najlepsze rozwiązania:

* Zawsze tworzyć kopie zapasowe aplikacji sieci web i bazy danych przed uaktualnieniem. Aplikacji sieci web na platformie Azure można skonfigurować automatycznego tworzenia kopii zapasowych dla witryny sieci Web za pomocą funkcji Kopia zapasowa hello i przywrócić witryny, w razie potrzeby, używając funkcji przywracania hello. Aby uzyskać więcej informacji, zobacz [jak tooback zapasowej swojej aplikacji sieci web](web-sites-backup.md) i [jak toorestore aplikacji sieci web](web-sites-restore.md).
* Sprawdź, czy pakiety partnerów są zgodne z wersją hello, które w przypadku uaktualniania. Przejrzyj hello projektu zgodności z wersją Umbraco CMS, pakietów hello strony pobierania.

Aby uzyskać więcej informacji o tym, jak tooupgrade aplikację sieci web lokalnie, [Zobacz hello ogólne wskazówki uaktualnienia](https://our.umbraco.org/documentation/getting-started/setup/upgrading/general).

Po uaktualnieniu witrynie lokalnej publikowania toohello zmiany hello przemieszczania aplikacji sieci web. Testowanie aplikacji. Jeśli wszystko wygląda dobrze, użyj hello **wymiany** przycisk tooswap przemieszczania lokacji toohello produkcji aplikacji sieci web. Jeśli używasz hello **wymiany** operacji, można wyświetlić hello zmiany, które zostaną zmodyfikowane w konfiguracji aplikacji sieci web. To **wymiany** operacji zamienia hello aplikacji sieci web i baz danych. Po hello **wymiany**hello produkcyjnej sieci web aplikacji będzie toohello punktu umbraco — etap db z bazy danych i hello tymczasowej bazie tooumbraco punkt-produkcyjną db zostanie aplikacji sieci web.

![Do wdrażania Umbraco CMS w wersji zapoznawczej wymiany](./media/app-service-web-staged-publishing-realworld-scenarios/22umbswap.png)

Poniżej przedstawiono zalety wymiany zarówno hello aplikacji sieci web i bazy danych hello:

* Możesz je wycofać toohello poprzedniej wersji aplikacji sieci web z inną **wymiany** Jeśli występują problemy z aplikacji.
* W przypadku uaktualnienia należy toodeploy plików i baz danych z hello przemieszczania aplikacji sieci web produkcyjnej toohello aplikacji sieci web i bazy danych. Wiele można wystąpienia problemów podczas wdrażania plików i baz danych. Za pomocą hello **wymiany** funkcji gniazd, firma Microsoft może skrócić czas przestojów podczas uaktualniania i zmniejszyć hello ryzyko błędów, które mogą wystąpić podczas wdrażania zmian.
* Możesz zrobić **A / B, testowanie** przy użyciu hello [testowanie w produkcji](https://azure.microsoft.com/documentation/videos/introduction-to-azure-websites-testing-in-production-with-galin-iliev/) funkcji.

Ten przedstawia przykład hello elastyczność platformy hello, których można tworzyć niestandardowe moduły podobne tooUmbraco Courier modułu toomanage wdrożenia w środowiskach.

## <a name="references"></a>Dokumentacja
[Programowanie zwinne oprogramowania z usługi aplikacji Azure](app-service-agile-software-development.md)

[Konfigurowanie środowisk dla aplikacji sieci web w usłudze Azure App Service przejściowych](web-sites-staged-publishing.md)

[Jak tooblock web uzyskują dostęp do miejsc wdrożenia produkcyjnego toonon](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
