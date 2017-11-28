---
title: "Wdrażanie światła na maszynie wirtualnej systemu Linux na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zainstalować stosu światła na Maszynę wirtualną systemu Linux na platformie Azure"
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
ms.devlang: azurecli
ms.topic: article
ms.date: 2/21/2017
ms.author: juluk
ms.openlocfilehash: ad69876bfbeba5f948a81e5c48c659fdf2265ae2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-lamp-stack-on-azure"></a><span data-ttu-id="4dac7-103">Wdrażanie stosu światła na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="4dac7-103">Deploy LAMP stack on Azure</span></span>
<span data-ttu-id="4dac7-104">W tym artykule przedstawiono sposób wdrażania serwera sieci web Apache, MySQL i PHP (stos światła) na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="4dac7-104">This article walks you through how to deploy an Apache web server, MySQL, and PHP (the LAMP stack) on Azure.</span></span> <span data-ttu-id="4dac7-105">Musisz mieć konto platformy Azure ([Pobierz bezpłatną wersję próbną](https://azure.microsoft.com/pricing/free-trial/)) i [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="4dac7-105">You need an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)) and the [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span> <span data-ttu-id="4dac7-106">Czynności te można również wykonać przy użyciu [interfejsu wiersza polecenia platformy Azure w wersji 1.0](create-lamp-stack-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4dac7-106">You can also perform these steps with the [Azure CLI 1.0](create-lamp-stack-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="quick-command-summary"></a><span data-ttu-id="4dac7-107">Szybkie polecenia podsumowania</span><span class="sxs-lookup"><span data-stu-id="4dac7-107">Quick command summary</span></span>

1. <span data-ttu-id="4dac7-108">Zapisywanie i edycja [pliku azuredeploy.parameters.json](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) do swoich preferencji na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="4dac7-108">Save and edit the [azuredeploy.parameters.json file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) to your preference on your local machine.</span></span>
2. <span data-ttu-id="4dac7-109">Uruchom dwa poniższe polecenia, aby utworzyć grupę zasobów, a następnie wdrożyć szablon:</span><span class="sxs-lookup"><span data-stu-id="4dac7-109">Run the following two commands to create a resource group and then deploy your template:</span></span>

```azurecli
az group create -l westus -n myResourceGroup
az group deployment create -g myResourceGroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json \
    --parameters @filepathToParameters.json
```

### <a name="deploy-lamp-on-existing-vm"></a><span data-ttu-id="4dac7-110">Wdrażanie światła w istniejącej maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="4dac7-110">Deploy LAMP on existing VM</span></span>
<span data-ttu-id="4dac7-111">Następujące polecenia pakiety aktualizacji, a następnie instaluje Apache, MySQL i PHP:</span><span class="sxs-lookup"><span data-stu-id="4dac7-111">The following commands updates packages, then installs Apache, MySQL, and PHP:</span></span>

```bash
sudo apt-get update
sudo apt-get install apache2 mysql-server php5 php5-mysql
```

## <a name="deploy-lamp-on-new-vm-walkthrough"></a><span data-ttu-id="4dac7-112">Wdrażanie światła na nowe wskazówki maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="4dac7-112">Deploy LAMP on new VM walkthrough</span></span>

1. <span data-ttu-id="4dac7-113">Utwórz nową grupę zasobów o [Tworzenie grupy az](/cli/azure/group#create) zawiera nowej maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="4dac7-113">Create a resource group with [az group create](/cli/azure/group#create) to contain the new VM:</span></span>

```azurecli
az group create -l westus -n myResourceGroup
```
<span data-ttu-id="4dac7-114">Aby utworzyć samej maszyny Wirtualnej, można użyć już zapisany można odnaleźć szablonu usługi Azure Resource Manager [tutaj w serwisie GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).</span><span class="sxs-lookup"><span data-stu-id="4dac7-114">To create the VM itself, you can use an already written Azure Resource Manager template found [here on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).</span></span>

2. <span data-ttu-id="4dac7-115">Zapisz [pliku azuredeploy.parameters.json](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="4dac7-115">Save the [azuredeploy.parameters.json file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) to your local machine.</span></span>
3. <span data-ttu-id="4dac7-116">Edytuj **azuredeploy.parameters.json** pliku do preferowanego dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="4dac7-116">Edit the **azuredeploy.parameters.json** file to your preferred inputs.</span></span>
4. <span data-ttu-id="4dac7-117">Wdrażanie szablonu z [Utwórz wdrożenie grupy az] odwołuje się do pliku json pobranych:</span><span class="sxs-lookup"><span data-stu-id="4dac7-117">Deploy the template with [az group deployment create] referencing the downloaded json file:</span></span>

```azurecli
az group deployment create -g myResourceGroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json \
    --parameters @filepathToParameters.json
```

<span data-ttu-id="4dac7-118">Dane wyjściowe są podobne do poniższego przykładu:</span><span class="sxs-lookup"><span data-stu-id="4dac7-118">The output is similar to the following example:</span></span>

```json
{
"id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroup/providers/Microsoft.Resources/deployments/azuredeploy",
"name": "azuredeploy",
"properties": {
    "correlationId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "debugSetting": null,
}
...
"provisioningState": "Succeeded",
"template": null,
"templateLink": {
    "contentVersion": "1.0.0.0",
    "uri": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json"
    },
    "timestamp": "2017-02-22T00:05:51.860411+00:00"
},
"resourceGroup": "myResourceGroup"
}
```

<span data-ttu-id="4dac7-119">Maszynę wirtualną systemu Linux został utworzony z już zainstalowanym światła.</span><span class="sxs-lookup"><span data-stu-id="4dac7-119">You have now created a Linux VM with LAMP already installed on it.</span></span> <span data-ttu-id="4dac7-120">Jeśli chcesz, możesz sprawdzić instalację przez przejście do [Sprawdź światła pomyślnie zainstalował](#verify-lamp-successfully-installed).</span><span class="sxs-lookup"><span data-stu-id="4dac7-120">If you wish, you can verify the install by jumping down to [Verify LAMP Successfully Installed](#verify-lamp-successfully-installed).</span></span>

## <a name="deploy-lamp-on-existing-vm-walkthrough"></a><span data-ttu-id="4dac7-121">Wdrażanie światła w istniejących wskazówki maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="4dac7-121">Deploy LAMP on existing VM walkthrough</span></span>
<span data-ttu-id="4dac7-122">Jeśli potrzebujesz pomocy tworzenia maszyny Wirtualnej systemu Linux, można head [tutaj, aby dowiedzieć się, jak utworzyć Maszynę wirtualną systemu Linux](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-quick-create-cli).</span><span class="sxs-lookup"><span data-stu-id="4dac7-122">If you need help creating a Linux VM, you can head [here to learn how to create a Linux VM](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-quick-create-cli).</span></span> <span data-ttu-id="4dac7-123">Następnie należy SSH do maszyny Wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="4dac7-123">Next, you need to SSH into the Linux VM.</span></span> <span data-ttu-id="4dac7-124">Jeśli potrzebujesz pomocy dotyczącej Tworzenie klucza SSH, można head [tutaj, aby dowiedzieć się, jak tworzenie klucza SSH w systemie Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4dac7-124">If you need help with creating an SSH key, you can head [here to learn how to create an SSH key on Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
<span data-ttu-id="4dac7-125">Jeśli masz już klucz SSH, przejdź dalej i SSH w wierszu polecenia do maszyny Wirtualnej systemu Linux z `ssh azureuser@mypublicdns.westus.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="4dac7-125">If you have an SSH key already, go ahead and SSH from your command line into your Linux VM with `ssh azureuser@mypublicdns.westus.cloudapp.azure.com`.</span></span>

<span data-ttu-id="4dac7-126">Teraz, gdy pracujesz w sieci maszyny Wirtualnej systemu Linux, możemy przeprowadzenie instalacji stosu światła na podstawie Debian dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="4dac7-126">Now that you are working within your Linux VM, we can walk through installing the LAMP stack on Debian-based distributions.</span></span> <span data-ttu-id="4dac7-127">Dokładne polecenia mogą być inne dla innych dystrybucjach systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="4dac7-127">The exact commands might differ for other Linux distros.</span></span>

#### <a name="installing-on-debianubuntu"></a><span data-ttu-id="4dac7-128">Instalowanie na Debian/Ubuntu</span><span class="sxs-lookup"><span data-stu-id="4dac7-128">Installing on Debian/Ubuntu</span></span>
<span data-ttu-id="4dac7-129">Potrzebujesz następujących pakietów, które są zainstalowane: `apache2`, `mysql-server`, `php5`, i `php5-mysql`.</span><span class="sxs-lookup"><span data-stu-id="4dac7-129">You need the following packages installed: `apache2`, `mysql-server`, `php5`, and `php5-mysql`.</span></span> <span data-ttu-id="4dac7-130">Te pakiety można zainstalować bezpośrednio dane te pakiety lub używając Tasksel.</span><span class="sxs-lookup"><span data-stu-id="4dac7-130">You can install these packages by directly grabbing these packages or using Tasksel.</span></span>
<span data-ttu-id="4dac7-131">Przed rozpoczęciem instalacji należy pobrać i zainstalować aktualizację list pakietu.</span><span class="sxs-lookup"><span data-stu-id="4dac7-131">Before installing you need to download and update package lists.</span></span>

```bash
sudo apt-get update
```

##### <a name="individual-packages"></a><span data-ttu-id="4dac7-132">Indywidualne pakiety</span><span class="sxs-lookup"><span data-stu-id="4dac7-132">Individual packages</span></span>
<span data-ttu-id="4dac7-133">Przy użyciu get stanie:</span><span class="sxs-lookup"><span data-stu-id="4dac7-133">Using apt-get:</span></span>

```bash
sudo apt-get install apache2 mysql-server php5 php5-mysql
```

##### <a name="using-tasksel"></a><span data-ttu-id="4dac7-134">Przy użyciu tasksel</span><span class="sxs-lookup"><span data-stu-id="4dac7-134">Using tasksel</span></span>
<span data-ttu-id="4dac7-135">Alternatywnie możesz pobrać Tasksel, narzędzie Debian/Ubuntu wielu powiązanych pakietów jest instalowany jako skoordynowanego "zadania" do systemu.</span><span class="sxs-lookup"><span data-stu-id="4dac7-135">Alternatively you can download Tasksel, a Debian/Ubuntu tool that installs multiple related packages as a coordinated "task" onto your system.</span></span>

```bash
sudo apt-get install tasksel
sudo tasksel install lamp-server
```

<span data-ttu-id="4dac7-136">Po uruchomieniu poprzedniej opcji, pojawi się monit, aby zainstalować te pakiety i różnych innych zależności.</span><span class="sxs-lookup"><span data-stu-id="4dac7-136">After running either of the previous options, you will be prompted to install these packages and various other dependencies.</span></span> <span data-ttu-id="4dac7-137">Aby ustawić hasło administracyjne dla programu MySQL, naciśnij klawisz "y", a następnie "Enter, aby kontynuować, a następnie postępuj zgodnie z innymi monitów.</span><span class="sxs-lookup"><span data-stu-id="4dac7-137">To set an administrative password for MySQL, press 'y' and then 'Enter' to continue, and follow any other prompts.</span></span> <span data-ttu-id="4dac7-138">Ten proces instaluje minimalne wymagane rozszerzeń PHP potrzebne do korzystania z MySQL PHP.</span><span class="sxs-lookup"><span data-stu-id="4dac7-138">This process installs the minimum required PHP extensions needed to use PHP with MySQL.</span></span> 

![][1]

<span data-ttu-id="4dac7-139">Uruchom następujące polecenie, aby wyświetlić innych rozszerzeń PHP, które są dostępne w postaci pakietów:</span><span class="sxs-lookup"><span data-stu-id="4dac7-139">Run the following command to see other PHP extensions that are available as packages:</span></span>

```bash
apt-cache search php5
```

#### <a name="create-infophp-document"></a><span data-ttu-id="4dac7-140">Utwórz dokument info.php</span><span class="sxs-lookup"><span data-stu-id="4dac7-140">Create info.php document</span></span>
<span data-ttu-id="4dac7-141">Teraz powinno być możliwe do sprawdzenia Apache, MySQL i PHP którą wersję należy za pomocą wiersza polecenia, wpisując `apache2 -v`, `mysql -v`, lub `php -v`.</span><span class="sxs-lookup"><span data-stu-id="4dac7-141">You should now be able to check what version of Apache, MySQL, and PHP you have through the command line by typing `apache2 -v`, `mysql -v`, or `php -v`.</span></span>

<span data-ttu-id="4dac7-142">Jeśli chcesz przetestować dalsze, można utworzyć szybkie stronę informacji PHP do wyświetlania w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="4dac7-142">If you would like to test further, you can create a quick PHP info page to view in a browser.</span></span> <span data-ttu-id="4dac7-143">Utwórz plik z Nano edytora tekstu, korzystając z tego polecenia:</span><span class="sxs-lookup"><span data-stu-id="4dac7-143">Create a file with Nano text editor with this command:</span></span>

```bash
sudo nano /var/www/html/info.php
```

<span data-ttu-id="4dac7-144">W edytorze tekstu GNU Nano Dodaj następujące wiersze:</span><span class="sxs-lookup"><span data-stu-id="4dac7-144">Within the GNU Nano text editor, add the following lines:</span></span>

```php
<?php
phpinfo();
?>
```

<span data-ttu-id="4dac7-145">Następnie zapisz i zamknij Edytor tekstu.</span><span class="sxs-lookup"><span data-stu-id="4dac7-145">Then save and exit the text editor.</span></span>

<span data-ttu-id="4dac7-146">Dlatego wszystkie nowe instalacje zostały uwzględnione, uruchom ponownie Apache za pomocą tego polecenia.</span><span class="sxs-lookup"><span data-stu-id="4dac7-146">Restart Apache with this command so all new installs take effect.</span></span>

```bash
sudo service apache2 restart
```

## <a name="verify-lamp-successfully-installed"></a><span data-ttu-id="4dac7-147">Sprawdź światła pomyślnie zainstalowany</span><span class="sxs-lookup"><span data-stu-id="4dac7-147">Verify LAMP successfully installed</span></span>
<span data-ttu-id="4dac7-148">Teraz można sprawdzić stronę informacji PHP, utworzonego przez otwarcie przeglądarki i przechodzi do http://youruniqueDNS/info.php.</span><span class="sxs-lookup"><span data-stu-id="4dac7-148">Now you can check the PHP info page you created by opening a browser and going to http://youruniqueDNS/info.php.</span></span> <span data-ttu-id="4dac7-149">Powinien być podobny do tego obrazu.</span><span class="sxs-lookup"><span data-stu-id="4dac7-149">It should look similar to this image.</span></span>

![][2]

<span data-ttu-id="4dac7-150">Apache instalację można sprawdzić, wyświetlając stronę domyślne Ubuntu Apache2, przechodząc do http://youruniqueDNS/ należy.</span><span class="sxs-lookup"><span data-stu-id="4dac7-150">You can check your Apache installation by viewing the Apache2 Ubuntu Default Page by going to you http://youruniqueDNS/.</span></span> <span data-ttu-id="4dac7-151">Dane wyjściowe są podobne do poniższego przykładu:</span><span class="sxs-lookup"><span data-stu-id="4dac7-151">The output is similar to the following example:</span></span>

![][3]

<span data-ttu-id="4dac7-152">Gratulacje, mają stos światła tylko Instalatora na maszynie Wirtualnej platformy Azure!</span><span class="sxs-lookup"><span data-stu-id="4dac7-152">Congratulations, you have just setup a LAMP stack on your Azure VM!</span></span>

## <a name="next-steps"></a><span data-ttu-id="4dac7-153">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4dac7-153">Next steps</span></span>
<span data-ttu-id="4dac7-154">Zapoznaj się z dokumentacją systemu Ubuntu na stosie światła:</span><span class="sxs-lookup"><span data-stu-id="4dac7-154">Check out the Ubuntu documentation on the LAMP stack:</span></span>

* [<span data-ttu-id="4dac7-155">https://help.ubuntu.com/Community/ApacheMySQLPHP</span><span class="sxs-lookup"><span data-stu-id="4dac7-155">https://help.ubuntu.com/community/ApacheMySQLPHP</span></span>](https://help.ubuntu.com/community/ApacheMySQLPHP)

[1]: ./media/deploy-lamp-stack/configmysqlpassword-small.png
[2]: ./media/deploy-lamp-stack/phpsuccesspage.png
[3]: ./media/deploy-lamp-stack/apachesuccesspage.png
