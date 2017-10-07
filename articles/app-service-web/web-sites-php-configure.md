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
# <a name="configure-php-in-azure-app-service-web-apps"></a>Skonfigurować PHP w aplikacjach sieci Web usługi aplikacji Azure
## <a name="introduction"></a>Wprowadzenie
W tym przewodniku opisano, jak tooconfigure hello wbudowanych środowiska uruchomieniowego języka PHP dla aplikacji sieci Web w [usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714), podaj niestandardowego środowiska uruchomieniowego języka PHP i Włącz rozszerzenia. toouse App Service, zarejestruj się, aby hello [bezpłatnej wersji próbnej]. Witaj tooget najbardziej z tego podręcznika, należy najpierw utworzyć aplikację sieci web PHP w usłudze App Service.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="how-to-change-hello-built-in-php-version"></a>Porady: zmiana hello wbudowanych wersji PHP
Domyślnie program PHP w wersji 5.5 jest zainstalowana i natychmiast dostępnej do użycia podczas tworzenia aplikacji sieci web usługi aplikacji. Witaj najlepsze sposób toosee hello dostępnych wersji zmian w, konfiguracji domyślnej i hello włączonego rozszerzenia jest toodeploy skrypt, który wywołuje hello [phpinfo()] funkcji.

Wersje PHP 5.6 i PHP 7.0 są również dostępne, ale nie jest włączony domyślnie. tooupdate hello wersji PHP, wykonaj jedną z następujących metod:

### <a name="azure-portal"></a>Azure Portal
1. Przeglądaj tooyour aplikacji sieci web w hello [Azure Portal](https://portal.azure.com) i kliknij na powitania **ustawienia** przycisku.
   
    ![Ustawienia aplikacji sieci Web][settings-button]
2. Z hello **ustawienia** wybierz bloku **ustawienia aplikacji** i wybierz nową wersję PHP hello.
   
    ![Ustawienia aplikacji][application-settings]
3. Kliknij przycisk hello **zapisać** u góry hello hello **ustawienia aplikacji w sieci Web** bloku.
   
    ![Zapisanie ustawień konfiguracji][save-button]

### <a name="azure-powershell-windows"></a>Program Azure PowerShell (system Windows)
1. Otwórz program Azure PowerShell i konta logowania tooyour:
   
        PS C:\> Login-AzureRmAccount
2. Ustaw wersję PHP hello hello aplikacji sieci web.
   
        PS C:\> Set-AzureWebsite -PhpVersion {5.5 | 5.6 | 7.0} -Name {app-name}
3. Wersja PHP Hello ma teraz wartość. Można potwierdzić te ustawienia:
   
        PS C:\> Get-AzureWebsite -Name {app-name} | findstr PhpVersion

### <a name="azure-command-line-interface-linux-mac-windows"></a>Interfejs wiersza polecenia platformy Azure (Linux, Mac, system Windows)
toouse hello interfejsu wiersza polecenia platformy Azure, musisz mieć **Node.js** zainstalowany na tym komputerze.

1. Otwórz Terminal i konta logowania tooyour.
   
        azure login
2. Ustaw wersję PHP hello hello aplikacji sieci web.
   
        azure site set --php-version {5.5 | 5.6 | 7.0} {app-name}

3. Wersja PHP Hello ma teraz wartość. Można potwierdzić te ustawienia:
   
        azure site show {app-name}

> [!NOTE] 
> Witaj [Azure CLI 2.0](https://github.com/Azure/azure-cli) są poleceń, które są równoważne toohello powyżej:
>
>

    az login
    az appservice web config update --php-version {5.5 | 5.6 | 7.0} -g {resource-group-name} -n {app-name}
    az appservice web config show -g {resource-group-name} -n {app-name}

## <a name="how-to-change-hello-built-in-php-configurations"></a>Porady: Zmienianie hello wbudowanych konfiguracji PHP
Dla dowolnego wbudowanych środowiska uruchomieniowego języka PHP można zmienić hello opcje konfiguracji, wykonując poniższe kroki hello. (Informacje o dyrektywy php.ini znajdują się w temacie [listy dyrektywy php.ini].)

### <a name="changing-phpiniuser-phpiniperdir-phpiniall-configuration-settings"></a>Zmiana PHP\_INI\_użytkownika, PHP\_INI\_PERDIR, PHP\_INI\_wszystkie ustawienia konfiguracji
1. Dodaj [. user.ini] katalog główny tooyour pliku.
2. Dodaj toohello ustawienia konfiguracji `.user.ini` plik za pomocą hello samej składni, należy użyć w `php.ini` pliku. Na przykład, jeśli potrzebujesz tooturn hello `display_errors` ustawienia i określ `upload_max_filesize` ustawienie too10M, Twoje `.user.ini` plik będzie zawierać ten tekst:
   
        ; Example Settings
        display_errors=On
        upload_max_filesize=10M
   
        ; OPTIONAL: Turn this on toowrite errors tood:\home\LogFiles\php_errors.log
        ; log_errors=On
3. Wdrażanie aplikacji sieci web.
4. Uruchom ponownie hello aplikacji sieci web. (Ponowne uruchomienie jest konieczne, ponieważ odczytuje hello częstotliwość, z którym PHP `.user.ini` plików podlega hello `user_ini.cache_ttl` ustawienie, które jest to ustawienie systemowe i jest domyślnie 300 sekund (5 minut). Nowe ustawienia hello tooread PHP w hello wymusza ponownie uruchomić aplikacji sieci web hello `.user.ini` pliku.)

Jako alternatywne toousing `.user.ini` plików, można użyć hello [ini_set()] funkcji w opcje konfiguracji tooset skrypty, które nie są dyrektywy na poziomie systemu.

### <a name="changing-phpinisystem-configuration-settings"></a>Zmiana PHP\_INI\_ustawień konfiguracji systemu
1. Dodaj ustawienie aplikacji tooyour aplikacji sieci Web z kluczem hello `PHP_INI_SCAN_DIR` i wartości`d:\home\site\ini`
2. Utwórz `settings.ini` plików przy użyciu konsoli Kudu (http://&lt;-Nazwa lokacji&gt;. scm.azurewebsite.net) w hello `d:\home\site\ini` katalogu.
3. Dodaj toohello ustawienia konfiguracji `settings.ini` plik za pomocą hello samej składni, należy użyć w pliku php.ini. Na przykład, jeśli potrzebujesz toopoint hello `curl.cainfo` ustawienie tooa `*.crt` pliku i ustaw "wincache.maxfilesize" ustawienie too512K, Twoje `settings.ini` plik będzie zawierać ten tekst:
   
        ; Example Settings
        curl.cainfo="%ProgramFiles(x86)%\Git\bin\curl-ca-bundle.crt"
        wincache.maxfilesize=512
4. Uruchom ponownie zmiany hello tooload aplikacji sieci Web.

## <a name="how-to-enable-extensions-in-hello-default-php-runtime"></a>Porady: Włączanie rozszerzenia w środowisku uruchomieniowym PHP domyślne hello
Zgodnie z opisem w poprzedniej sekcji hello, hello najlepsze sposób toosee hello domyślną wersję PHP jego domyślna konfiguracja i hello włączone rozszerzenia jest toodeploy skrypt, który wywołuje [phpinfo()]. tooenable dodatkowe rozszerzenia, wykonaj poniższe kroki hello:

### <a name="configure-via-ini-settings"></a>Konfigurowanie za pomocą ustawienia ini
1. Dodaj `ext` toohello katalogu `d:\home\site` katalogu.
2. Umieść `.dll` pliki rozszerzeń w hello `ext` katalog (na przykład `php_xdebug.dll`). Upewnij się, że rozszerzenia hello są zgodne z domyślną wersją PHP i są VC9 i zgodne z systemem innym niż wątkowo (nts).
3. Dodaj ustawienie aplikacji tooyour aplikacji sieci Web z kluczem hello `PHP_INI_SCAN_DIR` i wartości`d:\home\site\ini`
4. Utwórz `ini` w pliku `d:\home\site\ini` o nazwie `extensions.ini`.
5. Dodaj toohello ustawienia konfiguracji `extensions.ini` plik za pomocą hello samej składni, należy użyć w pliku php.ini. Na przykład, jeśli potrzebujesz rozszerzenia bazy danych MongoDB i narzędzia XDebug tooenable hello Twoje `extensions.ini` plik będzie zawierać ten tekst:
   
        ; Enable Extensions
        extension=d:\home\site\ext\php_mongo.dll
        zend_extension=d:\home\site\ext\php_xdebug.dll
6. Uruchom ponownie zmiany hello tooload aplikacji sieci Web.

### <a name="configure-via-app-setting"></a>Konfigurowanie za pomocą ustawienia aplikacji
1. Dodaj `bin` katalog główny toohello katalogu.
2. Umieść `.dll` pliki rozszerzeń w hello `bin` katalog (na przykład `php_xdebug.dll`). Upewnij się, że rozszerzenia hello są zgodne z domyślną wersją PHP i są VC9 i zgodne z systemem innym niż wątkowo (nts).
3. Wdrażanie aplikacji sieci web.
4. Przeglądaj tooyour aplikacji sieci web w portalu Azure hello i kliknij na powitania **ustawienia** przycisku.
   
    ![Ustawienia aplikacji sieci Web][settings-button]
5. Z hello **ustawienia** wybierz bloku **ustawienia aplikacji** i przewiń toohello **ustawień aplikacji** sekcji.
6. W hello **ustawień aplikacji** sekcji, Utwórz **PHP_EXTENSIONS** klucza. Witaj wartość tego klucza będzie głównego toowebsite względną ścieżkę: **bin\your ext, rozszerzenie pliku**.
   
    ![Włączanie rozszerzenia w ustawieniach aplikacji][php-extensions]
7. Kliknij przycisk hello **zapisać** u góry hello hello **ustawienia aplikacji w sieci Web** bloku.
   
    ![Zapisanie ustawień konfiguracji][save-button]

Zend rozszerzenia również są obsługiwane przy użyciu **PHP_ZENDEXTENSIONS** klucza. tooenable obejmują wiele rozszerzeń rozdzielaną przecinkami listę `.dll` pliki do wartości ustawienia aplikacji hello.

## <a name="how-to-use-a-custom-php-runtime"></a>Porady: Użyj niestandardowego środowiska uruchomieniowego języka PHP
Zamiast hello środowiska uruchomieniowego języka PHP domyślne aplikacje sieci Web usługi aplikacji można użyć środowiska uruchomieniowego języka PHP Podaj tooexecute skrypty PHP. środowisko uruchomieniowe Hello, które należy podać można skonfigurować przy `php.ini` pliku, który też podać. toouse niestandardowego środowiska uruchomieniowego języka PHP z aplikacjami sieci Web, wykonaj kroki hello poniżej.

1. Uzyskaj z systemem innym niż wątkowo, VC9 lub VC11 zgodnej wersji programu PHP dla systemu Windows. Najnowsze wersje PHP dla systemu Windows można znaleźć tutaj: [http://windows.php.net/download/]. Starsze wersje można znaleźć w tym miejscu archiwum hello: [http://windows.php.net/downloads/releases/archives/].
2. Modyfikowanie hello `php.ini` Twojego środowiska uruchomieniowego w pliku. Należy pamiętać, że wszystkie ustawienia konfiguracji, które są dyrektywy system poziom — tylko do będą ignorowane przez aplikacje sieci Web. (Informacje dyrektywy system poziom wyłącznie-, zobacz [listy dyrektywy php.ini]).
3. Opcjonalnie dodaj środowiska uruchomieniowego języka PHP tooyour rozszerzenia i włączyć je w hello `php.ini` pliku.
4. Dodaj `bin` katalog główny tooyour katalog i umieść hello katalog, który zawiera Twojego środowiska uruchomieniowego języka PHP w nim (na przykład `bin\php`).
5. Wdrażanie aplikacji sieci web.
6. Przeglądaj tooyour aplikacji sieci web w portalu Azure hello i kliknij na powitania **ustawienia** przycisku.
   
    ![Ustawienia aplikacji sieci Web][settings-button]
7. Z hello **ustawienia** wybierz bloku **ustawienia aplikacji** i przewiń toohello **mapowania obsługi** sekcji. Dodaj `*.php` toohello rozszerzenie pola i Dodaj hello ścieżki toohello `php-cgi.exe` pliku wykonywalnego. Jeśli umieścisz Twojego środowiska uruchomieniowego języka PHP w hello `bin` katalog w katalogu głównym aplikacji hello, ścieżka hello będzie `D:\home\site\wwwroot\bin\php\php-cgi.exe`.
   
    ![Określ w mapowania programu obsługi program obsługi][handler-mappings]
8. Kliknij przycisk hello **zapisać** u góry hello hello **ustawienia aplikacji w sieci Web** bloku.
   
    ![Zapisanie ustawień konfiguracji][save-button]

<a name="composer" />

## <a name="how-to-enable-composer-automation-in-azure"></a>Porady: Automatyzowanie Composer na platformie Azure
Domyślnie usługi aplikacji nie są wykonywane z composer.json, jeśli istnieje w projekcie PHP. Jeśli używasz [wdrożenia Git](app-service-deploy-local-git.md), można włączyć composer.json przetwarzania podczas `git push` , należy włączyć rozszerzenie Composer hello.

> [!NOTE]
> Możesz [głos najwyższej jakości Composer pomocy technicznej w usłudze App Service w tym miejscu](https://feedback.azure.com/forums/169385-web-apps-formerly-websites/suggestions/6477437-first-class-support-for-composer-and-pip)!
> 
> 

1. W przypadku programu PHP sieci web bloku aplikacji w hello [portalu Azure](https://portal.azure.com), kliknij przycisk **narzędzia** > **rozszerzenia**.
   
    ![Azure Portal ustawienia bloku tooenable Composer Automatyzacja na platformie Azure](./media/web-sites-php-configure/composer-extension-settings.png)
2. Kliknij przycisk **Dodaj**, następnie kliknij przycisk **Composer**.
   
    ![Dodaj automatyzacji Composer tooenable rozszerzenie Composer na platformie Azure](./media/web-sites-php-configure/composer-extension-add.png)
3. Kliknij przycisk **OK** tooaccept postanowienia prawne. Kliknij przycisk **OK** ponownie tooadd hello rozszerzenia.
   
    Witaj **zainstalowanych rozszerzeń** bloku będzie zawierać teraz rozszerzenie Composer hello.  
    ![Zaakceptuj postanowienia prawne tooenable Composer Automatyzacja na platformie Azure](./media/web-sites-php-configure/composer-extension-view.png)
4. Teraz, wykonywać `git add`, `git commit`, i `git push` podobnie jak w poprzedniej sekcji hello. Pojawi się, czy Composer jest instalowany zdefiniowane w composer.json zależności.
   
    ![Wdrażanie Git za pomocą automatyzacji Composer na platformie Azure](./media/web-sites-php-configure/composer-extension-success.png)

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji, zobacz hello [Centrum deweloperów języka PHP](/develop/php/).

> [!NOTE]
> Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service. Bez kart kredytowych i bez zobowiązań.
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

