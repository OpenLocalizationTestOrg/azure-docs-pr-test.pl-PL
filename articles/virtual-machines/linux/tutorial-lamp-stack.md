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
# <a name="install-a-lamp-web-server-on-an-azure-vm"></a><span data-ttu-id="1bef4-103">Instalacja serwera sieci web światła w maszynie Wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="1bef4-103">Install a LAMP web server on an Azure VM</span></span>
<span data-ttu-id="1bef4-104">W tym artykule przedstawiono sposób toodeploy Apache serwera sieci web, MySQL i PHP (stos hello światła) na maszynie Wirtualnej systemu Ubuntu na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="1bef4-104">This article walks you through how toodeploy an Apache web server, MySQL, and PHP (hello LAMP stack) on an Ubuntu VM in Azure.</span></span> <span data-ttu-id="1bef4-105">Jeśli chcesz, aby serwer sieci web hello NGINX, zobacz hello [stosu LEMP](tutorial-lemp-stack.md) samouczka.</span><span class="sxs-lookup"><span data-stu-id="1bef4-105">If you prefer hello NGINX web server, see hello [LEMP stack](tutorial-lemp-stack.md) tutorial.</span></span> <span data-ttu-id="1bef4-106">toosee hello światła serwera akcji, można opcjonalnie zainstalować i skonfigurować witrynę WordPress.</span><span class="sxs-lookup"><span data-stu-id="1bef4-106">toosee hello LAMP server in action, you can optionally install and configure a WordPress site.</span></span> <span data-ttu-id="1bef4-107">Ten samouczek zawiera informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="1bef4-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1bef4-108">Tworzenie maszyny Wirtualnej systemu Ubuntu (hello "L" hello światła stosu)</span><span class="sxs-lookup"><span data-stu-id="1bef4-108">Create an Ubuntu VM (hello 'L' in hello LAMP stack)</span></span>
> * <span data-ttu-id="1bef4-109">Otwieranie portu 80 na potrzeby ruchu w sieci Web</span><span class="sxs-lookup"><span data-stu-id="1bef4-109">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="1bef4-110">Instalowanie Apache, MySQL i PHP</span><span class="sxs-lookup"><span data-stu-id="1bef4-110">Install Apache, MySQL, and PHP</span></span>
> * <span data-ttu-id="1bef4-111">Sprawdź, instalacja i Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="1bef4-111">Verify installation and configuration</span></span>
> * <span data-ttu-id="1bef4-112">Zainstaluj program WordPress na serwerze światła hello</span><span class="sxs-lookup"><span data-stu-id="1bef4-112">Install WordPress on hello LAMP server</span></span>


<span data-ttu-id="1bef4-113">Aby uzyskać więcej informacji na stosie światła hello, w tym zalecenia w środowisku produkcyjnym, zobacz hello [dokumentacji Ubuntu](https://help.ubuntu.com/community/ApacheMySQLPHP).</span><span class="sxs-lookup"><span data-stu-id="1bef4-113">For more on hello LAMP stack, including recommendations for a production environment, see hello [Ubuntu documentation](https://help.ubuntu.com/community/ApacheMySQLPHP).</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="1bef4-114">Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym samouczku wymaga działają hello Azure CLI w wersji 2.0.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="1bef4-114">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="1bef4-115">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="1bef4-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="1bef4-116">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="1bef4-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [virtual-machines-linux-tutorial-stack-intro.md](../../../includes/virtual-machines-linux-tutorial-stack-intro.md)]

## <a name="install-apache-mysql-and-php"></a><span data-ttu-id="1bef4-117">Instalowanie Apache, MySQL i PHP</span><span class="sxs-lookup"><span data-stu-id="1bef4-117">Install Apache, MySQL, and PHP</span></span>

<span data-ttu-id="1bef4-118">Uruchom następujące polecenie tooupdate Ubuntu pakietu źródła hello i zainstaluj Apache, MySQL i PHP.</span><span class="sxs-lookup"><span data-stu-id="1bef4-118">Run hello following command tooupdate Ubuntu package sources and install Apache, MySQL, and PHP.</span></span> <span data-ttu-id="1bef4-119">Należy zwrócić uwagę hello daszek (^) na końcu hello hello polecenia.</span><span class="sxs-lookup"><span data-stu-id="1bef4-119">Note hello caret (^) at hello end of hello command.</span></span>


```bash
sudo apt update && sudo apt install lamp-server^
```



<span data-ttu-id="1bef4-120">Jesteś pakietów hello zostanie wyświetlony monit o tooinstall i innych zależności.</span><span class="sxs-lookup"><span data-stu-id="1bef4-120">You are prompted tooinstall hello packages and other dependencies.</span></span> <span data-ttu-id="1bef4-121">Po wyświetleniu monitu MySQL, a następnie toocontinue [Enter] należy ustawić hasło główne.</span><span class="sxs-lookup"><span data-stu-id="1bef4-121">When prompted, set a root password for MySQL, and then [Enter] toocontinue.</span></span> <span data-ttu-id="1bef4-122">Wykonaj hello pozostałych monitów.</span><span class="sxs-lookup"><span data-stu-id="1bef4-122">Follow hello remaining prompts.</span></span> <span data-ttu-id="1bef4-123">Ten proces instaluje hello minimalne wymagane PHP rozszerzenia potrzebne toouse PHP z programem MySQL.</span><span class="sxs-lookup"><span data-stu-id="1bef4-123">This process installs hello minimum required PHP extensions needed toouse PHP with MySQL.</span></span> 

![Strona hasła głównego MySQL][1]

## <a name="verify-installation-and-configuration"></a><span data-ttu-id="1bef4-125">Sprawdź, instalacja i Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="1bef4-125">Verify installation and configuration</span></span>


### <a name="apache"></a><span data-ttu-id="1bef4-126">Apache</span><span class="sxs-lookup"><span data-stu-id="1bef4-126">Apache</span></span>

<span data-ttu-id="1bef4-127">Sprawdź wersję hello Apache z hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="1bef4-127">Check hello version of Apache with hello following command:</span></span>
```bash
apache2 -v
```

<span data-ttu-id="1bef4-128">Apache zainstalowana i port 80 Otwórz tooyour maszyny Wirtualnej, powitania serwera sieci web jest teraz dostępna z hello internet.</span><span class="sxs-lookup"><span data-stu-id="1bef4-128">With Apache installed, and port 80 open tooyour VM, hello web server can now be accessed from hello internet.</span></span> <span data-ttu-id="1bef4-129">hello tooview Apache2 Ubuntu strona domyślna, otwórz przeglądarkę sieci web, a następnie wprowadź hello publicznego adresu IP hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1bef4-129">tooview hello Apache2 Ubuntu Default Page, open a web browser, and enter hello public IP address of hello VM.</span></span> <span data-ttu-id="1bef4-130">Użyj hello publiczny adres IP używany toohello tooSSH maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="1bef4-130">Use hello public IP address you used tooSSH toohello VM:</span></span>

![Apache domyślnej strony][3]


### <a name="mysql"></a><span data-ttu-id="1bef4-132">MySQL</span><span class="sxs-lookup"><span data-stu-id="1bef4-132">MySQL</span></span>

<span data-ttu-id="1bef4-133">Sprawdź wersję hello MySQL z hello następujące polecenie (należy pamiętać, kapitału hello `V` parametru):</span><span class="sxs-lookup"><span data-stu-id="1bef4-133">Check hello version of MySQL with hello following command (note hello capital `V` parameter):</span></span>

```bash
msql -V
```

<span data-ttu-id="1bef4-134">Zaleca się uruchomienie skryptu toohelp hello bezpiecznej instalacji programu MySQL hello:</span><span class="sxs-lookup"><span data-stu-id="1bef4-134">We recommend running hello following script toohelp secure hello installation of MySQL:</span></span>

```bash
mysql_secure_installation
```

<span data-ttu-id="1bef4-135">Wprowadź hasło głównego MySQL i skonfiguruj ustawienia zabezpieczeń hello w danym środowisku.</span><span class="sxs-lookup"><span data-stu-id="1bef4-135">Enter your MySQL root password, and configure hello security settings for your environment.</span></span>

<span data-ttu-id="1bef4-136">Jeśli chcesz toocreate bazę danych MySQL, dodać użytkowników lub zmienić ustawienia konfiguracji, tooMySQL logowania:</span><span class="sxs-lookup"><span data-stu-id="1bef4-136">If you want toocreate a MySQL database, add users, or change configuration settings, login tooMySQL:</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="1bef4-137">Po zakończeniu zamknij wiersz mysql hello wpisując `\q`.</span><span class="sxs-lookup"><span data-stu-id="1bef4-137">When done, exit hello mysql prompt by typing `\q`.</span></span>

### <a name="php"></a><span data-ttu-id="1bef4-138">PHP</span><span class="sxs-lookup"><span data-stu-id="1bef4-138">PHP</span></span>

<span data-ttu-id="1bef4-139">Sprawdź wersję hello PHP z hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="1bef4-139">Check hello version of PHP with hello following command:</span></span>

```bash
php -v
```

<span data-ttu-id="1bef4-140">Dalsze tootest, utworzyć szybkie tooview strony informacji PHP w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="1bef4-140">If you want tootest further, create a quick PHP info page tooview in a browser.</span></span> <span data-ttu-id="1bef4-141">Witaj następujące polecenie tworzy stronę informacji PHP hello:</span><span class="sxs-lookup"><span data-stu-id="1bef4-141">hello following command creates hello PHP info page:</span></span>

```bash
sudo sh -c 'echo "<?php phpinfo(); ?>" > /var/www/html/info.php'
```

<span data-ttu-id="1bef4-142">Teraz można sprawdzić stronę informacji PHP hello utworzony.</span><span class="sxs-lookup"><span data-stu-id="1bef4-142">Now you can check hello PHP info page you created.</span></span> <span data-ttu-id="1bef4-143">Otwórz przeglądarkę i przejdź zbyt`http://yourPublicIPAddress/info.php`.</span><span class="sxs-lookup"><span data-stu-id="1bef4-143">Open a browser and go too`http://yourPublicIPAddress/info.php`.</span></span> <span data-ttu-id="1bef4-144">Zastąp hello publicznego adresu IP maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1bef4-144">Substitute hello public IP address of your VM.</span></span> <span data-ttu-id="1bef4-145">Jego wygląd powinien być podobny toothis obrazu.</span><span class="sxs-lookup"><span data-stu-id="1bef4-145">It should look similar toothis image.</span></span>

![Strona informacje o PHP][2]

[!INCLUDE [virtual-machines-linux-tutorial-wordpress.md](../../../includes/virtual-machines-linux-tutorial-wordpress.md)]


## <a name="next-steps"></a><span data-ttu-id="1bef4-147">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1bef4-147">Next steps</span></span>

<span data-ttu-id="1bef4-148">W tym samouczku wdrożono serwer światła na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="1bef4-148">In this tutorial, you deployed a LAMP server in Azure.</span></span> <span data-ttu-id="1bef4-149">W tym samouczku omówiono:</span><span class="sxs-lookup"><span data-stu-id="1bef4-149">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1bef4-150">Tworzenie maszyny Wirtualnej systemu Ubuntu</span><span class="sxs-lookup"><span data-stu-id="1bef4-150">Create an Ubuntu VM</span></span>
> * <span data-ttu-id="1bef4-151">Otwieranie portu 80 na potrzeby ruchu w sieci Web</span><span class="sxs-lookup"><span data-stu-id="1bef4-151">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="1bef4-152">Instalowanie Apache, MySQL i PHP</span><span class="sxs-lookup"><span data-stu-id="1bef4-152">Install Apache, MySQL, and PHP</span></span>
> * <span data-ttu-id="1bef4-153">Sprawdź, instalacja i Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="1bef4-153">Verify installation and configuration</span></span>
> * <span data-ttu-id="1bef4-154">Zainstaluj program WordPress na serwerze światła hello</span><span class="sxs-lookup"><span data-stu-id="1bef4-154">Install WordPress on hello LAMP server</span></span>

<span data-ttu-id="1bef4-155">Jak przejść dalej toolearn samouczka toohello toosecure serwerów sieci web z certyfikatów SSL.</span><span class="sxs-lookup"><span data-stu-id="1bef4-155">Advance toohello next tutorial toolearn how toosecure web servers with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1bef4-156">Zabezpieczenia serwera sieci web przy użyciu protokołu SSL</span><span class="sxs-lookup"><span data-stu-id="1bef4-156">Secure web server with SSL</span></span>](tutorial-secure-web-server.md)

[1]: ./media/tutorial-lamp-stack/configmysqlpassword-small.png
[2]: ./media/tutorial-lamp-stack/phpsuccesspage.png
[3]: ./media/tutorial-lamp-stack/apachesuccesspage.png