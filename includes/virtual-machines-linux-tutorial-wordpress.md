## <a name="install-wordpress"></a>Zainstaluj program WordPress

Jeśli chcesz tootry stosu, należy zainstalować przykładową aplikację. Na przykład hello następujące kroki instalowania typu open source hello [WordPress](https://wordpress.org/) platformy toocreate witryn sieci Web i blogów. Tootry innych obciążeń obejmują [Drupal](http://www.drupal.org) i [Moodle](https://moodle.org/). 

Jest to Instalator WordPress do weryfikacji koncepcji. Aby uzyskać więcej informacji i ustawienia instalacji produkcyjnym, zobacz hello [dokumentacji WordPress](https://codex.wordpress.org/Main_Page). 



### <a name="install-hello-wordpress-package"></a>Zainstaluj pakiet WordPress hello

Uruchom następujące polecenie hello:

```bash
sudo apt install wordpress
```

### <a name="configure-wordpress"></a>Konfigurowanie usługi WordPress

Skonfiguruj WordPress toouse MySQL i PHP. Uruchom następujące polecenie tooopen hello wybranym w edytorze tekstu i Utwórz plik hello `/etc/wordpress/config-localhost.php`:

```bash
sudo sensible-editor /etc/wordpress/config-localhost.php
```
Kopiuj hello poniższe wiersze toohello plik, zastępując hasła bazy danych dla *yourPassword* (Pozostaw bez zmian wartości). Następnie zapisz plik hello.

```php
<?php
define('DB_NAME', 'wordpress');
define('DB_USER', 'wordpress');
define('DB_PASSWORD', 'yourPassword');
define('DB_HOST', 'localhost');
define('WP_CONTENT_DIR', '/usr/share/wordpress/wp-content');
?>
```

W katalogu roboczym, Utwórz plik tekstowy `wordpress.sql` tooconfigure hello WordPress w bazie danych: 

```bash
sudo sensible-editor wordpress.sql
```

Dodaj hello następujące polecenia, zastępując hasła bazy danych dla *yourPassword* (Pozostaw bez zmian wartości). Następnie zapisz plik hello.

```sql
CREATE DATABASE wordpress;
GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,ALTER
ON wordpress.*
toowordpress@localhost
IDENTIFIED BY 'yourPassword';
FLUSH PRIVILEGES;
```


Witaj uruchom następujące polecenie toocreate hello w bazie danych:

```bash
cat wordpress.sql | sudo mysql --defaults-extra-file=/etc/mysql/debian.cnf
```

Po zakończeniu wykonywania polecenia hello, usuń plik hello `wordpress.sql`.

Przenieś instalacji WordPress hello toohello głównego dokumentu serwera sieci web:

```bash
sudo ln -s /usr/share/wordpress /var/www/html/wordpress

sudo mv /etc/wordpress/config-localhost.php /etc/wordpress/config-default.php
```

Teraz możesz ukończyć powitalnych WordPress instalacji i publikowanie na platformie hello. Otwórz przeglądarkę i przejdź zbyt`http://yourPublicIPAddress/wordpress`. Zastąp hello publicznego adresu IP maszyny Wirtualnej. Jego wygląd powinien być podobny toothis obrazu.

![Strona instalacji WordPress](./media/virtual-machines-linux-tutorial-wordpress/wordpressstartpage.png)