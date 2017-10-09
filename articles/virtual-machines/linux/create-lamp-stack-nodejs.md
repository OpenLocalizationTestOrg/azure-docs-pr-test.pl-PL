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
# <a name="deploy-lamp-stack-with-hello-azure-cli-10"></a>Wdrażanie światła stos hello Azure CLI w wersji 1.0
W tym artykule przedstawiono sposób toodeploy Apache serwera sieci web, MySQL i PHP (stos hello światła) na platformie Azure. Potrzebne jest konto platformy Azure ([Pobierz bezpłatną wersję próbną](https://azure.microsoft.com/pricing/free-trial/)) i hello [interfejsu wiersza polecenia Azure](../../cli-install-nodejs.md) oznacza to [połączone tooyour konta Azure](../../xplat-cli-connect.md).

## <a name="cli-versions-toocomplete-hello-task"></a>Zadanie hello toocomplete wersje interfejsu wiersza polecenia
Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:

- [1.0 interfejsu wiersza polecenia platformy azure] — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania wdrażania modeli (w tym artykule)
- [Azure CLI 2.0](create-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania zasobów hello

```
# One command toocreate a resource group holding a VM with LAMP already on it
$ azure group create -n uniqueResourceGroup -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json
```

* Wdrażanie światła w istniejącej maszyny Wirtualnej

```
# Two commands: one updates packages, hello other installs Apache, MySQL, and PHP
user@ubuntu$ sudo apt-get update
user@ubuntu$ sudo apt-get install apache2 mysql-server php5 php5-mysql
```

## <a name="deploy-lamp-on-new-vm-walkthrough"></a>Wdrażanie światła na nowe wskazówki maszyny Wirtualnej
Można uruchomić tworzenia [grupy zasobów](../../azure-resource-manager/resource-group-overview.md) który będzie zawierał hello nowej maszyny Wirtualnej:

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

toocreate hello samej maszyny Wirtualnej, można użyć już zapisany można odnaleźć szablonu usługi Azure Resource Manager [tutaj w serwisie GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).

    $ azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json uniqueResourceGroup uniqueLampName

Powinna zostać wyświetlona odpowiedź monitowania niektórych więcej danych wejściowych:

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

Maszynę wirtualną systemu Linux został utworzony z już zainstalowanym światła. Jeśli chcesz, możesz sprawdzić hello instalacji przez przeskakiwanie dół za[Sprawdź światła pomyślnie zainstalował](#verify-lamp-successfully-installed).

## <a name="deploy-lamp-on-existing-vm-walkthrough"></a>Wdrażanie światła w istniejących wskazówki maszyny Wirtualnej
Jeśli potrzebujesz pomocy tworzenia maszyny Wirtualnej systemu Linux, można head [toolearn tutaj jak toocreate Maszynę wirtualną systemu Linux](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Następnie należy tooSSH do hello maszyny Wirtualnej systemu Linux. Jeśli potrzebujesz pomocy dotyczącej Tworzenie klucza SSH, można head [toolearn tutaj jak toocreate klucza SSH w systemie Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
Jeśli masz już klucz SSH, przejdź dalej i SSH w wierszu polecenia do maszyny Wirtualnej systemu Linux z `ssh exampleUsername@exampleDNS`.

Teraz, gdy pracujesz w sieci maszyny Wirtualnej systemu Linux, możemy przeprowadzenie instalacji stosu światła hello na podstawie Debian dystrybucji. dokładne polecenia Hello może się różnić dla innych dystrybucjach systemu Linux.

#### <a name="installing-on-debianubuntu"></a>Instalowanie na Debian/Ubuntu
Należy hello następujące pakiety zainstalowane: `apache2`, `mysql-server`, `php5`, i `php5-mysql`. Te pakiety można zainstalować bezpośrednio dane te pakiety lub używając Tasksel. Poniżej przedstawiono instrukcje dla obu opcji.
Przed rozpoczęciem instalacji należy toodownload i zaktualizowanie listy pakietu.

    user@ubuntu$ sudo apt-get update

##### <a name="individual-packages"></a>Indywidualne pakiety
Przy użyciu get stanie:

    user@ubuntu$ sudo apt-get install apache2 mysql-server php5 php5-mysql

##### <a name="using-tasksel"></a>Przy użyciu tasksel
Alternatywnie możesz pobrać Tasksel, narzędzie Debian/Ubuntu wielu powiązanych pakietów jest instalowany jako skoordynowanego "zadania" do systemu.

    user@ubuntu$ sudo apt-get install tasksel
    user@ubuntu$ sudo tasksel install lamp-server

Po uruchomieniu hello poprzedniej opcji, należy być tooinstall zostanie wyświetlony monit o te pakiety i różnych innych zależności. Naciśnij "y", a następnie toocontinue "Wprowadź" i wykonać żadnych innych monity tooset hasła administratora dla programu MySQL. Spowoduje to zainstalowanie hello minimalne wymagane PHP rozszerzenia potrzebne toouse PHP z programem MySQL. 

![][1]

Uruchom następujące polecenie toosee hello innych rozszerzeń PHP, które są dostępne w postaci pakietów:

    user@ubuntu$ apt-cache search php5


#### <a name="create-infophp-document"></a>Utwórz dokument info.php
Teraz powinno być możliwe toocheck Apache, MySQL i PHP którą wersję należy za pomocą wiersza polecenia hello wpisując `apache2 -v`, `mysql -v`, lub `php -v`.

Jeśli użytkownik będzie jak tootest bardziej, można utworzyć szybkie tooview strony informacji PHP w przeglądarce. Utwórz plik z Nano edytora tekstu, korzystając z tego polecenia:

    user@ubuntu$ sudo nano /var/www/html/info.php

W edytorze tekstu GNU Nano hello Dodaj następujące wiersze hello:

    <?php
    phpinfo();
    ?>

Następnie zapisz i zamknij Edytor tekstu hello.

Dlatego wszystkie nowe instalacje zostały uwzględnione, uruchom ponownie Apache za pomocą tego polecenia.

    user@ubuntu$ sudo service apache2 restart

## <a name="verify-lamp-successfully-installed"></a>Sprawdź światła pomyślnie zainstalowany
Teraz można sprawdzić stronę informacji PHP hello utworzonego przez otwarcie przeglądarki i przechodzi do toohttp://youruniqueDNS/info.php. Jego wygląd powinien być podobny toothis obrazu.

![][2]

Apache instalację można sprawdzić, wyświetlając hello Apache2 Ubuntu domyślna strona przechodząc tooyou http://youruniqueDNS/. Powinien zostać wyświetlony ekran podobny do tego obrazu.

![][3]

Gratulacje, mają stos światła tylko Instalatora na maszynie Wirtualnej platformy Azure!

## <a name="next-steps"></a>Następne kroki
Wyewidencjonuj hello dokumentacji Ubuntu na stosie światła hello:

* [https://help.ubuntu.com/Community/ApacheMySQLPHP](https://help.ubuntu.com/community/ApacheMySQLPHP)

[1]: ./media/deploy-lamp-stack/configmysqlpassword-small.png
[2]: ./media/deploy-lamp-stack/phpsuccesspage.png
[3]: ./media/deploy-lamp-stack/apachesuccesspage.png