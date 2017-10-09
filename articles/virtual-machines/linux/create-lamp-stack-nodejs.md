---
title: "aaaDeploy światła na maszynie wirtualnej systemu Linux z hello Azure CLI 1.0 | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak hello tooinstall światła stosu na maszynie Wirtualnej systemu Linux na platformie Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: jluk
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 6c12603a-e391-4d3e-acce-442dd7ebb2fe
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: NA
ms.topic: article
ms.date: 2/21/2017
ms.author: juluk
ms.openlocfilehash: e78a82d388ce68710933b9b673aa1b2460bdbb14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-lamp-stack-with-hello-azure-cli-10"></a><span data-ttu-id="b3323-103">Wdrażanie światła stos hello Azure CLI w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="b3323-103">Deploy LAMP stack with hello Azure CLI 1.0</span></span>
<span data-ttu-id="b3323-104">W tym artykule przedstawiono sposób toodeploy Apache serwera sieci web, MySQL i PHP (stos hello światła) na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="b3323-104">This article walks you through how toodeploy an Apache web server, MySQL, and PHP (hello LAMP stack) on Azure.</span></span> <span data-ttu-id="b3323-105">Potrzebne jest konto platformy Azure ([Pobierz bezpłatną wersję próbną](https://azure.microsoft.com/pricing/free-trial/)) i hello [interfejsu wiersza polecenia Azure](../../cli-install-nodejs.md) oznacza to [połączone tooyour konta Azure](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="b3323-105">You need an Azure Account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)) and hello [Azure CLI](../../cli-install-nodejs.md) that is [connected tooyour Azure account](../../xplat-cli-connect.md).</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="b3323-106">Zadanie hello toocomplete wersje interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="b3323-106">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="b3323-107">Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="b3323-107">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="b3323-108">[1.0 interfejsu wiersza polecenia platformy azure] — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania wdrażania modeli (w tym artykule)</span><span class="sxs-lookup"><span data-stu-id="b3323-108">[Azure CLI 1.0] – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="b3323-109">[Azure CLI 2.0](create-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania zasobów hello</span><span class="sxs-lookup"><span data-stu-id="b3323-109">[Azure CLI 2.0](create-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>

```
# One command toocreate a resource group holding a VM with LAMP already on it
$ azure group create -n uniqueResourceGroup -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json
```

* <span data-ttu-id="b3323-110">Wdrażanie światła w istniejącej maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="b3323-110">Deploy LAMP on existing VM</span></span>

```
# Two commands: one updates packages, hello other installs Apache, MySQL, and PHP
user@ubuntu$ sudo apt-get update
user@ubuntu$ sudo apt-get install apache2 mysql-server php5 php5-mysql
```

## <a name="deploy-lamp-on-new-vm-walkthrough"></a><span data-ttu-id="b3323-111">Wdrażanie światła na nowe wskazówki maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="b3323-111">Deploy LAMP on new VM walkthrough</span></span>
<span data-ttu-id="b3323-112">Można uruchomić tworzenia [grupy zasobów](../../azure-resource-manager/resource-group-overview.md) który będzie zawierał hello nowej maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="b3323-112">You can start by creating a [resource group](../../azure-resource-manager/resource-group-overview.md) that will contain hello new VM:</span></span>

    $ azure group create uniqueResourceGroup westus
    info:    Executing command group create
    info:    Getting resource group uniqueResourceGroup
    info:    Creating resource group uniqueResourceGroup
    info:    Created resource group uniqueResourceGroup
    data:    Id:                  /subscriptions/########-####-####-####-############/resourceGroups/uniqueResourceGroup
    data:    Name:                uniqueResourceGroup
    data:    Location:            westus
    data:    Provisioning State:  Succeeded
    data:    Tags: null
    data:
    info:    group create command OK

<span data-ttu-id="b3323-113">toocreate hello samej maszyny Wirtualnej, można użyć już zapisany można odnaleźć szablonu usługi Azure Resource Manager [tutaj w serwisie GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).</span><span class="sxs-lookup"><span data-stu-id="b3323-113">toocreate hello VM itself, you can use an already written Azure Resource Manager template found [here on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).</span></span>

    $ azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json uniqueResourceGroup uniqueLampName

<span data-ttu-id="b3323-114">Powinna zostać wyświetlona odpowiedź monitowania niektórych więcej danych wejściowych:</span><span class="sxs-lookup"><span data-stu-id="b3323-114">You should see a response prompting some more inputs:</span></span>

    info:    Executing command group deployment create
    info:    Supply values for hello following parameters
    storageAccountNamePrefix: lampprefix
    location: westus
    adminUsername: someUsername
    adminPassword: somePassword
    mySqlPassword: somePassword
    dnsLabelPrefix: azlamptest
    info:    Initializing template configurations and parameters
    info:    Creating a deployment
    info:    Created template deployment "uniqueLampName"
    info:    Waiting for deployment toocomplete
    data:    DeploymentName     : uniqueLampName
    data:    ResourceGroupName  : uniqueResourceGroup
    data:    ProvisioningState  : Succeeded
    data:    Timestamp          :
    data:    Mode               : Incremental
    data:    CorrelationId      : d51bbf3c-88f1-4cf3-a8b3-942c6925f381
    data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json
    data:    ContentVersion     : 1.0.0.0
    data:    DeploymentParameters :
    data:    Name                      Type          Value
    data:    ------------------------  ------------  -----------
    data:    storageAccountNamePrefix  String        lampprefix
    data:    location                  String        westus
    data:    adminUsername             String        someUsername
    data:    adminPassword             SecureString  undefined
    data:    mySqlPassword             SecureString  undefined
    data:    dnsLabelPrefix            String        azlamptest
    data:    ubuntuOSVersion           String        14.04.2-LTS
    info:    group deployment create command OK

<span data-ttu-id="b3323-115">Maszynę wirtualną systemu Linux został utworzony z już zainstalowanym światła.</span><span class="sxs-lookup"><span data-stu-id="b3323-115">You have now created a Linux VM with LAMP already installed on it.</span></span> <span data-ttu-id="b3323-116">Jeśli chcesz, możesz sprawdzić hello instalacji przez przeskakiwanie dół za[Sprawdź światła pomyślnie zainstalował](#verify-lamp-successfully-installed).</span><span class="sxs-lookup"><span data-stu-id="b3323-116">If you wish, you can verify hello install by jumping down too[Verify LAMP Successfully Installed](#verify-lamp-successfully-installed).</span></span>

## <a name="deploy-lamp-on-existing-vm-walkthrough"></a><span data-ttu-id="b3323-117">Wdrażanie światła w istniejących wskazówki maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="b3323-117">Deploy LAMP on existing VM walkthrough</span></span>
<span data-ttu-id="b3323-118">Jeśli potrzebujesz pomocy tworzenia maszyny Wirtualnej systemu Linux, można head [toolearn tutaj jak toocreate Maszynę wirtualną systemu Linux](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b3323-118">If you need help creating a Linux VM, you can head [here toolearn how toocreate a Linux VM](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="b3323-119">Następnie należy tooSSH do hello maszyny Wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="b3323-119">Next, you need tooSSH into hello Linux VM.</span></span> <span data-ttu-id="b3323-120">Jeśli potrzebujesz pomocy dotyczącej Tworzenie klucza SSH, można head [toolearn tutaj jak toocreate klucza SSH w systemie Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b3323-120">If you need help with creating an SSH key, you can head [here toolearn how toocreate an SSH key on Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
<span data-ttu-id="b3323-121">Jeśli masz już klucz SSH, przejdź dalej i SSH w wierszu polecenia do maszyny Wirtualnej systemu Linux z `ssh exampleUsername@exampleDNS`.</span><span class="sxs-lookup"><span data-stu-id="b3323-121">If you have an SSH key already, go ahead and SSH from your command line into your Linux VM with `ssh exampleUsername@exampleDNS`.</span></span>

<span data-ttu-id="b3323-122">Teraz, gdy pracujesz w sieci maszyny Wirtualnej systemu Linux, możemy przeprowadzenie instalacji stosu światła hello na podstawie Debian dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="b3323-122">Now that you are working within your Linux VM, we can walk through installing hello LAMP stack on Debian-based distributions.</span></span> <span data-ttu-id="b3323-123">dokładne polecenia Hello może się różnić dla innych dystrybucjach systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="b3323-123">hello exact commands might differ for other Linux distros.</span></span>

#### <a name="installing-on-debianubuntu"></a><span data-ttu-id="b3323-124">Instalowanie na Debian/Ubuntu</span><span class="sxs-lookup"><span data-stu-id="b3323-124">Installing on Debian/Ubuntu</span></span>
<span data-ttu-id="b3323-125">Należy hello następujące pakiety zainstalowane: `apache2`, `mysql-server`, `php5`, i `php5-mysql`.</span><span class="sxs-lookup"><span data-stu-id="b3323-125">You need hello following packages installed: `apache2`, `mysql-server`, `php5`, and `php5-mysql`.</span></span> <span data-ttu-id="b3323-126">Te pakiety można zainstalować bezpośrednio dane te pakiety lub używając Tasksel.</span><span class="sxs-lookup"><span data-stu-id="b3323-126">You can install these packages by directly grabbing these packages or using Tasksel.</span></span> <span data-ttu-id="b3323-127">Poniżej przedstawiono instrukcje dla obu opcji.</span><span class="sxs-lookup"><span data-stu-id="b3323-127">Instructions for both options are listed below.</span></span>
<span data-ttu-id="b3323-128">Przed rozpoczęciem instalacji należy toodownload i zaktualizowanie listy pakietu.</span><span class="sxs-lookup"><span data-stu-id="b3323-128">Before installing you need toodownload and update package lists.</span></span>

    user@ubuntu$ sudo apt-get update

##### <a name="individual-packages"></a><span data-ttu-id="b3323-129">Indywidualne pakiety</span><span class="sxs-lookup"><span data-stu-id="b3323-129">Individual packages</span></span>
<span data-ttu-id="b3323-130">Przy użyciu get stanie:</span><span class="sxs-lookup"><span data-stu-id="b3323-130">Using apt-get:</span></span>

    user@ubuntu$ sudo apt-get install apache2 mysql-server php5 php5-mysql

##### <a name="using-tasksel"></a><span data-ttu-id="b3323-131">Przy użyciu tasksel</span><span class="sxs-lookup"><span data-stu-id="b3323-131">Using tasksel</span></span>
<span data-ttu-id="b3323-132">Alternatywnie możesz pobrać Tasksel, narzędzie Debian/Ubuntu wielu powiązanych pakietów jest instalowany jako skoordynowanego "zadania" do systemu.</span><span class="sxs-lookup"><span data-stu-id="b3323-132">Alternatively you can download Tasksel, a Debian/Ubuntu tool that installs multiple related packages as a coordinated "task" onto your system.</span></span>

    user@ubuntu$ sudo apt-get install tasksel
    user@ubuntu$ sudo tasksel install lamp-server

<span data-ttu-id="b3323-133">Po uruchomieniu hello poprzedniej opcji, należy być tooinstall zostanie wyświetlony monit o te pakiety i różnych innych zależności.</span><span class="sxs-lookup"><span data-stu-id="b3323-133">After running either of hello previous options, you will be prompted tooinstall these packages and various other dependencies.</span></span> <span data-ttu-id="b3323-134">Naciśnij "y", a następnie toocontinue "Wprowadź" i wykonać żadnych innych monity tooset hasła administratora dla programu MySQL.</span><span class="sxs-lookup"><span data-stu-id="b3323-134">Press 'y' and then 'Enter' toocontinue, and follow any other prompts tooset an administrative password for MySQL.</span></span> <span data-ttu-id="b3323-135">Spowoduje to zainstalowanie hello minimalne wymagane PHP rozszerzenia potrzebne toouse PHP z programem MySQL.</span><span class="sxs-lookup"><span data-stu-id="b3323-135">This installs hello minimum required PHP extensions needed toouse PHP with MySQL.</span></span> 

![][1]

<span data-ttu-id="b3323-136">Uruchom następujące polecenie toosee hello innych rozszerzeń PHP, które są dostępne w postaci pakietów:</span><span class="sxs-lookup"><span data-stu-id="b3323-136">Run hello following command toosee other PHP extensions that are available as packages:</span></span>

    user@ubuntu$ apt-cache search php5


#### <a name="create-infophp-document"></a><span data-ttu-id="b3323-137">Utwórz dokument info.php</span><span class="sxs-lookup"><span data-stu-id="b3323-137">Create info.php document</span></span>
<span data-ttu-id="b3323-138">Teraz powinno być możliwe toocheck Apache, MySQL i PHP którą wersję należy za pomocą wiersza polecenia hello wpisując `apache2 -v`, `mysql -v`, lub `php -v`.</span><span class="sxs-lookup"><span data-stu-id="b3323-138">You should now be able toocheck what version of Apache, MySQL, and PHP you have through hello command line by typing `apache2 -v`, `mysql -v`, or `php -v`.</span></span>

<span data-ttu-id="b3323-139">Jeśli użytkownik będzie jak tootest bardziej, można utworzyć szybkie tooview strony informacji PHP w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="b3323-139">If you would like tootest further, you can create a quick PHP info page tooview in a browser.</span></span> <span data-ttu-id="b3323-140">Utwórz plik z Nano edytora tekstu, korzystając z tego polecenia:</span><span class="sxs-lookup"><span data-stu-id="b3323-140">Create a file with Nano text editor with this command:</span></span>

    user@ubuntu$ sudo nano /var/www/html/info.php

<span data-ttu-id="b3323-141">W edytorze tekstu GNU Nano hello Dodaj następujące wiersze hello:</span><span class="sxs-lookup"><span data-stu-id="b3323-141">Within hello GNU Nano text editor, add hello following lines:</span></span>

    <?php
    phpinfo();
    ?>

<span data-ttu-id="b3323-142">Następnie zapisz i zamknij Edytor tekstu hello.</span><span class="sxs-lookup"><span data-stu-id="b3323-142">Then save and exit hello text editor.</span></span>

<span data-ttu-id="b3323-143">Dlatego wszystkie nowe instalacje zostały uwzględnione, uruchom ponownie Apache za pomocą tego polecenia.</span><span class="sxs-lookup"><span data-stu-id="b3323-143">Restart Apache with this command so all new installs take effect.</span></span>

    user@ubuntu$ sudo service apache2 restart

## <a name="verify-lamp-successfully-installed"></a><span data-ttu-id="b3323-144">Sprawdź światła pomyślnie zainstalowany</span><span class="sxs-lookup"><span data-stu-id="b3323-144">Verify LAMP successfully installed</span></span>
<span data-ttu-id="b3323-145">Teraz można sprawdzić stronę informacji PHP hello utworzonego przez otwarcie przeglądarki i przechodzi do toohttp://youruniqueDNS/info.php.</span><span class="sxs-lookup"><span data-stu-id="b3323-145">Now you can check hello PHP info page you created by opening a browser and going toohttp://youruniqueDNS/info.php.</span></span> <span data-ttu-id="b3323-146">Jego wygląd powinien być podobny toothis obrazu.</span><span class="sxs-lookup"><span data-stu-id="b3323-146">It should look similar toothis image.</span></span>

![][2]

<span data-ttu-id="b3323-147">Apache instalację można sprawdzić, wyświetlając hello Apache2 Ubuntu domyślna strona przechodząc tooyou http://youruniqueDNS/.</span><span class="sxs-lookup"><span data-stu-id="b3323-147">You can check your Apache installation by viewing hello Apache2 Ubuntu Default Page by going tooyou http://youruniqueDNS/.</span></span> <span data-ttu-id="b3323-148">Powinien zostać wyświetlony ekran podobny do tego obrazu.</span><span class="sxs-lookup"><span data-stu-id="b3323-148">You should see something like this image.</span></span>

![][3]

<span data-ttu-id="b3323-149">Gratulacje, mają stos światła tylko Instalatora na maszynie Wirtualnej platformy Azure!</span><span class="sxs-lookup"><span data-stu-id="b3323-149">Congratulations, you have just setup a LAMP stack on your Azure VM!</span></span>

## <a name="next-steps"></a><span data-ttu-id="b3323-150">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b3323-150">Next steps</span></span>
<span data-ttu-id="b3323-151">Wyewidencjonuj hello dokumentacji Ubuntu na stosie światła hello:</span><span class="sxs-lookup"><span data-stu-id="b3323-151">Check out hello Ubuntu documentation on hello LAMP stack:</span></span>

* [<span data-ttu-id="b3323-152">https://help.ubuntu.com/Community/ApacheMySQLPHP</span><span class="sxs-lookup"><span data-stu-id="b3323-152">https://help.ubuntu.com/community/ApacheMySQLPHP</span></span>](https://help.ubuntu.com/community/ApacheMySQLPHP)

[1]: ./media/deploy-lamp-stack/configmysqlpassword-small.png
[2]: ./media/deploy-lamp-stack/phpsuccesspage.png
[3]: ./media/deploy-lamp-stack/apachesuccesspage.png