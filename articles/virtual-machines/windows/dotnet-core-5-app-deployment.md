---
title: "Automatyzowanie wdrażaniem aplikacji za pomocą rozszerzenia maszyny wirtualnej | Dokumentacja firmy Microsoft"
description: Samouczek DotNet podstawowej maszyny wirtualnej platformy Azure
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 79c91304-6c1b-4354-a185-fecc129b139d
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f2996eef71b39c6240fac5484854f72d3e657d0f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="application-deployment-with-azure-resource-manager-templates-for-windows-vms"></a><span data-ttu-id="424a2-103">Wdrażanie aplikacji przy użyciu szablonów usługi Azure Resource Manager dla maszyn wirtualnych systemu Windows</span><span class="sxs-lookup"><span data-stu-id="424a2-103">Application deployment with Azure Resource Manager templates for Windows VMs</span></span>

<span data-ttu-id="424a2-104">Po zidentyfikowaniu wszystkie wymagania infrastrukturalne Azure i przetłumaczyć Szablon wdrożenia, wdrożenia aplikacji rzeczywistych musi należy się zająć.</span><span class="sxs-lookup"><span data-stu-id="424a2-104">Once all Azure infrastructural requirements have been identified and translated into a deployment template, the actual application deployment needs to be addressed.</span></span> <span data-ttu-id="424a2-105">Wdrażanie aplikacji w tym miejscu odwołuje się do instalowania plików binarnych aplikacji rzeczywistych na zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="424a2-105">Application deployment here is referring to installing the actual application binaries onto Azure resources.</span></span> <span data-ttu-id="424a2-106">Dla przykładu magazynu muzyki, .net Core i IIS muszą być zainstalowana i skonfigurowana na każdej maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="424a2-106">For the Music Store sample, .Net Core and IIS need to be installed and configured on each virtual machine.</span></span> <span data-ttu-id="424a2-107">Pliki binarne utworów muzycznych magazynu muszą być zainstalowane na maszynie wirtualnej, a wstępnie utworzonej bazy danych magazynu utworów muzycznych.</span><span class="sxs-lookup"><span data-stu-id="424a2-107">The Music Store binaries need to be installed onto the virtual machine, and the Music Store database pre-created.</span></span>

<span data-ttu-id="424a2-108">Ten dokument zawiera szczegóły dotyczące sposobu rozszerzenia maszyny wirtualnej można zautomatyzować wdrożenie aplikacji i konfiguracji do maszyn wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="424a2-108">This document details how Virtual Machine extensions can automate application deployment and configuration to Azure virtual machines.</span></span> <span data-ttu-id="424a2-109">Wszystkie zależności i unikatowe konfiguracje są wyróżnione.</span><span class="sxs-lookup"><span data-stu-id="424a2-109">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="424a2-110">Aby uzyskać najlepsze wyniki wykonaj wstępne wdrożenie wystąpienia rozwiązania do subskrypcji platformy Azure i pracy wraz z szablonu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="424a2-110">For the best experience, pre-deploy an instance of the solution to your Azure subscription and work along with the Azure Resource Manager template.</span></span> <span data-ttu-id="424a2-111">Zakończenie szablonu można znaleźć tutaj — [utworów muzycznych wdrożenia magazynu w systemie Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="424a2-111">The complete template can be found here – [Music Store Deployment on Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="configuration-script"></a><span data-ttu-id="424a2-112">Skrypt konfiguracji</span><span class="sxs-lookup"><span data-stu-id="424a2-112">Configuration script</span></span>
<span data-ttu-id="424a2-113">Rozszerzenia maszyn wirtualnych to specjalne programy, które wykonać przed maszynami wirtualnymi w celu zapewnienia automatyzacji konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="424a2-113">Virtual Machine extensions are specialized programs that execute against virtual machines to provide configuration automation.</span></span> <span data-ttu-id="424a2-114">Rozszerzenia są dostępne dla wielu określonych celów, takich jak oprogramowanie antywirusowe, Konfiguracja rejestrowania i konfiguracji Docker.</span><span class="sxs-lookup"><span data-stu-id="424a2-114">Extensions are available for many specific purposes such as anti-virus, logging configuration, and Docker configuration.</span></span> <span data-ttu-id="424a2-115">Rozszerzenie skryptu niestandardowego może służyć do wykonywania dowolny skrypt do maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="424a2-115">The Custom Script extension can be used to run any script against a virtual machine.</span></span> <span data-ttu-id="424a2-116">Przykład utworów muzycznych magazynu jest rozszerzenie skryptu niestandardowego do konfigurowania maszyn wirtualnych systemu Windows i instalowanie aplikacji do sklepu utworów muzycznych.</span><span class="sxs-lookup"><span data-stu-id="424a2-116">With the Music Store sample, it is up to the custom script extension to configure the Windows virtual machines and install the Music Store application.</span></span>

<span data-ttu-id="424a2-117">Przed opisujące, jak został zadeklarowany rozszerzenia maszyny wirtualnej w szablonie usługi Azure Resource Manager, Sprawdź skrypt, który jest uruchamiany.</span><span class="sxs-lookup"><span data-stu-id="424a2-117">Before detailing how virtual machine extensions are declared in an Azure Resource Manager template, examine the script that is run.</span></span> <span data-ttu-id="424a2-118">Ten skrypt służy do konfigurowania maszyny wirtualnej systemu Windows do obsługi aplikacji utworów muzycznych magazynu.</span><span class="sxs-lookup"><span data-stu-id="424a2-118">This script configures the Windows virtual machine to host the Music Store application.</span></span> <span data-ttu-id="424a2-119">Uruchom skrypt instaluje wszystkie wymagane oprogramowanie, instalowania aplikacji do sklepu utworów muzycznych z kontroli źródła i przygotowanie bazy danych.</span><span class="sxs-lookup"><span data-stu-id="424a2-119">When run, the script installs all needed software, install the Music store application from source control, and prepare the database.</span></span> 

> <span data-ttu-id="424a2-120">Ten przykład jest w celach demonstracyjnych.</span><span class="sxs-lookup"><span data-stu-id="424a2-120">This sample is for demonstration purposes.</span></span>

```PowerShell
<#
    .SYNOPSIS
        Downloads and configures .Net Core Music Store application sample across IIS and Azure SQL DB.
#>

Param (
    [string]$user,
    [string]$password,
    [string]$sqlserver
)

# Firewall
netsh advfirewall firewall add rule name="http" dir=in action=allow protocol=TCP localport=80

# Folders
New-Item -ItemType Directory c:\temp
New-Item -ItemType Directory c:\music

# Install iis
Install-WindowsFeature web-server -IncludeManagementTools

# Install dot.net core sdk
Invoke-WebRequest http://go.microsoft.com/fwlink/?LinkID=615460 -outfile c:\temp\vc_redistx64.exe
Start-Process c:\temp\vc_redistx64.exe -ArgumentList '/quiet' -Wait
Invoke-WebRequest https://go.microsoft.com/fwlink/?LinkID=809122 -outfile c:\temp\DotNetCore.1.0.0-SDK.Preview2-x64.exe
Start-Process c:\temp\DotNetCore.1.0.0-SDK.Preview2-x64.exe -ArgumentList '/quiet' -Wait
Invoke-WebRequest https://go.microsoft.com/fwlink/?LinkId=817246 -outfile c:\temp\DotNetCore.WindowsHosting.exe
Start-Process c:\temp\DotNetCore.WindowsHosting.exe -ArgumentList '/quiet' -Wait

# Download music app
Invoke-WebRequest  https://github.com/Microsoft/dotnet-core-sample-templates/raw/master/dotnet-core-music-windows/music-app/music-store-azure-demo-pub.zip -OutFile c:\temp\musicstore.zip
Expand-Archive C:\temp\musicstore.zip c:\music

# Azure SQL connection sting in environment variable
[Environment]::SetEnvironmentVariable("Data:DefaultConnection:ConnectionString", "Server=$sqlserver;Database=MusicStore;Integrated Security=False;User Id=$user;Password=$password;MultipleActiveResultSets=True;Connect Timeout=30",[EnvironmentVariableTarget]::Machine)

# Pre-create database
$env:Data:DefaultConnection:ConnectionString = "Server=$sqlserver;Database=MusicStore;Integrated Security=False;User Id=$user;Password=$password;MultipleActiveResultSets=True;Connect Timeout=30"
Start-Process 'C:\Program Files\dotnet\dotnet.exe' -ArgumentList 'c:\music\MusicStore.dll'

# Configure iis
Remove-WebSite -Name "Default Web Site"
Set-ItemProperty IIS:\AppPools\DefaultAppPool\ managedRuntimeVersion ""
New-Website -Name "MusicStore" -Port 80 -PhysicalPath C:\music\ -ApplicationPool DefaultAppPool
& iisreset
```

## <a name="vm-script-extension"></a><span data-ttu-id="424a2-121">Rozszerzenie skryptu maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="424a2-121">VM Script Extension</span></span>
<span data-ttu-id="424a2-122">Rozszerzenia maszyny Wirtualnej mogą być uruchamiane na maszynie wirtualnej w czasie kompilacji poprzez włączenie rozszerzenia zasobu w szablonie usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="424a2-122">VM Extensions can be run against a virtual machine at build time by including the extension resource in the Azure Resource Manager template.</span></span> <span data-ttu-id="424a2-123">Rozszerzenie można dodać przy użyciu Kreatora programu Visual Studio dodawania zasobów lub przez wstawienie poprawne dane JSON do szablonu.</span><span class="sxs-lookup"><span data-stu-id="424a2-123">The extension can be added with the Visual Studio Add Resource wizard, or by inserting valid JSON into the template.</span></span> <span data-ttu-id="424a2-124">Zasób rozszerzenie skryptu jest zagnieżdżona zasobu maszyny wirtualnej. Można to zaobserwować w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="424a2-124">The Script Extension resource is nested inside the Virtual Machine resource; this can be seen in the following example.</span></span>

<span data-ttu-id="424a2-125">Wykonaj to łącze, aby zobaczyć przykładowy JSON w szablonie usługi Resource Manager — [rozszerzenia maszyny Wirtualnej skryptu](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L339).</span><span class="sxs-lookup"><span data-stu-id="424a2-125">Follow this link to see the JSON sample within the Resource Manager template – [VM Script Extension](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L339).</span></span> 

<span data-ttu-id="424a2-126">Zwróć uwagę, w poniżej JSON, że skrypt jest przechowywany w serwisie GitHub.</span><span class="sxs-lookup"><span data-stu-id="424a2-126">Notice in the below JSON that the script is stored in GitHub.</span></span> <span data-ttu-id="424a2-127">Ten skrypt może być również przechowywane w magazynie obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="424a2-127">This script could also be stored in Azure Blob storage.</span></span> <span data-ttu-id="424a2-128">Ponadto szablonów usługi Azure Resource Manager Zezwalaj ciąg wykonywania skryptu do być skonstruowany w taki sposób, że wartości parametrów szablonu mogą być używane jako parametry do wykonania skryptu.</span><span class="sxs-lookup"><span data-stu-id="424a2-128">Also, Azure Resource Manager templates allow the script execution string to be constructed such that template parameters values can be used as parameters for script execution.</span></span> <span data-ttu-id="424a2-129">W takim przypadku danych jest dostępne w przypadku wdrażania szablonów, a następnie można używać tych wartości, podczas wykonywania skryptu.</span><span class="sxs-lookup"><span data-stu-id="424a2-129">In this case data is provided when deploying the templates, and these values can then be used when executing the script.</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.4",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
  }
}
```

<span data-ttu-id="424a2-130">Jak wcześniej wspomniano, istnieje również możliwość przechowywania niestandardowych skryptów w magazynie obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="424a2-130">As mentioned above, it is also possible to store your custom scripts in Azure Blob storage.</span></span> <span data-ttu-id="424a2-131">Dostępne są dwie opcje do przechowywania zasobów skryptu w magazynie obiektów blob; albo udostępnić skryptu lub kontenera i wykonaj takie same jak powyżej podejścia lub również mogą być przechowywane w magazynie obiektów blob prywatnej, co wymaga podania storageAccountName i storageAccountKey CustomScriptExtension definicji zasobu.</span><span class="sxs-lookup"><span data-stu-id="424a2-131">There are two options for storing the script resources in blob storage; either make the container/script public and follow the same approach as above, or it can also be kept in private blob storage which requires you to provide the storageAccountName and storageAccountKey to the CustomScriptExtension resource definition.</span></span>

<span data-ttu-id="424a2-132">W poniższym przykładzie mamy przeszły krok dalej.</span><span class="sxs-lookup"><span data-stu-id="424a2-132">In the example below we have gone a step further.</span></span> <span data-ttu-id="424a2-133">W trakcie można podać nazwę konta magazynu i klucz jako parametr lub zmienna podczas wdrażania usługi Resource Manager Szablony zapewniają `listKeys` funkcji, które można programowo uzyskać klucz konta magazynu i wstawić go do szablonu na w czasie wdrażania.</span><span class="sxs-lookup"><span data-stu-id="424a2-133">While it is possible to provide the storage account name and key as a parameter or variable during deployment, Resource Manager templates provide the `listKeys` function that can obtain the storage account key programmatically and insert it in to the template for you at deployment time.</span></span>

<span data-ttu-id="424a2-134">W przykładzie poniżej definicji zasobu CustomScriptExtension naszych niestandardowego skryptu już został przekazany do konta magazynu platformy Azure o nazwie `mystorageaccount9999` który istnieje w innej grupie zasobów o nazwie `mysa999rgname`.</span><span class="sxs-lookup"><span data-stu-id="424a2-134">In the example CustomScriptExtension resource definition below, our custom script has already been uploaded to an Azure storage account called `mystorageaccount9999` which exists in another Resource Group called `mysa999rgname`.</span></span> <span data-ttu-id="424a2-135">Firma Microsoft wdrażania szablonu zawierającego ten zasób `listKeys` funkcja uzyskuje programowo klucz konta magazynu dla konta magazynu `mystorageaccount9999` w grupie zasobów `mysa999rgname` i wstawia go do szablonu firmie Microsoft.</span><span class="sxs-lookup"><span data-stu-id="424a2-135">When we deploy a template containing this resource, the `listKeys` function programmatically obtains the storage account key for the storage account `mystorageaccount9999` in the Resource Group `mysa999rgname` and inserts it in to the template for us.</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.7",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://mystorageaccount9999.blob.core.windows.net/container/configure-music-app.ps1"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]",
      "storageAccountName": "mystorageaccount9999",
      "storageAccountKey": "[listKeys(resourceId('mysa999rgname','Microsoft.Storage/storageAccounts', mystorageaccount9999), '2015-06-15').key1]"
    }
  }
}
```

<span data-ttu-id="424a2-136">Największą zaletą tej metody jest, że nie wymaga zmiany parametry szablonu lub wdrażania w przypadku magazynu konta klucza zmianę.</span><span class="sxs-lookup"><span data-stu-id="424a2-136">The main benefit of this approach is that it does not require you to change your template or deployment parameters in the event of the storage account key changing.</span></span>

<span data-ttu-id="424a2-137">Aby uzyskać więcej informacji na temat używania niestandardowego rozszerzenia skryptu, zobacz [niestandardowego rozszerzenia skryptu z szablonami usługi Resource Manager](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="424a2-137">For more information on using the custom script extension, see [Custom script extensions with Resource Manager templates](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="next-step"></a><span data-ttu-id="424a2-138">Następny krok</span><span class="sxs-lookup"><span data-stu-id="424a2-138">Next Step</span></span>
<hr>

[<span data-ttu-id="424a2-139">Eksploruj szablonów więcej Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="424a2-139">Explore More Azure Resource Manager Templates</span></span>](https://github.com/Azure/azure-quickstart-templates)

