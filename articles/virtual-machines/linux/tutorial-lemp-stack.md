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
# <a name="install-a-lemp-web-server-on-an-azure-vm"></a><span data-ttu-id="55c8a-103">Zainstaluj serwer sieci web LEMP na maszynie Wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="55c8a-103">Install a LEMP web server on an Azure VM</span></span>
<span data-ttu-id="55c8a-104">W tym artykule przedstawiono sposób toodeploy NGINX serwera sieci web, MySQL i PHP (hello LEMP stosu) na maszynie Wirtualnej systemu Ubuntu na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="55c8a-104">This article walks you through how toodeploy an NGINX web server, MySQL, and PHP (hello LEMP stack) on an Ubuntu VM in Azure.</span></span> <span data-ttu-id="55c8a-105">stos LEMP Hello jest alternatywnych toohello popularnych [stosu światła](tutorial-lamp-stack.md), które można także zainstalować na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="55c8a-105">hello LEMP stack is an alternative toohello popular [LAMP stack](tutorial-lamp-stack.md), which you can also install in Azure.</span></span> <span data-ttu-id="55c8a-106">toosee hello LEMP serwera akcji, można opcjonalnie zainstalować i skonfigurować witrynę WordPress.</span><span class="sxs-lookup"><span data-stu-id="55c8a-106">toosee hello LEMP server in action, you can optionally install and configure a WordPress site.</span></span> <span data-ttu-id="55c8a-107">Ten samouczek zawiera informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="55c8a-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="55c8a-108">Tworzenie maszyny Wirtualnej systemu Ubuntu (hello "L" hello LEMP stosu)</span><span class="sxs-lookup"><span data-stu-id="55c8a-108">Create an Ubuntu VM (hello 'L' in hello LEMP stack)</span></span>
> * <span data-ttu-id="55c8a-109">Otwieranie portu 80 na potrzeby ruchu w sieci Web</span><span class="sxs-lookup"><span data-stu-id="55c8a-109">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="55c8a-110">Zainstaluj NGINX, MySQL i PHP</span><span class="sxs-lookup"><span data-stu-id="55c8a-110">Install NGINX, MySQL, and PHP</span></span>
> * <span data-ttu-id="55c8a-111">Sprawdź, instalacja i Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="55c8a-111">Verify installation and configuration</span></span>
> * <span data-ttu-id="55c8a-112">Zainstaluj program WordPress na powitania serwera LEMP</span><span class="sxs-lookup"><span data-stu-id="55c8a-112">Install WordPress on hello LEMP server</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="55c8a-113">Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym samouczku wymaga działają hello Azure CLI w wersji 2.0.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="55c8a-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="55c8a-114">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="55c8a-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="55c8a-115">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="55c8a-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [virtual-machines-linux-tutorial-stack-intro.md](../../../includes/virtual-machines-linux-tutorial-stack-intro.md)]

## <a name="install-nginx-mysql-and-php"></a><span data-ttu-id="55c8a-116">Zainstaluj NGINX, MySQL i PHP</span><span class="sxs-lookup"><span data-stu-id="55c8a-116">Install NGINX, MySQL, and PHP</span></span>

<span data-ttu-id="55c8a-117">Uruchom następujące polecenie tooupdate Ubuntu pakietu źródła hello i zainstaluj NGINX, MySQL i PHP.</span><span class="sxs-lookup"><span data-stu-id="55c8a-117">Run hello following command tooupdate Ubuntu package sources and install NGINX, MySQL, and PHP.</span></span> 

```bash
sudo apt update && sudo apt install nginx mysql-server php-mysql php php-fpm
```

<span data-ttu-id="55c8a-118">Jesteś pakietów hello zostanie wyświetlony monit o tooinstall i innych zależności.</span><span class="sxs-lookup"><span data-stu-id="55c8a-118">You are prompted tooinstall hello packages and other dependencies.</span></span> <span data-ttu-id="55c8a-119">Po wyświetleniu monitu MySQL, a następnie toocontinue [Enter] należy ustawić hasło główne.</span><span class="sxs-lookup"><span data-stu-id="55c8a-119">When prompted, set a root password for MySQL, and then [Enter] toocontinue.</span></span> <span data-ttu-id="55c8a-120">Wykonaj hello pozostałych monitów.</span><span class="sxs-lookup"><span data-stu-id="55c8a-120">Follow hello remaining prompts.</span></span> <span data-ttu-id="55c8a-121">Ten proces instaluje hello minimalne wymagane PHP rozszerzenia potrzebne toouse PHP z programem MySQL.</span><span class="sxs-lookup"><span data-stu-id="55c8a-121">This process installs hello minimum required PHP extensions needed toouse PHP with MySQL.</span></span> 

![Strona hasła głównego MySQL][1]

## <a name="verify-installation-and-configuration"></a><span data-ttu-id="55c8a-123">Sprawdź, instalacja i Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="55c8a-123">Verify installation and configuration</span></span>


### <a name="nginx"></a><span data-ttu-id="55c8a-124">NGINX</span><span class="sxs-lookup"><span data-stu-id="55c8a-124">NGINX</span></span>

<span data-ttu-id="55c8a-125">Sprawdź wersję hello NGINX z hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="55c8a-125">Check hello version of NGINX with hello following command:</span></span>
```bash
nginx -v
```

<span data-ttu-id="55c8a-126">NGINX zainstalowana i port 80 Otwórz tooyour maszyny Wirtualnej, powitania serwera sieci web jest teraz dostępna z hello internet.</span><span class="sxs-lookup"><span data-stu-id="55c8a-126">With NGINX installed, and port 80 open tooyour VM, hello web server can now be accessed from hello internet.</span></span> <span data-ttu-id="55c8a-127">Witaj tooview NGINX stronę powitalną, otwórz przeglądarkę sieci web, a następnie wprowadź hello publicznego adresu IP hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="55c8a-127">tooview hello NGINX welcome page, open a web browser, and enter hello public IP address of hello VM.</span></span> <span data-ttu-id="55c8a-128">Użyj hello publiczny adres IP używany toohello tooSSH maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="55c8a-128">Use hello public IP address you used tooSSH toohello VM:</span></span>

![NGINX domyślnej strony][3]


### <a name="mysql"></a><span data-ttu-id="55c8a-130">MySQL</span><span class="sxs-lookup"><span data-stu-id="55c8a-130">MySQL</span></span>

<span data-ttu-id="55c8a-131">Sprawdź wersję hello MySQL z hello następujące polecenie (należy pamiętać, kapitału hello `V` parametru):</span><span class="sxs-lookup"><span data-stu-id="55c8a-131">Check hello version of MySQL with hello following command (note hello capital `V` parameter):</span></span>

```bash
msql -V
```

<span data-ttu-id="55c8a-132">Zaleca się uruchomienie skryptu toohelp hello bezpiecznej instalacji programu MySQL hello:</span><span class="sxs-lookup"><span data-stu-id="55c8a-132">We recommend running hello following script toohelp secure hello installation of MySQL:</span></span>

```bash
mysql_secure_installation
```

<span data-ttu-id="55c8a-133">Wprowadź hasło głównego MySQL i skonfiguruj ustawienia zabezpieczeń hello w danym środowisku.</span><span class="sxs-lookup"><span data-stu-id="55c8a-133">Enter your MySQL root password, and configure hello security settings for your environment.</span></span>

<span data-ttu-id="55c8a-134">Jeśli chcesz toocreate bazę danych MySQL, dodać użytkowników lub zmienić ustawienia konfiguracji, tooMySQL logowania:</span><span class="sxs-lookup"><span data-stu-id="55c8a-134">If you want toocreate a MySQL database, add users, or change configuration settings, login tooMySQL:</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="55c8a-135">Po zakończeniu zamknij wiersz mysql hello wpisując `\q`.</span><span class="sxs-lookup"><span data-stu-id="55c8a-135">When done, exit hello mysql prompt by typing `\q`.</span></span>

### <a name="php"></a><span data-ttu-id="55c8a-136">PHP</span><span class="sxs-lookup"><span data-stu-id="55c8a-136">PHP</span></span>

<span data-ttu-id="55c8a-137">Sprawdź wersję hello PHP z hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="55c8a-137">Check hello version of PHP with hello following command:</span></span>

```bash
php -v
```

<span data-ttu-id="55c8a-138">Skonfiguruj NGINX toouse hello Menedżera procesu FastCGI PHP (PHP FPM).</span><span class="sxs-lookup"><span data-stu-id="55c8a-138">Configure NGINX toouse hello PHP FastCGI Process Manager (PHP-FPM).</span></span> <span data-ttu-id="55c8a-139">Uruchom następujące polecenia tooback hello oryginalny serwer NGINX plik konfiguracji, a następnie edytuj oryginalny plik hello w wybranym edytorze hello:</span><span class="sxs-lookup"><span data-stu-id="55c8a-139">Run hello following commands tooback up hello original NGINX server block config file and then edit hello original file in an editor of your choice:</span></span>

```bash
sudo cp /etc/nginx/sites-available/default /etc/nginx/sites-available/default_backup

sudo sensible-editor /etc/nginx/sites-available/default
```

<span data-ttu-id="55c8a-140">W edytorze hello Zastąp zawartość hello `/etc/nginx/sites-available/default` następujący hello.</span><span class="sxs-lookup"><span data-stu-id="55c8a-140">In hello editor, replace hello contents of `/etc/nginx/sites-available/default` with hello following.</span></span> <span data-ttu-id="55c8a-141">Zobacz komentarze hello wyjaśnienie hello ustawienia.</span><span class="sxs-lookup"><span data-stu-id="55c8a-141">See hello comments for explanation of hello settings.</span></span> <span data-ttu-id="55c8a-142">Zastąp hello publicznego adresu IP dla maszyny Wirtualnej *yourPublicIPAddress*i pozostawić hello pozostałe ustawienia.</span><span class="sxs-lookup"><span data-stu-id="55c8a-142">Substitute hello public IP address of your VM for *yourPublicIPAddress*, and leave hello remaining settings.</span></span> <span data-ttu-id="55c8a-143">Następnie zapisz plik hello.</span><span class="sxs-lookup"><span data-stu-id="55c8a-143">Then save hello file.</span></span>

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

<span data-ttu-id="55c8a-144">Sprawdź konfigurację NGINX hello błędy składniowe:</span><span class="sxs-lookup"><span data-stu-id="55c8a-144">Check hello NGINX configuration for syntax errors:</span></span>

```bash
sudo nginx -t
```

<span data-ttu-id="55c8a-145">Jeśli hello składnia jest poprawna, uruchom ponownie NGINX z hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="55c8a-145">If hello syntax is correct, restart NGINX with hello following command:</span></span>

```bash
sudo service nginx restart
```

<span data-ttu-id="55c8a-146">Dalsze tootest, utworzyć szybkie tooview strony informacji PHP w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="55c8a-146">If you want tootest further, create a quick PHP info page tooview in a browser.</span></span> <span data-ttu-id="55c8a-147">Witaj następujące polecenie tworzy stronę informacji PHP hello:</span><span class="sxs-lookup"><span data-stu-id="55c8a-147">hello following command creates hello PHP info page:</span></span>

```bash
sudo sh -c 'echo "<?php phpinfo(); ?>" > /var/www/html/info.php'
```



<span data-ttu-id="55c8a-148">Teraz można sprawdzić stronę informacji PHP hello utworzony.</span><span class="sxs-lookup"><span data-stu-id="55c8a-148">Now you can check hello PHP info page you created.</span></span> <span data-ttu-id="55c8a-149">Otwórz przeglądarkę i przejdź zbyt`http://yourPublicIPAddress/info.php`.</span><span class="sxs-lookup"><span data-stu-id="55c8a-149">Open a browser and go too`http://yourPublicIPAddress/info.php`.</span></span> <span data-ttu-id="55c8a-150">Zastąp hello publicznego adresu IP maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="55c8a-150">Substitute hello public IP address of your VM.</span></span> <span data-ttu-id="55c8a-151">Jego wygląd powinien być podobny toothis obrazu.</span><span class="sxs-lookup"><span data-stu-id="55c8a-151">It should look similar toothis image.</span></span>

![Strona informacje o PHP][2]


[!INCLUDE [virtual-machines-linux-tutorial-wordpress.md](../../../includes/virtual-machines-linux-tutorial-wordpress.md)]

## <a name="next-steps"></a><span data-ttu-id="55c8a-153">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="55c8a-153">Next steps</span></span>

<span data-ttu-id="55c8a-154">W tym samouczku wdrożono serwer LEMP na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="55c8a-154">In this tutorial, you deployed a LEMP server in Azure.</span></span> <span data-ttu-id="55c8a-155">W tym samouczku omówiono:</span><span class="sxs-lookup"><span data-stu-id="55c8a-155">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="55c8a-156">Tworzenie maszyny Wirtualnej systemu Ubuntu</span><span class="sxs-lookup"><span data-stu-id="55c8a-156">Create an Ubuntu VM</span></span>
> * <span data-ttu-id="55c8a-157">Otwieranie portu 80 na potrzeby ruchu w sieci Web</span><span class="sxs-lookup"><span data-stu-id="55c8a-157">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="55c8a-158">Zainstaluj NGINX, MySQL i PHP</span><span class="sxs-lookup"><span data-stu-id="55c8a-158">Install NGINX, MySQL, and PHP</span></span>
> * <span data-ttu-id="55c8a-159">Sprawdź, instalacja i Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="55c8a-159">Verify installation and configuration</span></span>
> * <span data-ttu-id="55c8a-160">Zainstaluj program WordPress na powitania LEMP stosu</span><span class="sxs-lookup"><span data-stu-id="55c8a-160">Install WordPress on hello LEMP stack</span></span>

<span data-ttu-id="55c8a-161">Jak przejść dalej toolearn samouczka toohello toosecure serwerów sieci web z certyfikatów SSL.</span><span class="sxs-lookup"><span data-stu-id="55c8a-161">Advance toohello next tutorial toolearn how toosecure web servers with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="55c8a-162">Zabezpieczenia serwera sieci web przy użyciu protokołu SSL</span><span class="sxs-lookup"><span data-stu-id="55c8a-162">Secure web server with SSL</span></span>](tutorial-secure-web-server.md)

[1]: ./media/tutorial-lemp-stack/configmysqlpassword-small.png
[2]: ./media/tutorial-lemp-stack/phpsuccesspage.png
[3]: ./media/tutorial-lemp-stack/nginx.png
