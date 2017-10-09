---
title: aaaUse hello rozszerzenia CustomScript na maszynie Wirtualnej systemu Linux | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toouse hello CustomScript rozszerzenia toodeploy aplikacji na maszynach wirtualnych systemu Linux na platformie Azure utworzone przy użyciu hello klasycznego modelu wdrażania."
editor: tysonn
manager: timlt
documentationcenter: 
services: virtual-machines-linux
author: gbowerman
tags: azure-service-management
ms.assetid: e535241d-feca-4412-b07a-67c936ba88a0
ms.service: virtual-machines-linux
ms.workload: multiple
ms.tgt_pltfrm: linux
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: guybo
ms.openlocfilehash: 864a586e70093eefbabc065a3c05e1cf9e315704
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-lamp-app-using-hello-azure-customscript-extension-for-linux"></a>Wdrażanie aplikacji światła przy użyciu hello rozszerzenia CustomScript Azure dla systemu Linux
> [!IMPORTANT] 
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager. Informacje o wdrażaniu przy użyciu modelu Resource Manager hello stosu światło, zobacz [tutaj](../tutorial-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Witaj rozszerzenia CustomScript Azure firmy Microsoft dla systemu Linux udostępnia toocustomize sposób maszyn wirtualnych (VM), uruchamiając dowolny kod napisany w dowolnym języku skryptowym obsługiwane przez hello maszyny Wirtualnej (na przykład, Python i Bash). Zapewnia to tooautomate bardzo elastyczny sposób maszyny toomultiple wdrożenia aplikacji.

Witaj rozszerzenia CustomScript można wdrożyć przy użyciu hello portalu Azure, programu Windows PowerShell lub hello interfejsu wiersza polecenia platformy Azure (Azure CLI).

W tym artykule, które będą używane hello Azure CLI toodeploy proste tooan aplikacji światła maszyny Wirtualnej systemu Ubuntu utworzone przy użyciu hello klasycznego modelu wdrażania.

## <a name="prerequisites"></a>Wymagania wstępne
W tym przykładzie należy najpierw utworzyć dwie maszyny wirtualne Azure systemem Ubuntu 14.04 lub nowszej. Witaj maszyny wirtualne są nazywane *maszyny wirtualnej skryptu* i *światło vm*. Użyj unikatowej nazwy podczas tworzenia maszyn wirtualnych hello. Jeden z nich jest używana toorun hello polecenia interfejsu wiersza polecenia i jednym jest używana toodeploy hello światła aplikacji.

Należy również konta usługi Azure Storage i klucza tooaccess it (można uzyskać to hello portalu Azure).

Jeśli potrzebujesz, aby uzyskać pomoc przy tworzeniu maszyn wirtualnych systemu Linux na platformie Azure można znaleźć zbyt[tworzenia maszyny wirtualnej systemem Linux](createportal.md).

Witaj instalacji poleceniach założono, Ubuntu, ale hello instalacji można dostosować dowolne obsługiwane distro systemu Linux.

Witaj maszyny Wirtualnej vm skryptu musi toohave instalowania interfejsu wiersza polecenia Azure, z tooAzure połączenia pracy. Aby uzyskać pomoc na ten temat, zobacz zbyt[Instalowanie i Konfigurowanie interfejsu wiersza polecenia platformy Azure hello](../../../cli-install-nodejs.md).

## <a name="upload-a-script"></a>Przekaż skryptu
Firma Microsoft będzie hello rozszerzenia CustomScript toorun skrypt w systemie zdalnym stos światła hello tooinstall maszyny Wirtualnej i Utwórz stronę PHP. W skrypcie hello tooaccess zamówień z dowolnego miejsca będzie przekazać jako obiektów blob platformy Azure.

### <a name="script-overview"></a>Przegląd skryptu
Przykładowy skrypt Hello instaluje tooUbuntu stosu światło, (w tym konfigurowania instalacji dyskretnej programu MySQL), zapisuje prostego pliku PHP i uruchamia Apache.

    #!/bin/bash
    # set up a silent install of MySQL
    dbpass="mySQLPassw0rd"

    export DEBIAN_FRONTEND=noninteractive
    echo mysql-server-5.6 mysql-server/root_password password $dbpass | debconf-set-selections
    echo mysql-server-5.6 mysql-server/root_password_again password $dbpass | debconf-set-selections

    # install hello LAMP stack
    apt-get -y install apache2 mysql-server php5 php5-mysql  

    # write some PHP
    echo \<center\>\<h1\>My Demo App\</h1\>\<br/\>\</center\> > /var/www/html/phpinfo.php
    echo \<\?php phpinfo\(\)\; \?\> >> /var/www/html/phpinfo.php

    # restart Apache
    apachectl restart

### <a name="upload-script"></a>Przekaż skryptu
Zapisz skrypt hello jako pliku tekstowego, na przykład *install_lamp.sh*, a następnie przekaż tooAzure magazynu. Można to zrobić łatwo z wiersza polecenia platformy Azure. Witaj poniższy przykład przekazuje hello pliku tooa kontenera magazynu o nazwie "skrypty". Jeśli nie istnieje w kontenerze hello potrzebujesz toocreate go pierwszy.

    azure storage blob upload -a <yourStorageAccountName> -k <yourStorageKey> --container scripts ./install_lamp.sh

Utwórz również pliku JSON, który opisuje, jak toodownload hello skryptu z usługi Magazyn Azure. Zapisz jako *public_config.json* (zastępując "mystorage" hello nazwą konta magazynu):

    {"fileUris":["https://mystorage.blob.core.windows.net/scripts/install_lamp.sh"], "commandToExecute":"sh install_lamp.sh" }


## <a name="deploy-hello-extension"></a>Wdrażanie rozszerzenia hello
Teraz można używać hello następnego polecenia toodeploy hello rozszerzenia CustomScript Linux toohello zdalnego maszynę Wirtualną przy użyciu hello wiersza polecenia platformy Azure.

    azure vm extension set -c "./public_config.json" lamp-vm CustomScript Microsoft.Azure.Extensions 2.0

Witaj poprzednie polecenie pobiera i uruchamia hello *install_lamp.sh* skrypt na powitania maszyny Wirtualnej o nazwie *maszyny wirtualnej światła*.

Ponieważ aplikacja hello obejmuje serwer sieci web, pamiętaj tooopen HTTP port nasłuchiwania na powitania zdalnego maszyny Wirtualnej z hello następnego polecenia.

    azure vm endpoint create -n Apache -o tcp lamp-vm 80 80

## <a name="monitoring-and-troubleshooting"></a>Monitorowanie i rozwiązywanie problemów
Możesz sprawdzić na jak hello niestandardowy skrypt będzie uruchamiany sprawdzając plik dziennika hello hello zdalnego maszyny Wirtualnej. SSH za*maszyny wirtualnej światła* i pliku dziennika hello tail z hello następnego polecenia.

    cd /var/log/azure/customscript
    tail -f handler.log

Po uruchomieniu hello rozszerzenia CustomScript można przeglądać strony PHP toohello, utworzone informacji. Strona Hello PHP, na przykład hello w tym artykule jest *http://lamp-vm.cloudapp.net/phpinfo.php*.

## <a name="additional-resources"></a>Dodatkowe zasoby
Można użyć hello toodeploy podstawowe kroki tej samej bardziej złożonych aplikacji. W tym przykładzie skrypt instalacji hello został zapisany jako publiczny obiektów blob w usłudze Azure Storage. Opcja bardziej bezpieczna byłoby skrypt instalacji hello toostore jako bezpieczne obiektów blob z [bezpiecznego dostępu podpisu](https://msdn.microsoft.com/library/azure/ee395415.aspx) (SAS).

Dodatkowe zasoby dla wiersza polecenia platformy Azure, Linux i hello rozszerzenia CustomScript są wyświetlane obok.

[Automatyzowanie zadań dostosowania maszyny Wirtualnej systemu Linux za pomocą rozszerzenia CustomScript](https://azure.microsoft.com/blog/2014/08/20/automate-linux-vm-customization-tasks-using-customscript-extension/)

[Rozszerzenia Azure Linux (GitHub)](https://github.com/Azure/azure-linux-extensions)