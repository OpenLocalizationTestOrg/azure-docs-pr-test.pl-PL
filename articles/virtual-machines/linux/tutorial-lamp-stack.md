---
title: "aaaDeploy światła na maszynie wirtualnej systemu Linux na platformie Azure | Dokumentacja firmy Microsoft"
description: "Samouczek — stosu światła hello instalacji na maszynie Wirtualnej systemu Linux na platformie Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 6c12603a-e391-4d3e-acce-442dd7ebb2fe
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 08/03/2017
ms.author: danlep
ms.openlocfilehash: a3d0ecb3277f15bd0a2fdc0d85b738a760e68865
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-lamp-web-server-on-an-azure-vm"></a>Instalacja serwera sieci web światła w maszynie Wirtualnej platformy Azure
W tym artykule przedstawiono sposób toodeploy Apache serwera sieci web, MySQL i PHP (stos hello światła) na maszynie Wirtualnej systemu Ubuntu na platformie Azure. Jeśli chcesz, aby serwer sieci web hello NGINX, zobacz hello [stosu LEMP](tutorial-lemp-stack.md) samouczka. toosee hello światła serwera akcji, można opcjonalnie zainstalować i skonfigurować witrynę WordPress. Ten samouczek zawiera informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]
> * Tworzenie maszyny Wirtualnej systemu Ubuntu (hello "L" hello światła stosu)
> * Otwieranie portu 80 na potrzeby ruchu w sieci Web
> * Instalowanie Apache, MySQL i PHP
> * Sprawdź, instalacja i Konfiguracja
> * Zainstaluj program WordPress na serwerze światła hello


Aby uzyskać więcej informacji na stosie światła hello, w tym zalecenia w środowisku produkcyjnym, zobacz hello [dokumentacji Ubuntu](https://help.ubuntu.com/community/ApacheMySQLPHP).

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym samouczku wymaga działają hello Azure CLI w wersji 2.0.4 lub nowszej. Uruchom `az --version` toofind hello wersji. Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli). 

[!INCLUDE [virtual-machines-linux-tutorial-stack-intro.md](../../../includes/virtual-machines-linux-tutorial-stack-intro.md)]

## <a name="install-apache-mysql-and-php"></a>Instalowanie Apache, MySQL i PHP

Uruchom następujące polecenie tooupdate Ubuntu pakietu źródła hello i zainstaluj Apache, MySQL i PHP. Należy zwrócić uwagę hello daszek (^) na końcu hello hello polecenia.


```bash
sudo apt update && sudo apt install lamp-server^
```



Jesteś pakietów hello zostanie wyświetlony monit o tooinstall i innych zależności. Po wyświetleniu monitu MySQL, a następnie toocontinue [Enter] należy ustawić hasło główne. Wykonaj hello pozostałych monitów. Ten proces instaluje hello minimalne wymagane PHP rozszerzenia potrzebne toouse PHP z programem MySQL. 

![Strona hasła głównego MySQL][1]

## <a name="verify-installation-and-configuration"></a>Sprawdź, instalacja i Konfiguracja


### <a name="apache"></a>Apache

Sprawdź wersję hello Apache z hello następujące polecenie:
```bash
apache2 -v
```

Apache zainstalowana i port 80 Otwórz tooyour maszyny Wirtualnej, powitania serwera sieci web jest teraz dostępna z hello internet. hello tooview Apache2 Ubuntu strona domyślna, otwórz przeglądarkę sieci web, a następnie wprowadź hello publicznego adresu IP hello maszyny Wirtualnej. Użyj hello publiczny adres IP używany toohello tooSSH maszyny Wirtualnej:

![Apache domyślnej strony][3]


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

Dalsze tootest, utworzyć szybkie tooview strony informacji PHP w przeglądarce. Witaj następujące polecenie tworzy stronę informacji PHP hello:

```bash
sudo sh -c 'echo "<?php phpinfo(); ?>" > /var/www/html/info.php'
```

Teraz można sprawdzić stronę informacji PHP hello utworzony. Otwórz przeglądarkę i przejdź zbyt`http://yourPublicIPAddress/info.php`. Zastąp hello publicznego adresu IP maszyny Wirtualnej. Jego wygląd powinien być podobny toothis obrazu.

![Strona informacje o PHP][2]

[!INCLUDE [virtual-machines-linux-tutorial-wordpress.md](../../../includes/virtual-machines-linux-tutorial-wordpress.md)]


## <a name="next-steps"></a>Następne kroki

W tym samouczku wdrożono serwer światła na platformie Azure. W tym samouczku omówiono:

> [!div class="checklist"]
> * Tworzenie maszyny Wirtualnej systemu Ubuntu
> * Otwieranie portu 80 na potrzeby ruchu w sieci Web
> * Instalowanie Apache, MySQL i PHP
> * Sprawdź, instalacja i Konfiguracja
> * Zainstaluj program WordPress na serwerze światła hello

Jak przejść dalej toolearn samouczka toohello toosecure serwerów sieci web z certyfikatów SSL.

> [!div class="nextstepaction"]
> [Zabezpieczenia serwera sieci web przy użyciu protokołu SSL](tutorial-secure-web-server.md)

[1]: ./media/tutorial-lamp-stack/configmysqlpassword-small.png
[2]: ./media/tutorial-lamp-stack/phpsuccesspage.png
[3]: ./media/tutorial-lamp-stack/apachesuccesspage.png