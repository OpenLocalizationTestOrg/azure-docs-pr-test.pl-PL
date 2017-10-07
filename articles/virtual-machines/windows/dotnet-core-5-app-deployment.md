---
title: "aaaAutomating wdrażaniem aplikacji za pomocą rozszerzenia maszyny wirtualnej | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 6d52537fbd4e935f19d3864def11484f519f8598
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="application-deployment-with-azure-resource-manager-templates-for-windows-vms"></a><span data-ttu-id="06624-103">Wdrażanie aplikacji przy użyciu szablonów usługi Azure Resource Manager dla maszyn wirtualnych systemu Windows</span><span class="sxs-lookup"><span data-stu-id="06624-103">Application deployment with Azure Resource Manager templates for Windows VMs</span></span>

<span data-ttu-id="06624-104">Po zidentyfikowaniu wszystkie wymagania infrastrukturalne Azure i przetłumaczyć Szablon wdrożenia, wdrożenia rzeczywistej aplikacji hello musi toobe problemu.</span><span class="sxs-lookup"><span data-stu-id="06624-104">Once all Azure infrastructural requirements have been identified and translated into a deployment template, hello actual application deployment needs toobe addressed.</span></span> <span data-ttu-id="06624-105">Wdrażanie aplikacji w tym miejscu odwołuje się binarne rzeczywistej aplikacji hello tooinstalling na zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="06624-105">Application deployment here is referring tooinstalling hello actual application binaries onto Azure resources.</span></span> <span data-ttu-id="06624-106">Dla przykładu magazynu utworów muzycznych hello, .net Core i IIS wymagają toobe zainstalowany i skonfigurowany na każdej maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="06624-106">For hello Music Store sample, .Net Core and IIS need toobe installed and configured on each virtual machine.</span></span> <span data-ttu-id="06624-107">Hello utworów muzycznych magazynu plików binarnych muszą toobe zainstalowana na maszynie wirtualnej hello i hello bazy danych magazynu utworów muzycznych wstępnie utworzone.</span><span class="sxs-lookup"><span data-stu-id="06624-107">hello Music Store binaries need toobe installed onto hello virtual machine, and hello Music Store database pre-created.</span></span>

<span data-ttu-id="06624-108">Ten dokument zawiera szczegóły dotyczące sposobu rozszerzenia maszyny wirtualnej można zautomatyzować aplikacji wdrażania i konfigurowania tooAzure maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="06624-108">This document details how Virtual Machine extensions can automate application deployment and configuration tooAzure virtual machines.</span></span> <span data-ttu-id="06624-109">Wszystkie zależności i unikatowe konfiguracje są wyróżnione.</span><span class="sxs-lookup"><span data-stu-id="06624-109">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="06624-110">Hello najlepsze środowisko pracy wykonaj wstępne wdrożenie wystąpienie tooyour rozwiązania hello subskrypcji platformy Azure i pracy oraz hello szablonu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="06624-110">For hello best experience, pre-deploy an instance of hello solution tooyour Azure subscription and work along with hello Azure Resource Manager template.</span></span> <span data-ttu-id="06624-111">Szablon pełną Hello można znaleźć tutaj — [utworów muzycznych wdrożenia magazynu w systemie Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="06624-111">hello complete template can be found here – [Music Store Deployment on Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="configuration-script"></a><span data-ttu-id="06624-112">Skrypt konfiguracji</span><span class="sxs-lookup"><span data-stu-id="06624-112">Configuration script</span></span>
<span data-ttu-id="06624-113">Rozszerzenia maszyn wirtualnych to specjalne programy, które wykonać automatyzacji konfiguracji tooprovide maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="06624-113">Virtual Machine extensions are specialized programs that execute against virtual machines tooprovide configuration automation.</span></span> <span data-ttu-id="06624-114">Rozszerzenia są dostępne dla wielu określonych celów, takich jak oprogramowanie antywirusowe, Konfiguracja rejestrowania i konfiguracji Docker.</span><span class="sxs-lookup"><span data-stu-id="06624-114">Extensions are available for many specific purposes such as anti-virus, logging configuration, and Docker configuration.</span></span> <span data-ttu-id="06624-115">Hello rozszerzenia niestandardowego skryptu może być używane toorun dowolny skrypt na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="06624-115">hello Custom Script extension can be used toorun any script against a virtual machine.</span></span> <span data-ttu-id="06624-116">Przykład sklep muzyczny hello jest zapasowych maszyn wirtualnych systemu Windows hello tooconfigure toohello skryptu niestandardowego rozszerzenia i zainstaluj aplikację ze sklepu utworów muzycznych hello.</span><span class="sxs-lookup"><span data-stu-id="06624-116">With hello Music Store sample, it is up toohello custom script extension tooconfigure hello Windows virtual machines and install hello Music Store application.</span></span>

<span data-ttu-id="06624-117">Przed opisujące, jak został zadeklarowany rozszerzenia maszyny wirtualnej w szablonie usługi Azure Resource Manager, sprawdź hello skrypt, który jest uruchamiany.</span><span class="sxs-lookup"><span data-stu-id="06624-117">Before detailing how virtual machine extensions are declared in an Azure Resource Manager template, examine hello script that is run.</span></span> <span data-ttu-id="06624-118">Ten skrypt konfiguruje hello systemu Windows maszyny wirtualnej toohost hello aplikację ze sklepu utworów muzycznych.</span><span class="sxs-lookup"><span data-stu-id="06624-118">This script configures hello Windows virtual machine toohost hello Music Store application.</span></span> <span data-ttu-id="06624-119">Po uruchomieniu skryptu hello instaluje wszystkie niezbędne oprogramowanie, zainstaluj aplikację ze sklepu utworów muzycznych hello z kontroli źródła i przygotowanie hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="06624-119">When run, hello script installs all needed software, install hello Music store application from source control, and prepare hello database.</span></span> 

> <span data-ttu-id="06624-120">Ten przykład jest w celach demonstracyjnych.</span><span class="sxs-lookup"><span data-stu-id="06624-120">This sample is for demonstration purposes.</span></span>

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

## <a name="vm-script-extension"></a><span data-ttu-id="06624-121">Rozszerzenie skryptu maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="06624-121">VM Script Extension</span></span>
<span data-ttu-id="06624-122">Rozszerzenia maszyny Wirtualnej mogą być uruchamiane na maszynie wirtualnej w czasie kompilacji przez dołączenie hello rozszerzenie zasobu do szablonu usługi Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="06624-122">VM Extensions can be run against a virtual machine at build time by including hello extension resource in hello Azure Resource Manager template.</span></span> <span data-ttu-id="06624-123">rozszerzenie Hello można dodać za pomocą Kreatora programu Visual Studio dodawania zasobów hello lub wstawiając poprawne dane JSON do hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="06624-123">hello extension can be added with hello Visual Studio Add Resource wizard, or by inserting valid JSON into hello template.</span></span> <span data-ttu-id="06624-124">Hello zasobów rozszerzenie skryptu jest zagnieżdżona hello zasobu maszyny wirtualnej. Można to zaobserwować w hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="06624-124">hello Script Extension resource is nested inside hello Virtual Machine resource; this can be seen in hello following example.</span></span>

<span data-ttu-id="06624-125">Wykonaj ten przykład link toosee hello JSON w szablonie usługi Resource Manager hello — [rozszerzenia maszyny Wirtualnej skryptu](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L339).</span><span class="sxs-lookup"><span data-stu-id="06624-125">Follow this link toosee hello JSON sample within hello Resource Manager template – [VM Script Extension](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L339).</span></span> 

<span data-ttu-id="06624-126">Wyprzedzeniem hello poniżej JSON, który hello skrypt jest przechowywany w serwisie GitHub.</span><span class="sxs-lookup"><span data-stu-id="06624-126">Notice in hello below JSON that hello script is stored in GitHub.</span></span> <span data-ttu-id="06624-127">Ten skrypt może być również przechowywane w magazynie obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="06624-127">This script could also be stored in Azure Blob storage.</span></span> <span data-ttu-id="06624-128">Ponadto szablonów usługi Azure Resource Manager Zezwalaj hello skryptu wykonywania ciąg toobe skonstruowany w taki sposób, że wartości parametrów szablonu mogą być używane jako parametry do wykonania skryptu.</span><span class="sxs-lookup"><span data-stu-id="06624-128">Also, Azure Resource Manager templates allow hello script execution string toobe constructed such that template parameters values can be used as parameters for script execution.</span></span> <span data-ttu-id="06624-129">W takim przypadku danych jest dostępne w przypadku wdrażania hello szablony, a następnie można używać tych wartości, podczas wykonywania skryptu hello.</span><span class="sxs-lookup"><span data-stu-id="06624-129">In this case data is provided when deploying hello templates, and these values can then be used when executing hello script.</span></span>

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

<span data-ttu-id="06624-130">Jak wspomniano powyżej, jest również możliwe toostore niestandardowe skrypty w magazynie obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="06624-130">As mentioned above, it is also possible toostore your custom scripts in Azure Blob storage.</span></span> <span data-ttu-id="06624-131">Dostępne są dwie opcje do przechowywania zasobów skryptu hello w magazynie obiektów blob; Witaj publicznego kontenera skryptu i wykonaj hello podejścia takie same jak powyżej albo również mogą być przechowywane w magazynie obiektów blob prywatnej, co wymaga tooprovide hello storageAccountName i storageAccountKey toohello CustomScriptExtension definicji zasobu.</span><span class="sxs-lookup"><span data-stu-id="06624-131">There are two options for storing hello script resources in blob storage; either make hello container/script public and follow hello same approach as above, or it can also be kept in private blob storage which requires you tooprovide hello storageAccountName and storageAccountKey toohello CustomScriptExtension resource definition.</span></span>

<span data-ttu-id="06624-132">W poniższym przykładzie hello możemy przeszły krok dalej.</span><span class="sxs-lookup"><span data-stu-id="06624-132">In hello example below we have gone a step further.</span></span> <span data-ttu-id="06624-133">Mimo że jest nazwa konta magazynu hello możliwe tooprovide i klucz jako parametr lub zmienna podczas wdrażania, szablony Menedżera zasobów zapewniają hello `listKeys` funkcji, które można uzyskać konta magazynu hello klucza programowego i wstaw go w toohello Szablon można w czasie wdrażania.</span><span class="sxs-lookup"><span data-stu-id="06624-133">While it is possible tooprovide hello storage account name and key as a parameter or variable during deployment, Resource Manager templates provide hello `listKeys` function that can obtain hello storage account key programmatically and insert it in toohello template for you at deployment time.</span></span>

<span data-ttu-id="06624-134">W przykładzie hello CustomScriptExtension definicji zasobu poniżej, naszych niestandardowego skryptu został już przekazany tooan o nazwie konto magazynu Azure `mystorageaccount9999` który istnieje w innej grupie zasobów o nazwie `mysa999rgname`.</span><span class="sxs-lookup"><span data-stu-id="06624-134">In hello example CustomScriptExtension resource definition below, our custom script has already been uploaded tooan Azure storage account called `mystorageaccount9999` which exists in another Resource Group called `mysa999rgname`.</span></span> <span data-ttu-id="06624-135">Firma Microsoft wdrażania szablonu zawierającego ten zasób, hello `listKeys` funkcja uzyskuje programowo hello klucz konta magazynu dla konta magazynu hello `mystorageaccount9999` w hello grupy zasobów `mysa999rgname` i wstawia go w szablonie toohello firmie Microsoft.</span><span class="sxs-lookup"><span data-stu-id="06624-135">When we deploy a template containing this resource, hello `listKeys` function programmatically obtains hello storage account key for hello storage account `mystorageaccount9999` in hello Resource Group `mysa999rgname` and inserts it in toohello template for us.</span></span>

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

<span data-ttu-id="06624-136">Witaj Największą zaletą tej metody nie nie wymaga możesz toochange szablonu lub parametry wdrażania w przypadku hello hello zmianę kluczy konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="06624-136">hello main benefit of this approach is that it does not require you toochange your template or deployment parameters in hello event of hello storage account key changing.</span></span>

<span data-ttu-id="06624-137">Aby uzyskać więcej informacji na temat używania hello niestandardowe rozszerzenie skryptu, zobacz [niestandardowego rozszerzenia skryptu z szablonami usługi Resource Manager](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="06624-137">For more information on using hello custom script extension, see [Custom script extensions with Resource Manager templates](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="next-step"></a><span data-ttu-id="06624-138">Następny krok</span><span class="sxs-lookup"><span data-stu-id="06624-138">Next Step</span></span>
<hr>

[<span data-ttu-id="06624-139">Eksploruj szablonów więcej Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="06624-139">Explore More Azure Resource Manager Templates</span></span>](https://github.com/Azure/azure-quickstart-templates)

