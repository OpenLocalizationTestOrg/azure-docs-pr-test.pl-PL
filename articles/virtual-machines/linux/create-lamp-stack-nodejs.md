---
title: "Wdrażanie światła na maszynie wirtualnej systemu Linux z interfejsu wiersza polecenia platformy Azure w wersji 1.0 | Dokumentacja firmy Microsoft"
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
ms.devlang: NA
ms.topic: article
ms.date: 2/21/2017
ms.author: juluk
ms.openlocfilehash: feba2fb20d1831e92358ff5d1b4c9589d63d28dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-lamp-stack-with-the-azure-cli-10"></a>Wdrażanie stosu światła z interfejsu wiersza polecenia platformy Azure w wersji 1.0
W tym artykule przedstawiono sposób wdrażania serwera sieci web Apache, MySQL i PHP (stos światła) na platformie Azure. Potrzebne jest konto platformy Azure ([Pobierz bezpłatną wersję próbną](https://azure.microsoft.com/pricing/free-trial/)) i [interfejsu wiersza polecenia Azure](../../cli-install-nodejs.md) czyli [połączony z kontem platformy Azure](../../xplat-cli-connect.md).

## <a name="cli-versions-to-complete-the-task"></a>Wersje interfejsu wiersza polecenia umożliwiające wykonanie zadania
Zadanie można wykonać przy użyciu jednej z następujących wersji interfejsu wiersza polecenia:

- [1.0 interfejsu wiersza polecenia platformy azure] — nasze interfejsu wiersza polecenia dla klasycznego i zasobów zarządzania wdrażania modeli (w tym artykule)
- [Interfejs wiersza polecenia platformy Azure w wersji 2.0](create-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) — nasz interfejs wiersza polecenia nowej generacji dla modelu wdrażania na potrzeby zarządzania zasobami

```
# One command to create a resource group holding a VM with LAMP already on it
$ azure group create -n uniqueResourceGroup -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json
```

* Wdrażanie światła w istniejącej maszyny Wirtualnej

```
# Two commands: one updates packages, the other installs Apache, MySQL, and PHP
user@ubuntu$ sudo apt-get update
user@ubuntu$ sudo apt-get install apache2 mysql-server php5 php5-mysql
```

## <a name="deploy-lamp-on-new-vm-walkthrough"></a>Wdrażanie światła na nowe wskazówki maszyny Wirtualnej
Można uruchomić tworzenia [grupy zasobów](../../azure-resource-manager/resource-group-overview.md) który będzie zawierał nowej maszyny Wirtualnej:

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

Aby utworzyć samej maszyny Wirtualnej, można użyć już zapisany można odnaleźć szablonu usługi Azure Resource Manager [tutaj w serwisie GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).

    $ azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json uniqueResourceGroup uniqueLampName

Powinna zostać wyświetlona odpowiedź monitowania niektórych więcej danych wejściowych:

    info:    Executing command group deployment create
    info:    Supply values for the following parameters
    storageAccountNamePrefix: lampprefix
    location: westus
    adminUsername: someUsername
    adminPassword: somePassword
    mySqlPassword: somePassword
    dnsLabelPrefix: azlamptest
    info:    Initializing template configurations and parameters
    info:    Creating a deployment
    info:    Created template deployment "uniqueLampName"
    info:    Waiting for deployment to complete
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

Maszynę wirtualną systemu Linux został utworzony z już zainstalowanym światła. Jeśli chcesz, możesz sprawdzić instalację przez przejście do [Sprawdź światła pomyślnie zainstalował](#verify-lamp-successfully-installed).

## <a name="deploy-lamp-on-existing-vm-walkthrough"></a>Wdrażanie światła w istniejących wskazówki maszyny Wirtualnej
Jeśli potrzebujesz pomocy tworzenia maszyny Wirtualnej systemu Linux, można head [tutaj, aby dowiedzieć się, jak utworzyć Maszynę wirtualną systemu Linux](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Następnie należy SSH do maszyny Wirtualnej systemu Linux. Jeśli potrzebujesz pomocy dotyczącej Tworzenie klucza SSH, można head [tutaj, aby dowiedzieć się, jak tworzenie klucza SSH w systemie Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
Jeśli masz już klucz SSH, przejdź dalej i SSH w wierszu polecenia do maszyny Wirtualnej systemu Linux z `ssh exampleUsername@exampleDNS`.

Teraz, gdy pracujesz w sieci maszyny Wirtualnej systemu Linux, możemy przeprowadzenie instalacji stosu światła na podstawie Debian dystrybucji. Dokładne polecenia mogą być inne dla innych dystrybucjach systemu Linux.

#### <a name="installing-on-debianubuntu"></a>Instalowanie na Debian/Ubuntu
Potrzebujesz następujących pakietów, które są zainstalowane: `apache2`, `mysql-server`, `php5`, i `php5-mysql`. Te pakiety można zainstalować bezpośrednio dane te pakiety lub używając Tasksel. Poniżej przedstawiono instrukcje dla obu opcji.
Przed rozpoczęciem instalacji należy pobrać i zainstalować aktualizację list pakietu.

    user@ubuntu$ sudo apt-get update

##### <a name="individual-packages"></a>Indywidualne pakiety
Przy użyciu get stanie:

    user@ubuntu$ sudo apt-get install apache2 mysql-server php5 php5-mysql

##### <a name="using-tasksel"></a>Przy użyciu tasksel
Alternatywnie możesz pobrać Tasksel, narzędzie Debian/Ubuntu wielu powiązanych pakietów jest instalowany jako skoordynowanego "zadania" do systemu.

    user@ubuntu$ sudo apt-get install tasksel
    user@ubuntu$ sudo tasksel install lamp-server

Po uruchomieniu poprzedniej opcji, pojawi się monit, aby zainstalować te pakiety i różnych innych zależności. Naciśnij klawisz "y", a następnie "Enter, aby kontynuować, a inne monity, aby ustawić hasło administracyjne dla programu MySQL. Spowoduje to zainstalowanie minimalne wymagane rozszerzeń PHP potrzebne do korzystania z MySQL PHP. 

![][1]

Uruchom następujące polecenie, aby wyświetlić innych rozszerzeń PHP, które są dostępne w postaci pakietów:

    user@ubuntu$ apt-cache search php5


#### <a name="create-infophp-document"></a>Utwórz dokument info.php
Teraz powinno być możliwe do sprawdzenia Apache, MySQL i PHP którą wersję należy za pomocą wiersza polecenia, wpisując `apache2 -v`, `mysql -v`, lub `php -v`.

Jeśli chcesz przetestować dalsze, można utworzyć szybkie stronę informacji PHP do wyświetlania w przeglądarce. Utwórz plik z Nano edytora tekstu, korzystając z tego polecenia:

    user@ubuntu$ sudo nano /var/www/html/info.php

W edytorze tekstu GNU Nano Dodaj następujące wiersze:

    <?php
    phpinfo();
    ?>

Następnie zapisz i zamknij Edytor tekstu.

Dlatego wszystkie nowe instalacje zostały uwzględnione, uruchom ponownie Apache za pomocą tego polecenia.

    user@ubuntu$ sudo service apache2 restart

## <a name="verify-lamp-successfully-installed"></a>Sprawdź światła pomyślnie zainstalowany
Teraz można sprawdzić stronę informacji PHP, utworzonego przez otwarcie przeglądarki i przechodzi do http://youruniqueDNS/info.php. Powinien być podobny do tego obrazu.

![][2]

Apache instalację można sprawdzić, wyświetlając stronę domyślne Ubuntu Apache2, przechodząc do http://youruniqueDNS/ należy. Powinien zostać wyświetlony ekran podobny do tego obrazu.

![][3]

Gratulacje, mają stos światła tylko Instalatora na maszynie Wirtualnej platformy Azure!

## <a name="next-steps"></a>Następne kroki
Zapoznaj się z dokumentacją systemu Ubuntu na stosie światła:

* [https://help.ubuntu.com/Community/ApacheMySQLPHP](https://help.ubuntu.com/community/ApacheMySQLPHP)

[1]: ./media/deploy-lamp-stack/configmysqlpassword-small.png
[2]: ./media/deploy-lamp-stack/phpsuccesspage.png
[3]: ./media/deploy-lamp-stack/apachesuccesspage.png