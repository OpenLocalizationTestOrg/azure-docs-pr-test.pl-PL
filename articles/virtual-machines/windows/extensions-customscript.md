---
title: aaaAzure niestandardowe rozszerzenie skryptu systemu Windows | Dokumentacja firmy Microsoft
description: "Automatyzowanie zadań konfiguracji maszyny Wirtualnej systemu Windows przy użyciu rozszerzenia niestandardowego skryptu hello"
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f4181fee-7a9d-4a1c-b517-52956f5b7fa1
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/16/2017
ms.author: nepeters
ms.openlocfilehash: 97e065242e9fed116ee20b074f4e302a0cd10585
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="custom-script-extension-for-windows"></a>Niestandardowe rozszerzenie skryptu dla systemu Windows

Witaj niestandardowe rozszerzenie skryptu pobiera i uruchamia skrypty na maszynach wirtualnych Azure. To rozszerzenie jest przydatne w przypadku konfiguracji wdrożenia post, instalacja oprogramowania lub dowolnej innej konfiguracji / zadanie zarządzania. Skryptów można pobrać z magazynu Azure lub usługi GitHub lub podane toohello portalu Azure w rozszerzeniu czas wykonywania. Hello rozszerzenia niestandardowego skryptu integruje się z szablonów usługi Azure Resource Manager i można również uruchomić przy użyciu hello wiersza polecenia platformy Azure, programu PowerShell, portalu Azure lub hello interfejsu API REST maszyny wirtualnej Azure.

Ten dokument zawiera szczegóły, jak za pomocą niestandardowego rozszerzenia skryptu hello toouse hello modułu Azure PowerShell, szablony usługi Azure Resource Manager i szczegóły dotyczące rozwiązywania problemów z systemów Windows.

## <a name="prerequisites"></a>Wymagania wstępne

### <a name="operating-system"></a>System operacyjny

Witaj niestandardowe rozszerzenie skryptu dla systemu Windows mogą być uruchamiane na systemie Windows Server 2008 R2, 2012 i 2012 R2, 2016 wersje.

### <a name="script-location"></a>Lokalizacja skryptu

skrypt Hello musi toobe przechowywane w magazynie obiektów Blob Azure lub w innej lokalizacji dostępny za pośrednictwem prawidłowy adres URL.

### <a name="internet-connectivity"></a>Połączenie z Internetem

Hello niestandardowe rozszerzenie skryptu systemu Windows wymaga tego hello docelowej maszyny wirtualnej jest toohello połączenia internetowego. 

## <a name="extension-schema"></a>Rozszerzenie schematu

Witaj JSON następujące zawiera schemat hello hello niestandardowe rozszerzenie skryptu. rozszerzenie Hello wymaga lokalizacji skryptu (magazynu Azure lub innej lokalizacji z prawidłowym adresem URL) i tooexecute polecenia. Jeśli jako źródło skryptu hello przy użyciu usługi Azure Storage, usługa Azure storage konta nazwy i klucza konta jest wymagany. Te elementy powinny traktowane jako poufne dane i określony w konfiguracji chronionych ustawień rozszerzenia hello. Danych ustawieniem rozszerzenia chronione maszyny Wirtualnej Azure jest szyfrowany i odszyfrowane tylko na powitania docelowej maszyny wirtualnej.

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
        "typeHandlerVersion": "1.9",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "fileUris": [
                "script location"
            ]
        },
        "protectedSettings": {
            "commandToExecute": "myExecutionCommand",
            "storageAccountName": "myStorageAccountName",
            "storageAccountKey": "myStorageAccountKey"
        }
    }
}
```

### <a name="property-values"></a>Wartości właściwości

| Nazwa | Wartość / przykład |
| ---- | ---- |
| apiVersion | 2015-06-15 |
| Wydawcy | Microsoft.Compute |
| type | Rozszerzenia |
| typeHandlerVersion | 1.9 |
| fileUris (np.) | https://RAW.githubusercontent.com/Microsoft/DotNet-Core-Sample-Templates/Master/DotNet-Core-Music-Windows/scripts/Configure-Music-App.ps1 |
| commandToExecute (np.) | PowerShell - ExecutionPolicy Unrestricted - pliku skonfigurować muzyka app.ps1 |
| storageAccountName (np.) | examplestorageacct |
| storageAccountKey (np.) | TmJK/1N3AbAZ3q / + hOXoi/l73zOqsaxXDhqa9Y83/v5UpXQp2DQIBuv2Tifp60cE/OaHsJZmQZ7teQfczQj8hg == |

**Uwaga** — te nazwy właściwości jest uwzględniana wielkość liter. Użyj nazwy hello, jak pokazano powyżej problemy z wdrażaniem tooavoid.

## <a name="template-deployment"></a>Wdrażanie na podstawie szablonu

Rozszerzenia maszyny Wirtualnej platformy Azure można wdrożyć przy użyciu szablonów usługi Azure Resource Manager. można schematu JSON Hello szczegółowo opisane w poprzedniej sekcji hello w hello toorun szablonu usługi Azure Resource Manager niestandardowe rozszerzenie skryptu podczas wdrażania szablonu usługi Azure Resource Manager. Przykładowy szablon, który obejmuje hello niestandardowe rozszerzenie skryptu można znaleźć tutaj, [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).

## <a name="powershell-deployment"></a>Wdrożenie programu PowerShell

Witaj `Set-AzureRmVMCustomScriptExtension` polecenie może być używane tooadd hello niestandardowego skryptu rozszerzenia tooan istniejącej maszyny wirtualnej. Aby uzyskać więcej informacji, zobacz [AzureRmVMCustomScriptExtension zestawu ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).
```powershell
Set-AzureRmVMCustomScriptExtension -ResourceGroupName myResourceGroup `
    -VMName myVM `
    -Location myLocation `
    -FileUri myURL `
    -Run 'myScript.ps1' `
    -Name DemoScriptExtension
```

## <a name="troubleshoot-and-support"></a>Rozwiązywanie problemów i obsługa techniczna

### <a name="troubleshoot"></a>Rozwiązywanie problemów

Z hello portalu Azure i przy użyciu modułu Azure PowerShell hello można pobrać danych o stanie hello wdrożeń rozszerzenia. Stan wdrożenia hello toosee rozszerzeń dla danej maszyny Wirtualnej, uruchom następujące polecenie hello.

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

Wykonanie rozszerzenia danych wyjściowych jest rejestrowane toofiles omówionych w artykule hello następującego katalogu na powitania docelowej maszyny wirtualnej.
```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Compute.CustomScriptExtension
```

Witaj określony na powitania po katalog na docelowej maszynie wirtualnej hello są pobierane pliki.
```cmd
C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.*\Downloads\<n>
```
gdzie `<n>` jest dziesiętną liczbą całkowitą, która może zmienić pomiędzy wykonaniami hello rozszerzenia.  Witaj `1.*` wartość odpowiada bieżącej rzeczywiste hello `typeHandlerVersion` wartość hello rozszerzenia.  Na przykład może być katalogowych hello `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2`.  

Podczas wykonywania hello `commandToExecute` polecenia rozszerzenia hello spowoduje ustawienie tego katalogu (np. `...\Downloads\2`) jako bieżący katalog roboczy hello. Umożliwia zastosowanie hello ścieżek względnych toolocate hello pliki pobrane za pośrednictwem hello `fileURIs` właściwości. Zobacz poniższą tabelę hello do przykłady.

Ponieważ ścieżka bezwzględna pobierania hello mogą się zmieniać wraz z upływem czasu jest lepsze tooopt ścieżek względnych skryptów i plików w hello `commandToExecute` string, jeśli to możliwe. Na przykład:
```json
    "commandToExecute": "powershell.exe . . . -File './scripts/myscript.ps1'"
```

Informacje o ścieżce po hello pierwszy segment identyfikatora URI są przechowywane pliki pobrane za pośrednictwem hello `fileUris` listy właściwości.  Jak pokazano w poniższej tabeli hello, pobierane pliki są mapowane do pobierania podkatalogów tooreflect hello struktury hello `fileUris` wartości.  

#### <a name="examples-of-downloaded-files"></a>Przykłady pobrane pliki

| Identyfikator URI w fileUris | Względne położenie pobrany | Bezwzględna pobrać lokalizację * |
| ---- | ------- |:--- |
| `https://someAcct.blob.core.windows.net/aContainer/scripts/myscript.ps1` | `./scripts/myscript.ps1` |`C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2\scripts\myscript.ps1`  |
| `https://someAcct.blob.core.windows.net/aContainer/topLevel.ps1` | `./topLevel.ps1` | `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2\topLevel.ps1` |

\*Jako powyżej, hello bezwzględne ścieżki katalogów zmieni hello okresu istnienia, hello maszyny Wirtualnej, ale nie w ramach pojedynczego uruchomienia rozszerzenia CustomScript hello.

### <a name="support"></a>Pomoc techniczna

Jeśli potrzebujesz więcej pomocy w dowolnym momencie, w tym artykule, możesz skontaktować się hello Azure ekspertów hello [fora MSDN Azure i przepełnienie stosu] (https://azure.microsoft.com/en-us/support/forums/). Alternatywnie można pliku zdarzenia pomocy technicznej platformy Azure. Przejdź toohello [witrynę pomocy technicznej platformy Azure](https://azure.microsoft.com/en-us/support/options/) i wybierz Uzyskaj pomoc techniczną. Informacje o korzystaniu z platformy Azure obsługuje, przeczytaj hello [pomocy technicznej Microsoft Azure — często zadawane pytania](https://azure.microsoft.com/en-us/support/faq/).
