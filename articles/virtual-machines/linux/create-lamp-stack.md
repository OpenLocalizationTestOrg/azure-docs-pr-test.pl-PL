---
title: "aaaDeploy światła na maszynie wirtualnej systemu Linux na platformie Azure | Dokumentacja firmy Microsoft"
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
ms.devlang: azurecli
ms.topic: article
ms.date: 2/21/2017
ms.author: juluk
ms.openlocfilehash: 42d887bb9f78becc02505e336be25fdaaf78df70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-lamp-stack-on-azure"></a><span data-ttu-id="69839-103">Wdrażanie stosu światła na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="69839-103">Deploy LAMP stack on Azure</span></span>
<span data-ttu-id="69839-104">W tym artykule przedstawiono sposób toodeploy Apache serwera sieci web, MySQL i PHP (stos hello światła) na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="69839-104">This article walks you through how toodeploy an Apache web server, MySQL, and PHP (hello LAMP stack) on Azure.</span></span> <span data-ttu-id="69839-105">Musisz mieć konto platformy Azure ([Pobierz bezpłatną wersję próbną](https://azure.microsoft.com/pricing/free-trial/)) i hello [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="69839-105">You need an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)) and hello [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span> <span data-ttu-id="69839-106">Można również wykonać te kroki hello [Azure CLI 1.0](create-lamp-stack-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="69839-106">You can also perform these steps with hello [Azure CLI 1.0](create-lamp-stack-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="quick-command-summary"></a><span data-ttu-id="69839-107">Szybkie polecenia podsumowania</span><span class="sxs-lookup"><span data-stu-id="69839-107">Quick command summary</span></span>

1. <span data-ttu-id="69839-108">Zapisywanie i Edycja hello [pliku azuredeploy.parameters.json](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) preferencji tooyour na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="69839-108">Save and edit hello [azuredeploy.parameters.json file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) tooyour preference on your local machine.</span></span>
2. <span data-ttu-id="69839-109">Uruchom następujące dwa polecenia toocreate hello grupę zasobów, a następnie wdrożyć szablon:</span><span class="sxs-lookup"><span data-stu-id="69839-109">Run hello following two commands toocreate a resource group and then deploy your template:</span></span>

```azurecli
az group create -l westus -n myResourceGroup
az group deployment create -g myResourceGroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json \
    --parameters @filepathToParameters.json
```

### <a name="deploy-lamp-on-existing-vm"></a><span data-ttu-id="69839-110">Wdrażanie światła w istniejącej maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="69839-110">Deploy LAMP on existing VM</span></span>
<span data-ttu-id="69839-111">Witaj następujące polecenia pakietów aktualizacji, a następnie instaluje Apache, MySQL i PHP:</span><span class="sxs-lookup"><span data-stu-id="69839-111">hello following commands updates packages, then installs Apache, MySQL, and PHP:</span></span>

```bash
sudo apt-get update
sudo apt-get install apache2 mysql-server php5 php5-mysql
```

## <a name="deploy-lamp-on-new-vm-walkthrough"></a><span data-ttu-id="69839-112">Wdrażanie światła na nowe wskazówki maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="69839-112">Deploy LAMP on new VM walkthrough</span></span>

1. <span data-ttu-id="69839-113">Utwórz nową grupę zasobów o [Tworzenie grupy az](/cli/azure/group#create) toocontain hello nowej maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="69839-113">Create a resource group with [az group create](/cli/azure/group#create) toocontain hello new VM:</span></span>

```azurecli
az group create -l westus -n myResourceGroup
```
<span data-ttu-id="69839-114">toocreate hello samej maszyny Wirtualnej, można użyć już zapisany można odnaleźć szablonu usługi Azure Resource Manager [tutaj w serwisie GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).</span><span class="sxs-lookup"><span data-stu-id="69839-114">toocreate hello VM itself, you can use an already written Azure Resource Manager template found [here on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).</span></span>

2. <span data-ttu-id="69839-115">Zapisz hello [pliku azuredeploy.parameters.json](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) tooyour komputera lokalnego.</span><span class="sxs-lookup"><span data-stu-id="69839-115">Save hello [azuredeploy.parameters.json file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) tooyour local machine.</span></span>
3. <span data-ttu-id="69839-116">Edytuj hello **azuredeploy.parameters.json** tooyour pliku preferowane danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="69839-116">Edit hello **azuredeploy.parameters.json** file tooyour preferred inputs.</span></span>
4. <span data-ttu-id="69839-117">Wdrażanie szablonu hello [Utwórz wdrożenie grupy az] odwołuje się do hello pobrany plik json:</span><span class="sxs-lookup"><span data-stu-id="69839-117">Deploy hello template with [az group deployment create] referencing hello downloaded json file:</span></span>

```azurecli
az group deployment create -g myResourceGroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json \
    --parameters @filepathToParameters.json
```

<span data-ttu-id="69839-118">Witaj danych wyjściowych jest toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="69839-118">hello output is similar toohello following example:</span></span>

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

<span data-ttu-id="69839-119">Maszynę wirtualną systemu Linux został utworzony z już zainstalowanym światła.</span><span class="sxs-lookup"><span data-stu-id="69839-119">You have now created a Linux VM with LAMP already installed on it.</span></span> <span data-ttu-id="69839-120">Jeśli chcesz, możesz sprawdzić hello instalacji przez przeskakiwanie dół za[Sprawdź światła pomyślnie zainstalował](#verify-lamp-successfully-installed).</span><span class="sxs-lookup"><span data-stu-id="69839-120">If you wish, you can verify hello install by jumping down too[Verify LAMP Successfully Installed](#verify-lamp-successfully-installed).</span></span>

## <a name="deploy-lamp-on-existing-vm-walkthrough"></a><span data-ttu-id="69839-121">Wdrażanie światła w istniejących wskazówki maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="69839-121">Deploy LAMP on existing VM walkthrough</span></span>
<span data-ttu-id="69839-122">Jeśli potrzebujesz pomocy tworzenia maszyny Wirtualnej systemu Linux, można head [toolearn tutaj jak toocreate Maszynę wirtualną systemu Linux](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-quick-create-cli).</span><span class="sxs-lookup"><span data-stu-id="69839-122">If you need help creating a Linux VM, you can head [here toolearn how toocreate a Linux VM](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-quick-create-cli).</span></span> <span data-ttu-id="69839-123">Następnie należy tooSSH do hello maszyny Wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="69839-123">Next, you need tooSSH into hello Linux VM.</span></span> <span data-ttu-id="69839-124">Jeśli potrzebujesz pomocy dotyczącej Tworzenie klucza SSH, można head [toolearn tutaj jak toocreate klucza SSH w systemie Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="69839-124">If you need help with creating an SSH key, you can head [here toolearn how toocreate an SSH key on Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
<span data-ttu-id="69839-125">Jeśli masz już klucz SSH, przejdź dalej i SSH w wierszu polecenia do maszyny Wirtualnej systemu Linux z `ssh azureuser@mypublicdns.westus.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="69839-125">If you have an SSH key already, go ahead and SSH from your command line into your Linux VM with `ssh azureuser@mypublicdns.westus.cloudapp.azure.com`.</span></span>

<span data-ttu-id="69839-126">Teraz, gdy pracujesz w sieci maszyny Wirtualnej systemu Linux, możemy przeprowadzenie instalacji stosu światła hello na podstawie Debian dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="69839-126">Now that you are working within your Linux VM, we can walk through installing hello LAMP stack on Debian-based distributions.</span></span> <span data-ttu-id="69839-127">dokładne polecenia Hello może się różnić dla innych dystrybucjach systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="69839-127">hello exact commands might differ for other Linux distros.</span></span>

#### <a name="installing-on-debianubuntu"></a><span data-ttu-id="69839-128">Instalowanie na Debian/Ubuntu</span><span class="sxs-lookup"><span data-stu-id="69839-128">Installing on Debian/Ubuntu</span></span>
<span data-ttu-id="69839-129">Należy hello następujące pakiety zainstalowane: `apache2`, `mysql-server`, `php5`, i `php5-mysql`.</span><span class="sxs-lookup"><span data-stu-id="69839-129">You need hello following packages installed: `apache2`, `mysql-server`, `php5`, and `php5-mysql`.</span></span> <span data-ttu-id="69839-130">Te pakiety można zainstalować bezpośrednio dane te pakiety lub używając Tasksel.</span><span class="sxs-lookup"><span data-stu-id="69839-130">You can install these packages by directly grabbing these packages or using Tasksel.</span></span>
<span data-ttu-id="69839-131">Przed rozpoczęciem instalacji należy toodownload i zaktualizowanie listy pakietu.</span><span class="sxs-lookup"><span data-stu-id="69839-131">Before installing you need toodownload and update package lists.</span></span>

```bash
sudo apt-get update
```

##### <a name="individual-packages"></a><span data-ttu-id="69839-132">Indywidualne pakiety</span><span class="sxs-lookup"><span data-stu-id="69839-132">Individual packages</span></span>
<span data-ttu-id="69839-133">Przy użyciu get stanie:</span><span class="sxs-lookup"><span data-stu-id="69839-133">Using apt-get:</span></span>

```bash
sudo apt-get install apache2 mysql-server php5 php5-mysql
```

##### <a name="using-tasksel"></a><span data-ttu-id="69839-134">Przy użyciu tasksel</span><span class="sxs-lookup"><span data-stu-id="69839-134">Using tasksel</span></span>
<span data-ttu-id="69839-135">Alternatywnie możesz pobrać Tasksel, narzędzie Debian/Ubuntu wielu powiązanych pakietów jest instalowany jako skoordynowanego "zadania" do systemu.</span><span class="sxs-lookup"><span data-stu-id="69839-135">Alternatively you can download Tasksel, a Debian/Ubuntu tool that installs multiple related packages as a coordinated "task" onto your system.</span></span>

```bash
sudo apt-get install tasksel
sudo tasksel install lamp-server
```

<span data-ttu-id="69839-136">Po uruchomieniu hello poprzedniej opcji, należy być tooinstall zostanie wyświetlony monit o te pakiety i różnych innych zależności.</span><span class="sxs-lookup"><span data-stu-id="69839-136">After running either of hello previous options, you will be prompted tooinstall these packages and various other dependencies.</span></span> <span data-ttu-id="69839-137">tooset hasła administratora dla programu MySQL, naciśnij klawisz "y", a następnie toocontinue "Wprowadź", a następnie wykonaj inne monitów.</span><span class="sxs-lookup"><span data-stu-id="69839-137">tooset an administrative password for MySQL, press 'y' and then 'Enter' toocontinue, and follow any other prompts.</span></span> <span data-ttu-id="69839-138">Ten proces instaluje hello minimalne wymagane PHP rozszerzenia potrzebne toouse PHP z programem MySQL.</span><span class="sxs-lookup"><span data-stu-id="69839-138">This process installs hello minimum required PHP extensions needed toouse PHP with MySQL.</span></span> 

![][1]

<span data-ttu-id="69839-139">Uruchom następujące polecenie toosee hello innych rozszerzeń PHP, które są dostępne w postaci pakietów:</span><span class="sxs-lookup"><span data-stu-id="69839-139">Run hello following command toosee other PHP extensions that are available as packages:</span></span>

```bash
apt-cache search php5
```

#### <a name="create-infophp-document"></a><span data-ttu-id="69839-140">Utwórz dokument info.php</span><span class="sxs-lookup"><span data-stu-id="69839-140">Create info.php document</span></span>
<span data-ttu-id="69839-141">Teraz powinno być możliwe toocheck Apache, MySQL i PHP którą wersję należy za pomocą wiersza polecenia hello wpisując `apache2 -v`, `mysql -v`, lub `php -v`.</span><span class="sxs-lookup"><span data-stu-id="69839-141">You should now be able toocheck what version of Apache, MySQL, and PHP you have through hello command line by typing `apache2 -v`, `mysql -v`, or `php -v`.</span></span>

<span data-ttu-id="69839-142">Jeśli użytkownik będzie jak tootest bardziej, można utworzyć szybkie tooview strony informacji PHP w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="69839-142">If you would like tootest further, you can create a quick PHP info page tooview in a browser.</span></span> <span data-ttu-id="69839-143">Utwórz plik z Nano edytora tekstu, korzystając z tego polecenia:</span><span class="sxs-lookup"><span data-stu-id="69839-143">Create a file with Nano text editor with this command:</span></span>

```bash
sudo nano /var/www/html/info.php
```

<span data-ttu-id="69839-144">W edytorze tekstu GNU Nano hello Dodaj następujące wiersze hello:</span><span class="sxs-lookup"><span data-stu-id="69839-144">Within hello GNU Nano text editor, add hello following lines:</span></span>

```php
<?php
phpinfo();
?>
```

<span data-ttu-id="69839-145">Następnie zapisz i zamknij Edytor tekstu hello.</span><span class="sxs-lookup"><span data-stu-id="69839-145">Then save and exit hello text editor.</span></span>

<span data-ttu-id="69839-146">Dlatego wszystkie nowe instalacje zostały uwzględnione, uruchom ponownie Apache za pomocą tego polecenia.</span><span class="sxs-lookup"><span data-stu-id="69839-146">Restart Apache with this command so all new installs take effect.</span></span>

```bash
sudo service apache2 restart
```

## <a name="verify-lamp-successfully-installed"></a><span data-ttu-id="69839-147">Sprawdź światła pomyślnie zainstalowany</span><span class="sxs-lookup"><span data-stu-id="69839-147">Verify LAMP successfully installed</span></span>
<span data-ttu-id="69839-148">Teraz można sprawdzić stronę informacji PHP hello utworzonego przez otwarcie przeglądarki i przechodzi do toohttp://youruniqueDNS/info.php.</span><span class="sxs-lookup"><span data-stu-id="69839-148">Now you can check hello PHP info page you created by opening a browser and going toohttp://youruniqueDNS/info.php.</span></span> <span data-ttu-id="69839-149">Jego wygląd powinien być podobny toothis obrazu.</span><span class="sxs-lookup"><span data-stu-id="69839-149">It should look similar toothis image.</span></span>

![][2]

<span data-ttu-id="69839-150">Apache instalację można sprawdzić, wyświetlając hello Apache2 Ubuntu domyślna strona przechodząc tooyou http://youruniqueDNS/.</span><span class="sxs-lookup"><span data-stu-id="69839-150">You can check your Apache installation by viewing hello Apache2 Ubuntu Default Page by going tooyou http://youruniqueDNS/.</span></span> <span data-ttu-id="69839-151">Witaj danych wyjściowych jest toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="69839-151">hello output is similar toohello following example:</span></span>

![][3]

<span data-ttu-id="69839-152">Gratulacje, mają stos światła tylko Instalatora na maszynie Wirtualnej platformy Azure!</span><span class="sxs-lookup"><span data-stu-id="69839-152">Congratulations, you have just setup a LAMP stack on your Azure VM!</span></span>

## <a name="next-steps"></a><span data-ttu-id="69839-153">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="69839-153">Next steps</span></span>
<span data-ttu-id="69839-154">Wyewidencjonuj hello dokumentacji Ubuntu na stosie światła hello:</span><span class="sxs-lookup"><span data-stu-id="69839-154">Check out hello Ubuntu documentation on hello LAMP stack:</span></span>

* [<span data-ttu-id="69839-155">https://help.ubuntu.com/Community/ApacheMySQLPHP</span><span class="sxs-lookup"><span data-stu-id="69839-155">https://help.ubuntu.com/community/ApacheMySQLPHP</span></span>](https://help.ubuntu.com/community/ApacheMySQLPHP)

[1]: ./media/deploy-lamp-stack/configmysqlpassword-small.png
[2]: ./media/deploy-lamp-stack/phpsuccesspage.png
[3]: ./media/deploy-lamp-stack/apachesuccesspage.png
