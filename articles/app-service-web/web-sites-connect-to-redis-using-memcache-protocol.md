---
title: "aaaConnect tooRedis aplikacji sieci web usługi aplikacji za pośrednictwem protokołu Memcache - Azure hello | Dokumentacja firmy Microsoft"
description: "Łączenie aplikacji sieci web w usłudze Azure App service tooRedis pamięci podręcznej przy użyciu protokołu Memcache hello"
services: app-service\web
documentationcenter: php
author: SyntaxC4
manager: erikre
editor: riande
ms.assetid: 0fcdf9fa-2995-4839-ba4d-cfa389c4ba06
ms.service: app-service-web
ms.devlang: php
ms.topic: get-started-article
ms.tgt_pltfrm: windows
ms.workload: na
ms.date: 02/29/2016
ms.author: cfowler
ms.openlocfilehash: 48036d60fbbced59eb1e37584f507fffffff753d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# Łączenie aplikacji sieci web w usłudze Azure App Service tooRedis pamięci podręcznej za pośrednictwem protokołu Memcache hello
W tym artykule dowiesz się, jak tooconnect WordPress sieci web aplikacji w [usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) za[pamięć podręczna Redis Azure] [ 12] przy użyciu hello [Memcache] [ 13] protokołu. Jeśli masz istniejącej aplikacji sieci web, który korzysta z serwera Memcached do buforowania w pamięci, można migrować tooAzure usługi aplikacji i użyj hello firmy buforowania rozwiązania w systemie Microsoft Azure z niewielkiego lub żadnego kodu aplikacji tooyour zmiany. Ponadto można użyć istniejącego Memcache doświadczenia toocreate wysoce skalowalnych, rozproszonych aplikacji w usłudze Azure App Service z pamięcią podręczną Redis Azure do buforowania w pamięci, używając przy tym popularnych struktur aplikacji, takich jak .NET, PHP, Node.js, Java i Python.  

Usługi aplikacji Web Apps umożliwia tego scenariusza aplikacji z hello podkładki Memcache aplikacji Web, które jest lokalnym serwerem Memcached, który działa jako serwer proxy Memcache do buforowania wywołań tooAzure pamięci podręcznej Redis. Dzięki temu dowolna aplikacja, która komunikuje się z pamięcią podręczną Redis przy użyciu danych toocache protokołu Memcache hello. Ta podkładka Memcache działa na poziomie protokołu hello, więc można go użyć przez dowolną aplikację lub strukturę aplikacji tak długo, jak komunikacji przy użyciu protokołu Memcache hello.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## Wymagania wstępne
podkładki Memcache aplikacji Web Hello można używać dla dowolnej aplikacji, komunikuje się przy użyciu protokołu Memcache hello. W tym przykładzie aplikacja referencyjna hello jest skalowalną witryną WordPress, który można uzyskać z hello Azure Marketplace.

Wykonaj kroki hello opisane w tych artykułach:

* [Zapewnij wystąpienia hello usługi pamięć podręczna Redis Azure][0]
* [Deploy a Scalable WordPress site in Azure][1] (Wdrażanie skalowalnej witryny WordPress na platformie Azure)

Po utworzeniu hello wdrożeniu skalowalnej witryny WordPress i aprowizowaniu wystąpienia pamięci podręcznej Redis będzie gotowy tooproceed z włączaniem podkładki Memcache hello w aplikacji sieci Web usługi aplikacji Azure.

## Włącz podkładki Memcache aplikacji Web hello
W kolejności podkładki Memcache tooconfigure musisz utworzyć trzy ustawienia aplikacji. Można to zrobić przy użyciu różnych metod, w tym hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715), hello [klasyczny portal][3], hello [poleceń cmdlet programu Azure PowerShell] [ 5] lub hello [interfejsu wiersza polecenia platformy Azure][5]. Do celów hello tego wpisu, użyjemy toouse hello [Azure Portal] [ 4] ustawień aplikacji hello tooset. Witaj następujące wartości można pobrać z **ustawienia** bloku wystąpienia pamięci podręcznej Redis.

![Blok ustawień usługi Azure Redis Cache](./media/web-sites-connect-to-redis-using-memcache-protocol/1-azure-redis-cache-settings.png)

### Dodawanie ustawienia aplikacji REDIS_HOST
Witaj pierwsze ustawienie aplikacji należy hello jest toocreate **REDIS\_hosta** ustawienia aplikacji. To ustawienie określa hello toowhich hello podkładki przekazuje hello pamięci podręcznej informacji o lokalizacji docelowej. Witaj wartość wymaganą dla ustawienia aplikacji redis_host hello mogą być pobierane z hello **właściwości** bloku wystąpienia pamięci podręcznej Redis.

![Nazwa hosta usługi Azure Redis Cache](./media/web-sites-connect-to-redis-using-memcache-protocol/2-azure-redis-cache-hostname.png)

Zestaw hello klucz hello aplikacji ustawienie zbyt**REDIS\_hosta** i wartości hello toohello ustawienie aplikacji hello **hostname** hello wystąpienia pamięci podręcznej Redis.

![Ustawienie aplikacji sieci Web REDIS_HOST](./media/web-sites-connect-to-redis-using-memcache-protocol/3-azure-website-appsettings-redis-host.png)

### Dodawanie ustawienia aplikacji REDIS_KEY
Witaj drugie ustawienie aplikacji należy hello jest toocreate **REDIS\_klucza** ustawienia aplikacji. To ustawienie zapewnia wystąpienia pamięci podręcznej Redis hello hello uwierzytelniania toosecurely wymaganego tokenu dostępu. Można pobrać wartość hello wymagane dla hello aplikacji redis_key z hello **klucze dostępu** bloku hello wystąpienia pamięci podręcznej Redis.

![Klucz podstawowy usługi Azure Redis Cache](./media/web-sites-connect-to-redis-using-memcache-protocol/4-azure-redis-cache-primarykey.png)

Zestaw hello klucz hello aplikacji ustawienie zbyt**REDIS\_klucza** i wartości hello toohello ustawienie aplikacji hello **klucz podstawowy** hello wystąpienia pamięci podręcznej Redis.

![Ustawienie aplikacji witryny sieci Web Azure REDIS_KEY](./media/web-sites-connect-to-redis-using-memcache-protocol/5-azure-website-appsettings-redis-primarykey.png)

### Dodawanie ustawienia aplikacji MEMCACHESHIM_REDIS_ENABLE
Ostatnie ustawienie aplikacji Hello jest używany tooenable hello podkładki Memcache w aplikacjach sieci Web, używający hello kluczy REDIS_HOST i REDIS_KEY toohello tooconnect pamięć podręczna Redis Azure oraz do przodu hello wywołań pamięci podręcznej. Zestaw hello klucz hello aplikacji ustawienie zbyt**MEMCACHESHIM\_REDIS\_włączyć** i hello wartość zbyt**true**.

![Ustawienie aplikacji sieci Web MEMCACHESHIM_REDIS_ENABLE](./media/web-sites-connect-to-redis-using-memcache-protocol/6-azure-website-appsettings-enable-shim.png)

Po zakończeniu dodawania ustawienia aplikacji hello trzech (3), kliknij przycisk **zapisać**.

## Włączanie rozszerzenia Memcache dla języka PHP
Aby hello toospeak aplikacji hello protokołu Memcache jest konieczne tooinstall hello Memcache rozszerzenia tooPHP — Witaj struktury języka dla witryny WordPress.

### Pobieranie rozszerzenia php_memcache hello
Przeglądaj zbyt[PECL][6]. W obszarze hello buforowanie kategorii, kliknij [memcache][7]. W kolumnie materiałów powitania kliknij link biblioteki DLL hello.

![Witryna sieci Web PHP PECL](./media/web-sites-connect-to-redis-using-memcache-protocol/7-php-pecl-website.png)

Pobierz łącze Non-Thread bezpieczne (NTS) x86 hello hello wersji PHP włączonej w aplikacjach sieci Web. (Wartość domyślna to PHP 5.4)

![Pakiet Memcache dla witryny sieci Web PHP PECL](./media/web-sites-connect-to-redis-using-memcache-protocol/8-php-pecl-memcache-package.png)

### Włączanie rozszerzenia php_memcache hello
Po pobraniu pliku hello Wyodrębnij i przekaż hello **php\_memcache.dll** do hello **d:\\macierzystego\\lokacji\\wwwroot\\bin\\ext\\**  katalogu. Po przekazaniu pliku php_memcache.dll hello w aplikacji sieci web hello, należy tooenable hello rozszerzenia toohello środowiska uruchomieniowego języka PHP. Witaj tooenable rozszerzenie Memcache w portalu Azure, otwórz hello hello **ustawienia aplikacji** bloku hello aplikacji sieci web, następnie dodaj nowe ustawienie aplikacji hello klucz **PHP\_rozszerzenia** i hello wartość **bin\\ext\\php_memcache.dll**.

> [!NOTE]
> Jeśli aplikacja sieci web hello musi tooload wiele rozszerzeń PHP, hello wartość klucza php_extensions powinna być rozdzielaną przecinkami listę plików tooDLL ścieżek względnych.
> 
> 

![Ustawienie aplikacji sieci Web PHP_EXTENSIONS](./media/web-sites-connect-to-redis-using-memcache-protocol/9-azure-website-appsettings-php-extensions.png)

Po skończeniu kliknij przycisk **Zapisz**.

## Instalowanie wtyczki Memcache WordPress
> [!NOTE]
> Możesz również pobrać hello [wtyczkę Memcached Object Cache](https://wordpress.org/plugins/memcached/) z witryny WordPress.org.
> 
> 

Na stronie wtyczek hello WordPress kliknij **Dodaj nowy**.

![Strona wtyczek witryny WordPress](./media/web-sites-connect-to-redis-using-memcache-protocol/10-wordpress-plugin.png)

W polu wyszukiwania hello wpisz **memcached** i naciśnij klawisz **Enter**.

![Dodawanie nowej wtyczki WordPress](./media/web-sites-connect-to-redis-using-memcache-protocol/11-wordpress-add-new-plugin.png)

Znajdź **Memcached Object Cache** liście hello, następnie kliknij przycisk **Zainstaluj teraz**.

![WordPress — instalowanie wtyczki Memcache](./media/web-sites-connect-to-redis-using-memcache-protocol/12-wordpress-install-memcache-plugin.png)

### Włącz hello wtyczki Memcache WordPress
> [!NOTE]
> Postępuj zgodnie z instrukcjami hello na tym blogu [jak tooenable rozszerzeniem lokacji w aplikacji sieci Web] [ 8] tooinstall Visual Studio Team Services.
> 
> 

W hello `wp-config.php` plików, dodawanie hello następującego kodu powyżej hello stop edycji komentarzem hello koniec pliku hello.

```php
$memcached_servers = array(
    'default' => array('localhost:' . getenv("MEMCACHESHIM_PORT"))
);
```

Po wklejeniu tego kodu narzędzie monaco automatycznie zapisze dokument hello.

Witaj następnym krokiem jest wtyczki object-cache hello tooenable. Odbywa się to poprzez przeciągnięcie i upuszczenie **object-cache.php** z **wp-content/plugins/memcached** toohello folderu **wp-content** tooenable folderu hello obiektu Memcache Funkcje pamięci podręcznej.

![Zlokalizuj wtyczki hello memcache object-cache.php](./media/web-sites-connect-to-redis-using-memcache-protocol/13-locate-memcache-object-cache-plugin.png)

Teraz tego hello **object-cache.php** plik znajduje się w hello **wp-content** folderu, hello Memcached Object Cache jest teraz włączony.

![Włączanie wtyczki hello memcache object-cache.php](./media/web-sites-connect-to-redis-using-memcache-protocol/14-enable-memcache-object-cache-plugin.png)

## Sprawdź hello Memcache Object Cache funkcjonowania wtyczki
Wszystkie podkładki Memcache aplikacji Web Apps hello kroki tooenable hello są teraz zakończone. Witaj tylko pozostało tooverify czy hello dane wypełniają wystąpienie pamięci podręcznej Redis.

### Włączanie wsparcia portu bez protokołu SSL hello w pamięci podręcznej Redis Azure
> [!NOTE]
> W czasie hello pisania tego artykułu hello Redis CLI nie obsługuje łączności SSL, w związku z tym hello poniższe kroki są niezbędne.
> 
> 

W hello portalu Azure Przejdź toohello wystąpienia pamięci podręcznej Redis, który został utworzony dla tej aplikacji sieci web. Po otwarciu bloku pamięci podręcznej powitania kliknij hello **ustawienia** ikony.

![Przycisk ustawień usługi Azure Redis Cache](./media/web-sites-connect-to-redis-using-memcache-protocol/15-azure-redis-cache-settings-button.png)

Wybierz **porty dostępu** z listy hello.

![Port dostępu usługi Azure Redis Cache](./media/web-sites-connect-to-redis-using-memcache-protocol/16-azure-redis-cache-access-port.png)

Kliknij wartość **Nie** dla opcji **Zezwalaj na dostęp tylko za pomocą protokołu SSL**.

![Port dostępu usługi Azure Redis Cache — tylko protokół SSL](./media/web-sites-connect-to-redis-using-memcache-protocol/17-azure-redis-cache-access-port-ssl-only.png)

Zobaczysz, że został ustawiony port bez protokołu SSL hello. Kliknij pozycję **Zapisz**.

![Dostęp do portalu bez użycia protokołu SSL — Azure Redis Cache](./media/web-sites-connect-to-redis-using-memcache-protocol/18-azure-redis-cache-access-port-non-ssl.png)

### Połącz z interfejsu wiersza polecenia redis tooAzure pamięci podręcznej Redis
> [!NOTE]
> W tym kroku przyjęto założenie, że na komputerze deweloperskim zainstalowano lokalnie usługę Redis. [Zainstaluj usługę Redis lokalnie przy użyciu tych instrukcji][9].
> 
> 

Otwórz konsolę wiersza polecenia hello wyboru i wpisz następujące polecenie:

```shell
redis-cli –h <hostname-for-redis-cache> –a <primary-key-for-redis-cache> –p 6379
```

Zastąp hello  **&lt;hostname do redis-cache&gt;**  hello faktyczną nazwą hosta xxxxx.redis.cache.windows.net i hello  **&lt;podstawowy klucz — dla redis-cache&gt;**  z hello klucza dostępu dla pamięci podręcznej hello, naciśnij klawisz **Enter**. Po hello interfejsu wiersza polecenia został podłączony toohello wystąpienia pamięci podręcznej Redis, należy wydać dowolne polecenie redis. W poniższym zrzucie ekranu hello zawarto toolist hello kluczy.

![Połącz z CLI Redis w terminalu tooAzure pamięci podręcznej Redis](./media/web-sites-connect-to-redis-using-memcache-protocol/19-redis-cli-terminal.png)

Hello wywołania toolist hello kluczy powinien zwracać wartość. W przeciwnym razie spróbuj Nawigacja toohello aplikacji sieci web i podjęcie ponownej próby.

## Podsumowanie
Gratulacje! Witaj aplikacja WordPress ma teraz tooaid scentralizowane w pamięci podręcznej, w zwiększyć przepustowość. Należy pamiętać, że hello podkładki Memcache aplikacji sieci Web mogą być używane z dowolnym klientem Memcache, niezależnie od języka lub aplikacji struktury programistycznej. tooprovide opinii lub tooask pytania dotyczące podkładki Memcache aplikacji Web hello, post zbyt[fora MSDN] [ 10] lub [Stackoverflow][11].

> [!NOTE]
> Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service. Bez kart kredytowych i bez zobowiązań.
> 
> 

## Co zostało zmienione
* Toohello przewodnik zmiany z tooApp witryn sieci Web usługi dla: [usłudze Azure App Service i jej wpływ na istniejące usługi platformy Azure](http://go.microsoft.com/fwlink/?LinkId=529714)

[0]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache
[1]: http://bit.ly/1t0KxBQ
[2]: http://manage.windowsazure.com
[3]: http://portal.azure.com
[4]: /powershell/azureps-cmdlets-docs
[5]: /downloads
[6]: http://pecl.php.net
[7]: http://pecl.php.net/package/memcache
[8]: http://blog.syntaxc4.net/post/2015/02/05/how-to-enable-a-site-extension-in-azure-websites.aspx
[9]: http://redis.io/download#installation
[10]: https://social.msdn.microsoft.com/Forums/home?forum=windowsazurewebsitespreview
[11]: http://stackoverflow.com/questions/tagged/azure-web-sites
[12]: /services/cache/
[13]: http://memcached.org
