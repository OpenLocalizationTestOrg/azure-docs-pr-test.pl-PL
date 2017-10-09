---
title: "aaaAutomating wdrażaniem aplikacji za pomocą rozszerzenia maszyny wirtualnej | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 38a02a4271d6b9ba02a473a51794a7bd90ca3a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="application-deployment-with-azure-resource-manager-templates-for-linux-vms"></a><span data-ttu-id="f5d08-103">Wdrażanie aplikacji przy użyciu szablonów usługi Azure Resource Manager dla maszyn wirtualnych systemu Linux</span><span class="sxs-lookup"><span data-stu-id="f5d08-103">Application deployment with Azure Resource Manager templates for Linux VMs</span></span>

<span data-ttu-id="f5d08-104">Po zidentyfikowaniu wszystkie wymagania infrastrukturalne Azure i przetłumaczyć Szablon wdrożenia, wdrożenia rzeczywistej aplikacji hello musi toobe problemu.</span><span class="sxs-lookup"><span data-stu-id="f5d08-104">Once all Azure infrastructural requirements have been identified and translated into a deployment template, hello actual application deployment needs toobe addressed.</span></span> <span data-ttu-id="f5d08-105">Wdrażanie aplikacji w tym miejscu odwołuje się binarne rzeczywistej aplikacji hello tooinstalling na zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f5d08-105">Application deployment here is referring tooinstalling hello actual application binaries onto Azure resources.</span></span> <span data-ttu-id="f5d08-106">Dla przykładu magazynu utworów muzycznych hello, .net Core, NGINX i przełożonego muszą toobe zainstalowany i skonfigurowany na każdej maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f5d08-106">For hello Music Store sample, .Net Core, NGINX, and Supervisor need toobe installed and configured on each virtual machine.</span></span> <span data-ttu-id="f5d08-107">Hello utworów muzycznych magazynu plików binarnych muszą toobe zainstalowana na maszynie wirtualnej hello i hello bazy danych magazynu utworów muzycznych wstępnie utworzone.</span><span class="sxs-lookup"><span data-stu-id="f5d08-107">hello Music Store binaries need toobe installed onto hello virtual machine, and hello Music Store database pre-created.</span></span>

<span data-ttu-id="f5d08-108">Ten dokument zawiera szczegóły dotyczące sposobu rozszerzenia maszyny wirtualnej można zautomatyzować aplikacji wdrażania i konfigurowania tooAzure maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="f5d08-108">This document details how Virtual Machine extensions can automate application deployment and configuration tooAzure virtual machines.</span></span> <span data-ttu-id="f5d08-109">Wszystkie zależności i unikatowe konfiguracje są wyróżnione.</span><span class="sxs-lookup"><span data-stu-id="f5d08-109">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="f5d08-110">Hello najlepsze środowisko pracy wykonaj wstępne wdrożenie wystąpienie tooyour rozwiązania hello subskrypcji platformy Azure i pracy oraz hello szablonu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f5d08-110">For hello best experience, pre-deploy an instance of hello solution tooyour Azure subscription and work along with hello Azure Resource Manager template.</span></span> <span data-ttu-id="f5d08-111">Szablon pełną Hello można znaleźć tutaj — [wdrożenia magazynu utworów muzycznych na Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span><span class="sxs-lookup"><span data-stu-id="f5d08-111">hello complete template can be found here – [Music Store Deployment on Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span>

## <a name="configuration-script"></a><span data-ttu-id="f5d08-112">Skrypt konfiguracji</span><span class="sxs-lookup"><span data-stu-id="f5d08-112">Configuration script</span></span>
<span data-ttu-id="f5d08-113">Rozszerzenia maszyn wirtualnych to specjalne programy, które wykonać automatyzacji konfiguracji tooprovide maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="f5d08-113">Virtual Machine extensions are specialized programs that execute against virtual machines tooprovide configuration automation.</span></span> <span data-ttu-id="f5d08-114">Rozszerzenia są dostępne dla wielu określonych celów, takich jak oprogramowanie antywirusowe, Konfiguracja rejestrowania i konfiguracji Docker.</span><span class="sxs-lookup"><span data-stu-id="f5d08-114">Extensions are available for many specific purposes such as anti-virus, logging configuration, and Docker configuration.</span></span> <span data-ttu-id="f5d08-115">Rozszerzenie skryptu niestandardowego mogą być używane toorun dowolny skrypt na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f5d08-115">A custom script extension can be used toorun any script against a virtual machine.</span></span> <span data-ttu-id="f5d08-116">Przykład sklep muzyczny hello jest zapasowych maszyn wirtualnych Ubuntu hello tooconfigure toohello skryptu niestandardowego rozszerzenia i zainstaluj aplikację ze sklepu utworów muzycznych hello.</span><span class="sxs-lookup"><span data-stu-id="f5d08-116">With hello Music Store sample, it is up toohello custom script extension tooconfigure hello Ubuntu virtual machines and install hello Music Store application.</span></span> 

<span data-ttu-id="f5d08-117">Przed opisujące, jak został zadeklarowany rozszerzenia maszyny wirtualnej w szablonie usługi Azure Resource Manager, sprawdź hello skrypt, który jest uruchamiany.</span><span class="sxs-lookup"><span data-stu-id="f5d08-117">Before detailing how virtual machine extensions are declared in an Azure Resource Manager template, examine hello script that is run.</span></span> <span data-ttu-id="f5d08-118">Ten skrypt konfiguruje hello Ubuntu maszyny wirtualnej toohost hello aplikację ze sklepu utworów muzycznych.</span><span class="sxs-lookup"><span data-stu-id="f5d08-118">This script configures hello Ubuntu virtual machine toohost hello Music Store application.</span></span> <span data-ttu-id="f5d08-119">Po uruchomieniu skryptu hello instaluje wszystkie niezbędne oprogramowanie, zainstaluj aplikację ze sklepu utworów muzycznych hello z kontroli źródła i przygotowanie hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="f5d08-119">When run, hello script installs all needed software, install hello Music store application from source control, and prepare hello database.</span></span> 

<span data-ttu-id="f5d08-120">toolearn więcej informacji na temat hostingu .net Core aplikacji w systemie Linux, zobacz [środowiska produkcyjnego Linux tooa publikowania](https://docs.asp.net/en/latest/publishing/linuxproduction.html).</span><span class="sxs-lookup"><span data-stu-id="f5d08-120">toolearn more about hosting a .Net Core application on Linux, see [Publish tooa Linux production environment](https://docs.asp.net/en/latest/publishing/linuxproduction.html).</span></span>

> <span data-ttu-id="f5d08-121">Ten przykład jest w celach demonstracyjnych.</span><span class="sxs-lookup"><span data-stu-id="f5d08-121">This sample is for demonstration purposes.</span></span>
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

## <a name="vm-script-extension"></a><span data-ttu-id="f5d08-122">Rozszerzenie skryptu maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="f5d08-122">VM Script Extension</span></span>
<span data-ttu-id="f5d08-123">Rozszerzenia maszyny Wirtualnej mogą być uruchamiane na maszynie wirtualnej w czasie kompilacji przez dołączenie hello rozszerzenie zasobu do szablonu usługi Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="f5d08-123">VM Extensions can be run against a virtual machine at build time by including hello extension resource in hello Azure Resource Manager template.</span></span> <span data-ttu-id="f5d08-124">rozszerzenie Hello można dodać za pomocą Kreatora programu Visual Studio dodawania zasobów hello lub wstawiając poprawne dane JSON do hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="f5d08-124">hello extension can be added with hello Visual Studio Add Resource wizard, or by inserting valid JSON into hello template.</span></span> <span data-ttu-id="f5d08-125">Hello zasobów rozszerzenie skryptu jest zagnieżdżona hello zasobu maszyny wirtualnej. Można to zaobserwować w hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="f5d08-125">hello Script Extension resource is nested inside hello Virtual Machine resource; this can be seen in hello following example.</span></span>

<span data-ttu-id="f5d08-126">Wykonaj ten przykład link toosee hello JSON w szablonie usługi Resource Manager hello — [rozszerzenia maszyny Wirtualnej skryptu](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L359).</span><span class="sxs-lookup"><span data-stu-id="f5d08-126">Follow this link toosee hello JSON sample within hello Resource Manager template – [VM Script Extension](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L359).</span></span> 

<span data-ttu-id="f5d08-127">Wyprzedzeniem hello poniżej JSON, który hello skrypt jest przechowywany w serwisie GitHub.</span><span class="sxs-lookup"><span data-stu-id="f5d08-127">Notice in hello below JSON that hello script is stored in GitHub.</span></span> <span data-ttu-id="f5d08-128">Ten skrypt może być również przechowywane w magazynie obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="f5d08-128">This script could also be stored in Azure Blob storage.</span></span> <span data-ttu-id="f5d08-129">Ponadto szablonów usługi Azure Resource Manager Zezwalaj tooconstructed ciąg wykonywania skryptu hello tak, aby wartości parametrów szablonu mogą być używane jako parametry do wykonania skryptu.</span><span class="sxs-lookup"><span data-stu-id="f5d08-129">Also, Azure Resource Manager templates allow hello script execution string tooconstructed such that template parameters values can be used as parameters for script execution.</span></span> <span data-ttu-id="f5d08-130">W takim przypadku danych jest dostępne w przypadku wdrażania hello szablony, a następnie można używać tych wartości, podczas wykonywania skryptu hello.</span><span class="sxs-lookup"><span data-stu-id="f5d08-130">In this case data is provided when deploying hello templates, and these values can then be used when executing hello script.</span></span>

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

<span data-ttu-id="f5d08-131">Aby uzyskać więcej informacji na temat używania hello niestandardowe rozszerzenie skryptu, zobacz [niestandardowego rozszerzenia skryptu z szablonami usługi Resource Manager](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f5d08-131">For more information on using hello custom script extension, see [Custom script extensions with Resource Manager templates](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="next-step"></a><span data-ttu-id="f5d08-132">Następny krok</span><span class="sxs-lookup"><span data-stu-id="f5d08-132">Next Step</span></span>
<hr>

[<span data-ttu-id="f5d08-133">Eksploruj szablonów więcej Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f5d08-133">Explore More Azure Resource Manager Templates</span></span>](https://github.com/Azure/azure-quickstart-templates)

