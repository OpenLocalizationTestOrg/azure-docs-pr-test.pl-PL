---
title: "Automatyzowanie wdrażaniem aplikacji za pomocą rozszerzenia maszyny wirtualnej | Dokumentacja firmy Microsoft"
description: Samouczek DotNet podstawowej maszyny wirtualnej platformy Azure
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 9fc8b1ba-60f5-410b-8190-9f1ff885e50e
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2f972fef75aa8e13af7dab908c2b0e2ec28f1324
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="application-deployment-with-azure-resource-manager-templates-for-linux-vms"></a>Wdrażanie aplikacji przy użyciu szablonów usługi Azure Resource Manager dla maszyn wirtualnych systemu Linux

Po zidentyfikowaniu wszystkie wymagania infrastrukturalne Azure i przetłumaczyć Szablon wdrożenia, wdrożenia aplikacji rzeczywistych musi należy się zająć. Wdrażanie aplikacji w tym miejscu odwołuje się do instalowania plików binarnych aplikacji rzeczywistych na zasobów platformy Azure. Dla przykładu magazynu muzyki, .net Core, NGINX i przełożonego muszą być zainstalowane i skonfigurowane na każdej maszynie wirtualnej. Pliki binarne utworów muzycznych magazynu muszą być zainstalowane na maszynie wirtualnej, a wstępnie utworzonej bazy danych magazynu utworów muzycznych.

Ten dokument zawiera szczegóły dotyczące sposobu rozszerzenia maszyny wirtualnej można zautomatyzować wdrożenie aplikacji i konfiguracji do maszyn wirtualnych platformy Azure. Wszystkie zależności i unikatowe konfiguracje są wyróżnione. Aby uzyskać najlepsze wyniki wykonaj wstępne wdrożenie wystąpienia rozwiązania do subskrypcji platformy Azure i pracy wraz z szablonu usługi Azure Resource Manager. Zakończenie szablonu można znaleźć tutaj — [wdrożenia magazynu utworów muzycznych na Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).

## <a name="configuration-script"></a>Skrypt konfiguracji
Rozszerzenia maszyn wirtualnych to specjalne programy, które wykonać przed maszynami wirtualnymi w celu zapewnienia automatyzacji konfiguracji. Rozszerzenia są dostępne dla wielu określonych celów, takich jak oprogramowanie antywirusowe, Konfiguracja rejestrowania i konfiguracji Docker. Rozszerzenie skryptu niestandardowego może służyć do wykonywania dowolny skrypt do maszyny wirtualnej. Przykład utworów muzycznych magazynu jest rozszerzenie skryptu niestandardowego do konfigurowania maszyny wirtualnej systemu Ubuntu i instalowanie aplikacji do sklepu utworów muzycznych. 

Przed opisujące, jak został zadeklarowany rozszerzenia maszyny wirtualnej w szablonie usługi Azure Resource Manager, Sprawdź skrypt, który jest uruchamiany. Ten skrypt służy do konfigurowania maszyny wirtualnej systemu Ubuntu na potrzeby hostowania aplikacji utworów muzycznych magazynu. Uruchom skrypt instaluje wszystkie wymagane oprogramowanie, instalowania aplikacji do sklepu utworów muzycznych z kontroli źródła i przygotowanie bazy danych. 

Aby dowiedzieć się więcej o hostingu .net Core aplikacji w systemie Linux, zobacz [publikowania w środowisku produkcyjnym Linux](https://docs.asp.net/en/latest/publishing/linuxproduction.html).

> Ten przykład jest w celach demonstracyjnych.
> 
> 

```bash
#!/bin/bash

# install dotnet core
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ trusty main" > /etc/apt/sources.list.d/dotnetdev.list'
sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
sudo apt-get update
sudo apt-get install -y dotnet-dev-1.0.0-preview2-003121

# download application
sudo wget https://raw.github.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/music-app/music-store-azure-demo-pub.tar /
sudo mkdir /opt/music
sudo tar -xf music-store-azure-demo-pub.tar -C /opt/music

# install nginx, update config file
sudo apt-get install -y nginx
sudo service nginx start
sudo touch /etc/nginx/sites-available/default
sudo wget https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/music-app/nginx-config/default -O /etc/nginx/sites-available/default
sudo cp /opt/music/nginx-config/default /etc/nginx/sites-available/
sudo nginx -s reload

# update and secure music config file
sed -i "s/<replaceserver>/$1/g" /opt/music/config.json
sed -i "s/<replaceuser>/$2/g" /opt/music/config.json
sed -i "s/<replacepass>/$3/g" /opt/music/config.json
sudo chown $2 /opt/music/config.json
sudo chmod 0400 /opt/music/config.json

# config supervisor
sudo apt-get install -y supervisor
sudo touch /etc/supervisor/conf.d/music.conf
sudo wget https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/music-app/supervisor/music.conf -O /etc/supervisor/conf.d/music.conf
sudo service supervisor stop
sudo service supervisor start

# pre-create music store database
/usr/bin/dotnet /opt/music/MusicStore.dll &
```

## <a name="vm-script-extension"></a>Rozszerzenie skryptu maszyny Wirtualnej
Rozszerzenia maszyny Wirtualnej mogą być uruchamiane na maszynie wirtualnej w czasie kompilacji poprzez włączenie rozszerzenia zasobu w szablonie usługi Azure Resource Manager. Rozszerzenie można dodać przy użyciu Kreatora programu Visual Studio dodawania zasobów lub przez wstawienie poprawne dane JSON do szablonu. Zasób rozszerzenie skryptu jest zagnieżdżona zasobu maszyny wirtualnej. Można to zaobserwować w poniższym przykładzie.

Wykonaj to łącze, aby zobaczyć przykładowy JSON w szablonie usługi Resource Manager — [rozszerzenia maszyny Wirtualnej skryptu](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L359). 

Zwróć uwagę, w poniżej JSON, że skrypt jest przechowywany w serwisie GitHub. Ten skrypt może być również przechowywane w magazynie obiektów Blob Azure. Ponadto szablonów usługi Azure Resource Manager Zezwalaj ciąg wykonywania skryptu do skonstruowany w taki sposób, że wartości parametrów szablonu mogą być używane jako parametry do wykonania skryptu. W takim przypadku danych jest dostępne w przypadku wdrażania szablonów, a następnie można używać tych wartości, podczas wykonywania skryptu.

```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
  }
}
```

Aby uzyskać więcej informacji na temat używania niestandardowego rozszerzenia skryptu, zobacz [niestandardowego rozszerzenia skryptu z szablonami usługi Resource Manager](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="next-step"></a>Następny krok
<hr>

[Eksploruj szablonów więcej Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates)

