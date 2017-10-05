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
# <a name="deploy-lamp-stack-on-azure"></a>Wdrażanie stosu światła na platformie Azure
W tym artykule przedstawiono sposób wdrażania serwera sieci web Apache, MySQL i PHP (stos światła) na platformie Azure. Musisz mieć konto platformy Azure ([Pobierz bezpłatną wersję próbną](https://azure.microsoft.com/pricing/free-trial/)) i [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2). Czynności te można również wykonać przy użyciu [interfejsu wiersza polecenia platformy Azure w wersji 1.0](create-lamp-stack-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="quick-command-summary"></a>Szybkie polecenia podsumowania

1. Zapisywanie i edycja [pliku azuredeploy.parameters.json](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) do swoich preferencji na komputerze lokalnym.
2. Uruchom dwa poniższe polecenia, aby utworzyć grupę zasobów, a następnie wdrożyć szablon:

```azurecli
az group create -l westus -n myResourceGroup
az group deployment create -g myResourceGroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json \
    --parameters @filepathToParameters.json
```

### <a name="deploy-lamp-on-existing-vm"></a>Wdrażanie światła w istniejącej maszyny Wirtualnej
Następujące polecenia pakiety aktualizacji, a następnie instaluje Apache, MySQL i PHP:

```bash
sudo apt-get update
sudo apt-get install apache2 mysql-server php5 php5-mysql
```

## <a name="deploy-lamp-on-new-vm-walkthrough"></a>Wdrażanie światła na nowe wskazówki maszyny Wirtualnej

1. Utwórz nową grupę zasobów o [Tworzenie grupy az](/cli/azure/group#create) zawiera nowej maszyny Wirtualnej:

```azurecli
az group create -l westus -n myResourceGroup
```
Aby utworzyć samej maszyny Wirtualnej, można użyć już zapisany można odnaleźć szablonu usługi Azure Resource Manager [tutaj w serwisie GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).

2. Zapisz [pliku azuredeploy.parameters.json](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) na komputerze lokalnym.
3. Edytuj **azuredeploy.parameters.json** pliku do preferowanego dane wejściowe.
4. Wdrażanie szablonu z [Utwórz wdrożenie grupy az] odwołuje się do pliku json pobranych:

```azurecli
az group deployment create -g myResourceGroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json \
    --parameters @filepathToParameters.json
```

Dane wyjściowe są podobne do poniższego przykładu:

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

Maszynę wirtualną systemu Linux został utworzony z już zainstalowanym światła. Jeśli chcesz, możesz sprawdzić instalację przez przejście do [Sprawdź światła pomyślnie zainstalował](#verify-lamp-successfully-installed).

## <a name="deploy-lamp-on-existing-vm-walkthrough"></a>Wdrażanie światła w istniejących wskazówki maszyny Wirtualnej
Jeśli potrzebujesz pomocy tworzenia maszyny Wirtualnej systemu Linux, można head [tutaj, aby dowiedzieć się, jak utworzyć Maszynę wirtualną systemu Linux](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-quick-create-cli). Następnie należy SSH do maszyny Wirtualnej systemu Linux. Jeśli potrzebujesz pomocy dotyczącej Tworzenie klucza SSH, można head [tutaj, aby dowiedzieć się, jak tworzenie klucza SSH w systemie Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
Jeśli masz już klucz SSH, przejdź dalej i SSH w wierszu polecenia do maszyny Wirtualnej systemu Linux z `ssh azureuser@mypublicdns.westus.cloudapp.azure.com`.

Teraz, gdy pracujesz w sieci maszyny Wirtualnej systemu Linux, możemy przeprowadzenie instalacji stosu światła na podstawie Debian dystrybucji. Dokładne polecenia mogą być inne dla innych dystrybucjach systemu Linux.

#### <a name="installing-on-debianubuntu"></a>Instalowanie na Debian/Ubuntu
Potrzebujesz następujących pakietów, które są zainstalowane: `apache2`, `mysql-server`, `php5`, i `php5-mysql`. Te pakiety można zainstalować bezpośrednio dane te pakiety lub używając Tasksel.
Przed rozpoczęciem instalacji należy pobrać i zainstalować aktualizację list pakietu.

```bash
sudo apt-get update
```

##### <a name="individual-packages"></a>Indywidualne pakiety
Przy użyciu get stanie:

```bash
sudo apt-get install apache2 mysql-server php5 php5-mysql
```

##### <a name="using-tasksel"></a>Przy użyciu tasksel
Alternatywnie możesz pobrać Tasksel, narzędzie Debian/Ubuntu wielu powiązanych pakietów jest instalowany jako skoordynowanego "zadania" do systemu.

```bash
sudo apt-get install tasksel
sudo tasksel install lamp-server
```

Po uruchomieniu poprzedniej opcji, pojawi się monit, aby zainstalować te pakiety i różnych innych zależności. Aby ustawić hasło administracyjne dla programu MySQL, naciśnij klawisz "y", a następnie "Enter, aby kontynuować, a następnie postępuj zgodnie z innymi monitów. Ten proces instaluje minimalne wymagane rozszerzeń PHP potrzebne do korzystania z MySQL PHP. 

![][1]

Uruchom następujące polecenie, aby wyświetlić innych rozszerzeń PHP, które są dostępne w postaci pakietów:

```bash
apt-cache search php5
```

#### <a name="create-infophp-document"></a>Utwórz dokument info.php
Teraz powinno być możliwe do sprawdzenia Apache, MySQL i PHP którą wersję należy za pomocą wiersza polecenia, wpisując `apache2 -v`, `mysql -v`, lub `php -v`.

Jeśli chcesz przetestować dalsze, można utworzyć szybkie stronę informacji PHP do wyświetlania w przeglądarce. Utwórz plik z Nano edytora tekstu, korzystając z tego polecenia:

```bash
sudo nano /var/www/html/info.php
```

W edytorze tekstu GNU Nano Dodaj następujące wiersze:

```php
<?php
phpinfo();
?>
```

Następnie zapisz i zamknij Edytor tekstu.

Dlatego wszystkie nowe instalacje zostały uwzględnione, uruchom ponownie Apache za pomocą tego polecenia.

```bash
sudo service apache2 restart
```

## <a name="verify-lamp-successfully-installed"></a>Sprawdź światła pomyślnie zainstalowany
Teraz można sprawdzić stronę informacji PHP, utworzonego przez otwarcie przeglądarki i przechodzi do http://youruniqueDNS/info.php. Powinien być podobny do tego obrazu.

![][2]

Apache instalację można sprawdzić, wyświetlając stronę domyślne Ubuntu Apache2, przechodząc do http://youruniqueDNS/ należy. Dane wyjściowe są podobne do poniższego przykładu:

![][3]

Gratulacje, mają stos światła tylko Instalatora na maszynie Wirtualnej platformy Azure!

## <a name="next-steps"></a>Następne kroki
Zapoznaj się z dokumentacją systemu Ubuntu na stosie światła:

* [https://help.ubuntu.com/Community/ApacheMySQLPHP](https://help.ubuntu.com/community/ApacheMySQLPHP)

[1]: ./media/deploy-lamp-stack/configmysqlpassword-small.png
[2]: ./media/deploy-lamp-stack/phpsuccesspage.png
[3]: ./media/deploy-lamp-stack/apachesuccesspage.png
