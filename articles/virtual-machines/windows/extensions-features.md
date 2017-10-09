---
title: "aaaVirtual komputera rozszerzeń i funkcji systemu Windows na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jakie rozszerzenia są dostępne dla maszyn wirtualnych platformy Azure, pogrupowane według co ich Podaj puli zasobów i zwiększyć."
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 999d63ee-890e-432e-9391-25b3fc6cde28
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/06/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 61ccfd696b38e9be1026d836d5796c2346fd650f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-machine-extensions-and-features-for-windows"></a>Rozszerzenia maszyn wirtualnych i funkcje systemu Windows

Rozszerzenia maszyny wirtualnej platformy Azure są małe aplikacji, które mają po wdrożeniu i automatyzację zadań na maszynach wirtualnych Azure. Na przykład, jeśli maszyna wirtualna wymaga instalacji oprogramowania, ochrony oprogramowania antywirusowego lub Docker konfiguracji, rozszerzenia maszyny Wirtualnej mogą być używane toocomplete tych zadań. Azure rozszerzeń maszyny Wirtualnej może być uruchamiany przy użyciu hello wiersza polecenia platformy Azure, programu PowerShell, szablony usługi Azure Resource Manager i hello portalu Azure. Rozszerzenia mogą powiązany z nowego wdrożenia maszyny wirtualnej lub uruchomienia dowolnego istniejącego systemu.

Ten dokument zawiera omówienie rozszerzeń maszyny wirtualnej, wymagań wstępnych dotyczących używania rozszerzenia maszyny wirtualnej i wskazówki na sposób toodetect, zarządzania i usunąć rozszerzenia maszyny wirtualnej. Ten dokument zawiera informacje uogólniony wielu rozszerzeń maszyny Wirtualnej nie są dostępne, każde z nich potencjalnie unikatowych konfiguracji. Rozszerzenie szczegółowe znajdują się w poszczególnych rozszerzeń poszczególnych toohello określonego dokumentu.

## <a name="use-cases-and-samples"></a>Przypadki użycia i przykłady

Istnieje wiele różnych rozszerzeń maszyny Wirtualnej platformy Azure, każde z nich określony przypadek użycia. Niektóre przykładowe przypadki użycia są:

- Stosowanie programu PowerShell żądany stan konfiguracji tooa maszyny wirtualnej za pomocą rozszerzenia hello DSC dla systemu Windows. Aby uzyskać więcej informacji, zobacz [Azure żądany stan konfiguracji rozszerzenia](extensions-dsc-overview.md).
- Skonfiguruj monitorowanie za pomocą rozszerzenia maszyny Wirtualnej agenta monitorowania firmy Microsoft hello maszyny wirtualnej. Aby uzyskać więcej informacji, zobacz [tooLog maszyny wirtualne Azure połączyć Analytics](../../log-analytics/log-analytics-azure-vm-extension.md).
- Skonfiguruj Monitorowanie infrastruktury platformy Azure z hello Datadog rozszerzenia. Aby uzyskać więcej informacji, zobacz hello [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).
- Skonfiguruj maszynę wirtualną platformy Azure przy użyciu Chef. Aby uzyskać więcej informacji, zobacz [automatyzacji Azure wdrożenia maszyny wirtualnej z Chef](chef-automation.md).

Ponadto rozszerzenia tooprocess rozszerzenia niestandardowego skryptu dostępnej dla maszyn wirtualnych w systemach Windows i Linux. Witaj rozszerzenia niestandardowego skryptu dla systemu Windows umożliwia żadnych toobe skrypt programu PowerShell uruchomić na maszynie wirtualnej. Jest to przydatne podczas projektowania wdrożeń platformy Azure, które wymagają konfiguracji oprócz zapewniają jakie natywnego narzędzia Azure. Aby uzyskać więcej informacji, zobacz [rozszerzenie skryptu niestandardowego maszyny Wirtualnej systemu Windows](extensions-customscript.md).


## <a name="prerequisites"></a>Wymagania wstępne

Każde rozszerzenie maszyny wirtualnej może mieć własny zestaw wymagań wstępnych. Na przykład hello rozszerzenia maszyny Wirtualnej platformy Docker ma wymagań wstępnych obsługiwanych dystrybucji systemu Linux. Wymagania dotyczące poszczególnych rozszerzeń są szczegółowo opisane w dokumentacji konkretnego rozszerzenia hello.

### <a name="azure-vm-agent"></a>Agent maszyny wirtualnej platformy Azure
agent maszyny Wirtualnej Azure Hello zarządza interakcji między maszyny wirtualnej platformy Azure i hello kontrolera sieci szkieletowej Azure. agent maszyny Wirtualnej Hello jest odpowiedzialny za dużo aspekty funkcjonalne, wdrażania i zarządzania maszynami wirtualnymi platformy Azure, łącznie z rozszerzeniami maszyny Wirtualnej. agent maszyny Wirtualnej Azure Hello jest preinstalowany na portalu Azure Marketplace obrazów i można zainstalować w obsługiwanych systemach operacyjnych.

Aby uzyskać informacje dotyczące obsługiwanych systemów operacyjnych i instrukcje dotyczące instalacji, zobacz [agenta maszyny wirtualnej platformy Azure](agent-user-guide.md).

## <a name="discover-vm-extensions"></a>Odnajdywanie rozszerzeń maszyny Wirtualnej
Wiele różnych rozszerzeń maszyny Wirtualnej są dostępne do użycia z maszyn wirtualnych platformy Azure. toosee pełną listę, uruchom następujące polecenie z modułu programu PowerShell usługi Azure Resource Manager hello hello. Upewnij się, że lokalizacja hello potrzeby toospecify po uruchomieniu tego polecenia.

```powershell
Get-AzureRmVmImagePublisher -Location WestUS | `
Get-AzureRmVMExtensionImageType | `
Get-AzureRmVMExtensionImage | Select Type, Version
```

## <a name="run-vm-extensions"></a>Uruchom rozszerzeń maszyny Wirtualnej

Rozszerzenia maszyny wirtualnej platformy Azure może działać w istniejących maszyn wirtualnych, które jest przydatne, gdy potrzebne zmiany w konfiguracji toomake lub Przywróć łączność w przypadku wdrożonej maszyny Wirtualnej. Rozszerzenia maszyny Wirtualnej dołączany także wdrażanie szablonów usługi Azure Resource Manager. Za pomocą rozszerzeń z szablonami usługi Resource Manager, można włączyć toobe maszyn wirtualnych platformy Azure, wdrożyć i skonfigurować bez potrzeby interwencji po wdrożeniu hello.

Hello następujące metody mogą być używane toorun rozszerzenie dla istniejącej maszyny wirtualnej.

### <a name="powershell"></a>PowerShell

Istnieje kilka poleceń programu PowerShell do uruchamiania poszczególnych rozszerzeń. toosee listy, uruchom następujące polecenia programu PowerShell hello.

```powershell
get-command Set-AzureRM*Extension* -Module AzureRM.Compute
```

Zapewnia to dane wyjściowe podobne toohello poniżej:

```powershell
CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Set-AzureRmVMAccessExtension                       2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMADDomainExtension                     2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMAEMExtension                          2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMBackupExtension                       2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMBginfoExtension                       2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMChefExtension                         2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMCustomScriptExtension                 2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMDiagnosticsExtension                  2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMDiskEncryptionExtension               2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMDscExtension                          2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMExtension                             2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMSqlServerExtension                    2.2.0      AzureRM.Compute
```

Witaj poniższy przykład używa toodownload rozszerzenia niestandardowego skryptu hello skryptu z repozytorium GitHub na powitania docelowej maszyny wirtualnej, a następnie uruchom skrypt hello. Aby uzyskać więcej informacji na powitania rozszerzenia niestandardowego skryptu, zobacz [Omówienie rozszerzenia niestandardowego skryptu](extensions-customscript.md).

```powershell
Set-AzureRmVMCustomScriptExtension -ResourceGroupName "myResourceGroup" `
    -VMName "myVM" -Name "myCustomScript" `
    -FileUri "https://raw.githubusercontent.com/neilpeterson/nepeters-azure-templates/master/windows-custom-script-simple/support-scripts/Create-File.ps1" `
    -Run "Create-File.ps1" -Location "West US"
```

W tym przykładzie hello rozszerzenia dostępu do maszyny Wirtualnej jest używane tooreset hello hasło administratora maszyny wirtualnej systemu Windows. Aby uzyskać więcej informacji na powitania rozszerzenia dostępu do maszyny Wirtualnej, zobacz [usługi pulpitu zdalnego resetowania na maszynie wirtualnej Windows](reset-rdp.md).

```powershell
$cred=Get-Credential

Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" -VMName "myVM" -Name "myVMAccess" `
    -Location WestUS -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password -typeHandlerVersion "2.0"
```

Witaj `Set-AzureRmVMExtension` polecenie może być używane toostart wszystkie rozszerzenia maszyny Wirtualnej. Aby uzyskać więcej informacji, zobacz hello [odwołania zestawu AzureRmVMExtension](https://msdn.microsoft.com/en-us/library/mt603745.aspx).


### <a name="azure-portal"></a>Azure Portal

Rozszerzenia maszyny Wirtualnej może być zastosowane tooan istniejącej maszyny wirtualnej za pośrednictwem hello portalu Azure. toodo tak, wybierz maszynę wirtualną hello mają toouse, wybierz **rozszerzenia**i kliknij przycisk **Dodaj**. Zapewnia to listę dostępnych rozszerzeń. Wybierz hello mają i wykonaj kroki powitania w Kreatorze hello.

Witaj poniższy obraz przedstawia hello instalacji hello rozszerzenia Microsoft Antimalware hello portalu Azure.

![Zainstaluj rozszerzenie ochrony przed złośliwym oprogramowaniem](./media/extensions-features/installantimalwareextension.png)

### <a name="azure-resource-manager-templates"></a>Szablony usługi Azure Resource Manager

Rozszerzeń maszyny Wirtualnej może być dodany tooan szablonu usługi Azure Resource Manager i wykonany przy użyciu wdrożenia hello hello szablonu. Wdrażanie rozszerzeń przy użyciu szablonu jest przydatne w przypadku tworzenia wdrożeń platformy Azure w pełni skonfigurowany. Na przykład powitalne następujące JSON jest pobierana z szablonem usługi Resource Manager, który wdraża zestaw maszyn wirtualnych z równoważeniem obciążenia i bazy danych Azure SQL, a następnie instaluje aplikację .NET Core na każdej maszynie Wirtualnej. Instalacja oprogramowania hello odpowiada on za Hello rozszerzenia maszyny Wirtualnej.

Aby uzyskać więcej informacji, zobacz hello [pełne szablonu usługi Resource Manager](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).

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

Aby uzyskać więcej informacji, zobacz [szablony Authoring Azure Resource Manager z rozszerzeniami maszyny Wirtualnej systemu Windows](template-description.md#extensions).

## <a name="secure-vm-extension-data"></a>Zabezpieczanie danych rozszerzenia maszyny Wirtualnej

Jeśli korzystasz z rozszerzenia maszyny Wirtualnej, może być konieczne tooinclude poufne informacje, takie jak poświadczeń, nazwy konta magazynu i klucze dostępu do konta magazynu. Wiele rozszerzeń maszyny Wirtualnej obejmują konfiguracji chronionych danych i tylko odszyfrowującego wewnątrz hello docelowej maszyny wirtualnej. Każde rozszerzenie ma używającym w dokumentacji konkretnego rozszerzenia schematu określonej konfiguracji chronionych.

Witaj poniższy przykład przedstawia wystąpienie hello rozszerzenia niestandardowego skryptu dla systemu Windows. Należy zauważyć, że tego tooexecute polecenia hello zawiera zestaw poświadczeń. W tym przykładzie hello tooexecute polecenia nie będą szyfrowane.


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
        ],
        "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
    }
}
```

Bezpieczny ciąg wykonywania hello przenosząc hello **tooexecute polecenia** toohello właściwości **chronione** konfiguracji.

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

## <a name="troubleshoot-vm-extensions"></a>Rozwiązywanie problemów z rozszerzeń maszyny Wirtualnej

Każde rozszerzenie maszyny Wirtualnej może być określone kroki rozwiązywania problemów. Na przykład podczas korzystania z rozszerzenia niestandardowego skryptu hello, skryptu wykonywania szczegóły można znaleźć lokalnie na maszynie wirtualnej hello, na którym uruchomiono hello rozszerzenia. Wszystkie kroki rozwiązywania problemów specyficzne dla rozszerzenia są szczegółowo opisane w dokumentacji specyficzne dla rozszerzenia.

następujące kroki rozwiązywania problemów Hello mają zastosowanie tooall rozszerzenia maszyny wirtualnej.

### <a name="view-extension-status"></a>Wyświetl stan rozszerzenia

Po uruchomieniu rozszerzenie maszyny wirtualnej na maszynie wirtualnej, użyj powitania po stan rozszerzenia tooreturn polecenia programu PowerShell. Zastąp przykładowe nazwy parametrów własne wartości. Witaj `Name` Parametr przyjmuje nazwę hello danego rozszerzenia toohello w czasie wykonywania.

```PowerShell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

dane wyjściowe Hello wygląda hello:

```json
ResourceGroupName       : myResourceGroup
VMName                  : myVM
Name                    : myExtensionName
Location                : westus
Etag                    : null
Publisher               : Microsoft.Azure.Extensions
ExtensionType           : DockerExtension
TypeHandlerVersion      : 1.0
Id                      : /subscriptions/mySubscriptionIS/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM/extensions/myExtensionName
PublicSettings          :
ProtectedSettings       :
ProvisioningState       : Succeeded
Statuses                :
SubStatuses             :
AutoUpgradeMinorVersion : False
ForceUpdateTag          :
```

Stan wykonania rozszerzenia można znaleźć w portalu Azure hello. Wybierz stan hello tooview rozszerzenia maszyny wirtualnej wybierz hello, **rozszerzenia**, i wybierz hello żądanego rozszerzenia.

### <a name="rerun-vm-extensions"></a>Uruchom ponownie rozszerzeń maszyny Wirtualnej

Może się zdarzyć, w których toobe, musi mieć rozszerzenie maszyny wirtualnej ponownie. Można to zrobić, usuwając hello rozszerzenia, a następnie ponowne uruchomienie rozszerzenia hello metodą wykonywania wybranych przez użytkownika. tooremove rozszerzenia, uruchom następujące polecenie z modułu Azure PowerShell hello hello. Zastąp przykładowe nazwy parametrów własne wartości.

```powershell
Remove-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

Rozszerzenie może zostać także usunięty przy użyciu hello portalu Azure. toodo tak:

1. Wybierz maszynę wirtualną.
2. Wybierz **rozszerzenia**.
3. Wybierz żądaną hello rozszerzenie.
4. Wybierz **odinstalować**.

## <a name="common-vm-extensions-reference"></a>Typowe odwołanie do rozszerzenia maszyny Wirtualnej
| Nazwa rozszerzenia | Opis | Więcej informacji |
| --- | --- | --- |
| Niestandardowe rozszerzenie skryptu dla systemu Windows |Uruchom skrypty przed maszyny wirtualnej platformy Azure |[Niestandardowe rozszerzenie skryptu dla systemu Windows](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| Rozszerzenia konfiguracji DSC dla systemu Windows |Rozszerzenia DSC (konfiguracji żądanego stanu) programu PowerShell |[Rozszerzenia konfiguracji DSC dla systemu Windows](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| Rozszerzenie Diagnostyki Azure |Zarządzanie Diagnostyka Azure |[Rozszerzenie diagnostyki platformy Azure](https://azure.microsoft.com/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/) |
| Rozszerzenia dostępu do maszyny Wirtualnej platformy Azure |Zarządzaj użytkownikami i poświadczenia |[Rozszerzenia dostępu do maszyny Wirtualnej dla systemu Linux](https://azure.microsoft.com/en-us/blog/using-vmaccess-extension-to-reset-login-credentials-for-linux-vm/) |
