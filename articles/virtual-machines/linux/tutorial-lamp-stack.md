---
title: "Wdrażanie światła na maszynie wirtualnej systemu Linux na platformie Azure | Dokumentacja firmy Microsoft"
description: "Samouczek — instalacja stosu światła na maszynie Wirtualnej systemu Linux na platformie Azure"
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
ms.openlocfilehash: 9148ac9646e4e1cfeff8f20c096e390499437e78
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="install-a-lamp-web-server-on-an-azure-vm"></a><span data-ttu-id="30e17-103">Instalacja serwera sieci web światła w maszynie Wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="30e17-103">Install a LAMP web server on an Azure VM</span></span>
<span data-ttu-id="30e17-104">W tym artykule przedstawiono sposób wdrażania serwera sieci web Apache, MySQL i PHP (stos światła) na maszynie Wirtualnej systemu Ubuntu na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="30e17-104">This article walks you through how to deploy an Apache web server, MySQL, and PHP (the LAMP stack) on an Ubuntu VM in Azure.</span></span> <span data-ttu-id="30e17-105">Jeśli wolisz NGINX serwera sieci web, zobacz [stosu LEMP](tutorial-lemp-stack.md) samouczka.</span><span class="sxs-lookup"><span data-stu-id="30e17-105">If you prefer the NGINX web server, see the [LEMP stack](tutorial-lemp-stack.md) tutorial.</span></span> <span data-ttu-id="30e17-106">Aby wyświetlić serwera światła w akcji, można opcjonalnie zainstalować i skonfigurować witrynę WordPress.</span><span class="sxs-lookup"><span data-stu-id="30e17-106">To see the LAMP server in action, you can optionally install and configure a WordPress site.</span></span> <span data-ttu-id="30e17-107">Ten samouczek zawiera informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="30e17-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="30e17-108">Tworzenie maszyny Wirtualnej systemu Ubuntu ("L" w stosie światła)</span><span class="sxs-lookup"><span data-stu-id="30e17-108">Create an Ubuntu VM (the 'L' in the LAMP stack)</span></span>
> * <span data-ttu-id="30e17-109">Otwieranie portu 80 na potrzeby ruchu w sieci Web</span><span class="sxs-lookup"><span data-stu-id="30e17-109">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="30e17-110">Instalowanie Apache, MySQL i PHP</span><span class="sxs-lookup"><span data-stu-id="30e17-110">Install Apache, MySQL, and PHP</span></span>
> * <span data-ttu-id="30e17-111">Sprawdź, instalacja i Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="30e17-111">Verify installation and configuration</span></span>
> * <span data-ttu-id="30e17-112">Zainstaluj program WordPress na serwerze światła</span><span class="sxs-lookup"><span data-stu-id="30e17-112">Install WordPress on the LAMP server</span></span>


<span data-ttu-id="30e17-113">Aby uzyskać więcej informacji na temat stosu światło, w tym zalecenia w środowisku produkcyjnym zobacz [dokumentacji Ubuntu](https://help.ubuntu.com/community/ApacheMySQLPHP).</span><span class="sxs-lookup"><span data-stu-id="30e17-113">For more on the LAMP stack, including recommendations for a production environment, see the [Ubuntu documentation](https://help.ubuntu.com/community/ApacheMySQLPHP).</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="30e17-114">Jeśli wybierzesz do zainstalowania i używania interfejsu wiersza polecenia lokalnie, w tym samouczku wymaga używasz interfejsu wiersza polecenia Azure w wersji 2.0.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="30e17-114">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="30e17-115">Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="30e17-115">Run `az --version` to find the version.</span></span> <span data-ttu-id="30e17-116">Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="30e17-116">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [virtual-machines-linux-tutorial-stack-intro.md](../../../includes/virtual-machines-linux-tutorial-stack-intro.md)]

## <a name="install-apache-mysql-and-php"></a><span data-ttu-id="30e17-117">Instalowanie Apache, MySQL i PHP</span><span class="sxs-lookup"><span data-stu-id="30e17-117">Install Apache, MySQL, and PHP</span></span>

<span data-ttu-id="30e17-118">Uruchom następujące polecenie, aby zaktualizować źródła pakietu Ubuntu i zainstaluj Apache, MySQL i PHP.</span><span class="sxs-lookup"><span data-stu-id="30e17-118">Run the following command to update Ubuntu package sources and install Apache, MySQL, and PHP.</span></span> <span data-ttu-id="30e17-119">Należy pamiętać, daszek (^) na końcu polecenia.</span><span class="sxs-lookup"><span data-stu-id="30e17-119">Note the caret (^) at the end of the command.</span></span>


```bash
sudo apt update && sudo apt install lamp-server^
```



<span data-ttu-id="30e17-120">Monit, aby zainstalować pakiety i innych zależności.</span><span class="sxs-lookup"><span data-stu-id="30e17-120">You are prompted to install the packages and other dependencies.</span></span> <span data-ttu-id="30e17-121">Po wyświetleniu monitu ustawienia hasła głównego dla programu MySQL, a następnie [Enter], aby kontynuować.</span><span class="sxs-lookup"><span data-stu-id="30e17-121">When prompted, set a root password for MySQL, and then [Enter] to continue.</span></span> <span data-ttu-id="30e17-122">Postępuj zgodnie z monitami pozostałych.</span><span class="sxs-lookup"><span data-stu-id="30e17-122">Follow the remaining prompts.</span></span> <span data-ttu-id="30e17-123">Ten proces instaluje minimalne wymagane rozszerzeń PHP potrzebne do korzystania z MySQL PHP.</span><span class="sxs-lookup"><span data-stu-id="30e17-123">This process installs the minimum required PHP extensions needed to use PHP with MySQL.</span></span> 

![Strona hasła głównego MySQL][1]

## <a name="verify-installation-and-configuration"></a><span data-ttu-id="30e17-125">Sprawdź, instalacja i Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="30e17-125">Verify installation and configuration</span></span>


### <a name="apache"></a><span data-ttu-id="30e17-126">Apache</span><span class="sxs-lookup"><span data-stu-id="30e17-126">Apache</span></span>

<span data-ttu-id="30e17-127">Sprawdź wersję programu Apache przy użyciu następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="30e17-127">Check the version of Apache with the following command:</span></span>
```bash
apache2 -v
```

<span data-ttu-id="30e17-128">Apache zainstalowana, i port 80 jest otwarty do maszyny Wirtualnej teraz są dostępne serwera sieci web z Internetu.</span><span class="sxs-lookup"><span data-stu-id="30e17-128">With Apache installed, and port 80 open to your VM, the web server can now be accessed from the internet.</span></span> <span data-ttu-id="30e17-129">Aby wyświetlić stronę domyślne Ubuntu Apache2, otwórz przeglądarkę sieci web, a następnie wprowadź publiczny adres IP maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="30e17-129">To view the Apache2 Ubuntu Default Page, open a web browser, and enter the public IP address of the VM.</span></span> <span data-ttu-id="30e17-130">Użyj publicznego adresu IP używanego do SSH do maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="30e17-130">Use the public IP address you used to SSH to the VM:</span></span>

![Apache domyślnej strony][3]


### <a name="mysql"></a><span data-ttu-id="30e17-132">MySQL</span><span class="sxs-lookup"><span data-stu-id="30e17-132">MySQL</span></span>

<span data-ttu-id="30e17-133">Sprawdź wersję programu MySQL przy użyciu następującego polecenia (należy pamiętać, kapitału `V` parametru):</span><span class="sxs-lookup"><span data-stu-id="30e17-133">Check the version of MySQL with the following command (note the capital `V` parameter):</span></span>

```bash
msql -V
```

<span data-ttu-id="30e17-134">Zaleca się uruchomienie następujący skrypt, aby pomóc w zabezpieczeniu instalacji MySQL:</span><span class="sxs-lookup"><span data-stu-id="30e17-134">We recommend running the following script to help secure the installation of MySQL:</span></span>

```bash
mysql_secure_installation
```

<span data-ttu-id="30e17-135">Wprowadź hasło głównego MySQL i skonfiguruj ustawienia zabezpieczeń dla danego środowiska.</span><span class="sxs-lookup"><span data-stu-id="30e17-135">Enter your MySQL root password, and configure the security settings for your environment.</span></span>

<span data-ttu-id="30e17-136">Jeśli chcesz utworzyć bazę danych MySQL, dodać użytkowników, lub zmienić ustawienia konfiguracji, zaloguj się do MySQL:</span><span class="sxs-lookup"><span data-stu-id="30e17-136">If you want to create a MySQL database, add users, or change configuration settings, login to MySQL:</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="30e17-137">Po zakończeniu zamknij wiersz mysql, wpisując `\q`.</span><span class="sxs-lookup"><span data-stu-id="30e17-137">When done, exit the mysql prompt by typing `\q`.</span></span>

### <a name="php"></a><span data-ttu-id="30e17-138">PHP</span><span class="sxs-lookup"><span data-stu-id="30e17-138">PHP</span></span>

<span data-ttu-id="30e17-139">Sprawdź wersję programu PHP za pomocą następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="30e17-139">Check the version of PHP with the following command:</span></span>

```bash
php -v
```

<span data-ttu-id="30e17-140">Jeśli chcesz przetestować dalsze, Utwórz szybkie stronę informacji PHP do wyświetlania w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="30e17-140">If you want to test further, create a quick PHP info page to view in a browser.</span></span> <span data-ttu-id="30e17-141">Poniższe polecenie tworzy stronę informacji PHP:</span><span class="sxs-lookup"><span data-stu-id="30e17-141">The following command creates the PHP info page:</span></span>

```bash
sudo sh -c 'echo "<?php phpinfo(); ?>" > /var/www/html/info.php'
```

<span data-ttu-id="30e17-142">Teraz można sprawdzić stronę informacji PHP utworzony.</span><span class="sxs-lookup"><span data-stu-id="30e17-142">Now you can check the PHP info page you created.</span></span> <span data-ttu-id="30e17-143">Otwórz przeglądarkę i przejdź do `http://yourPublicIPAddress/info.php`.</span><span class="sxs-lookup"><span data-stu-id="30e17-143">Open a browser and go to `http://yourPublicIPAddress/info.php`.</span></span> <span data-ttu-id="30e17-144">Należy zastąpić publicznego adresu IP maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="30e17-144">Substitute the public IP address of your VM.</span></span> <span data-ttu-id="30e17-145">Powinien być podobny do tego obrazu.</span><span class="sxs-lookup"><span data-stu-id="30e17-145">It should look similar to this image.</span></span>

![Strona informacje o PHP][2]

[!INCLUDE [virtual-machines-linux-tutorial-wordpress.md](../../../includes/virtual-machines-linux-tutorial-wordpress.md)]


## <a name="next-steps"></a><span data-ttu-id="30e17-147">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="30e17-147">Next steps</span></span>

<span data-ttu-id="30e17-148">W tym samouczku wdrożono serwer światła na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="30e17-148">In this tutorial, you deployed a LAMP server in Azure.</span></span> <span data-ttu-id="30e17-149">Możesz przedstawiono sposób do:</span><span class="sxs-lookup"><span data-stu-id="30e17-149">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="30e17-150">Tworzenie maszyny Wirtualnej systemu Ubuntu</span><span class="sxs-lookup"><span data-stu-id="30e17-150">Create an Ubuntu VM</span></span>
> * <span data-ttu-id="30e17-151">Otwieranie portu 80 na potrzeby ruchu w sieci Web</span><span class="sxs-lookup"><span data-stu-id="30e17-151">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="30e17-152">Instalowanie Apache, MySQL i PHP</span><span class="sxs-lookup"><span data-stu-id="30e17-152">Install Apache, MySQL, and PHP</span></span>
> * <span data-ttu-id="30e17-153">Sprawdź, instalacja i Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="30e17-153">Verify installation and configuration</span></span>
> * <span data-ttu-id="30e17-154">Zainstaluj program WordPress na serwerze światła</span><span class="sxs-lookup"><span data-stu-id="30e17-154">Install WordPress on the LAMP server</span></span>

<span data-ttu-id="30e17-155">Przejście do następnym samouczku, aby dowiedzieć się, jak zabezpieczyć serwerów sieci web za pomocą certyfikatów SSL.</span><span class="sxs-lookup"><span data-stu-id="30e17-155">Advance to the next tutorial to learn how to secure web servers with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="30e17-156">Zabezpieczenia serwera sieci web przy użyciu protokołu SSL</span><span class="sxs-lookup"><span data-stu-id="30e17-156">Secure web server with SSL</span></span>](tutorial-secure-web-server.md)

[1]: ./media/tutorial-lamp-stack/configmysqlpassword-small.png
[2]: ./media/tutorial-lamp-stack/phpsuccesspage.png
[3]: ./media/tutorial-lamp-stack/apachesuccesspage.png