---
title: "Wdrażanie LEMP na maszynie wirtualnej systemu Linux na platformie Azure | Dokumentacja firmy Microsoft"
description: "Samouczek — instalacja stosu LEMP na maszynie Wirtualnej systemu Linux na platformie Azure"
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
ms.openlocfilehash: 653af144eb12cacf955f96a5442efd73add38e88
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="install-a-lemp-web-server-on-an-azure-vm"></a><span data-ttu-id="e05d1-103">Zainstaluj serwer sieci web LEMP na maszynie Wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e05d1-103">Install a LEMP web server on an Azure VM</span></span>
<span data-ttu-id="e05d1-104">W tym artykule przedstawiono sposób wdrażania serwera sieci web NGINX, MySQL i PHP (stos LEMP) na maszynie Wirtualnej systemu Ubuntu na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="e05d1-104">This article walks you through how to deploy an NGINX web server, MySQL, and PHP (the LEMP stack) on an Ubuntu VM in Azure.</span></span> <span data-ttu-id="e05d1-105">Stos LEMP stanowi alternatywę dla popularnych [stosu światła](tutorial-lamp-stack.md), które można także zainstalować na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="e05d1-105">The LEMP stack is an alternative to the popular [LAMP stack](tutorial-lamp-stack.md), which you can also install in Azure.</span></span> <span data-ttu-id="e05d1-106">Aby wyświetlić serwera LEMP w akcji, można opcjonalnie zainstalować i skonfigurować witrynę WordPress.</span><span class="sxs-lookup"><span data-stu-id="e05d1-106">To see the LEMP server in action, you can optionally install and configure a WordPress site.</span></span> <span data-ttu-id="e05d1-107">Ten samouczek zawiera informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="e05d1-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e05d1-108">Tworzenie maszyny Wirtualnej systemu Ubuntu ("L" w stosie LEMP)</span><span class="sxs-lookup"><span data-stu-id="e05d1-108">Create an Ubuntu VM (the 'L' in the LEMP stack)</span></span>
> * <span data-ttu-id="e05d1-109">Otwieranie portu 80 na potrzeby ruchu w sieci Web</span><span class="sxs-lookup"><span data-stu-id="e05d1-109">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="e05d1-110">Zainstaluj NGINX, MySQL i PHP</span><span class="sxs-lookup"><span data-stu-id="e05d1-110">Install NGINX, MySQL, and PHP</span></span>
> * <span data-ttu-id="e05d1-111">Sprawdź, instalacja i Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="e05d1-111">Verify installation and configuration</span></span>
> * <span data-ttu-id="e05d1-112">Zainstaluj program WordPress na serwerze LEMP</span><span class="sxs-lookup"><span data-stu-id="e05d1-112">Install WordPress on the LEMP server</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="e05d1-113">Jeśli wybierzesz do zainstalowania i używania interfejsu wiersza polecenia lokalnie, w tym samouczku wymaga używasz interfejsu wiersza polecenia Azure w wersji 2.0.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="e05d1-113">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="e05d1-114">Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="e05d1-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="e05d1-115">Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e05d1-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [virtual-machines-linux-tutorial-stack-intro.md](../../../includes/virtual-machines-linux-tutorial-stack-intro.md)]

## <a name="install-nginx-mysql-and-php"></a><span data-ttu-id="e05d1-116">Zainstaluj NGINX, MySQL i PHP</span><span class="sxs-lookup"><span data-stu-id="e05d1-116">Install NGINX, MySQL, and PHP</span></span>

<span data-ttu-id="e05d1-117">Uruchom następujące polecenie, aby zaktualizować źródła pakietu Ubuntu i zainstaluj NGINX, MySQL i PHP.</span><span class="sxs-lookup"><span data-stu-id="e05d1-117">Run the following command to update Ubuntu package sources and install NGINX, MySQL, and PHP.</span></span> 

```bash
sudo apt update && sudo apt install nginx mysql-server php-mysql php php-fpm
```

<span data-ttu-id="e05d1-118">Monit, aby zainstalować pakiety i innych zależności.</span><span class="sxs-lookup"><span data-stu-id="e05d1-118">You are prompted to install the packages and other dependencies.</span></span> <span data-ttu-id="e05d1-119">Po wyświetleniu monitu ustawienia hasła głównego dla programu MySQL, a następnie [Enter], aby kontynuować.</span><span class="sxs-lookup"><span data-stu-id="e05d1-119">When prompted, set a root password for MySQL, and then [Enter] to continue.</span></span> <span data-ttu-id="e05d1-120">Postępuj zgodnie z monitami pozostałych.</span><span class="sxs-lookup"><span data-stu-id="e05d1-120">Follow the remaining prompts.</span></span> <span data-ttu-id="e05d1-121">Ten proces instaluje minimalne wymagane rozszerzeń PHP potrzebne do korzystania z MySQL PHP.</span><span class="sxs-lookup"><span data-stu-id="e05d1-121">This process installs the minimum required PHP extensions needed to use PHP with MySQL.</span></span> 

![Strona hasła głównego MySQL][1]

## <a name="verify-installation-and-configuration"></a><span data-ttu-id="e05d1-123">Sprawdź, instalacja i Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="e05d1-123">Verify installation and configuration</span></span>


### <a name="nginx"></a><span data-ttu-id="e05d1-124">NGINX</span><span class="sxs-lookup"><span data-stu-id="e05d1-124">NGINX</span></span>

<span data-ttu-id="e05d1-125">Sprawdź wersję programu NGINX przy użyciu następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="e05d1-125">Check the version of NGINX with the following command:</span></span>
```bash
nginx -v
```

<span data-ttu-id="e05d1-126">Z NGINX zainstalowane, a port 80 jest otwarty do maszyny Wirtualnej teraz są dostępne serwera sieci web z Internetu.</span><span class="sxs-lookup"><span data-stu-id="e05d1-126">With NGINX installed, and port 80 open to your VM, the web server can now be accessed from the internet.</span></span> <span data-ttu-id="e05d1-127">Aby wyświetlić stronę powitalną NGINX, otwórz przeglądarkę sieci web, a następnie wprowadź publiczny adres IP maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e05d1-127">To view the NGINX welcome page, open a web browser, and enter the public IP address of the VM.</span></span> <span data-ttu-id="e05d1-128">Użyj publicznego adresu IP używanego do SSH do maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="e05d1-128">Use the public IP address you used to SSH to the VM:</span></span>

![NGINX domyślnej strony][3]


### <a name="mysql"></a><span data-ttu-id="e05d1-130">MySQL</span><span class="sxs-lookup"><span data-stu-id="e05d1-130">MySQL</span></span>

<span data-ttu-id="e05d1-131">Sprawdź wersję programu MySQL przy użyciu następującego polecenia (należy pamiętać, kapitału `V` parametru):</span><span class="sxs-lookup"><span data-stu-id="e05d1-131">Check the version of MySQL with the following command (note the capital `V` parameter):</span></span>

```bash
msql -V
```

<span data-ttu-id="e05d1-132">Zaleca się uruchomienie następujący skrypt, aby pomóc w zabezpieczeniu instalacji MySQL:</span><span class="sxs-lookup"><span data-stu-id="e05d1-132">We recommend running the following script to help secure the installation of MySQL:</span></span>

```bash
mysql_secure_installation
```

<span data-ttu-id="e05d1-133">Wprowadź hasło głównego MySQL i skonfiguruj ustawienia zabezpieczeń dla danego środowiska.</span><span class="sxs-lookup"><span data-stu-id="e05d1-133">Enter your MySQL root password, and configure the security settings for your environment.</span></span>

<span data-ttu-id="e05d1-134">Jeśli chcesz utworzyć bazę danych MySQL, dodać użytkowników, lub zmienić ustawienia konfiguracji, zaloguj się do MySQL:</span><span class="sxs-lookup"><span data-stu-id="e05d1-134">If you want to create a MySQL database, add users, or change configuration settings, login to MySQL:</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="e05d1-135">Po zakończeniu zamknij wiersz mysql, wpisując `\q`.</span><span class="sxs-lookup"><span data-stu-id="e05d1-135">When done, exit the mysql prompt by typing `\q`.</span></span>

### <a name="php"></a><span data-ttu-id="e05d1-136">PHP</span><span class="sxs-lookup"><span data-stu-id="e05d1-136">PHP</span></span>

<span data-ttu-id="e05d1-137">Sprawdź wersję programu PHP za pomocą następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="e05d1-137">Check the version of PHP with the following command:</span></span>

```bash
php -v
```

<span data-ttu-id="e05d1-138">Skonfiguruj NGINX, aby użyć Menedżera procesu FastCGI PHP (PHP FPM).</span><span class="sxs-lookup"><span data-stu-id="e05d1-138">Configure NGINX to use the PHP FastCGI Process Manager (PHP-FPM).</span></span> <span data-ttu-id="e05d1-139">Uruchom następujące polecenia, aby utworzyć kopię zapasową oryginalnego pliku konfiguracji blok serwera NGINX, a następnie edytuj oryginalny plik w wybranym edytorze:</span><span class="sxs-lookup"><span data-stu-id="e05d1-139">Run the following commands to back up the original NGINX server block config file and then edit the original file in an editor of your choice:</span></span>

```bash
sudo cp /etc/nginx/sites-available/default /etc/nginx/sites-available/default_backup

sudo sensible-editor /etc/nginx/sites-available/default
```

<span data-ttu-id="e05d1-140">W edytorze, Zastąp zawartość `/etc/nginx/sites-available/default` następującym kodem.</span><span class="sxs-lookup"><span data-stu-id="e05d1-140">In the editor, replace the contents of `/etc/nginx/sites-available/default` with the following.</span></span> <span data-ttu-id="e05d1-141">Zobacz komentarze opis ustawienia.</span><span class="sxs-lookup"><span data-stu-id="e05d1-141">See the comments for explanation of the settings.</span></span> <span data-ttu-id="e05d1-142">Zastąp publicznego adresu IP dla maszyny Wirtualnej *yourPublicIPAddress*i pozostawić pozostałe ustawienia.</span><span class="sxs-lookup"><span data-stu-id="e05d1-142">Substitute the public IP address of your VM for *yourPublicIPAddress*, and leave the remaining settings.</span></span> <span data-ttu-id="e05d1-143">Następnie zapisz plik.</span><span class="sxs-lookup"><span data-stu-id="e05d1-143">Then save the file.</span></span>

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

<span data-ttu-id="e05d1-144">Sprawdź konfigurację NGINX błędy składniowe:</span><span class="sxs-lookup"><span data-stu-id="e05d1-144">Check the NGINX configuration for syntax errors:</span></span>

```bash
sudo nginx -t
```

<span data-ttu-id="e05d1-145">Jeśli składnia jest poprawna, uruchom ponownie NGINX za pomocą następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="e05d1-145">If the syntax is correct, restart NGINX with the following command:</span></span>

```bash
sudo service nginx restart
```

<span data-ttu-id="e05d1-146">Jeśli chcesz przetestować dalsze, Utwórz szybkie stronę informacji PHP do wyświetlania w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="e05d1-146">If you want to test further, create a quick PHP info page to view in a browser.</span></span> <span data-ttu-id="e05d1-147">Poniższe polecenie tworzy stronę informacji PHP:</span><span class="sxs-lookup"><span data-stu-id="e05d1-147">The following command creates the PHP info page:</span></span>

```bash
sudo sh -c 'echo "<?php phpinfo(); ?>" > /var/www/html/info.php'
```



<span data-ttu-id="e05d1-148">Teraz można sprawdzić stronę informacji PHP utworzony.</span><span class="sxs-lookup"><span data-stu-id="e05d1-148">Now you can check the PHP info page you created.</span></span> <span data-ttu-id="e05d1-149">Otwórz przeglądarkę i przejdź do `http://yourPublicIPAddress/info.php`.</span><span class="sxs-lookup"><span data-stu-id="e05d1-149">Open a browser and go to `http://yourPublicIPAddress/info.php`.</span></span> <span data-ttu-id="e05d1-150">Należy zastąpić publicznego adresu IP maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e05d1-150">Substitute the public IP address of your VM.</span></span> <span data-ttu-id="e05d1-151">Powinien być podobny do tego obrazu.</span><span class="sxs-lookup"><span data-stu-id="e05d1-151">It should look similar to this image.</span></span>

![Strona informacje o PHP][2]


[!INCLUDE [virtual-machines-linux-tutorial-wordpress.md](../../../includes/virtual-machines-linux-tutorial-wordpress.md)]

## <a name="next-steps"></a><span data-ttu-id="e05d1-153">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e05d1-153">Next steps</span></span>

<span data-ttu-id="e05d1-154">W tym samouczku wdrożono serwer LEMP na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="e05d1-154">In this tutorial, you deployed a LEMP server in Azure.</span></span> <span data-ttu-id="e05d1-155">Możesz przedstawiono sposób do:</span><span class="sxs-lookup"><span data-stu-id="e05d1-155">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e05d1-156">Tworzenie maszyny Wirtualnej systemu Ubuntu</span><span class="sxs-lookup"><span data-stu-id="e05d1-156">Create an Ubuntu VM</span></span>
> * <span data-ttu-id="e05d1-157">Otwieranie portu 80 na potrzeby ruchu w sieci Web</span><span class="sxs-lookup"><span data-stu-id="e05d1-157">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="e05d1-158">Zainstaluj NGINX, MySQL i PHP</span><span class="sxs-lookup"><span data-stu-id="e05d1-158">Install NGINX, MySQL, and PHP</span></span>
> * <span data-ttu-id="e05d1-159">Sprawdź, instalacja i Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="e05d1-159">Verify installation and configuration</span></span>
> * <span data-ttu-id="e05d1-160">Zainstaluj program WordPress na stosie LEMP</span><span class="sxs-lookup"><span data-stu-id="e05d1-160">Install WordPress on the LEMP stack</span></span>

<span data-ttu-id="e05d1-161">Przejście do następnym samouczku, aby dowiedzieć się, jak zabezpieczyć serwerów sieci web za pomocą certyfikatów SSL.</span><span class="sxs-lookup"><span data-stu-id="e05d1-161">Advance to the next tutorial to learn how to secure web servers with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e05d1-162">Zabezpieczenia serwera sieci web przy użyciu protokołu SSL</span><span class="sxs-lookup"><span data-stu-id="e05d1-162">Secure web server with SSL</span></span>](tutorial-secure-web-server.md)

[1]: ./media/tutorial-lemp-stack/configmysqlpassword-small.png
[2]: ./media/tutorial-lemp-stack/phpsuccesspage.png
[3]: ./media/tutorial-lemp-stack/nginx.png
