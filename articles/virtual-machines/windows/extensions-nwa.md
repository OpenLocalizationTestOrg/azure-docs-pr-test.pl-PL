---
title: "aaaAzure rozszerzenie maszyny wirtualnej sieci obserwatorów agenta dla systemu Windows | Dokumentacja firmy Microsoft"
description: "Wdróż hello Agent monitora sieci na maszynie wirtualnej z systemem Windows przy użyciu rozszerzenia maszyny wirtualnej."
services: virtual-machines-windows
documentationcenter: 
author: dennisg
manager: amku
editor: 
tags: azure-resource-manager
ms.assetid: 27e46af7-2150-45e8-b084-ba33de8c5e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 02/14/2017
ms.author: dennisg
ms.openlocfilehash: 21298706e462ff32c4d314f9a1ad127074ddf481
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="network-watcher-agent-virtual-machine-extension-for-windows"></a>Rozszerzenie maszyny wirtualnej obserwatorów agenta sieciowe dla systemu Windows

## <a name="overview"></a>Omówienie

[Azure obserwatora sieciowego](https://review.docs.microsoft.com/en-us/azure/network-watcher/) jest sieci performance monitoring, Diagnostyka i analiza usługa, która umożliwia monitorowanie sieci platformy Azure. Hello rozszerzenie maszyny wirtualnej sieci obserwatorów agenta jest wymagane dla niektórych funkcji obserwatora sieciowego hello na maszynach wirtualnych Azure. Dotyczy to również Przechwytywanie ruchu sieciowego na żądanie i inne zaawansowane funkcje.

Hello szczegóły tego dokumentu obsługiwane platformy i opcje wdrażania dla hello rozszerzenie maszyny wirtualnej sieci obserwatorów agenta dla systemu Windows.

## <a name="prerequisites"></a>Wymagania wstępne

### <a name="operating-system"></a>System operacyjny

Witaj rozszerzenia sieci obserwatorów agenta dla systemu Windows mogą być uruchamiane na systemie Windows Server 2008 R2, 2012 i 2012 R2, 2016 wersje. Należy pamiętać, że hello Nano Server nie jest obsługiwana w tej chwili.

### <a name="internet-connectivity"></a>Łączność z Internetem

Niektóre hello funkcji Agent monitora sieci wymaga tego hello docelowej maszyny wirtualnej toohello połączenia internetowego. Bez połączeń wychodzących hello możliwości tooestablish niektóre funkcje sieciowe obserwatorów agenta hello nieprawidłowe działanie lub stała się niedostępna. Aby uzyskać więcej informacji, zobacz hello [dokumentacji obserwatora sieciowego](../../network-watcher/network-watcher-monitoring-overview.md).

## <a name="extension-schema"></a>Rozszerzenie schematu

Hello następujące JSON zawiera schemat hello hello rozszerzenia Agent monitora sieci. rozszerzenie Hello ani wymaga nie obsługuje ustawienia dostarczone przez użytkownika w tej chwili i zależy od konfiguracji domyślnej.

```json
{
    "type": "extensions",
    "name": "Microsoft.Azure.NetworkWatcher",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.Azure.NetworkWatcher",
        "type": "NetworkWatcherAgentWindows",
        "typeHandlerVersion": "1.4",
        "autoUpgradeMinorVersion": true
    }
}
```

### <a name="property-values"></a>Wartości właściwości

| Nazwa | Wartość / przykład |
| ---- | ---- |
| apiVersion | 2015-06-15 |
| Wydawcy | Microsoft.Azure.NetworkWatcher |
| type | NetworkWatcherAgentWindows |
| typeHandlerVersion | 1.4 |


## <a name="template-deployment"></a>Wdrażanie na podstawie szablonu

Rozszerzenia maszyny Wirtualnej platformy Azure można wdrożyć przy użyciu szablonów usługi Azure Resource Manager. Podczas wdrażania szablonu usługi Azure Resource Manager hello toorun szablonu usługi Azure Resource Manager Agent monitora sieci rozszerzenia schematu JSON Hello szczegółowo opisane w poprzedniej sekcji hello w można.

## <a name="powershell-deployment"></a>Wdrożenie programu PowerShell

Witaj `Set-AzureRmVMExtension` polecenie może być używane toodeploy hello Agent monitora sieci maszyny wirtualnej rozszerzenia tooan istniejącej maszyny wirtualnej.

```powershell
Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup1" `
                       -Location "WestUS" `
                       -VMName "myVM1" `
                       -Name "networkWatcherAgent" `
                       -Publisher "Microsoft.Azure.NetworkWatcher" `
                       -Type "NetworkWatcherAgentWindows" `
                       -TypeHandlerVersion "1.4"
```

## <a name="troubleshooting-and-support"></a>Rozwiązywanie problemów i pomoc techniczna

### <a name="troubleshooting"></a>Rozwiązywanie problemów

Z hello portalu Azure i przy użyciu modułu Azure PowerShell hello można pobrać danych o stanie hello wdrożeń rozszerzenia. Stan wdrożenia hello toosee rozszerzeń dla danej maszyny Wirtualnej hello uruchom następujące polecenia przy użyciu hello modułu Azure PowerShell.

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup1 -VMName myVM1 -Name networkWatcherAgent
```

Wykonanie rozszerzenia danych wyjściowych jest rejestrowane toofiles w hello następującego katalogu:

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.NetworkWatcher.NetworkWatcherAgentWindows\
```

### <a name="support"></a>Pomoc techniczna

Jeśli potrzebujesz więcej pomocy w dowolnym momencie, w tym artykule można zapoznaj się z dokumentacją Podręcznik użytkownika obserwatora sieciowego toohello lub skontaktuj się z hello Azure ekspertów hello [fora MSDN Azure i przepełnienie stosu](https://azure.microsoft.com/en-us/support/forums/). Alternatywnie można pliku zdarzenia pomocy technicznej platformy Azure. Przejdź toohello [witrynę pomocy technicznej platformy Azure](https://azure.microsoft.com/en-us/support/options/) i wybierz Uzyskaj pomoc techniczną. Informacje o korzystaniu z platformy Azure obsługuje, przeczytaj hello [pomocy technicznej Microsoft Azure — często zadawane pytania](https://azure.microsoft.com/en-us/support/faq/).
