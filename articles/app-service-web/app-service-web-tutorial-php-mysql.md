---
title: aaaBuild aplikacji sieci web PHP i MySQL na platformie Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooget aplikacji PHP, działa na platformie Azure, z połączenia tooa MySQL bazy danych na platformie Azure."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 14feb4f3-5095-496e-9a40-690e1414bd73
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 07/21/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 3c050b30e2e2c80d011bed989cd5f8cecac35d15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-php-and-mysql-web-app-in-azure"></a>Tworzenie aplikacji sieci web PHP i MySQL na platformie Azure

Usługa [Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) oferuje wysoce skalowalną i samonaprawialną usługę hostowaną w Internecie. Ten samouczek pokazuje, jak toocreate PHP sieci web aplikacji na platformie Azure i podłącz go tooa baza danych MySQL. Po zakończeniu będziesz mieć [Laravel](https://laravel.com/) aplikacji uruchomionej na aplikacje sieci Web usługi aplikacji Azure.

![Aplikacja PHP działające w usłudze aplikacji Azure](./media/app-service-web-tutorial-php-mysql/complete-checkbox-published.png)

Ten samouczek zawiera informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]
> * Utwórz bazę danych MySQL na platformie Azure
> * Połącz tooMySQL aplikacji PHP
> * Wdrażanie tooAzure aplikacji hello
> * Aktualizacja modelu danych hello i wdrożenie aplikacji hello
> * Strumieniowe przesyłanie dzienników diagnostycznych z platformy Azure
> * Zarządzanie aplikacją hello w hello portalu Azure

## <a name="prerequisites"></a>Wymagania wstępne

toocomplete tego samouczka:

* [Zainstaluj oprogramowanie Git](https://git-scm.com/)
* [Instalowanie języka PHP 5.6.4 lub nowszy](http://php.net/downloads.php)
* [Zainstaluj Composer](https://getcomposer.org/doc/00-intro.md)
* Włącz następujące rozszerzenia PHP potrzeb Laravel hello: biblioteki OpenSSL, PDO MySQL, Mbstring, Tokenizatora, XML
* [Zainstaluj i uruchom MySQL](https://dev.mysql.com/doc/refman/5.7/en/installing.html) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prepare-local-mysql"></a>Przygotowywanie lokalnej MySQL

W tym kroku utworzysz bazę danych na lokalnym serwerze MySQL do użycia w tym samouczku.

### <a name="connect-toolocal-mysql-server"></a>Połącz serwer MySQL toolocal

W oknie terminalu Połącz tooyour lokalny serwer MySQL. Wszystkie polecenia hello toorun to okno terminalu można użyć w tym samouczku.

```bash
mysql -u root -p
```

Jeśli zostanie wyświetlony monit o podanie hasła, wprowadź hasło hello hello `root` konta. Jeśli nie pamiętasz hasła do konta głównego, zobacz [MySQL: jak tooReset hello hasła użytkownika Root](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).

Jeśli polecenie zostanie wykonane pomyślnie, jest uruchomiony serwer MySQL. Jeśli nie, upewnij się, że serwera lokalnego MySQL została uruchomiona z następujących hello [MySQL poinstalacyjne czynności](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).

### <a name="create-a-database-locally"></a>Utwórz bazę danych lokalnie

Na powitania `mysql` należy utworzyć bazę danych.

```sql 
CREATE DATABASE sampledb;
```

Zakończyć połączenie z serwerem, wpisując `quit`.

```sql
quit
```

<a name="step2"></a>

## <a name="create-a-php-app-locally"></a>Utwórz aplikację PHP lokalnie
W tym kroku Pobierz przykładową aplikację Laravel, skonfiguruj połączenie bazy danych i uruchom lokalnie. 

### <a name="clone-hello-sample"></a>Przykład Witaj klonowania

Okno terminalu hello `cd` tooa katalog roboczy.

Hello uruchom następujące polecenie tooclone hello próbki repozytorium.

```bash
git clone https://github.com/Azure-Samples/laravel-tasks
```

`cd`katalog sklonowany tooyour.
Instalowanie pakietów hello wymagane.

```bash
cd laravel-tasks
composer install
```

### <a name="configure-mysql-connection"></a>Skonfiguruj połączenie MySQL

W katalogu głównym repozytorium hello, Utwórz plik o nazwie *.env*. Następujące zmienne do hello hello kopiowania *.env* pliku. Zastąp hello  _&lt;root_password >_ symbol zastępczy hello MySQL głównego hasła użytkownika.

```
APP_ENV=local
APP_DEBUG=true
APP_KEY=SomeRandomString

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_DATABASE=sampledb
DB_USERNAME=root
DB_PASSWORD=<root_password>
```

Aby uzyskać informacje o używaniu hello Laravel _.env_ plików, zobacz [konfiguracji środowiska Laravel](https://laravel.com/docs/5.4/configuration#environment-configuration).

### <a name="run-hello-sample-locally"></a>Uruchamianie przykładowych hello lokalnie

Uruchom [Laravel bazy danych migracji](https://laravel.com/docs/5.4/migrations) toocreate hello tabele hello potrzeb aplikacji. toosee tabel, które są tworzone w migracje hello poszukać w hello _bazy danych/migracje_ katalogu w repozytorium Git hello.

```bash
php artisan migrate
```

Wygeneruj nowy klucz aplikacji Laravel.

```bash
php artisan key:generate
```

Uruchamianie aplikacji hello.

```bash
php artisan serve
```

Przejdź do zbyt`http://localhost:8000` w przeglądarce. Dodać kilka zadań na stronie powitania.

![PHP pomyślnie łączy tooMySQL](./media/app-service-web-tutorial-php-mysql/mysql-connect-success.png)

Wpisz toostop PHP, `Ctrl + C` w hello terminala.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-mysql-in-azure"></a>Tworzenie MySQL na platformie Azure

W tym kroku utworzysz bazę danych MySQL w [bazy danych Azure dla programu MySQL (wersja zapoznawcza)](/azure/mysql). Następnie należy skonfigurować hello PHP aplikacji tooconnect toothis bazy danych.

### <a name="create-a-resource-group"></a>Tworzenie grupy zasobów

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group-no-h.md)] 

### <a name="create-a-mysql-server"></a>Utwórz serwer MySQL

Utwórz serwer bazy danych Azure dla programu MySQL (wersja zapoznawcza) z hello [utworzenie przez serwer mysql az](/cli/azure/mysql/server#create) polecenia.

W hello następujące polecenia, należy zastąpić nazwę serwera MySQL, w której występuje hello  _&lt;mysql_server_name >_ symbolu zastępczego (prawidłowe znaki to `a-z`, `0-9`, i `-`). Ta nazwa jest częścią nazwy hosta serwera MySQL hello (`<mysql_server_name>.database.windows.net`), musi on toobe globalnie unikatowe.

```azurecli-interactive
az mysql server create \
    --name <mysql_server_name> \
    --resource-group myResourceGroup \
    --location "North Europe" \
    --admin-user adminuser \
    --admin-password MySQLAzure2017
```

Po utworzeniu serwer MySQL hello hello Azure CLI pokazuje informacje toohello podobnie poniższy przykład:

```json
{
  "administratorLogin": "adminuser",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "<mysql_server_name>.database.windows.net",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforMySQL/servers/<mysql_server_name>",
  "location": "northeurope",
  "name": "<mysql_server_name>",
  "resourceGroup": "myResourceGroup",
  ...
}
```

### <a name="configure-server-firewall"></a>Konfigurowanie zapory serwera

Tworzenie reguły zapory klienta MySQL serwera tooallow połączeń przy użyciu hello [az mysql reguły zapory serwera — Utwórz](/cli/azure/mysql/server/firewall-rule#create) polecenia.

```azurecli-interactive
az mysql server firewall-rule create \
    --name allIPs \
    --server <mysql_server_name> \
    --resource-group myResourceGroup \
    --start-ip-address 0.0.0.0 \
    --end-ip-address 255.255.255.255
```

> [!NOTE]
> Bazy danych platformy Azure dla programu MySQL (wersja zapoznawcza) aktualnie nie ograniczyć zakres usług tooAzure tylko połączeń. Adresy IP na platformie Azure są przypisywane dynamicznie, jest lepsze tooenable wszystkich adresów IP. Usługa Hello jest w wersji zapoznawczej. Zaplanowano lepsze metody zabezpieczania bazy danych.
>
>

### <a name="connect-tooproduction-mysql-server-locally"></a>Połącz serwer MySQL tooproduction lokalnie

Okno terminalu hello połączyć toohello serwer MySQL na platformie Azure. Użyj wartości hello wcześniej określona dla  _&lt;mysql_server_name >_.

```bash
mysql -u adminuser@<mysql_server_name> -h <mysql_server_name>.database.windows.net -P 3306 -p
```

Po wyświetleniu monitu o podanie hasła, użyj _$tr0ngPa$ w0rd!_, określony podczas tworzenia hello bazy danych.

### <a name="create-a-production-database"></a>Utwórz bazę danych produkcyjnych

Na powitania `mysql` należy utworzyć bazę danych.

```sql
CREATE DATABASE sampledb;
```

### <a name="create-a-user-with-permissions"></a>Utwórz użytkownika z uprawnieniami

Utwórz użytkownika bazy danych o nazwie _phpappuser_ i nadaj mu wszystkie uprawnienia w hello `sampledb` bazy danych.

```sql
CREATE USER 'phpappuser' IDENTIFIED BY 'MySQLAzure2017'; 
GRANT ALL PRIVILEGES ON sampledb.* too'phpappuser';
```

Zakończyć połączenie z serwerem hello wpisując `quit`.

```sql
quit
```

## <a name="connect-app-tooazure-mysql"></a>Łączenie aplikacji tooAzure MySQL

W tym kroku łączysz hello PHP aplikacji toohello baza danych MySQL utworzonej w bazie danych Azure dla programu MySQL (wersja zapoznawcza).

<a name="devconfig"></a>

### <a name="configure-hello-database-connection"></a>Skonfiguruj połączenie bazy danych hello

W katalogu głównym repozytorium hello, Utwórz _. env.production_ hello plik i skopiuj następujące zmienne do niego. Zastąp symbol zastępczy hello  _&lt;mysql_server_name >_.

```
APP_ENV=production
APP_DEBUG=true
APP_KEY=SomeRandomString

DB_CONNECTION=mysql
DB_HOST=<mysql_server_name>.database.windows.net
DB_DATABASE=sampledb
DB_USERNAME=phpappuser@<mysql_server_name>
DB_PASSWORD=MySQLAzure2017
MYSQL_SSL=true
```

Zapisz zmiany hello.

> [!TIP]
> toosecure MySQL informacje o połączeniu, ten plik jest już wykluczone z repozytorium Git hello (zobacz _.gitignore_ w katalogu głównym repozytorium hello). Później możesz dowiedzieć się, jak tooconfigure zmienne środowiskowe w tooyour tooconnect usługi aplikacji bazy danych w bazie danych Azure dla programu MySQL (wersja zapoznawcza). Zmienne środowiskowe nie wymagają hello *.env* pliku w usłudze App Service.
>

### <a name="configure-ssl-certificate"></a>Konfigurowanie certyfikatu protokołu SSL

Domyślnie baza danych Azure dla programu MySQL wymusza połączenia SSL od klientów. tooconnect tooyour bazy danych MySQL na platformie Azure, należy użyć _PEM_ certyfikatu SSL.

Otwórz _config/database.php_ i Dodaj hello _sslmode_ i _opcje_ parametry zbyt`connections.mysql`, jak pokazano w hello następującego kodu.

```php
'mysql' => [
    ...
    'sslmode' => env('DB_SSLMODE', 'prefer'),
    'options' => (env('MYSQL_SSL')) ? [
        PDO::MYSQL_ATTR_SSL_KEY    => '/ssl/certificate.pem', 
    ] : []
],
```

toolearn jak toogenerate to _certificate.pem_, zobacz [łączności Konfigurowanie protokołu SSL w Twojej aplikacji toosecurely połączyć tooAzure bazy danych MySQL](../mysql/howto-configure-ssl.md).

> [!TIP]
> Ścieżka Hello _/ssl/certificate.pem_ wskazuje istniejący tooan _certificate.pem_ plik w repozytorium Git hello. Ten plik jest dostarczany jako udogodnienie, w tym samouczku. Ze względów, nie należy zatwierdzić Twoje _PEM_ certyfikatów do kontroli źródła. 
>

### <a name="test-hello-application-locally"></a>Testowanie aplikacji hello lokalnie

Uruchom Laravel migracji bazy danych z _. env.production_ jako hello środowiska pliku toocreate hello tabel bazy danych MySQL w bazie danych Azure dla programu MySQL (wersja zapoznawcza). Należy pamiętać, że _. env.production_ ma hello połączenia informacji tooyour baza danych MySQL na platformie Azure.

```bash
php artisan migrate --env=production --force
```

_. env.production_ nie ma jeszcze klucza prawidłową aplikację. Generuj nową dla niego w hello terminala.

```bash
php artisan key:generate --env=production --force
```

Uruchom hello przykładową aplikację z _. env.production_ hello środowiska pliku.

```bash
php artisan serve --env=production
```

Przejdź do zbyt`http://localhost:8000`. Jeśli strona hello ładuje bez błędów, hello aplikacji PHP łączy toohello baza danych MySQL na platformie Azure.

Dodać kilka zadań na stronie powitania.

![PHP pomyślnie łączy tooAzure bazy danych dla programu MySQL (wersja zapoznawcza)](./media/app-service-web-tutorial-php-mysql/mysql-connect-success.png)

Wpisz toostop PHP, `Ctrl + C` w hello terminala.

### <a name="commit-your-changes"></a>Zatwierdź zmiany

Uruchom hello toocommit polecenia Git następujące zmiany:

```bash
git add .
git commit -m "database.php updates"
```

Aplikacja jest gotowa toobe wdrożone.

## <a name="deploy-tooazure"></a>Wdrażanie tooAzure

W tym kroku możesz wdrożyć tooAzure aplikacji PHP, MySQL, połączone hello usługi aplikacji.

### <a name="create-an-app-service-plan"></a>Tworzenie planu usługi App Service

[!INCLUDE [Create app service plan no h](../../includes/app-service-web-create-app-service-plan-no-h.md)]

### <a name="create-a-web-app"></a>Tworzenie aplikacji sieci Web

[!INCLUDE [Create web app no h](../../includes/app-service-web-create-web-app-no-h.md)]

### <a name="set-hello-php-version"></a>Ustaw wersję PHP hello

Wersję PHP hello zestaw aplikacji hello wymaga przy użyciu hello [zestaw konfiguracyjny aplikacji sieci Web az](/cli/azure/webapp/config#set) polecenia.

Witaj poniższe polecenie ustawia too_7.0_ wersji PHP hello.

```azurecli-interactive
az webapp config set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --php-version 7.0
```

### <a name="configure-database-settings"></a>Konfigurowanie ustawień bazy danych

Jak wskazano wcześniej, można połączyć z bazy danych MySQL na platformie Azure tooyour zmiennych środowiskowych przy użyciu aplikacji usługi.

W usłudze App Service można ustawić zmienne środowiskowe jako _ustawień aplikacji_ przy użyciu hello [az aplikacji sieci Web config appsettings zestaw](/cli/azure/webapp/config/appsettings#set) polecenia.

Witaj następujące polecenie konfiguruje ustawienia aplikacji hello `DB_HOST`, `DB_DATABASE`, `DB_USERNAME`, i `DB_PASSWORD`. Zastąp symbole zastępcze hello  _&lt;nazwa_aplikacji >_ i  _&lt;mysql_server_name >_.

```azurecli-interactive
az webapp config appsettings set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings DB_HOST="<mysql_server_name>.database.windows.net" DB_DATABASE="sampledb" DB_USERNAME="phpappuser@<mysql_server_name>" DB_PASSWORD="MySQLAzure2017" MYSQL_SSL="true"
```

Można użyć hello PHP [getenv —](http://www.php.net/manual/function.getenv.php) tooaccess metody hello ustawienia. używa Hello kodu Laravel [env](https://laravel.com/docs/5.4/helpers#method-env) otoki za pośrednictwem hello PHP `getenv`. Na przykład hello MySQL konfiguracji w _config/database.php_ wygląda hello następującego kodu:

```php
'mysql' => [
    'driver'    => 'mysql',
    'host'      => env('DB_HOST', 'localhost'),
    'database'  => env('DB_DATABASE', 'forge'),
    'username'  => env('DB_USERNAME', 'forge'),
    'password'  => env('DB_PASSWORD', ''),
    ...
],
```

### <a name="configure-laravel-environment-variables"></a>Skonfiguruj Laravel zmienne środowiskowe

Laravel musi mieć klucz aplikacji w usłudze App Service. Możesz ją skonfigurować z ustawieniami aplikacji.

Użyj `php artisan` toogenerate nowy klucz aplikacji bez jej zapisania too_.env_.

```bash
php artisan key:generate --show
```

Ustawić klucz aplikacji hello w hello aplikację usługi aplikacji sieci web przy użyciu hello [az aplikacji sieci Web config appsettings zestaw](/cli/azure/webapp/config/appsettings#set) polecenia. Zastąp symbole zastępcze hello  _&lt;nazwa_aplikacji >_ i  _&lt;outputofphpartisankey: generowanie >_.

```azurecli-interactive
az webapp config appsettings set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings APP_KEY="<output_of_php_artisan_key:generate>" APP_DEBUG="true"
```

`APP_DEBUG="true"`informuje, że Laravel tooreturn informacje o debugowaniu podczas hello wdrażania aplikacji sieci web wystąpią błędy. Podczas uruchamiania aplikacji produkcyjnych, ustaw go za`false`, który jest bardziej bezpieczne.

### <a name="set-hello-virtual-application-path"></a>Ścieżka aplikacji wirtualnej hello zestawu

Ustaw ścieżkę aplikacji wirtualnej hello hello aplikacji sieci web. Ten krok jest wymagany, ponieważ hello [cyklem życia aplikacji Laravel](https://laravel.com/docs/5.4/lifecycle) rozpoczyna się w hello _publicznego_ katalogu zamiast katalog główny aplikacji hello. Innych platform PHP, na których cyklu życia start w katalogu głównym hello może działać bez ręcznej konfiguracji hello ścieżkę aplikacji wirtualnej.

Ścieżka aplikacji wirtualnej hello zestawu przy użyciu hello [aktualizacja zasobu az](/cli/azure/resource#update) polecenia. Zastąp hello  _&lt;nazwa_aplikacji >_ symbolu zastępczego.

```azurecli-interactive
az resource update \
    --name web \
    --resource-group myResourceGroup \
    --namespace Microsoft.Web \
    --resource-type config \
    --parent sites/<app_name> \
    --set properties.virtualApplications[0].physicalPath="site\wwwroot\public" \
    --api-version 2015-06-01
```

Domyślnie usługi Azure App Service punktów ścieżki aplikacji wirtualnej katalogu głównego hello (_/_) katalog główny toohello hello wdrażane pliki aplikacji (_sites\wwwroot_).

### <a name="configure-a-deployment-user"></a>Konfigurowanie użytkownika wdrożenia

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user-no-h.md)]

### <a name="configure-local-git-deployment"></a>Konfigurowanie lokalnego wdrożenia narzędzia Git

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git-no-h.md)]

### <a name="push-tooazure-from-git"></a>Wypychać tooAzure za pomocą narzędzia Git

Dodaj Azure tooyour zdalnego lokalnego repozytorium Git.

```bash
git remote add azure <paste_copied_url_here>
```

Wypchnij aplikacji PHP hello Azure toodeploy zdalnego toohello. Zostanie wyświetlony monit o hello hasło wcześniej w ramach tworzenia hello hello wdrożenia użytkownika.

```bash
git push azure master
```

Podczas wdrażania usługi Azure App Service komunikuje się postęp za pomocą narzędzia Git.

```bash
Counting objects: 3, done.
Delta compression using up too8 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 291 bytes | 0 bytes/s, done.
Total 3 (delta 2), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id 'a5e076db9c'.
remote: Running custom deployment command...
remote: Running deployment command...
...
< Output has been truncated for readability >
```

> [!NOTE]
> Można zauważyć, że proces wdrażania hello instaluje [Composer](https://getcomposer.org/) pakietów na końcu hello. Usługi aplikacji nie są uruchamiane te automatyzacji podczas wdrażania domyślne, tak to repozytorium przykładowej ma trzy dodatkowe plików w jego tooenable katalogu głównego:
>
> - `.deployment`— Ten plik zawiera toorun usługi aplikacji `bash deploy.sh` jako hello niestandardowe wdrożenie skryptu.
> - `deploy.sh`-hello niestandardowe wdrożenie skryptu. Jeśli możesz przejrzeć plik hello, zobaczysz, że działa `php composer.phar install` po `npm install`.
> - `composer.phar`-Menedżera pakietów hello Composer.
>
> Tooadd tej metody można użyć dowolnego kroku tooyour wdrożenia na podstawie Git tooApp usługi. Aby uzyskać więcej informacji, zobacz [niestandardowego skryptu wdrażania](https://github.com/projectkudu/kudu/wiki/Custom-Deployment-Script).
>

### <a name="browse-toohello-azure-web-app"></a>Przeglądaj toohello aplikacji sieci web Azure

Przeglądaj zbyt`http://<app_name>.azurewebsites.net` i dodaj kilka zadań toohello listy.

![Aplikacja PHP działające w usłudze aplikacji Azure](./media/app-service-web-tutorial-php-mysql/php-mysql-in-azure.png)

Gratulacje, używasz aplikacji PHP sieci opartych na danych w usłudze Azure App Service.

## <a name="update-model-locally-and-redeploy"></a>Aktualizuj model lokalnie i wdrożenie

W tym kroku należy toohello prosta zmiana `task` modelu danych i hello aplikacji sieci Web, a następnie opublikuj hello tooAzure aktualizacji.

W scenariuszu hello zadania możesz zmodyfikować aplikacji hello tak, aby oznaczyć zadanie jako ukończone.

### <a name="add-a-column"></a>Dodaj kolumnę

W terminalu hello Przejdź toohello katalogu głównego repozytorium Git hello.

Generuj nowe migracja bazy danych dla hello `tasks` tabeli:

```bash
php artisan make:migration add_complete_column --table=tasks
```

To polecenie zawiera hello nazwę hello migracji pliku, który zostanie wygenerowany. Ten plik w _bazy danych/migracje_ i otwórz go.

Zastąp hello `up` metody z hello następującego kodu:

```php
public function up()
{
    Schema::table('tasks', function (Blueprint $table) {
        $table->boolean('complete')->default(False);
    });
}
```

Witaj poprzedni kod dodaje logiczna kolumnę w hello `tasks` tabeli o nazwie `complete`.

Zastąp hello `down` metody za pomocą następującego kodu dla akcji wycofywania hello hello:

```php
public function down()
{
    Schema::table('tasks', function (Blueprint $table) {
        $table->dropColumn('complete');
    });
}
```

W terminalu hello Uruchom Laravel bazy danych migracji toomake hello zmiany w lokalnej bazie danych hello.

```bash
php artisan migrate
```

Oparte na powitania [konwencji nazewnictwa Laravel](https://laravel.com/docs/5.4/eloquent#defining-models), hello model `Task` (zobacz _app/Task.php_) mapuje toohello `tasks` tabeli domyślnie.

### <a name="update-application-logic"></a>Aktualizowanie aplikacji logiki

Otwórz hello *routes/web.php* pliku. definiuje aplikacja Hello jego tras i logiki biznesowej w tym miejscu.

Na końcu hello hello pliku należy dodać trasę z hello następującego kodu:

```php
/**
 * Toggle Task completeness
 */
Route::post('/task/{id}', function ($id) {
    error_log('INFO: post /task/'.$id);
    $task = Task::findOrFail($id);

    $task->complete = !$task->complete;
    $task->save();

    return redirect('/');
});
```

Witaj poprzedni kod sprawia, że model danych toohello proste aktualizacji przełączając wartość hello `complete`.

### <a name="update-hello-view"></a>Widok hello aktualizacji

Otwórz hello *resources/views/tasks.blade.php* pliku. Znajdź hello `<tr>` tagu początkowego i zastąpić go ciągiem:

```html
<tr class="{{ $task->complete ? 'success' : 'active' }}" >
```

Witaj poprzedzających kolor wiersza hello zmian kodu w zależności od tego, czy hello zadanie zostało ukończone.

W następnym wierszu hello masz hello następującego kodu:

```html
<td class="table-text"><div>{{ $task->name }}</div></td>
```

Zastąp cały wiersz hello hello następującego kodu:

```html
<td>
    <form action="{{ url('task/'.$task->id) }}" method="POST">
        {{ csrf_field() }}

        <button type="submit" class="btn btn-xs">
            <i class="fa {{$task->complete ? 'fa-check-square-o' : 'fa-square-o'}}"></i>
        </button>
        {{ $task->name }}
    </form>
</td>
```

Witaj poprzedni kod dodaje przycisk przesyłania hello odwołuje się do trasy hello, wcześniej zdefiniowany.

### <a name="test-hello-changes-locally"></a>Test hello zmiany lokalnie

Z katalogu głównego repozytorium Git hello hello należy uruchomić serwera wdrożeniowego hello.

```bash
php artisan serve
```

Witaj toosee zmiana stanu zadania, przejdź zbyt`http://localhost:8000` i hello zaznacz pole wyboru.

![Dodano pola wyboru tootask](./media/app-service-web-tutorial-php-mysql/complete-checkbox.png)

Wpisz toostop PHP, `Ctrl + C` w hello terminala.

### <a name="publish-changes-tooazure"></a>Publikowanie zmian tooAzure

W terminalu hello Uruchom Laravel bazy danych migracji hello produkcji połączenia ciąg toomake hello zmiany hello Azure bazy danych.

```bash
php artisan migrate --env=production --force
```

Przekaż wszystkie zmiany hello w usłudze Git, a następnie Wypchnij tooAzure zmiany kodu hello.

```bash
git add .
git commit -m "added complete checkbox"
git push azure master
```

Raz hello `git push` jest wykonać kolejno toohello sieci web platformy Azure aplikacji i testowania hello nowych funkcji.

![Zmiany modelu i bazy danych publikowanych tooAzure](media/app-service-web-tutorial-php-mysql/complete-checkbox-published.png)

Jeśli dodano żadnych zadań, są one przechowywane w bazie danych hello. Schemat danych toohello aktualizacje pozostawić istniejące dane bez zmian.

## <a name="stream-diagnostic-logs"></a>Dzienniki diagnostyczne strumienia

Podczas wykonywania hello aplikacji PHP w usłudze Azure App Service można uzyskać tooyour gazociągami dzienniki konsoli hello terminala. W ten sposób można uzyskać hello tego samego komunikaty diagnostyczne toohelp Debugowanie błędów aplikacji.

Dziennik toostart przesyłania strumieniowego, użyj hello [końcowego fragmentu dziennika aplikacji sieci Web az](/cli/azure/webapp/log#tail) polecenia.

```azurecli-interactive
az webapp log tail \
    --name <app_name> \
    --resource-group myResourceGroup
```

Po rozpoczęciu przesyłania strumieniowego dzienników Odśwież hello aplikacji sieci web platformy Azure w tooget przeglądarki hello część ruchu w sieci web. Możesz teraz przeglądać terminal gazociągami toohello dzienniki konsoli. Jeśli nie widzisz natychmiast dzienniki konsoli, sprawdź ponownie w ciągu 30 sekund.

Dziennik toostop przesyłania strumieniowego w dowolnym momencie, typ `Ctrl` + `C`.

> [!TIP]
> Aplikacja PHP można użyć standardowego hello [error_log()](http://php.net/manual/function.error-log.php) toooutput toohello konsoli. Witaj Przykładowa aplikacja korzysta z tej metody w _app/Http/routes.php_.
>
> Jako platforma sieci web [Laravel używa Monolog](https://laravel.com/docs/5.4/errors) jako hello rejestrowanie dostawcy. toosee tooget Monolog toooutput wiadomości toohello konsoli, zobacz [PHP: jak toouse monolog tooconsole toolog (php://out)](http://stackoverflow.com/questions/25787258/php-how-to-use-monolog-to-log-to-console-php-out).
>
>

## <a name="manage-hello-azure-web-app"></a>Zarządzanie hello aplikacji sieci web platformy Azure

Przejdź toohello [portalu Azure](https://portal.azure.com) aplikacji sieci web hello toomanage został utworzony.

W menu po lewej stronie powitania kliknij **usługi aplikacji**, a następnie kliknij nazwę hello aplikacji sieci web platformy Azure.

![Aplikacja sieci web tooAzure nawigacji w portalu](./media/app-service-web-tutorial-php-mysql/access-portal.png)

Zostanie wyświetlona strona Omówienie aplikacji internetowej. W tym miejscu można wykonać zadania podstawowe możliwości zarządzania, takie jak zatrzymanie, start ponownego uruchomienia, przeglądania i usuwania.

menu po lewej stronie powitania zawiera strony konfigurowania aplikacji.

![Strona usługi App Service w witrynie Azure Portal](./media/app-service-web-tutorial-php-mysql/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

<a name="next"></a>

## <a name="next-steps"></a>Następne kroki

W niniejszym samouczku zawarto informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]
> * Utwórz bazę danych MySQL na platformie Azure
> * Połącz tooMySQL aplikacji PHP
> * Wdrażanie tooAzure aplikacji hello
> * Aktualizacja modelu danych hello i wdrożenie aplikacji hello
> * Strumieniowe przesyłanie dzienników diagnostycznych z platformy Azure
> * Zarządzanie aplikacją hello w hello portalu Azure

Przejść dalej toolearn samouczka toohello jak toomap DNS niestandardowej nazwy tooa aplikacji sieci web.

> [!div class="nextstepaction"]
> [Mapowanie istniejących niestandardowe DNS nazwy tooAzure aplikacji sieci Web](app-service-web-tutorial-custom-domain.md)
