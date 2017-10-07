---
title: aaaDeploy LEMP na maszynie wirtualnej systemu Linux na platformie Azure | Dokumentacja firmy Microsoft
description: "Samouczek — stosu LEMP hello instalacji na maszynie Wirtualnej systemu Linux na platformie Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 08/03/2017
ms.author: danlep
ms.openlocfilehash: d8f9d84c5e9c0df4e9e985c10fe10f63a2f88214
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-lemp-web-server-on-an-azure-vm"></a>Zainstaluj serwer sieci web LEMP na maszynie Wirtualnej platformy Azure
W tym artykule przedstawiono sposób toodeploy NGINX serwera sieci web, MySQL i PHP (hello LEMP stosu) na maszynie Wirtualnej systemu Ubuntu na platformie Azure. stos LEMP Hello jest alternatywnych toohello popularnych [stosu światła](tutorial-lamp-stack.md), które można także zainstalować na platformie Azure. toosee hello LEMP serwera akcji, można opcjonalnie zainstalować i skonfigurować witrynę WordPress. Ten samouczek zawiera informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]
> * Tworzenie maszyny Wirtualnej systemu Ubuntu (hello "L" hello LEMP stosu)
> * Otwieranie portu 80 na potrzeby ruchu w sieci Web
> * Zainstaluj NGINX, MySQL i PHP
> * Sprawdź, instalacja i Konfiguracja
> * Zainstaluj program WordPress na powitania serwera LEMP


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym samouczku wymaga działają hello Azure CLI w wersji 2.0.4 lub nowszej. Uruchom `az --version` toofind hello wersji. Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli). 

[!INCLUDE [virtual-machines-linux-tutorial-stack-intro.md](../../../includes/virtual-machines-linux-tutorial-stack-intro.md)]

## <a name="install-nginx-mysql-and-php"></a>Zainstaluj NGINX, MySQL i PHP

Uruchom następujące polecenie tooupdate Ubuntu pakietu źródła hello i zainstaluj NGINX, MySQL i PHP. 

```bash
sudo apt update && sudo apt install nginx mysql-server php-mysql php php-fpm
```

Jesteś pakietów hello zostanie wyświetlony monit o tooinstall i innych zależności. Po wyświetleniu monitu MySQL, a następnie toocontinue [Enter] należy ustawić hasło główne. Wykonaj hello pozostałych monitów. Ten proces instaluje hello minimalne wymagane PHP rozszerzenia potrzebne toouse PHP z programem MySQL. 

![Strona hasła głównego MySQL][1]

## <a name="verify-installation-and-configuration"></a>Sprawdź, instalacja i Konfiguracja


### <a name="nginx"></a>NGINX

Sprawdź wersję hello NGINX z hello następujące polecenie:
```bash
nginx -v
```

NGINX zainstalowana i port 80 Otwórz tooyour maszyny Wirtualnej, powitania serwera sieci web jest teraz dostępna z hello internet. Witaj tooview NGINX stronę powitalną, otwórz przeglądarkę sieci web, a następnie wprowadź hello publicznego adresu IP hello maszyny Wirtualnej. Użyj hello publiczny adres IP używany toohello tooSSH maszyny Wirtualnej:

![NGINX domyślnej strony][3]


### <a name="mysql"></a>MySQL

Sprawdź wersję hello MySQL z hello następujące polecenie (należy pamiętać, kapitału hello `V` parametru):

```bash
msql -V
```

Zaleca się uruchomienie skryptu toohelp hello bezpiecznej instalacji programu MySQL hello:

```bash
mysql_secure_installation
```

Wprowadź hasło głównego MySQL i skonfiguruj ustawienia zabezpieczeń hello w danym środowisku.

Jeśli chcesz toocreate bazę danych MySQL, dodać użytkowników lub zmienić ustawienia konfiguracji, tooMySQL logowania:

```bash
mysql -u root -p
```

Po zakończeniu zamknij wiersz mysql hello wpisując `\q`.

### <a name="php"></a>PHP

Sprawdź wersję hello PHP z hello następujące polecenie:

```bash
php -v
```

Skonfiguruj NGINX toouse hello Menedżera procesu FastCGI PHP (PHP FPM). Uruchom następujące polecenia tooback hello oryginalny serwer NGINX plik konfiguracji, a następnie edytuj oryginalny plik hello w wybranym edytorze hello:

```bash
sudo cp /etc/nginx/sites-available/default /etc/nginx/sites-available/default_backup

sudo sensible-editor /etc/nginx/sites-available/default
```

W edytorze hello Zastąp zawartość hello `/etc/nginx/sites-available/default` następujący hello. Zobacz komentarze hello wyjaśnienie hello ustawienia. Zastąp hello publicznego adresu IP dla maszyny Wirtualnej *yourPublicIPAddress*i pozostawić hello pozostałe ustawienia. Następnie zapisz plik hello.

```
server {
    listen 80 default_server;
    listen [::]:80 default_server;

    root /var/www/html;
    # Homepage of website is index.php
    index index.php;

    server_name yourPublicIPAddress;

    location / {
        try_files $uri $uri/ =404;
    }

    # Include FastCGI configuration for NGINX
    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php7.0-fpm.sock;
    }
}
```

Sprawdź konfigurację NGINX hello błędy składniowe:

```bash
sudo nginx -t
```

Jeśli hello składnia jest poprawna, uruchom ponownie NGINX z hello następujące polecenie:

```bash
sudo service nginx restart
```

Dalsze tootest, utworzyć szybkie tooview strony informacji PHP w przeglądarce. Witaj następujące polecenie tworzy stronę informacji PHP hello:

```bash
sudo sh -c 'echo "<?php phpinfo(); ?>" > /var/www/html/info.php'
```



Teraz można sprawdzić stronę informacji PHP hello utworzony. Otwórz przeglądarkę i przejdź zbyt`http://yourPublicIPAddress/info.php`. Zastąp hello publicznego adresu IP maszyny Wirtualnej. Jego wygląd powinien być podobny toothis obrazu.

![Strona informacje o PHP][2]


[!INCLUDE [virtual-machines-linux-tutorial-wordpress.md](../../../includes/virtual-machines-linux-tutorial-wordpress.md)]

## <a name="next-steps"></a>Następne kroki

W tym samouczku wdrożono serwer LEMP na platformie Azure. W tym samouczku omówiono:

> [!div class="checklist"]
> * Tworzenie maszyny Wirtualnej systemu Ubuntu
> * Otwieranie portu 80 na potrzeby ruchu w sieci Web
> * Zainstaluj NGINX, MySQL i PHP
> * Sprawdź, instalacja i Konfiguracja
> * Zainstaluj program WordPress na powitania LEMP stosu

Jak przejść dalej toolearn samouczka toohello toosecure serwerów sieci web z certyfikatów SSL.

> [!div class="nextstepaction"]
> [Zabezpieczenia serwera sieci web przy użyciu protokołu SSL](tutorial-secure-web-server.md)

[1]: ./media/tutorial-lemp-stack/configmysqlpassword-small.png
[2]: ./media/tutorial-lemp-stack/phpsuccesspage.png
[3]: ./media/tutorial-lemp-stack/nginx.png
