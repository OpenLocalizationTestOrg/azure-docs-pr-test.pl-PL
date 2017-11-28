## <a name="install-wordpress"></a><span data-ttu-id="fffcd-101">Zainstaluj program WordPress</span><span class="sxs-lookup"><span data-stu-id="fffcd-101">Install WordPress</span></span>

<span data-ttu-id="fffcd-102">Jeśli chcesz spróbować stosu, należy zainstalować przykładową aplikację.</span><span class="sxs-lookup"><span data-stu-id="fffcd-102">If you want to try your stack, install a sample app.</span></span> <span data-ttu-id="fffcd-103">Na przykład następujące kroki instalowania typu open source [WordPress](https://wordpress.org/) platformę do tworzenia witryn sieci Web i blogów.</span><span class="sxs-lookup"><span data-stu-id="fffcd-103">As an example, the following steps install the open source [WordPress](https://wordpress.org/) platform to create websites and blogs.</span></span> <span data-ttu-id="fffcd-104">Inne obciążenia, aby spróbować zawierają [Drupal](http://www.drupal.org) i [Moodle](https://moodle.org/).</span><span class="sxs-lookup"><span data-stu-id="fffcd-104">Other workloads to try include [Drupal](http://www.drupal.org) and [Moodle](https://moodle.org/).</span></span> 

<span data-ttu-id="fffcd-105">Jest to Instalator WordPress do weryfikacji koncepcji.</span><span class="sxs-lookup"><span data-stu-id="fffcd-105">This WordPress setup is for proof of concept.</span></span> <span data-ttu-id="fffcd-106">Aby uzyskać więcej informacji i ustawienia instalacji produkcyjnym, zobacz [dokumentacji WordPress](https://codex.wordpress.org/Main_Page).</span><span class="sxs-lookup"><span data-stu-id="fffcd-106">For more information and settings for production installation, see the [WordPress documentation](https://codex.wordpress.org/Main_Page).</span></span> 



### <a name="install-the-wordpress-package"></a><span data-ttu-id="fffcd-107">Zainstaluj pakiet WordPress</span><span class="sxs-lookup"><span data-stu-id="fffcd-107">Install the WordPress package</span></span>

<span data-ttu-id="fffcd-108">Uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="fffcd-108">Run the following command:</span></span>

```bash
sudo apt install wordpress
```

### <a name="configure-wordpress"></a><span data-ttu-id="fffcd-109">Konfigurowanie usługi WordPress</span><span class="sxs-lookup"><span data-stu-id="fffcd-109">Configure WordPress</span></span>

<span data-ttu-id="fffcd-110">Konfigurowanie usługi WordPress, aby użyć MySQL i PHP.</span><span class="sxs-lookup"><span data-stu-id="fffcd-110">Configure WordPress to use MySQL and PHP.</span></span> <span data-ttu-id="fffcd-111">Uruchom następujące polecenie, aby otworzyć wybranym w edytorze tekstu i utworzyć plik `/etc/wordpress/config-localhost.php`:</span><span class="sxs-lookup"><span data-stu-id="fffcd-111">Run the following command to open a text editor of your choice and create the file `/etc/wordpress/config-localhost.php`:</span></span>

```bash
sudo sensible-editor /etc/wordpress/config-localhost.php
```
<span data-ttu-id="fffcd-112">Skopiuj następujące wiersze do pliku, zastępując hasła bazy danych dla *yourPassword* (Pozostaw bez zmian wartości).</span><span class="sxs-lookup"><span data-stu-id="fffcd-112">Copy the following lines to the file, substituting your database password for *yourPassword* (leave other values unchanged).</span></span> <span data-ttu-id="fffcd-113">Następnie zapisz plik.</span><span class="sxs-lookup"><span data-stu-id="fffcd-113">Then save the file.</span></span>

```php
<?php
define('DB_NAME', 'wordpress');
define('DB_USER', 'wordpress');
define('DB_PASSWORD', 'yourPassword');
define('DB_HOST', 'localhost');
define('WP_CONTENT_DIR', '/usr/share/wordpress/wp-content');
?>
```

<span data-ttu-id="fffcd-114">W katalogu roboczym, Utwórz plik tekstowy `wordpress.sql` skonfigurować WordPress bazy danych:</span><span class="sxs-lookup"><span data-stu-id="fffcd-114">In a working directory, create a text file `wordpress.sql` to configure the WordPress database:</span></span> 

```bash
sudo sensible-editor wordpress.sql
```

<span data-ttu-id="fffcd-115">Dodaj następujące polecenia, zastępując hasła bazy danych dla *yourPassword* (Pozostaw bez zmian wartości).</span><span class="sxs-lookup"><span data-stu-id="fffcd-115">Add the following commands, substituting your database password for *yourPassword* (leave other values unchanged).</span></span> <span data-ttu-id="fffcd-116">Następnie zapisz plik.</span><span class="sxs-lookup"><span data-stu-id="fffcd-116">Then save the file.</span></span>

```sql
CREATE DATABASE wordpress;
GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,ALTER
ON wordpress.*
TO wordpress@localhost
IDENTIFIED BY 'yourPassword';
FLUSH PRIVILEGES;
```


<span data-ttu-id="fffcd-117">Uruchom następujące polecenie, aby utworzyć bazę danych:</span><span class="sxs-lookup"><span data-stu-id="fffcd-117">Run the following command to create the database:</span></span>

```bash
cat wordpress.sql | sudo mysql --defaults-extra-file=/etc/mysql/debian.cnf
```

<span data-ttu-id="fffcd-118">Po zakończeniu wykonywania polecenia, usuń plik `wordpress.sql`.</span><span class="sxs-lookup"><span data-stu-id="fffcd-118">After the command completes, delete the file `wordpress.sql`.</span></span>

<span data-ttu-id="fffcd-119">Przenoszenie instalacji WordPress głównego dokumentu serwera sieci web:</span><span class="sxs-lookup"><span data-stu-id="fffcd-119">Move the WordPress installation to the web server document root:</span></span>

```bash
sudo ln -s /usr/share/wordpress /var/www/html/wordpress

sudo mv /etc/wordpress/config-localhost.php /etc/wordpress/config-default.php
```

<span data-ttu-id="fffcd-120">Można teraz zakończyć WordPress i publikowanie na platformie.</span><span class="sxs-lookup"><span data-stu-id="fffcd-120">Now you can complete the WordPress setup and publish on the platform.</span></span> <span data-ttu-id="fffcd-121">Otwórz przeglądarkę i przejdź do `http://yourPublicIPAddress/wordpress`.</span><span class="sxs-lookup"><span data-stu-id="fffcd-121">Open a browser and go to `http://yourPublicIPAddress/wordpress`.</span></span> <span data-ttu-id="fffcd-122">Należy zastąpić publicznego adresu IP maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fffcd-122">Substitute the public IP address of your VM.</span></span> <span data-ttu-id="fffcd-123">Powinien być podobny do tego obrazu.</span><span class="sxs-lookup"><span data-stu-id="fffcd-123">It should look similar to this image.</span></span>

![Strona instalacji WordPress](./media/virtual-machines-linux-tutorial-wordpress/wordpressstartpage.png)