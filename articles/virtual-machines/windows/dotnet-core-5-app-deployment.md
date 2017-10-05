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
# <a name="application-deployment-with-azure-resource-manager-templates-for-windows-vms"></a>Wdrażanie aplikacji przy użyciu szablonów usługi Azure Resource Manager dla maszyn wirtualnych systemu Windows

Po zidentyfikowaniu wszystkie wymagania infrastrukturalne Azure i przetłumaczyć Szablon wdrożenia, wdrożenia aplikacji rzeczywistych musi należy się zająć. Wdrażanie aplikacji w tym miejscu odwołuje się do instalowania plików binarnych aplikacji rzeczywistych na zasobów platformy Azure. Dla przykładu magazynu muzyki, .net Core i IIS muszą być zainstalowana i skonfigurowana na każdej maszynie wirtualnej. Pliki binarne utworów muzycznych magazynu muszą być zainstalowane na maszynie wirtualnej, a wstępnie utworzonej bazy danych magazynu utworów muzycznych.

Ten dokument zawiera szczegóły dotyczące sposobu rozszerzenia maszyny wirtualnej można zautomatyzować wdrożenie aplikacji i konfiguracji do maszyn wirtualnych platformy Azure. Wszystkie zależności i unikatowe konfiguracje są wyróżnione. Aby uzyskać najlepsze wyniki wykonaj wstępne wdrożenie wystąpienia rozwiązania do subskrypcji platformy Azure i pracy wraz z szablonu usługi Azure Resource Manager. Zakończenie szablonu można znaleźć tutaj — [utworów muzycznych wdrożenia magazynu w systemie Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).

## <a name="configuration-script"></a>Skrypt konfiguracji
Rozszerzenia maszyn wirtualnych to specjalne programy, które wykonać przed maszynami wirtualnymi w celu zapewnienia automatyzacji konfiguracji. Rozszerzenia są dostępne dla wielu określonych celów, takich jak oprogramowanie antywirusowe, Konfiguracja rejestrowania i konfiguracji Docker. Rozszerzenie skryptu niestandardowego może służyć do wykonywania dowolny skrypt do maszyny wirtualnej. Przykład utworów muzycznych magazynu jest rozszerzenie skryptu niestandardowego do konfigurowania maszyn wirtualnych systemu Windows i instalowanie aplikacji do sklepu utworów muzycznych.

Przed opisujące, jak został zadeklarowany rozszerzenia maszyny wirtualnej w szablonie usługi Azure Resource Manager, Sprawdź skrypt, który jest uruchamiany. Ten skrypt służy do konfigurowania maszyny wirtualnej systemu Windows do obsługi aplikacji utworów muzycznych magazynu. Uruchom skrypt instaluje wszystkie wymagane oprogramowanie, instalowania aplikacji do sklepu utworów muzycznych z kontroli źródła i przygotowanie bazy danych. 

> Ten przykład jest w celach demonstracyjnych.

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

## <a name="vm-script-extension"></a>Rozszerzenie skryptu maszyny Wirtualnej
Rozszerzenia maszyny Wirtualnej mogą być uruchamiane na maszynie wirtualnej w czasie kompilacji poprzez włączenie rozszerzenia zasobu w szablonie usługi Azure Resource Manager. Rozszerzenie można dodać przy użyciu Kreatora programu Visual Studio dodawania zasobów lub przez wstawienie poprawne dane JSON do szablonu. Zasób rozszerzenie skryptu jest zagnieżdżona zasobu maszyny wirtualnej. Można to zaobserwować w poniższym przykładzie.

Wykonaj to łącze, aby zobaczyć przykładowy JSON w szablonie usługi Resource Manager — [rozszerzenia maszyny Wirtualnej skryptu](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L339). 

Zwróć uwagę, w poniżej JSON, że skrypt jest przechowywany w serwisie GitHub. Ten skrypt może być również przechowywane w magazynie obiektów Blob Azure. Ponadto szablonów usługi Azure Resource Manager Zezwalaj ciąg wykonywania skryptu do być skonstruowany w taki sposób, że wartości parametrów szablonu mogą być używane jako parametry do wykonania skryptu. W takim przypadku danych jest dostępne w przypadku wdrażania szablonów, a następnie można używać tych wartości, podczas wykonywania skryptu.

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

Jak wcześniej wspomniano, istnieje również możliwość przechowywania niestandardowych skryptów w magazynie obiektów Blob Azure. Dostępne są dwie opcje do przechowywania zasobów skryptu w magazynie obiektów blob; albo udostępnić skryptu lub kontenera i wykonaj takie same jak powyżej podejścia lub również mogą być przechowywane w magazynie obiektów blob prywatnej, co wymaga podania storageAccountName i storageAccountKey CustomScriptExtension definicji zasobu.

W poniższym przykładzie mamy przeszły krok dalej. W trakcie można podać nazwę konta magazynu i klucz jako parametr lub zmienna podczas wdrażania usługi Resource Manager Szablony zapewniają `listKeys` funkcji, które można programowo uzyskać klucz konta magazynu i wstawić go do szablonu na w czasie wdrażania.

W przykładzie poniżej definicji zasobu CustomScriptExtension naszych niestandardowego skryptu już został przekazany do konta magazynu platformy Azure o nazwie `mystorageaccount9999` który istnieje w innej grupie zasobów o nazwie `mysa999rgname`. Firma Microsoft wdrażania szablonu zawierającego ten zasób `listKeys` funkcja uzyskuje programowo klucz konta magazynu dla konta magazynu `mystorageaccount9999` w grupie zasobów `mysa999rgname` i wstawia go do szablonu firmie Microsoft.

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

Największą zaletą tej metody jest, że nie wymaga zmiany parametry szablonu lub wdrażania w przypadku magazynu konta klucza zmianę.

Aby uzyskać więcej informacji na temat używania niestandardowego rozszerzenia skryptu, zobacz [niestandardowego rozszerzenia skryptu z szablonami usługi Resource Manager](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="next-step"></a>Następny krok
<hr>

[Eksploruj szablonów więcej Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates)

