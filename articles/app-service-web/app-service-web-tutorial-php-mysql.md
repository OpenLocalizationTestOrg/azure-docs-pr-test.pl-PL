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
# <a name="build-a-php-and-mysql-web-app-in-azure"></a><span data-ttu-id="5e9f5-103">Tworzenie aplikacji sieci web PHP i MySQL na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="5e9f5-103">Build a PHP and MySQL web app in Azure</span></span>

<span data-ttu-id="5e9f5-104">Usługa [Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) oferuje wysoce skalowalną i samonaprawialną usługę hostowaną w Internecie.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="5e9f5-105">Ten samouczek pokazuje, jak toocreate PHP sieci web aplikacji na platformie Azure i podłącz go tooa baza danych MySQL.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-105">This tutorial shows how toocreate a PHP web app in Azure and connect it tooa MySQL database.</span></span> <span data-ttu-id="5e9f5-106">Po zakończeniu będziesz mieć [Laravel](https://laravel.com/) aplikacji uruchomionej na aplikacje sieci Web usługi aplikacji Azure.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-106">When you're finished, you'll have a [Laravel](https://laravel.com/) app running on Azure App Service Web Apps.</span></span>

![Aplikacja PHP działające w usłudze aplikacji Azure](./media/app-service-web-tutorial-php-mysql/complete-checkbox-published.png)

<span data-ttu-id="5e9f5-108">Ten samouczek zawiera informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="5e9f5-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5e9f5-109">Utwórz bazę danych MySQL na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="5e9f5-109">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="5e9f5-110">Połącz tooMySQL aplikacji PHP</span><span class="sxs-lookup"><span data-stu-id="5e9f5-110">Connect a PHP app tooMySQL</span></span>
> * <span data-ttu-id="5e9f5-111">Wdrażanie tooAzure aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="5e9f5-111">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="5e9f5-112">Aktualizacja modelu danych hello i wdrożenie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="5e9f5-112">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="5e9f5-113">Strumieniowe przesyłanie dzienników diagnostycznych z platformy Azure</span><span class="sxs-lookup"><span data-stu-id="5e9f5-113">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="5e9f5-114">Zarządzanie aplikacją hello w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="5e9f5-114">Manage hello app in hello Azure portal</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5e9f5-115">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5e9f5-115">Prerequisites</span></span>

<span data-ttu-id="5e9f5-116">toocomplete tego samouczka:</span><span class="sxs-lookup"><span data-stu-id="5e9f5-116">toocomplete this tutorial:</span></span>

* [<span data-ttu-id="5e9f5-117">Zainstaluj oprogramowanie Git</span><span class="sxs-lookup"><span data-stu-id="5e9f5-117">Install Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="5e9f5-118">Instalowanie języka PHP 5.6.4 lub nowszy</span><span class="sxs-lookup"><span data-stu-id="5e9f5-118">Install PHP 5.6.4 or above</span></span>](http://php.net/downloads.php)
* [<span data-ttu-id="5e9f5-119">Zainstaluj Composer</span><span class="sxs-lookup"><span data-stu-id="5e9f5-119">Install Composer</span></span>](https://getcomposer.org/doc/00-intro.md)
* <span data-ttu-id="5e9f5-120">Włącz następujące rozszerzenia PHP potrzeb Laravel hello: biblioteki OpenSSL, PDO MySQL, Mbstring, Tokenizatora, XML</span><span class="sxs-lookup"><span data-stu-id="5e9f5-120">Enable hello following PHP extensions Laravel needs: OpenSSL, PDO-MySQL, Mbstring, Tokenizer, XML</span></span>
* [<span data-ttu-id="5e9f5-121">Zainstaluj i uruchom MySQL</span><span class="sxs-lookup"><span data-stu-id="5e9f5-121">Install and start MySQL</span></span>](https://dev.mysql.com/doc/refman/5.7/en/installing.html) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prepare-local-mysql"></a><span data-ttu-id="5e9f5-122">Przygotowywanie lokalnej MySQL</span><span class="sxs-lookup"><span data-stu-id="5e9f5-122">Prepare local MySQL</span></span>

<span data-ttu-id="5e9f5-123">W tym kroku utworzysz bazę danych na lokalnym serwerze MySQL do użycia w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-123">In this step, you create a database in your local MySQL server for your use in this tutorial.</span></span>

### <a name="connect-toolocal-mysql-server"></a><span data-ttu-id="5e9f5-124">Połącz serwer MySQL toolocal</span><span class="sxs-lookup"><span data-stu-id="5e9f5-124">Connect toolocal MySQL server</span></span>

<span data-ttu-id="5e9f5-125">W oknie terminalu Połącz tooyour lokalny serwer MySQL.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-125">In a terminal window, connect tooyour local MySQL server.</span></span> <span data-ttu-id="5e9f5-126">Wszystkie polecenia hello toorun to okno terminalu można użyć w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-126">You can use this terminal window toorun all hello commands in this tutorial.</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="5e9f5-127">Jeśli zostanie wyświetlony monit o podanie hasła, wprowadź hasło hello hello `root` konta.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-127">If you're prompted for a password, enter hello password for hello `root` account.</span></span> <span data-ttu-id="5e9f5-128">Jeśli nie pamiętasz hasła do konta głównego, zobacz [MySQL: jak tooReset hello hasła użytkownika Root](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span><span class="sxs-lookup"><span data-stu-id="5e9f5-128">If you don't remember your root account password, see [MySQL: How tooReset hello Root Password](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span></span>

<span data-ttu-id="5e9f5-129">Jeśli polecenie zostanie wykonane pomyślnie, jest uruchomiony serwer MySQL.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-129">If your command runs successfully, then your MySQL server is running.</span></span> <span data-ttu-id="5e9f5-130">Jeśli nie, upewnij się, że serwera lokalnego MySQL została uruchomiona z następujących hello [MySQL poinstalacyjne czynności](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span><span class="sxs-lookup"><span data-stu-id="5e9f5-130">If not, make sure that your local MySQL server is started by following hello [MySQL post-installation steps](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span></span>

### <a name="create-a-database-locally"></a><span data-ttu-id="5e9f5-131">Utwórz bazę danych lokalnie</span><span class="sxs-lookup"><span data-stu-id="5e9f5-131">Create a database locally</span></span>

<span data-ttu-id="5e9f5-132">Na powitania `mysql` należy utworzyć bazę danych.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-132">At hello `mysql` prompt, create a database.</span></span>

```sql 
CREATE DATABASE sampledb;
```

<span data-ttu-id="5e9f5-133">Zakończyć połączenie z serwerem, wpisując `quit`.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-133">Exit your server connection by typing `quit`.</span></span>

```sql
quit
```

<a name="step2"></a>

## <a name="create-a-php-app-locally"></a><span data-ttu-id="5e9f5-134">Utwórz aplikację PHP lokalnie</span><span class="sxs-lookup"><span data-stu-id="5e9f5-134">Create a PHP app locally</span></span>
<span data-ttu-id="5e9f5-135">W tym kroku Pobierz przykładową aplikację Laravel, skonfiguruj połączenie bazy danych i uruchom lokalnie.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-135">In this step, you get a Laravel sample application, configure its database connection, and run it locally.</span></span> 

### <a name="clone-hello-sample"></a><span data-ttu-id="5e9f5-136">Przykład Witaj klonowania</span><span class="sxs-lookup"><span data-stu-id="5e9f5-136">Clone hello sample</span></span>

<span data-ttu-id="5e9f5-137">Okno terminalu hello `cd` tooa katalog roboczy.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-137">In hello terminal window, `cd` tooa working directory.</span></span>

<span data-ttu-id="5e9f5-138">Hello uruchom następujące polecenie tooclone hello próbki repozytorium.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-138">Run hello following command tooclone hello sample repository.</span></span>

```bash
git clone https://github.com/Azure-Samples/laravel-tasks
```

<span data-ttu-id="5e9f5-139">`cd`katalog sklonowany tooyour.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-139">`cd` tooyour cloned directory.</span></span>
<span data-ttu-id="5e9f5-140">Instalowanie pakietów hello wymagane.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-140">Install hello required packages.</span></span>

```bash
cd laravel-tasks
composer install
```

### <a name="configure-mysql-connection"></a><span data-ttu-id="5e9f5-141">Skonfiguruj połączenie MySQL</span><span class="sxs-lookup"><span data-stu-id="5e9f5-141">Configure MySQL connection</span></span>

<span data-ttu-id="5e9f5-142">W katalogu głównym repozytorium hello, Utwórz plik o nazwie *.env*.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-142">In hello repository root, create a file named *.env*.</span></span> <span data-ttu-id="5e9f5-143">Następujące zmienne do hello hello kopiowania *.env* pliku.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-143">Copy hello following variables into hello *.env* file.</span></span> <span data-ttu-id="5e9f5-144">Zastąp hello  _&lt;root_password >_ symbol zastępczy hello MySQL głównego hasła użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-144">Replace hello _&lt;root_password>_ placeholder with hello MySQL root user's password.</span></span>

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

<span data-ttu-id="5e9f5-145">Aby uzyskać informacje o używaniu hello Laravel _.env_ plików, zobacz [konfiguracji środowiska Laravel](https://laravel.com/docs/5.4/configuration#environment-configuration).</span><span class="sxs-lookup"><span data-stu-id="5e9f5-145">For information on how Laravel uses hello _.env_ file, see [Laravel Environment Configuration](https://laravel.com/docs/5.4/configuration#environment-configuration).</span></span>

### <a name="run-hello-sample-locally"></a><span data-ttu-id="5e9f5-146">Uruchamianie przykładowych hello lokalnie</span><span class="sxs-lookup"><span data-stu-id="5e9f5-146">Run hello sample locally</span></span>

<span data-ttu-id="5e9f5-147">Uruchom [Laravel bazy danych migracji](https://laravel.com/docs/5.4/migrations) toocreate hello tabele hello potrzeb aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-147">Run [Laravel database migrations](https://laravel.com/docs/5.4/migrations) toocreate hello tables hello application needs.</span></span> <span data-ttu-id="5e9f5-148">toosee tabel, które są tworzone w migracje hello poszukać w hello _bazy danych/migracje_ katalogu w repozytorium Git hello.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-148">toosee which tables are created in hello migrations, look in hello _database/migrations_ directory in hello Git repository.</span></span>

```bash
php artisan migrate
```

<span data-ttu-id="5e9f5-149">Wygeneruj nowy klucz aplikacji Laravel.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-149">Generate a new Laravel application key.</span></span>

```bash
php artisan key:generate
```

<span data-ttu-id="5e9f5-150">Uruchamianie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-150">Run hello application.</span></span>

```bash
php artisan serve
```

<span data-ttu-id="5e9f5-151">Przejdź do zbyt`http://localhost:8000` w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-151">Navigate too`http://localhost:8000` in a browser.</span></span> <span data-ttu-id="5e9f5-152">Dodać kilka zadań na stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-152">Add a few tasks in hello page.</span></span>

![PHP pomyślnie łączy tooMySQL](./media/app-service-web-tutorial-php-mysql/mysql-connect-success.png)

<span data-ttu-id="5e9f5-154">Wpisz toostop PHP, `Ctrl + C` w hello terminala.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-154">toostop PHP, type `Ctrl + C` in hello terminal.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-mysql-in-azure"></a><span data-ttu-id="5e9f5-155">Tworzenie MySQL na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="5e9f5-155">Create MySQL in Azure</span></span>

<span data-ttu-id="5e9f5-156">W tym kroku utworzysz bazę danych MySQL w [bazy danych Azure dla programu MySQL (wersja zapoznawcza)](/azure/mysql).</span><span class="sxs-lookup"><span data-stu-id="5e9f5-156">In this step, you create a MySQL database in [Azure Database for MySQL (Preview)](/azure/mysql).</span></span> <span data-ttu-id="5e9f5-157">Następnie należy skonfigurować hello PHP aplikacji tooconnect toothis bazy danych.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-157">Later, you configure hello PHP application tooconnect toothis database.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="5e9f5-158">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="5e9f5-158">Create a resource group</span></span>

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group-no-h.md)] 

### <a name="create-a-mysql-server"></a><span data-ttu-id="5e9f5-159">Utwórz serwer MySQL</span><span class="sxs-lookup"><span data-stu-id="5e9f5-159">Create a MySQL server</span></span>

<span data-ttu-id="5e9f5-160">Utwórz serwer bazy danych Azure dla programu MySQL (wersja zapoznawcza) z hello [utworzenie przez serwer mysql az](/cli/azure/mysql/server#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-160">Create a server in Azure Database for MySQL (Preview) with hello [az mysql server create](/cli/azure/mysql/server#create) command.</span></span>

<span data-ttu-id="5e9f5-161">W hello następujące polecenia, należy zastąpić nazwę serwera MySQL, w której występuje hello  _&lt;mysql_server_name >_ symbolu zastępczego (prawidłowe znaki to `a-z`, `0-9`, i `-`).</span><span class="sxs-lookup"><span data-stu-id="5e9f5-161">In hello following command, substitute your MySQL server name where you see hello _&lt;mysql_server_name>_ placeholder (valid characters are `a-z`, `0-9`, and `-`).</span></span> <span data-ttu-id="5e9f5-162">Ta nazwa jest częścią nazwy hosta serwera MySQL hello (`<mysql_server_name>.database.windows.net`), musi on toobe globalnie unikatowe.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-162">This name is part of hello MySQL server's hostname  (`<mysql_server_name>.database.windows.net`), it needs toobe globally unique.</span></span>

```azurecli-interactive
az mysql server create \
    --name <mysql_server_name> \
    --resource-group myResourceGroup \
    --location "North Europe" \
    --admin-user adminuser \
    --admin-password MySQLAzure2017
```

<span data-ttu-id="5e9f5-163">Po utworzeniu serwer MySQL hello hello Azure CLI pokazuje informacje toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="5e9f5-163">When hello MySQL server is created, hello Azure CLI shows information similar toohello following example:</span></span>

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

### <a name="configure-server-firewall"></a><span data-ttu-id="5e9f5-164">Konfigurowanie zapory serwera</span><span class="sxs-lookup"><span data-stu-id="5e9f5-164">Configure server firewall</span></span>

<span data-ttu-id="5e9f5-165">Tworzenie reguły zapory klienta MySQL serwera tooallow połączeń przy użyciu hello [az mysql reguły zapory serwera — Utwórz](/cli/azure/mysql/server/firewall-rule#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-165">Create a firewall rule for your MySQL server tooallow client connections by using hello [az mysql server firewall-rule create](/cli/azure/mysql/server/firewall-rule#create) command.</span></span>

```azurecli-interactive
az mysql server firewall-rule create \
    --name allIPs \
    --server <mysql_server_name> \
    --resource-group myResourceGroup \
    --start-ip-address 0.0.0.0 \
    --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="5e9f5-166">Bazy danych platformy Azure dla programu MySQL (wersja zapoznawcza) aktualnie nie ograniczyć zakres usług tooAzure tylko połączeń.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-166">Azure Database for MySQL (Preview) doesn't currently limit connections only tooAzure services.</span></span> <span data-ttu-id="5e9f5-167">Adresy IP na platformie Azure są przypisywane dynamicznie, jest lepsze tooenable wszystkich adresów IP.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-167">As IP addresses in Azure are dynamically assigned, it is better tooenable all IP addresses.</span></span> <span data-ttu-id="5e9f5-168">Usługa Hello jest w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-168">hello service is in preview.</span></span> <span data-ttu-id="5e9f5-169">Zaplanowano lepsze metody zabezpieczania bazy danych.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-169">Better methods for securing your database are planned.</span></span>
>
>

### <a name="connect-tooproduction-mysql-server-locally"></a><span data-ttu-id="5e9f5-170">Połącz serwer MySQL tooproduction lokalnie</span><span class="sxs-lookup"><span data-stu-id="5e9f5-170">Connect tooproduction MySQL server locally</span></span>

<span data-ttu-id="5e9f5-171">Okno terminalu hello połączyć toohello serwer MySQL na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-171">In hello terminal window, connect toohello MySQL server in Azure.</span></span> <span data-ttu-id="5e9f5-172">Użyj wartości hello wcześniej określona dla  _&lt;mysql_server_name >_.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-172">Use hello value you specified previously for _&lt;mysql_server_name>_.</span></span>

```bash
mysql -u adminuser@<mysql_server_name> -h <mysql_server_name>.database.windows.net -P 3306 -p
```

<span data-ttu-id="5e9f5-173">Po wyświetleniu monitu o podanie hasła, użyj _$tr0ngPa$ w0rd!_, określony podczas tworzenia hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-173">When prompted for a password, use _$tr0ngPa$w0rd!_, which you specified when you created hello database.</span></span>

### <a name="create-a-production-database"></a><span data-ttu-id="5e9f5-174">Utwórz bazę danych produkcyjnych</span><span class="sxs-lookup"><span data-stu-id="5e9f5-174">Create a production database</span></span>

<span data-ttu-id="5e9f5-175">Na powitania `mysql` należy utworzyć bazę danych.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-175">At hello `mysql` prompt, create a database.</span></span>

```sql
CREATE DATABASE sampledb;
```

### <a name="create-a-user-with-permissions"></a><span data-ttu-id="5e9f5-176">Utwórz użytkownika z uprawnieniami</span><span class="sxs-lookup"><span data-stu-id="5e9f5-176">Create a user with permissions</span></span>

<span data-ttu-id="5e9f5-177">Utwórz użytkownika bazy danych o nazwie _phpappuser_ i nadaj mu wszystkie uprawnienia w hello `sampledb` bazy danych.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-177">Create a database user called _phpappuser_ and give it all privileges in hello `sampledb` database.</span></span>

```sql
CREATE USER 'phpappuser' IDENTIFIED BY 'MySQLAzure2017'; 
GRANT ALL PRIVILEGES ON sampledb.* too'phpappuser';
```

<span data-ttu-id="5e9f5-178">Zakończyć połączenie z serwerem hello wpisując `quit`.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-178">Exit hello server connection by typing `quit`.</span></span>

```sql
quit
```

## <a name="connect-app-tooazure-mysql"></a><span data-ttu-id="5e9f5-179">Łączenie aplikacji tooAzure MySQL</span><span class="sxs-lookup"><span data-stu-id="5e9f5-179">Connect app tooAzure MySQL</span></span>

<span data-ttu-id="5e9f5-180">W tym kroku łączysz hello PHP aplikacji toohello baza danych MySQL utworzonej w bazie danych Azure dla programu MySQL (wersja zapoznawcza).</span><span class="sxs-lookup"><span data-stu-id="5e9f5-180">In this step, you connect hello PHP application toohello MySQL database you created in Azure Database for MySQL (Preview).</span></span>

<a name="devconfig"></a>

### <a name="configure-hello-database-connection"></a><span data-ttu-id="5e9f5-181">Skonfiguruj połączenie bazy danych hello</span><span class="sxs-lookup"><span data-stu-id="5e9f5-181">Configure hello database connection</span></span>

<span data-ttu-id="5e9f5-182">W katalogu głównym repozytorium hello, Utwórz _. env.production_ hello plik i skopiuj następujące zmienne do niego.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-182">In hello repository root, create an _.env.production_ file and copy hello following variables into it.</span></span> <span data-ttu-id="5e9f5-183">Zastąp symbol zastępczy hello  _&lt;mysql_server_name >_.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-183">Replace hello placeholder _&lt;mysql_server_name>_.</span></span>

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

<span data-ttu-id="5e9f5-184">Zapisz zmiany hello.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-184">Save hello changes.</span></span>

> [!TIP]
> <span data-ttu-id="5e9f5-185">toosecure MySQL informacje o połączeniu, ten plik jest już wykluczone z repozytorium Git hello (zobacz _.gitignore_ w katalogu głównym repozytorium hello).</span><span class="sxs-lookup"><span data-stu-id="5e9f5-185">toosecure your MySQL connection information, this file is already excluded from hello Git repository (See _.gitignore_ in hello repository root).</span></span> <span data-ttu-id="5e9f5-186">Później możesz dowiedzieć się, jak tooconfigure zmienne środowiskowe w tooyour tooconnect usługi aplikacji bazy danych w bazie danych Azure dla programu MySQL (wersja zapoznawcza).</span><span class="sxs-lookup"><span data-stu-id="5e9f5-186">Later, you learn how tooconfigure environment variables in App Service tooconnect tooyour database in Azure Database for MySQL (Preview).</span></span> <span data-ttu-id="5e9f5-187">Zmienne środowiskowe nie wymagają hello *.env* pliku w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-187">With environment variables, you don't need hello *.env* file in App Service.</span></span>
>

### <a name="configure-ssl-certificate"></a><span data-ttu-id="5e9f5-188">Konfigurowanie certyfikatu protokołu SSL</span><span class="sxs-lookup"><span data-stu-id="5e9f5-188">Configure SSL certificate</span></span>

<span data-ttu-id="5e9f5-189">Domyślnie baza danych Azure dla programu MySQL wymusza połączenia SSL od klientów.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-189">By default, Azure Database for MySQL enforces SSL connections from clients.</span></span> <span data-ttu-id="5e9f5-190">tooconnect tooyour bazy danych MySQL na platformie Azure, należy użyć _PEM_ certyfikatu SSL.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-190">tooconnect tooyour MySQL database in Azure, you must use a _.pem_ SSL certificate.</span></span>

<span data-ttu-id="5e9f5-191">Otwórz _config/database.php_ i Dodaj hello _sslmode_ i _opcje_ parametry zbyt`connections.mysql`, jak pokazano w hello następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-191">Open _config/database.php_ and add hello _sslmode_ and _options_ parameters too`connections.mysql`, as shown in hello following code.</span></span>

```php
'mysql' => [
    ...
    'sslmode' => env('DB_SSLMODE', 'prefer'),
    'options' => (env('MYSQL_SSL')) ? [
        PDO::MYSQL_ATTR_SSL_KEY    => '/ssl/certificate.pem', 
    ] : []
],
```

<span data-ttu-id="5e9f5-192">toolearn jak toogenerate to _certificate.pem_, zobacz [łączności Konfigurowanie protokołu SSL w Twojej aplikacji toosecurely połączyć tooAzure bazy danych MySQL](../mysql/howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="5e9f5-192">toolearn how toogenerate this _certificate.pem_, see [Configure SSL connectivity in your application toosecurely connect tooAzure Database for MySQL](../mysql/howto-configure-ssl.md).</span></span>

> [!TIP]
> <span data-ttu-id="5e9f5-193">Ścieżka Hello _/ssl/certificate.pem_ wskazuje istniejący tooan _certificate.pem_ plik w repozytorium Git hello.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-193">hello path _/ssl/certificate.pem_ points tooan existing _certificate.pem_ file in hello Git repository.</span></span> <span data-ttu-id="5e9f5-194">Ten plik jest dostarczany jako udogodnienie, w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-194">This file is provided for convenience in this tutorial.</span></span> <span data-ttu-id="5e9f5-195">Ze względów, nie należy zatwierdzić Twoje _PEM_ certyfikatów do kontroli źródła.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-195">For best practice, you should not commit your _.pem_ certificates into source control.</span></span> 
>

### <a name="test-hello-application-locally"></a><span data-ttu-id="5e9f5-196">Testowanie aplikacji hello lokalnie</span><span class="sxs-lookup"><span data-stu-id="5e9f5-196">Test hello application locally</span></span>

<span data-ttu-id="5e9f5-197">Uruchom Laravel migracji bazy danych z _. env.production_ jako hello środowiska pliku toocreate hello tabel bazy danych MySQL w bazie danych Azure dla programu MySQL (wersja zapoznawcza).</span><span class="sxs-lookup"><span data-stu-id="5e9f5-197">Run Laravel database migrations with _.env.production_ as hello environment file toocreate hello tables in your MySQL database in Azure Database for MySQL (Preview).</span></span> <span data-ttu-id="5e9f5-198">Należy pamiętać, że _. env.production_ ma hello połączenia informacji tooyour baza danych MySQL na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-198">Remember that _.env.production_ has hello connection information tooyour MySQL database in Azure.</span></span>

```bash
php artisan migrate --env=production --force
```

<span data-ttu-id="5e9f5-199">_. env.production_ nie ma jeszcze klucza prawidłową aplikację.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-199">_.env.production_ doesn't have a valid application key yet.</span></span> <span data-ttu-id="5e9f5-200">Generuj nową dla niego w hello terminala.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-200">Generate a new one for it in hello terminal.</span></span>

```bash
php artisan key:generate --env=production --force
```

<span data-ttu-id="5e9f5-201">Uruchom hello przykładową aplikację z _. env.production_ hello środowiska pliku.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-201">Run hello sample application with _.env.production_ as hello environment file.</span></span>

```bash
php artisan serve --env=production
```

<span data-ttu-id="5e9f5-202">Przejdź do zbyt`http://localhost:8000`.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-202">Navigate too`http://localhost:8000`.</span></span> <span data-ttu-id="5e9f5-203">Jeśli strona hello ładuje bez błędów, hello aplikacji PHP łączy toohello baza danych MySQL na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-203">If hello page loads without errors, hello PHP application is connecting toohello MySQL database in Azure.</span></span>

<span data-ttu-id="5e9f5-204">Dodać kilka zadań na stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-204">Add a few tasks in hello page.</span></span>

![PHP pomyślnie łączy tooAzure bazy danych dla programu MySQL (wersja zapoznawcza)](./media/app-service-web-tutorial-php-mysql/mysql-connect-success.png)

<span data-ttu-id="5e9f5-206">Wpisz toostop PHP, `Ctrl + C` w hello terminala.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-206">toostop PHP, type `Ctrl + C` in hello terminal.</span></span>

### <a name="commit-your-changes"></a><span data-ttu-id="5e9f5-207">Zatwierdź zmiany</span><span class="sxs-lookup"><span data-stu-id="5e9f5-207">Commit your changes</span></span>

<span data-ttu-id="5e9f5-208">Uruchom hello toocommit polecenia Git następujące zmiany:</span><span class="sxs-lookup"><span data-stu-id="5e9f5-208">Run hello following Git commands toocommit your changes:</span></span>

```bash
git add .
git commit -m "database.php updates"
```

<span data-ttu-id="5e9f5-209">Aplikacja jest gotowa toobe wdrożone.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-209">Your app is ready toobe deployed.</span></span>

## <a name="deploy-tooazure"></a><span data-ttu-id="5e9f5-210">Wdrażanie tooAzure</span><span class="sxs-lookup"><span data-stu-id="5e9f5-210">Deploy tooAzure</span></span>

<span data-ttu-id="5e9f5-211">W tym kroku możesz wdrożyć tooAzure aplikacji PHP, MySQL, połączone hello usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-211">In this step, you deploy hello MySQL-connected PHP application tooAzure App Service.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="5e9f5-212">Tworzenie planu usługi App Service</span><span class="sxs-lookup"><span data-stu-id="5e9f5-212">Create an App Service plan</span></span>

[!INCLUDE [Create app service plan no h](../../includes/app-service-web-create-app-service-plan-no-h.md)]

### <a name="create-a-web-app"></a><span data-ttu-id="5e9f5-213">Tworzenie aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="5e9f5-213">Create a web app</span></span>

[!INCLUDE [Create web app no h](../../includes/app-service-web-create-web-app-no-h.md)]

### <a name="set-hello-php-version"></a><span data-ttu-id="5e9f5-214">Ustaw wersję PHP hello</span><span class="sxs-lookup"><span data-stu-id="5e9f5-214">Set hello PHP version</span></span>

<span data-ttu-id="5e9f5-215">Wersję PHP hello zestaw aplikacji hello wymaga przy użyciu hello [zestaw konfiguracyjny aplikacji sieci Web az](/cli/azure/webapp/config#set) polecenia.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-215">Set hello PHP version that hello application requires by using hello [az webapp config set](/cli/azure/webapp/config#set) command.</span></span>

<span data-ttu-id="5e9f5-216">Witaj poniższe polecenie ustawia too_7.0_ wersji PHP hello.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-216">hello following command sets hello PHP version too_7.0_.</span></span>

```azurecli-interactive
az webapp config set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --php-version 7.0
```

### <a name="configure-database-settings"></a><span data-ttu-id="5e9f5-217">Konfigurowanie ustawień bazy danych</span><span class="sxs-lookup"><span data-stu-id="5e9f5-217">Configure database settings</span></span>

<span data-ttu-id="5e9f5-218">Jak wskazano wcześniej, można połączyć z bazy danych MySQL na platformie Azure tooyour zmiennych środowiskowych przy użyciu aplikacji usługi.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-218">As pointed out previously, you can connect tooyour Azure MySQL database using environment variables in App Service.</span></span>

<span data-ttu-id="5e9f5-219">W usłudze App Service można ustawić zmienne środowiskowe jako _ustawień aplikacji_ przy użyciu hello [az aplikacji sieci Web config appsettings zestaw](/cli/azure/webapp/config/appsettings#set) polecenia.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-219">In App Service, you set environment variables as _app settings_ by using hello [az webapp config appsettings set](/cli/azure/webapp/config/appsettings#set) command.</span></span>

<span data-ttu-id="5e9f5-220">Witaj następujące polecenie konfiguruje ustawienia aplikacji hello `DB_HOST`, `DB_DATABASE`, `DB_USERNAME`, i `DB_PASSWORD`.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-220">hello following command configures hello app settings `DB_HOST`, `DB_DATABASE`, `DB_USERNAME`, and `DB_PASSWORD`.</span></span> <span data-ttu-id="5e9f5-221">Zastąp symbole zastępcze hello  _&lt;nazwa_aplikacji >_ i  _&lt;mysql_server_name >_.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-221">Replace hello placeholders _&lt;appname>_ and _&lt;mysql_server_name>_.</span></span>

```azurecli-interactive
az webapp config appsettings set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings DB_HOST="<mysql_server_name>.database.windows.net" DB_DATABASE="sampledb" DB_USERNAME="phpappuser@<mysql_server_name>" DB_PASSWORD="MySQLAzure2017" MYSQL_SSL="true"
```

<span data-ttu-id="5e9f5-222">Można użyć hello PHP [getenv —](http://www.php.net/manual/function.getenv.php) tooaccess metody hello ustawienia.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-222">You can use hello PHP [getenv](http://www.php.net/manual/function.getenv.php) method tooaccess hello settings.</span></span> <span data-ttu-id="5e9f5-223">używa Hello kodu Laravel [env](https://laravel.com/docs/5.4/helpers#method-env) otoki za pośrednictwem hello PHP `getenv`.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-223">hello Laravel code uses an [env](https://laravel.com/docs/5.4/helpers#method-env) wrapper over hello PHP `getenv`.</span></span> <span data-ttu-id="5e9f5-224">Na przykład hello MySQL konfiguracji w _config/database.php_ wygląda hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="5e9f5-224">For example, hello MySQL configuration in _config/database.php_ looks like hello following code:</span></span>

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

### <a name="configure-laravel-environment-variables"></a><span data-ttu-id="5e9f5-225">Skonfiguruj Laravel zmienne środowiskowe</span><span class="sxs-lookup"><span data-stu-id="5e9f5-225">Configure Laravel environment variables</span></span>

<span data-ttu-id="5e9f5-226">Laravel musi mieć klucz aplikacji w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-226">Laravel needs an application key in App Service.</span></span> <span data-ttu-id="5e9f5-227">Możesz ją skonfigurować z ustawieniami aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-227">You can configure it with app settings.</span></span>

<span data-ttu-id="5e9f5-228">Użyj `php artisan` toogenerate nowy klucz aplikacji bez jej zapisania too_.env_.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-228">Use `php artisan` toogenerate a new application key without saving it too_.env_.</span></span>

```bash
php artisan key:generate --show
```

<span data-ttu-id="5e9f5-229">Ustawić klucz aplikacji hello w hello aplikację usługi aplikacji sieci web przy użyciu hello [az aplikacji sieci Web config appsettings zestaw](/cli/azure/webapp/config/appsettings#set) polecenia.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-229">Set hello application key in hello App Service web app by using hello [az webapp config appsettings set](/cli/azure/webapp/config/appsettings#set) command.</span></span> <span data-ttu-id="5e9f5-230">Zastąp symbole zastępcze hello  _&lt;nazwa_aplikacji >_ i  _&lt;outputofphpartisankey: generowanie >_.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-230">Replace hello placeholders _&lt;appname>_ and _&lt;outputofphpartisankey:generate>_.</span></span>

```azurecli-interactive
az webapp config appsettings set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings APP_KEY="<output_of_php_artisan_key:generate>" APP_DEBUG="true"
```

<span data-ttu-id="5e9f5-231">`APP_DEBUG="true"`informuje, że Laravel tooreturn informacje o debugowaniu podczas hello wdrażania aplikacji sieci web wystąpią błędy.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-231">`APP_DEBUG="true"` tells Laravel tooreturn debugging information when hello deployed web app encounters errors.</span></span> <span data-ttu-id="5e9f5-232">Podczas uruchamiania aplikacji produkcyjnych, ustaw go za`false`, który jest bardziej bezpieczne.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-232">When running a production application, set it too`false`, which is more secure.</span></span>

### <a name="set-hello-virtual-application-path"></a><span data-ttu-id="5e9f5-233">Ścieżka aplikacji wirtualnej hello zestawu</span><span class="sxs-lookup"><span data-stu-id="5e9f5-233">Set hello virtual application path</span></span>

<span data-ttu-id="5e9f5-234">Ustaw ścieżkę aplikacji wirtualnej hello hello aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-234">Set hello virtual application path for hello web app.</span></span> <span data-ttu-id="5e9f5-235">Ten krok jest wymagany, ponieważ hello [cyklem życia aplikacji Laravel](https://laravel.com/docs/5.4/lifecycle) rozpoczyna się w hello _publicznego_ katalogu zamiast katalog główny aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-235">This step is required because hello [Laravel application lifecycle](https://laravel.com/docs/5.4/lifecycle) begins in hello _public_ directory instead of hello application's root directory.</span></span> <span data-ttu-id="5e9f5-236">Innych platform PHP, na których cyklu życia start w katalogu głównym hello może działać bez ręcznej konfiguracji hello ścieżkę aplikacji wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-236">Other PHP frameworks whose lifecycle start in hello root directory can work without manual configuration of hello virtual application path.</span></span>

<span data-ttu-id="5e9f5-237">Ścieżka aplikacji wirtualnej hello zestawu przy użyciu hello [aktualizacja zasobu az](/cli/azure/resource#update) polecenia.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-237">Set hello virtual application path by using hello [az resource update](/cli/azure/resource#update) command.</span></span> <span data-ttu-id="5e9f5-238">Zastąp hello  _&lt;nazwa_aplikacji >_ symbolu zastępczego.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-238">Replace hello _&lt;appname>_ placeholder.</span></span>

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

<span data-ttu-id="5e9f5-239">Domyślnie usługi Azure App Service punktów ścieżki aplikacji wirtualnej katalogu głównego hello (_/_) katalog główny toohello hello wdrażane pliki aplikacji (_sites\wwwroot_).</span><span class="sxs-lookup"><span data-stu-id="5e9f5-239">By default, Azure App Service points hello root virtual application path (_/_) toohello root directory of hello deployed application files (_sites\wwwroot_).</span></span>

### <a name="configure-a-deployment-user"></a><span data-ttu-id="5e9f5-240">Konfigurowanie użytkownika wdrożenia</span><span class="sxs-lookup"><span data-stu-id="5e9f5-240">Configure a deployment user</span></span>

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user-no-h.md)]

### <a name="configure-local-git-deployment"></a><span data-ttu-id="5e9f5-241">Konfigurowanie lokalnego wdrożenia narzędzia Git</span><span class="sxs-lookup"><span data-stu-id="5e9f5-241">Configure local Git deployment</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git-no-h.md)]

### <a name="push-tooazure-from-git"></a><span data-ttu-id="5e9f5-242">Wypychać tooAzure za pomocą narzędzia Git</span><span class="sxs-lookup"><span data-stu-id="5e9f5-242">Push tooAzure from Git</span></span>

<span data-ttu-id="5e9f5-243">Dodaj Azure tooyour zdalnego lokalnego repozytorium Git.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-243">Add an Azure remote tooyour local Git repository.</span></span>

```bash
git remote add azure <paste_copied_url_here>
```

<span data-ttu-id="5e9f5-244">Wypchnij aplikacji PHP hello Azure toodeploy zdalnego toohello.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-244">Push toohello Azure remote toodeploy hello PHP application.</span></span> <span data-ttu-id="5e9f5-245">Zostanie wyświetlony monit o hello hasło wcześniej w ramach tworzenia hello hello wdrożenia użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-245">You are prompted for hello password you supplied earlier as part of hello creation of hello deployment user.</span></span>

```bash
git push azure master
```

<span data-ttu-id="5e9f5-246">Podczas wdrażania usługi Azure App Service komunikuje się postęp za pomocą narzędzia Git.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-246">During deployment, Azure App Service communicates its progress with Git.</span></span>

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
> <span data-ttu-id="5e9f5-247">Można zauważyć, że proces wdrażania hello instaluje [Composer](https://getcomposer.org/) pakietów na końcu hello.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-247">You may notice that hello deployment process installs [Composer](https://getcomposer.org/) packages at hello end.</span></span> <span data-ttu-id="5e9f5-248">Usługi aplikacji nie są uruchamiane te automatyzacji podczas wdrażania domyślne, tak to repozytorium przykładowej ma trzy dodatkowe plików w jego tooenable katalogu głównego:</span><span class="sxs-lookup"><span data-stu-id="5e9f5-248">App Service does not run these automations during default deployment, so this sample repository has three additional files in its root directory tooenable it:</span></span>
>
> - <span data-ttu-id="5e9f5-249">`.deployment`— Ten plik zawiera toorun usługi aplikacji `bash deploy.sh` jako hello niestandardowe wdrożenie skryptu.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-249">`.deployment` - This file tells App Service toorun `bash deploy.sh` as hello custom deployment script.</span></span>
> - <span data-ttu-id="5e9f5-250">`deploy.sh`-hello niestandardowe wdrożenie skryptu.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-250">`deploy.sh` - hello custom deployment script.</span></span> <span data-ttu-id="5e9f5-251">Jeśli możesz przejrzeć plik hello, zobaczysz, że działa `php composer.phar install` po `npm install`.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-251">If you review hello file, you will see that it runs `php composer.phar install` after `npm install`.</span></span>
> - <span data-ttu-id="5e9f5-252">`composer.phar`-Menedżera pakietów hello Composer.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-252">`composer.phar` - hello Composer package manager.</span></span>
>
> <span data-ttu-id="5e9f5-253">Tooadd tej metody można użyć dowolnego kroku tooyour wdrożenia na podstawie Git tooApp usługi.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-253">You can use this approach tooadd any step tooyour Git-based deployment tooApp Service.</span></span> <span data-ttu-id="5e9f5-254">Aby uzyskać więcej informacji, zobacz [niestandardowego skryptu wdrażania](https://github.com/projectkudu/kudu/wiki/Custom-Deployment-Script).</span><span class="sxs-lookup"><span data-stu-id="5e9f5-254">For more information, see [Custom Deployment Script](https://github.com/projectkudu/kudu/wiki/Custom-Deployment-Script).</span></span>
>

### <a name="browse-toohello-azure-web-app"></a><span data-ttu-id="5e9f5-255">Przeglądaj toohello aplikacji sieci web Azure</span><span class="sxs-lookup"><span data-stu-id="5e9f5-255">Browse toohello Azure web app</span></span>

<span data-ttu-id="5e9f5-256">Przeglądaj zbyt`http://<app_name>.azurewebsites.net` i dodaj kilka zadań toohello listy.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-256">Browse too`http://<app_name>.azurewebsites.net` and add a few tasks toohello list.</span></span>

![Aplikacja PHP działające w usłudze aplikacji Azure](./media/app-service-web-tutorial-php-mysql/php-mysql-in-azure.png)

<span data-ttu-id="5e9f5-258">Gratulacje, używasz aplikacji PHP sieci opartych na danych w usłudze Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-258">Congratulations, you're running a data-driven PHP app in Azure App Service.</span></span>

## <a name="update-model-locally-and-redeploy"></a><span data-ttu-id="5e9f5-259">Aktualizuj model lokalnie i wdrożenie</span><span class="sxs-lookup"><span data-stu-id="5e9f5-259">Update model locally and redeploy</span></span>

<span data-ttu-id="5e9f5-260">W tym kroku należy toohello prosta zmiana `task` modelu danych i hello aplikacji sieci Web, a następnie opublikuj hello tooAzure aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-260">In this step, you make a simple change toohello `task` data model and hello webapp, and then publish hello update tooAzure.</span></span>

<span data-ttu-id="5e9f5-261">W scenariuszu hello zadania możesz zmodyfikować aplikacji hello tak, aby oznaczyć zadanie jako ukończone.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-261">For hello tasks scenario, you modify hello application so that you can mark a task as complete.</span></span>

### <a name="add-a-column"></a><span data-ttu-id="5e9f5-262">Dodaj kolumnę</span><span class="sxs-lookup"><span data-stu-id="5e9f5-262">Add a column</span></span>

<span data-ttu-id="5e9f5-263">W terminalu hello Przejdź toohello katalogu głównego repozytorium Git hello.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-263">In hello terminal, navigate toohello root of hello Git repository.</span></span>

<span data-ttu-id="5e9f5-264">Generuj nowe migracja bazy danych dla hello `tasks` tabeli:</span><span class="sxs-lookup"><span data-stu-id="5e9f5-264">Generate a new database migration for hello `tasks` table:</span></span>

```bash
php artisan make:migration add_complete_column --table=tasks
```

<span data-ttu-id="5e9f5-265">To polecenie zawiera hello nazwę hello migracji pliku, który zostanie wygenerowany.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-265">This command shows you hello name of hello migration file that's generated.</span></span> <span data-ttu-id="5e9f5-266">Ten plik w _bazy danych/migracje_ i otwórz go.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-266">Find this file in _database/migrations_ and open it.</span></span>

<span data-ttu-id="5e9f5-267">Zastąp hello `up` metody z hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="5e9f5-267">Replace hello `up` method with hello following code:</span></span>

```php
public function up()
{
    Schema::table('tasks', function (Blueprint $table) {
        $table->boolean('complete')->default(False);
    });
}
```

<span data-ttu-id="5e9f5-268">Witaj poprzedni kod dodaje logiczna kolumnę w hello `tasks` tabeli o nazwie `complete`.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-268">hello preceding code adds a boolean column in hello `tasks` table called `complete`.</span></span>

<span data-ttu-id="5e9f5-269">Zastąp hello `down` metody za pomocą następującego kodu dla akcji wycofywania hello hello:</span><span class="sxs-lookup"><span data-stu-id="5e9f5-269">Replace hello `down` method with hello following code for hello rollback action:</span></span>

```php
public function down()
{
    Schema::table('tasks', function (Blueprint $table) {
        $table->dropColumn('complete');
    });
}
```

<span data-ttu-id="5e9f5-270">W terminalu hello Uruchom Laravel bazy danych migracji toomake hello zmiany w lokalnej bazie danych hello.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-270">In hello terminal, run Laravel database migrations toomake hello change in hello local database.</span></span>

```bash
php artisan migrate
```

<span data-ttu-id="5e9f5-271">Oparte na powitania [konwencji nazewnictwa Laravel](https://laravel.com/docs/5.4/eloquent#defining-models), hello model `Task` (zobacz _app/Task.php_) mapuje toohello `tasks` tabeli domyślnie.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-271">Based on hello [Laravel naming convention](https://laravel.com/docs/5.4/eloquent#defining-models), hello model `Task` (see _app/Task.php_) maps toohello `tasks` table by default.</span></span>

### <a name="update-application-logic"></a><span data-ttu-id="5e9f5-272">Aktualizowanie aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="5e9f5-272">Update application logic</span></span>

<span data-ttu-id="5e9f5-273">Otwórz hello *routes/web.php* pliku.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-273">Open hello *routes/web.php* file.</span></span> <span data-ttu-id="5e9f5-274">definiuje aplikacja Hello jego tras i logiki biznesowej w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-274">hello application defines its routes and business logic here.</span></span>

<span data-ttu-id="5e9f5-275">Na końcu hello hello pliku należy dodać trasę z hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="5e9f5-275">At hello end of hello file, add a route with hello following code:</span></span>

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

<span data-ttu-id="5e9f5-276">Witaj poprzedni kod sprawia, że model danych toohello proste aktualizacji przełączając wartość hello `complete`.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-276">hello preceding code makes a simple update toohello data model by toggling hello value of `complete`.</span></span>

### <a name="update-hello-view"></a><span data-ttu-id="5e9f5-277">Widok hello aktualizacji</span><span class="sxs-lookup"><span data-stu-id="5e9f5-277">Update hello view</span></span>

<span data-ttu-id="5e9f5-278">Otwórz hello *resources/views/tasks.blade.php* pliku.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-278">Open hello *resources/views/tasks.blade.php* file.</span></span> <span data-ttu-id="5e9f5-279">Znajdź hello `<tr>` tagu początkowego i zastąpić go ciągiem:</span><span class="sxs-lookup"><span data-stu-id="5e9f5-279">Find hello `<tr>` opening tag and replace it with:</span></span>

```html
<tr class="{{ $task->complete ? 'success' : 'active' }}" >
```

<span data-ttu-id="5e9f5-280">Witaj poprzedzających kolor wiersza hello zmian kodu w zależności od tego, czy hello zadanie zostało ukończone.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-280">hello preceding code changes hello row color depending on whether hello task is complete.</span></span>

<span data-ttu-id="5e9f5-281">W następnym wierszu hello masz hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="5e9f5-281">In hello next line, you have hello following code:</span></span>

```html
<td class="table-text"><div>{{ $task->name }}</div></td>
```

<span data-ttu-id="5e9f5-282">Zastąp cały wiersz hello hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="5e9f5-282">Replace hello entire line with hello following code:</span></span>

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

<span data-ttu-id="5e9f5-283">Witaj poprzedni kod dodaje przycisk przesyłania hello odwołuje się do trasy hello, wcześniej zdefiniowany.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-283">hello preceding code adds hello submit button that references hello route that you defined earlier.</span></span>

### <a name="test-hello-changes-locally"></a><span data-ttu-id="5e9f5-284">Test hello zmiany lokalnie</span><span class="sxs-lookup"><span data-stu-id="5e9f5-284">Test hello changes locally</span></span>

<span data-ttu-id="5e9f5-285">Z katalogu głównego repozytorium Git hello hello należy uruchomić serwera wdrożeniowego hello.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-285">From hello root directory of hello Git repository, run hello development server.</span></span>

```bash
php artisan serve
```

<span data-ttu-id="5e9f5-286">Witaj toosee zmiana stanu zadania, przejdź zbyt`http://localhost:8000` i hello zaznacz pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-286">toosee hello task status change, navigate too`http://localhost:8000` and select hello checkbox.</span></span>

![Dodano pola wyboru tootask](./media/app-service-web-tutorial-php-mysql/complete-checkbox.png)

<span data-ttu-id="5e9f5-288">Wpisz toostop PHP, `Ctrl + C` w hello terminala.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-288">toostop PHP, type `Ctrl + C` in hello terminal.</span></span>

### <a name="publish-changes-tooazure"></a><span data-ttu-id="5e9f5-289">Publikowanie zmian tooAzure</span><span class="sxs-lookup"><span data-stu-id="5e9f5-289">Publish changes tooAzure</span></span>

<span data-ttu-id="5e9f5-290">W terminalu hello Uruchom Laravel bazy danych migracji hello produkcji połączenia ciąg toomake hello zmiany hello Azure bazy danych.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-290">In hello terminal, run Laravel database migrations with hello production connection string toomake hello change in hello Azure database.</span></span>

```bash
php artisan migrate --env=production --force
```

<span data-ttu-id="5e9f5-291">Przekaż wszystkie zmiany hello w usłudze Git, a następnie Wypchnij tooAzure zmiany kodu hello.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-291">Commit all hello changes in Git, and then push hello code changes tooAzure.</span></span>

```bash
git add .
git commit -m "added complete checkbox"
git push azure master
```

<span data-ttu-id="5e9f5-292">Raz hello `git push` jest wykonać kolejno toohello sieci web platformy Azure aplikacji i testowania hello nowych funkcji.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-292">Once hello `git push` is complete, navigate toohello Azure web app and test hello new functionality.</span></span>

![Zmiany modelu i bazy danych publikowanych tooAzure](media/app-service-web-tutorial-php-mysql/complete-checkbox-published.png)

<span data-ttu-id="5e9f5-294">Jeśli dodano żadnych zadań, są one przechowywane w bazie danych hello.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-294">If you added any tasks, they are retained in hello database.</span></span> <span data-ttu-id="5e9f5-295">Schemat danych toohello aktualizacje pozostawić istniejące dane bez zmian.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-295">Updates toohello data schema leave existing data intact.</span></span>

## <a name="stream-diagnostic-logs"></a><span data-ttu-id="5e9f5-296">Dzienniki diagnostyczne strumienia</span><span class="sxs-lookup"><span data-stu-id="5e9f5-296">Stream diagnostic logs</span></span>

<span data-ttu-id="5e9f5-297">Podczas wykonywania hello aplikacji PHP w usłudze Azure App Service można uzyskać tooyour gazociągami dzienniki konsoli hello terminala.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-297">While hello PHP application runs in Azure App Service, you can get hello console logs piped tooyour terminal.</span></span> <span data-ttu-id="5e9f5-298">W ten sposób można uzyskać hello tego samego komunikaty diagnostyczne toohelp Debugowanie błędów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-298">That way, you can get hello same diagnostic messages toohelp you debug application errors.</span></span>

<span data-ttu-id="5e9f5-299">Dziennik toostart przesyłania strumieniowego, użyj hello [końcowego fragmentu dziennika aplikacji sieci Web az](/cli/azure/webapp/log#tail) polecenia.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-299">toostart log streaming, use hello [az webapp log tail](/cli/azure/webapp/log#tail) command.</span></span>

```azurecli-interactive
az webapp log tail \
    --name <app_name> \
    --resource-group myResourceGroup
```

<span data-ttu-id="5e9f5-300">Po rozpoczęciu przesyłania strumieniowego dzienników Odśwież hello aplikacji sieci web platformy Azure w tooget przeglądarki hello część ruchu w sieci web.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-300">Once log streaming has started, refresh hello Azure web app in hello browser tooget some web traffic.</span></span> <span data-ttu-id="5e9f5-301">Możesz teraz przeglądać terminal gazociągami toohello dzienniki konsoli.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-301">You can now see console logs piped toohello terminal.</span></span> <span data-ttu-id="5e9f5-302">Jeśli nie widzisz natychmiast dzienniki konsoli, sprawdź ponownie w ciągu 30 sekund.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-302">If you don't see console logs immediately, check again in 30 seconds.</span></span>

<span data-ttu-id="5e9f5-303">Dziennik toostop przesyłania strumieniowego w dowolnym momencie, typ `Ctrl` + `C`.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-303">toostop log streaming at anytime, type `Ctrl`+`C`.</span></span>

> [!TIP]
> <span data-ttu-id="5e9f5-304">Aplikacja PHP można użyć standardowego hello [error_log()](http://php.net/manual/function.error-log.php) toooutput toohello konsoli.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-304">A PHP application can use hello standard [error_log()](http://php.net/manual/function.error-log.php) toooutput toohello console.</span></span> <span data-ttu-id="5e9f5-305">Witaj Przykładowa aplikacja korzysta z tej metody w _app/Http/routes.php_.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-305">hello sample application uses this approach in _app/Http/routes.php_.</span></span>
>
> <span data-ttu-id="5e9f5-306">Jako platforma sieci web [Laravel używa Monolog](https://laravel.com/docs/5.4/errors) jako hello rejestrowanie dostawcy.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-306">As a web framework, [Laravel uses Monolog](https://laravel.com/docs/5.4/errors) as hello logging provider.</span></span> <span data-ttu-id="5e9f5-307">toosee tooget Monolog toooutput wiadomości toohello konsoli, zobacz [PHP: jak toouse monolog tooconsole toolog (php://out)](http://stackoverflow.com/questions/25787258/php-how-to-use-monolog-to-log-to-console-php-out).</span><span class="sxs-lookup"><span data-stu-id="5e9f5-307">toosee how tooget Monolog toooutput messages toohello console, see [PHP: How toouse monolog toolog tooconsole (php://out)](http://stackoverflow.com/questions/25787258/php-how-to-use-monolog-to-log-to-console-php-out).</span></span>
>
>

## <a name="manage-hello-azure-web-app"></a><span data-ttu-id="5e9f5-308">Zarządzanie hello aplikacji sieci web platformy Azure</span><span class="sxs-lookup"><span data-stu-id="5e9f5-308">Manage hello Azure web app</span></span>

<span data-ttu-id="5e9f5-309">Przejdź toohello [portalu Azure](https://portal.azure.com) aplikacji sieci web hello toomanage został utworzony.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-309">Go toohello [Azure portal](https://portal.azure.com) toomanage hello web app you created.</span></span>

<span data-ttu-id="5e9f5-310">W menu po lewej stronie powitania kliknij **usługi aplikacji**, a następnie kliknij nazwę hello aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-310">From hello left menu, click **App Services**, and then click hello name of your Azure web app.</span></span>

![Aplikacja sieci web tooAzure nawigacji w portalu](./media/app-service-web-tutorial-php-mysql/access-portal.png)

<span data-ttu-id="5e9f5-312">Zostanie wyświetlona strona Omówienie aplikacji internetowej.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-312">You see your web app's Overview page.</span></span> <span data-ttu-id="5e9f5-313">W tym miejscu można wykonać zadania podstawowe możliwości zarządzania, takie jak zatrzymanie, start ponownego uruchomienia, przeglądania i usuwania.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-313">Here, you can perform basic management tasks like  stop, start, restart, browse, and delete.</span></span>

<span data-ttu-id="5e9f5-314">menu po lewej stronie powitania zawiera strony konfigurowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-314">hello left menu provides pages for configuring your app.</span></span>

![Strona usługi App Service w witrynie Azure Portal](./media/app-service-web-tutorial-php-mysql/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

<a name="next"></a>

## <a name="next-steps"></a><span data-ttu-id="5e9f5-316">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5e9f5-316">Next steps</span></span>

<span data-ttu-id="5e9f5-317">W niniejszym samouczku zawarto informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="5e9f5-317">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5e9f5-318">Utwórz bazę danych MySQL na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="5e9f5-318">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="5e9f5-319">Połącz tooMySQL aplikacji PHP</span><span class="sxs-lookup"><span data-stu-id="5e9f5-319">Connect a PHP app tooMySQL</span></span>
> * <span data-ttu-id="5e9f5-320">Wdrażanie tooAzure aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="5e9f5-320">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="5e9f5-321">Aktualizacja modelu danych hello i wdrożenie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="5e9f5-321">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="5e9f5-322">Strumieniowe przesyłanie dzienników diagnostycznych z platformy Azure</span><span class="sxs-lookup"><span data-stu-id="5e9f5-322">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="5e9f5-323">Zarządzanie aplikacją hello w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="5e9f5-323">Manage hello app in hello Azure portal</span></span>

<span data-ttu-id="5e9f5-324">Przejść dalej toolearn samouczka toohello jak toomap DNS niestandardowej nazwy tooa aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="5e9f5-324">Advance toohello next tutorial toolearn how toomap a custom DNS name tooa web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5e9f5-325">Mapowanie istniejących niestandardowe DNS nazwy tooAzure aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="5e9f5-325">Map an existing custom DNS name tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
