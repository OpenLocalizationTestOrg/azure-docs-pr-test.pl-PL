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
# <a name="application-deployment-with-azure-resource-manager-templates-for-windows-vms"></a>Wdrażanie aplikacji przy użyciu szablonów usługi Azure Resource Manager dla maszyn wirtualnych systemu Windows

Po zidentyfikowaniu wszystkie wymagania infrastrukturalne Azure i przetłumaczyć Szablon wdrożenia, wdrożenia rzeczywistej aplikacji hello musi toobe problemu. Wdrażanie aplikacji w tym miejscu odwołuje się binarne rzeczywistej aplikacji hello tooinstalling na zasobów platformy Azure. Dla przykładu magazynu utworów muzycznych hello, .net Core i IIS wymagają toobe zainstalowany i skonfigurowany na każdej maszynie wirtualnej. Hello utworów muzycznych magazynu plików binarnych muszą toobe zainstalowana na maszynie wirtualnej hello i hello bazy danych magazynu utworów muzycznych wstępnie utworzone.

Ten dokument zawiera szczegóły dotyczące sposobu rozszerzenia maszyny wirtualnej można zautomatyzować aplikacji wdrażania i konfigurowania tooAzure maszyn wirtualnych. Wszystkie zależności i unikatowe konfiguracje są wyróżnione. Hello najlepsze środowisko pracy wykonaj wstępne wdrożenie wystąpienie tooyour rozwiązania hello subskrypcji platformy Azure i pracy oraz hello szablonu usługi Azure Resource Manager. Szablon pełną Hello można znaleźć tutaj — [utworów muzycznych wdrożenia magazynu w systemie Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).

## <a name="configuration-script"></a>Skrypt konfiguracji
Rozszerzenia maszyn wirtualnych to specjalne programy, które wykonać automatyzacji konfiguracji tooprovide maszyn wirtualnych. Rozszerzenia są dostępne dla wielu określonych celów, takich jak oprogramowanie antywirusowe, Konfiguracja rejestrowania i konfiguracji Docker. Hello rozszerzenia niestandardowego skryptu może być używane toorun dowolny skrypt na maszynie wirtualnej. Przykład sklep muzyczny hello jest zapasowych maszyn wirtualnych systemu Windows hello tooconfigure toohello skryptu niestandardowego rozszerzenia i zainstaluj aplikację ze sklepu utworów muzycznych hello.

Przed opisujące, jak został zadeklarowany rozszerzenia maszyny wirtualnej w szablonie usługi Azure Resource Manager, sprawdź hello skrypt, który jest uruchamiany. Ten skrypt konfiguruje hello systemu Windows maszyny wirtualnej toohost hello aplikację ze sklepu utworów muzycznych. Po uruchomieniu skryptu hello instaluje wszystkie niezbędne oprogramowanie, zainstaluj aplikację ze sklepu utworów muzycznych hello z kontroli źródła i przygotowanie hello bazy danych. 

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
Rozszerzenia maszyny Wirtualnej mogą być uruchamiane na maszynie wirtualnej w czasie kompilacji przez dołączenie hello rozszerzenie zasobu do szablonu usługi Azure Resource Manager hello. rozszerzenie Hello można dodać za pomocą Kreatora programu Visual Studio dodawania zasobów hello lub wstawiając poprawne dane JSON do hello szablonu. Hello zasobów rozszerzenie skryptu jest zagnieżdżona hello zasobu maszyny wirtualnej. Można to zaobserwować w hello poniższy przykład.

Wykonaj ten przykład link toosee hello JSON w szablonie usługi Resource Manager hello — [rozszerzenia maszyny Wirtualnej skryptu](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L339). 

Wyprzedzeniem hello poniżej JSON, który hello skrypt jest przechowywany w serwisie GitHub. Ten skrypt może być również przechowywane w magazynie obiektów Blob Azure. Ponadto szablonów usługi Azure Resource Manager Zezwalaj hello skryptu wykonywania ciąg toobe skonstruowany w taki sposób, że wartości parametrów szablonu mogą być używane jako parametry do wykonania skryptu. W takim przypadku danych jest dostępne w przypadku wdrażania hello szablony, a następnie można używać tych wartości, podczas wykonywania skryptu hello.

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

Jak wspomniano powyżej, jest również możliwe toostore niestandardowe skrypty w magazynie obiektów Blob Azure. Dostępne są dwie opcje do przechowywania zasobów skryptu hello w magazynie obiektów blob; Witaj publicznego kontenera skryptu i wykonaj hello podejścia takie same jak powyżej albo również mogą być przechowywane w magazynie obiektów blob prywatnej, co wymaga tooprovide hello storageAccountName i storageAccountKey toohello CustomScriptExtension definicji zasobu.

W poniższym przykładzie hello możemy przeszły krok dalej. Mimo że jest nazwa konta magazynu hello możliwe tooprovide i klucz jako parametr lub zmienna podczas wdrażania, szablony Menedżera zasobów zapewniają hello `listKeys` funkcji, które można uzyskać konta magazynu hello klucza programowego i wstaw go w toohello Szablon można w czasie wdrażania.

W przykładzie hello CustomScriptExtension definicji zasobu poniżej, naszych niestandardowego skryptu został już przekazany tooan o nazwie konto magazynu Azure `mystorageaccount9999` który istnieje w innej grupie zasobów o nazwie `mysa999rgname`. Firma Microsoft wdrażania szablonu zawierającego ten zasób, hello `listKeys` funkcja uzyskuje programowo hello klucz konta magazynu dla konta magazynu hello `mystorageaccount9999` w hello grupy zasobów `mysa999rgname` i wstawia go w szablonie toohello firmie Microsoft.

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

Witaj Największą zaletą tej metody nie nie wymaga możesz toochange szablonu lub parametry wdrażania w przypadku hello hello zmianę kluczy konta magazynu.

Aby uzyskać więcej informacji na temat używania hello niestandardowe rozszerzenie skryptu, zobacz [niestandardowego rozszerzenia skryptu z szablonami usługi Resource Manager](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="next-step"></a>Następny krok
<hr>

[Eksploruj szablonów więcej Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates)

