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
# <a name="deploy-lamp-stack-on-azure"></a>Wdrażanie stosu światła na platformie Azure
W tym artykule przedstawiono sposób toodeploy Apache serwera sieci web, MySQL i PHP (stos hello światła) na platformie Azure. Musisz mieć konto platformy Azure ([Pobierz bezpłatną wersję próbną](https://azure.microsoft.com/pricing/free-trial/)) i hello [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2). Można również wykonać te kroki hello [Azure CLI 1.0](create-lamp-stack-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="quick-command-summary"></a>Szybkie polecenia podsumowania

1. Zapisywanie i Edycja hello [pliku azuredeploy.parameters.json](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) preferencji tooyour na komputerze lokalnym.
2. Uruchom następujące dwa polecenia toocreate hello grupę zasobów, a następnie wdrożyć szablon:

```azurecli
az group create -l westus -n myResourceGroup
az group deployment create -g myResourceGroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json \
    --parameters @filepathToParameters.json
```

### <a name="deploy-lamp-on-existing-vm"></a>Wdrażanie światła w istniejącej maszyny Wirtualnej
Witaj następujące polecenia pakietów aktualizacji, a następnie instaluje Apache, MySQL i PHP:

```bash
sudo apt-get update
sudo apt-get install apache2 mysql-server php5 php5-mysql
```

## <a name="deploy-lamp-on-new-vm-walkthrough"></a>Wdrażanie światła na nowe wskazówki maszyny Wirtualnej

1. Utwórz nową grupę zasobów o [Tworzenie grupy az](/cli/azure/group#create) toocontain hello nowej maszyny Wirtualnej:

```azurecli
az group create -l westus -n myResourceGroup
```
toocreate hello samej maszyny Wirtualnej, można użyć już zapisany można odnaleźć szablonu usługi Azure Resource Manager [tutaj w serwisie GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).

2. Zapisz hello [pliku azuredeploy.parameters.json](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) tooyour komputera lokalnego.
3. Edytuj hello **azuredeploy.parameters.json** tooyour pliku preferowane danych wejściowych.
4. Wdrażanie szablonu hello [Utwórz wdrożenie grupy az] odwołuje się do hello pobrany plik json:

```azurecli
az group deployment create -g myResourceGroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json \
    --parameters @filepathToParameters.json
```

Witaj danych wyjściowych jest toohello podobnie poniższy przykład:

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

Maszynę wirtualną systemu Linux został utworzony z już zainstalowanym światła. Jeśli chcesz, możesz sprawdzić hello instalacji przez przeskakiwanie dół za[Sprawdź światła pomyślnie zainstalował](#verify-lamp-successfully-installed).

## <a name="deploy-lamp-on-existing-vm-walkthrough"></a>Wdrażanie światła w istniejących wskazówki maszyny Wirtualnej
Jeśli potrzebujesz pomocy tworzenia maszyny Wirtualnej systemu Linux, można head [toolearn tutaj jak toocreate Maszynę wirtualną systemu Linux](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-quick-create-cli). Następnie należy tooSSH do hello maszyny Wirtualnej systemu Linux. Jeśli potrzebujesz pomocy dotyczącej Tworzenie klucza SSH, można head [toolearn tutaj jak toocreate klucza SSH w systemie Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
Jeśli masz już klucz SSH, przejdź dalej i SSH w wierszu polecenia do maszyny Wirtualnej systemu Linux z `ssh azureuser@mypublicdns.westus.cloudapp.azure.com`.

Teraz, gdy pracujesz w sieci maszyny Wirtualnej systemu Linux, możemy przeprowadzenie instalacji stosu światła hello na podstawie Debian dystrybucji. dokładne polecenia Hello może się różnić dla innych dystrybucjach systemu Linux.

#### <a name="installing-on-debianubuntu"></a>Instalowanie na Debian/Ubuntu
Należy hello następujące pakiety zainstalowane: `apache2`, `mysql-server`, `php5`, i `php5-mysql`. Te pakiety można zainstalować bezpośrednio dane te pakiety lub używając Tasksel.
Przed rozpoczęciem instalacji należy toodownload i zaktualizowanie listy pakietu.

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

Po uruchomieniu hello poprzedniej opcji, należy być tooinstall zostanie wyświetlony monit o te pakiety i różnych innych zależności. tooset hasła administratora dla programu MySQL, naciśnij klawisz "y", a następnie toocontinue "Wprowadź", a następnie wykonaj inne monitów. Ten proces instaluje hello minimalne wymagane PHP rozszerzenia potrzebne toouse PHP z programem MySQL. 

![][1]

Uruchom następujące polecenie toosee hello innych rozszerzeń PHP, które są dostępne w postaci pakietów:

```bash
apt-cache search php5
```

#### <a name="create-infophp-document"></a>Utwórz dokument info.php
Teraz powinno być możliwe toocheck Apache, MySQL i PHP którą wersję należy za pomocą wiersza polecenia hello wpisując `apache2 -v`, `mysql -v`, lub `php -v`.

Jeśli użytkownik będzie jak tootest bardziej, można utworzyć szybkie tooview strony informacji PHP w przeglądarce. Utwórz plik z Nano edytora tekstu, korzystając z tego polecenia:

```bash
sudo nano /var/www/html/info.php
```

W edytorze tekstu GNU Nano hello Dodaj następujące wiersze hello:

```php
<?php
phpinfo();
?>
```

Następnie zapisz i zamknij Edytor tekstu hello.

Dlatego wszystkie nowe instalacje zostały uwzględnione, uruchom ponownie Apache za pomocą tego polecenia.

```bash
sudo service apache2 restart
```

## <a name="verify-lamp-successfully-installed"></a>Sprawdź światła pomyślnie zainstalowany
Teraz można sprawdzić stronę informacji PHP hello utworzonego przez otwarcie przeglądarki i przechodzi do toohttp://youruniqueDNS/info.php. Jego wygląd powinien być podobny toothis obrazu.

![][2]

Apache instalację można sprawdzić, wyświetlając hello Apache2 Ubuntu domyślna strona przechodząc tooyou http://youruniqueDNS/. Witaj danych wyjściowych jest toohello podobnie poniższy przykład:

![][3]

Gratulacje, mają stos światła tylko Instalatora na maszynie Wirtualnej platformy Azure!

## <a name="next-steps"></a>Następne kroki
Wyewidencjonuj hello dokumentacji Ubuntu na stosie światła hello:

* [https://help.ubuntu.com/Community/ApacheMySQLPHP](https://help.ubuntu.com/community/ApacheMySQLPHP)

[1]: ./media/deploy-lamp-stack/configmysqlpassword-small.png
[2]: ./media/deploy-lamp-stack/phpsuccesspage.png
[3]: ./media/deploy-lamp-stack/apachesuccesspage.png
