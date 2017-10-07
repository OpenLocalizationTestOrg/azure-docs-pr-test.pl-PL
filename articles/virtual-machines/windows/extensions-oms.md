---
title: aaaOMS rozszerzenia maszyny wirtualnej platformy Azure dla systemu Windows | Dokumentacja firmy Microsoft
description: "Wdróż agenta pakietu OMS hello na maszynie wirtualnej z systemem Windows przy użyciu rozszerzenia maszyny wirtualnej."
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: feae6176-2373-4034-b5d9-a32c6b4e1f10
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/14/2017
ms.author: nepeters
ms.openlocfilehash: 3000f66c0acdec1d1fad2125b8c6b72a92b1ec92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="oms-virtual-machine-extension-for-windows"></a>Rozszerzenie maszyny wirtualnej OMS dla systemu Windows

Operations Management Suite (OMS) zapewnia możliwości korygowania monitorowania, alertów i alertów w chmurze i lokalnych zasobów. Witaj Agent pakietu OMS rozszerzenie maszyny wirtualnej dla systemu Windows publikowana i obsługiwane przez firmę Microsoft. rozszerzenie Hello instaluje agenta pakietu OMS hello na maszynach wirtualnych platformy Azure i rejestrowania maszyn wirtualnych w istniejącym obszarem roboczym pakietu OMS. Hello szczegóły tego dokumentu obsługiwanych platform, konfiguracji i opcji wdrażania dla hello OMS rozszerzenie maszyny wirtualnej dla systemu Windows.

## <a name="prerequisites"></a>Wymagania wstępne

### <a name="operating-system"></a>System operacyjny
Witaj Agent pakietu OMS rozszerzenia dla systemu Windows mogą być uruchamiane na systemie Windows Server 2008 R2, 2012 i 2012 R2, 2016 wersje.

### <a name="internet-connectivity"></a>Łączność z Internetem
Hello Agent pakietu OMS rozszerzenia dla systemu Windows wymaga tego hello docelowej maszyny wirtualnej jest połączonych toohello internet. 

## <a name="extension-schema"></a>Rozszerzenie schematu

Hello następujące JSON zawiera schemat hello hello rozszerzenia Agent pakietu OMS. rozszerzenie Hello wymaga hello klucz identyfikator i obszaru roboczego obszaru roboczego z obszarem roboczym pakietu OMS docelowej hello, te można znaleźć w portalu OMS hello. Ponieważ klucz obszaru roboczego hello powinny być traktowane jako poufne dane, powinny być przechowywane w chronionej konfiguracji. Danych ustawieniem rozszerzenia chronione maszyny Wirtualnej Azure jest szyfrowany i odszyfrowane tylko na powitania docelowej maszyny wirtualnej. Należy pamiętać, że **workspaceId** i **workspaceKey** jest rozróżniana wielkość liter.

```json
{
    "type": "extensions",
    "name": "OMSExtension",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.EnterpriseCloud.Monitoring",
        "type": "MicrosoftMonitoringAgent",
        "typeHandlerVersion": "1.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "workspaceId": "myWorkSpaceId"
        },
        "protectedSettings": {
            "workspaceKey": "myWorkspaceKey"
        }
    }
}
```
### <a name="property-values"></a>Wartości właściwości

| Nazwa | Wartość / przykład |
| ---- | ---- |
| apiVersion | 2015-06-15 |
| Wydawcy | Microsoft.EnterpriseCloud.Monitoring |
| type | MicrosoftMonitoringAgent |
| typeHandlerVersion | 1.0 |
| workspaceId (np.) | 6f680a37-00c6-41c7-a93f-1437e3462574 |
| workspaceKey (np.) | z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI + rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ == |

## <a name="template-deployment"></a>Wdrażanie na podstawie szablonu

Rozszerzenia maszyny Wirtualnej platformy Azure można wdrożyć przy użyciu szablonów usługi Azure Resource Manager. Podczas wdrażania szablonu usługi Azure Resource Manager hello toorun szablonu usługi Azure Resource Manager Agent pakietu OMS rozszerzenia schematu JSON Hello szczegółowo opisane w poprzedniej sekcji hello w można. Przykładowy szablon, która zawiera rozszerzenia maszyny Wirtualnej agenta pakietu OMS hello znajduje się na powitania [Azure Szybki Start galerii](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-windows-vm). 

Hello JSON dla rozszerzenia maszyny wirtualnej mogą być zagnieżdżone wewnątrz hello zasobu maszyny wirtualnej lub umieszczane na główny hello lub najwyższego poziomu szablonu usługi Resource Manager JSON. rozmieszczenie Hello hello JSON dotyczy wartości hello hello nazwy zasobów i typu. Aby uzyskać więcej informacji, zobacz [Ustaw nazwę i typ zasoby podrzędne](../../azure-resource-manager/resource-manager-template-child-resource.md). 

Witaj poniższym przykładzie przyjęto założenie, że rozszerzenie OMS hello jest zagnieżdżona hello zasobu maszyny wirtualnej. Podczas zagnieżdżania hello rozszerzenia zasobu, hello JSON jest umieszczany w hello `"resources": []` obiektu hello maszyny wirtualnej.


```json
{
    "type": "extensions",
    "name": "OMSExtension",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.EnterpriseCloud.Monitoring",
        "type": "MicrosoftMonitoringAgent",
        "typeHandlerVersion": "1.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "workspaceId": "myWorkSpaceId"
        },
        "protectedSettings": {
            "workspaceKey": "myWorkspaceKey"
        }
    }
}
```

Podczas umieszczania hello rozszerzenia JSON w głównym hello hello szablonu, hello Nazwa zasobu zawiera maszynę wirtualną nadrzędnej toohello odwołania, a typ hello odzwierciedla hello zagnieżdżonych konfiguracji. 

```json
{
    "type": "Microsoft.Compute/virtualMachines/extensions",
    "name": "<parentVmResource>/OMSExtension",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.EnterpriseCloud.Monitoring",
        "type": "MicrosoftMonitoringAgent",
        "typeHandlerVersion": "1.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "workspaceId": "myWorkSpaceId"
        },
        "protectedSettings": {
            "workspaceKey": "myWorkspaceKey"
        }
    }
}
```

## <a name="powershell-deployment"></a>Wdrożenie programu PowerShell

Witaj `Set-AzureRmVMExtension` polecenie może być używane toodeploy hello Agent pakietu OMS maszyny wirtualnej rozszerzenia tooan istniejącej maszyny wirtualnej. Przed uruchomieniem polecenia hello, konfiguracje hello publicznymi i prywatnymi muszą toobe przechowywane w tablicy skrótów programu PowerShell. 

```powershell
$PublicSettings = @{"workspaceId" = "myWorkspaceId"}
$ProtectedSettings = @{"workspaceKey" = "myWorkspaceKey"}

Set-AzureRmVMExtension -ExtensionName "Microsoft.EnterpriseCloud.Monitoring" `
    -ResourceGroupName "myResourceGroup" `
    -VMName "myVM" `
    -Publisher "Microsoft.EnterpriseCloud.Monitoring" `
    -ExtensionType "MicrosoftMonitoringAgent" `
    -TypeHandlerVersion 1.0 `
    -Settings $PublicSettings `
    -ProtectedSettings $ProtectedSettings `
    -Location WestUS ` 
```

## <a name="troubleshoot-and-support"></a>Rozwiązywanie problemów i obsługa techniczna

### <a name="troubleshoot"></a>Rozwiązywanie problemów

Z hello portalu Azure i przy użyciu modułu Azure PowerShell hello można pobrać danych o stanie hello wdrożeń rozszerzenia. Stan wdrożenia hello toosee rozszerzeń dla danej maszyny Wirtualnej hello uruchom następujące polecenia przy użyciu hello modułu Azure PowerShell.

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

Wykonanie rozszerzenia danych wyjściowych jest rejestrowane toofiles w hello następującego katalogu:

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\
```

### <a name="support"></a>Pomoc techniczna

Jeśli potrzebujesz więcej pomocy w dowolnym momencie, w tym artykule, możesz skontaktować się hello Azure ekspertów hello [fora MSDN Azure i przepełnienie stosu](https://azure.microsoft.com/en-us/support/forums/). Alternatywnie można pliku zdarzenia pomocy technicznej platformy Azure. Przejdź toohello [witrynę pomocy technicznej platformy Azure](https://azure.microsoft.com/en-us/support/options/) i wybierz Uzyskaj pomoc techniczną. Informacje o korzystaniu z platformy Azure obsługuje, przeczytaj hello [pomocy technicznej Microsoft Azure — często zadawane pytania](https://azure.microsoft.com/en-us/support/faq/).
