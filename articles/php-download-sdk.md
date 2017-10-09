---
title: Witaj aaaDownload zestaw Azure SDK for PHP
description: "Dowiedz się, jak toodownload i zainstaluj hello zestawu Azure SDK dla języka PHP."
documentationcenter: php
services: app-service\web
author: allclark
manager: douge
editor: 
ms.assetid: bac355ac-4c25-42f4-8273-c5112eafa8d4
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 06/01/2016
ms.author: allclark;yaqiyang
ms.openlocfilehash: 94f56fc4f91bb175c08b9f7a43cb221c827694a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="download-hello-azure-sdk-for-php"></a>Pobierz hello Azure SDK dla języka PHP
## <a name="overview"></a>Omówienie
zestaw Azure SDK for PHP Hello obejmuje składniki, które pozwalają toodevelop, wdrażania i zarządzania aplikacji PHP dla systemu Azure. W szczególności hello zestaw Azure SDK for PHP zawiera następujące hello:

* **Witaj bibliotek klienckich PHP na platformie Azure**. Te biblioteki klas zapewniają interfejs do uzyskiwania dostępu do funkcji platformy Azure, takich jak dane usługi zarządzania i usługi w chmurze.  
* **Witaj interfejsu wiersza polecenia platformy Azure dla komputerów Mac, Linux i Windows (Azure CLI)**. Jest to zestaw poleceń służących do wdrażania i zarządzania usługami Azure, takich jak witryny sieci Web Azure i maszyn wirtualnych platformy Azure. Praca z wiersza polecenia platformy Azure na dowolnej platformie, w tym Mac, Linux i Windows Hello.
* **Program Azure PowerShell (tylko system Windows)**. Jest to zestaw poleceń cmdlet programu PowerShell dotyczące wdrażania i zarządzania usługami Azure, takich jak usługi w chmurze i maszyn wirtualnych.
* **Hello (tylko system Windows) Azure emulatory**. emulatory Hello obliczeniowych i przestrzeni dyskowej są emulatory lokalne usługi w chmurze i usług zarządzania danych, które pozwalają tootest aplikacji lokalnie. emulatory Azure Hello uruchamianie tylko w systemie Windows.

w poniższych rozdziałach Hello opisano, jak toodownload i zainstaluj hello składniki opisane powyżej.

Witaj instrukcje w tym temacie założono, że istnieje [PHP] [ install-php] zainstalowane.

> [!NOTE]
> Musi mieć PHP 5.5 lub wyższej toouse hello PHP bibliotek klienta platformy Azure.
> 
> 

## <a name="php-client-libraries-for-azure"></a>Biblioteki klienckie języka PHP dla systemu Azure
Witaj PHP klienta biblioteki dla platformy Azure zapewniają interfejs do uzyskiwania dostępu do funkcji platformy Azure, takich jak dane usługi zarządzania i usługami w chmurze, z dowolnego systemu operacyjnego. Te biblioteki można zainstalować za pomocą hello Composer.

Informacje, jak toouse hello PHP bibliotek klienta platformy Azure, zobacz [jak tooUse hello usługa Blob][blob-service], [jak tooUse hello usługi tabel] [ table-service] i [jak tooUse hello usługi kolejki][queue-service].

### <a name="install-via-composer"></a>Zainstaluj za pośrednictwem Composer
1. [Zainstaluj usługę Git][install-git].

    > [AZURE.NOTE] W systemie Windows należy również zmiennej środowiskowej ŚCIEŻKA pliku wykonywalnego tooyour tooadd hello Git.

1. Utwórz plik o nazwie **composer.json** w hello katalogu głównym projektu i dodać powitania po tooit kodu:
   
        {
            "require": {
                "microsoft/windowsazure": "^0.4"
            }
        }
2. Pobierz  **[composer.phar] [ composer-phar]**  w katalogu głównym projektu.
3. Otwórz wiersz polecenia i wykonania tej operacji w katalogu głównym projektu
   
        php composer.phar install

## <a name="azure-powershell-and-azure-emulators"></a>Program Azure PowerShell i emulatory Azure
Program Azure PowerShell jest zestawem poleceń cmdlet programu PowerShell dotyczące wdrażania i zarządzania usługami Azure (takie jak usługi w chmurze i maszyn wirtualnych). emulatory Azure Hello są emulatory usługi w chmurze i usług zarządzania danych, które pozwalają tootest aplikacji lokalnie. Te składniki są obsługiwane tylko w systemie Windows.

Witaj tooinstall zalecany sposób programu Azure PowerShell i hello Azure emulatory jest toouse hello [Instalatora platformy sieci Web firmy Microsoft][download-wpi]. Należy pamiętać, że można także tooinstall inne składniki programowanie, takich jak PHP, SQL Server, hello Drivers firmy Microsoft dla programu SQL Server dla PHP i programu WebMatrix.

Aby uzyskać informacje na temat toouse programu Azure PowerShell, zobacz [jak tooUse programu Azure PowerShell][powershell-tools].

## <a name="azure-cli"></a>Interfejs wiersza polecenia platformy Azure
Hello Azure CLI jest zestaw poleceń służących do wdrażania i zarządzania usługami Azure, takich jak witryny sieci Web Azure i maszyn wirtualnych platformy Azure. Aby uzyskać informacje o instalowaniu interfejsu wiersza polecenia Azure, zobacz [hello instalowanie interfejsu wiersza polecenia Azure](cli-install-nodejs.md).

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji, zobacz hello [Centrum deweloperów języka PHP](/develop/php/).

[install-php]: http://www.php.net/manual/en/install.php
[composer-github]: https://github.com/composer/composer
[composer-phar]: http://getcomposer.org/composer.phar
[nodejs-org]: http://nodejs.org/
[install-node-linux]: https://github.com/joyent/node/wiki/Installing-Node.js-via-package-manager
[download-wpi]: http://go.microsoft.com/fwlink/?LinkId=253447
[mac-installer]: http://go.microsoft.com/fwlink/?LinkId=252249
[blob-service]: http://go.microsoft.com/fwlink/?LinkId=252714
[table-service]: http://go.microsoft.com/fwlink/?LinkId=252715
[queue-service]: http://go.microsoft.com/fwlink/?LinkId=252716
[azure cli]: http://go.microsoft.com/fwlink/?LinkId=252717
[powershell-tools]: http://go.microsoft.com/fwlink/?LinkId=252718
[php-sdk-github]: http://go.microsoft.com/fwlink/?LinkId=252719
[install-git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
