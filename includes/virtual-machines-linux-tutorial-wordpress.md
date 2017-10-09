## <a name="install-wordpress"></a><span data-ttu-id="f4001-101">Zainstaluj program WordPress</span><span class="sxs-lookup"><span data-stu-id="f4001-101">Install WordPress</span></span>

<span data-ttu-id="f4001-102">Jeśli chcesz tootry stosu, należy zainstalować przykładową aplikację.</span><span class="sxs-lookup"><span data-stu-id="f4001-102">If you want tootry your stack, install a sample app.</span></span> <span data-ttu-id="f4001-103">Na przykład hello następujące kroki instalowania typu open source hello [WordPress](https://wordpress.org/) platformy toocreate witryn sieci Web i blogów.</span><span class="sxs-lookup"><span data-stu-id="f4001-103">As an example, hello following steps install hello open source [WordPress](https://wordpress.org/) platform toocreate websites and blogs.</span></span> <span data-ttu-id="f4001-104">Tootry innych obciążeń obejmują [Drupal](http://www.drupal.org) i [Moodle](https://moodle.org/).</span><span class="sxs-lookup"><span data-stu-id="f4001-104">Other workloads tootry include [Drupal](http://www.drupal.org) and [Moodle](https://moodle.org/).</span></span> 

<span data-ttu-id="f4001-105">Jest to Instalator WordPress do weryfikacji koncepcji.</span><span class="sxs-lookup"><span data-stu-id="f4001-105">This WordPress setup is for proof of concept.</span></span> <span data-ttu-id="f4001-106">Aby uzyskać więcej informacji i ustawienia instalacji produkcyjnym, zobacz hello [dokumentacji WordPress](https://codex.wordpress.org/Main_Page).</span><span class="sxs-lookup"><span data-stu-id="f4001-106">For more information and settings for production installation, see hello [WordPress documentation](https://codex.wordpress.org/Main_Page).</span></span> 



### <a name="install-hello-wordpress-package"></a><span data-ttu-id="f4001-107">Zainstaluj pakiet WordPress hello</span><span class="sxs-lookup"><span data-stu-id="f4001-107">Install hello WordPress package</span></span>

<span data-ttu-id="f4001-108">Uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="f4001-108">Run hello following command:</span></span>

```bash
sudo apt install wordpress
```

### <a name="configure-wordpress"></a><span data-ttu-id="f4001-109">Konfigurowanie usługi WordPress</span><span class="sxs-lookup"><span data-stu-id="f4001-109">Configure WordPress</span></span>

<span data-ttu-id="f4001-110">Skonfiguruj WordPress toouse MySQL i PHP.</span><span class="sxs-lookup"><span data-stu-id="f4001-110">Configure WordPress toouse MySQL and PHP.</span></span> <span data-ttu-id="f4001-111">Uruchom następujące polecenie tooopen hello wybranym w edytorze tekstu i Utwórz plik hello `/etc/wordpress/config-localhost.php`:</span><span class="sxs-lookup"><span data-stu-id="f4001-111">Run hello following command tooopen a text editor of your choice and create hello file `/etc/wordpress/config-localhost.php`:</span></span>

```bash
sudo sensible-editor /etc/wordpress/config-localhost.php
```
<span data-ttu-id="f4001-112">Kopiuj hello poniższe wiersze toohello plik, zastępując hasła bazy danych dla *yourPassword* (Pozostaw bez zmian wartości).</span><span class="sxs-lookup"><span data-stu-id="f4001-112">Copy hello following lines toohello file, substituting your database password for *yourPassword* (leave other values unchanged).</span></span> <span data-ttu-id="f4001-113">Następnie zapisz plik hello.</span><span class="sxs-lookup"><span data-stu-id="f4001-113">Then save hello file.</span></span>

```php
<?php
define('DB_NAME', 'wordpress');
define('DB_USER', 'wordpress');
define('DB_PASSWORD', 'yourPassword');
define('DB_HOST', 'localhost');
define('WP_CONTENT_DIR', '/usr/share/wordpress/wp-content');
?>
```

<span data-ttu-id="f4001-114">W katalogu roboczym, Utwórz plik tekstowy `wordpress.sql` tooconfigure hello WordPress w bazie danych:</span><span class="sxs-lookup"><span data-stu-id="f4001-114">In a working directory, create a text file `wordpress.sql` tooconfigure hello WordPress database:</span></span> 

```bash
sudo sensible-editor wordpress.sql
```

<span data-ttu-id="f4001-115">Dodaj hello następujące polecenia, zastępując hasła bazy danych dla *yourPassword* (Pozostaw bez zmian wartości).</span><span class="sxs-lookup"><span data-stu-id="f4001-115">Add hello following commands, substituting your database password for *yourPassword* (leave other values unchanged).</span></span> <span data-ttu-id="f4001-116">Następnie zapisz plik hello.</span><span class="sxs-lookup"><span data-stu-id="f4001-116">Then save hello file.</span></span>

```sql
CREATE DATABASE wordpress;
GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,ALTER
ON wordpress.*
toowordpress@localhost
IDENTIFIED BY 'yourPassword';
FLUSH PRIVILEGES;
```


<span data-ttu-id="f4001-117">Witaj uruchom następujące polecenie toocreate hello w bazie danych:</span><span class="sxs-lookup"><span data-stu-id="f4001-117">Run hello following command toocreate hello database:</span></span>

```bash
cat wordpress.sql | sudo mysql --defaults-extra-file=/etc/mysql/debian.cnf
```

<span data-ttu-id="f4001-118">Po zakończeniu wykonywania polecenia hello, usuń plik hello `wordpress.sql`.</span><span class="sxs-lookup"><span data-stu-id="f4001-118">After hello command completes, delete hello file `wordpress.sql`.</span></span>

<span data-ttu-id="f4001-119">Przenieś instalacji WordPress hello toohello głównego dokumentu serwera sieci web:</span><span class="sxs-lookup"><span data-stu-id="f4001-119">Move hello WordPress installation toohello web server document root:</span></span>

```bash
sudo ln -s /usr/share/wordpress /var/www/html/wordpress

sudo mv /etc/wordpress/config-localhost.php /etc/wordpress/config-default.php
```

<span data-ttu-id="f4001-120">Teraz możesz ukończyć powitalnych WordPress instalacji i publikowanie na platformie hello.</span><span class="sxs-lookup"><span data-stu-id="f4001-120">Now you can complete hello WordPress setup and publish on hello platform.</span></span> <span data-ttu-id="f4001-121">Otwórz przeglądarkę i przejdź zbyt`http://yourPublicIPAddress/wordpress`.</span><span class="sxs-lookup"><span data-stu-id="f4001-121">Open a browser and go too`http://yourPublicIPAddress/wordpress`.</span></span> <span data-ttu-id="f4001-122">Zastąp hello publicznego adresu IP maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f4001-122">Substitute hello public IP address of your VM.</span></span> <span data-ttu-id="f4001-123">Jego wygląd powinien być podobny toothis obrazu.</span><span class="sxs-lookup"><span data-stu-id="f4001-123">It should look similar toothis image.</span></span>

![Strona instalacji WordPress](./media/virtual-machines-linux-tutorial-wordpress/wordpressstartpage.png)