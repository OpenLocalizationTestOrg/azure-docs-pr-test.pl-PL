---
title: "aaaAzure rozszerzenie maszyny wirtualnej sieci obserwatorów agenta dla systemu Linux | Dokumentacja firmy Microsoft"
description: "Wdróż hello Agent monitora sieci na maszynie wirtualnej systemu Linux przy użyciu rozszerzenia maszyny wirtualnej."
services: virtual-machines-linux
documentationcenter: 
author: dennisg
manager: amku
editor: 
tags: azure-resource-manager
ms.assetid: 5c81e94c-e127-4dd2-ae83-a236c4512345
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/14/2017
ms.author: dennisg
ms.openlocfilehash: 84bed132cbda83d0917be490f9a50914578952a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="network-watcher-agent-virtual-machine-extension-for-linux"></a>Rozszerzenie maszyny wirtualnej obserwatorów agenta sieciowe dla systemu Linux

## <a name="overview"></a>Omówienie

[Azure obserwatora sieciowego](https://review.docs.microsoft.com/en-us/azure/network-watcher/) jest sieci performance monitoring, Diagnostyka i analiza usługa, która umożliwia monitorowanie sieci platformy Azure. Hello rozszerzenie maszyny wirtualnej sieci obserwatorów agenta jest wymagane dla niektórych funkcji obserwatora sieciowego hello na maszynach wirtualnych Azure. Dotyczy to również Przechwytywanie ruchu sieciowego na żądanie i inne zaawansowane funkcje.

Hello szczegóły tego dokumentu obsługiwane platformy i opcje wdrażania dla hello rozszerzenie maszyny wirtualnej sieci obserwatorów agenta dla systemu Linux.

## <a name="prerequisites"></a>Wymagania wstępne

### <a name="operating-system"></a>System operacyjny

Hello rozszerzenia Agent monitora sieci mogą być uruchamiane na tych dystrybucje systemu Linux:

| Dystrybucja | Wersja |
|---|---|
| Ubuntu | 16.04 LTS, 14.04 LTS i 12.04 LTS |
| Debian | 7 i 8 |
| RedHat | 6.x i 7.x |
| Oracle Linux | 7 x |
| SUSE | 11 i 12 |
| OpenSuse | 7.0 |
| CentOS | 7.0 |

Należy pamiętać, że CoreOS nie jest obsługiwana w tej chwili.

### <a name="internet-connectivity"></a>Łączność z Internetem

Niektóre hello funkcji Agent monitora sieci wymaga tego hello docelowej maszyny wirtualnej toohello połączenia internetowego. Bez połączeń wychodzących hello możliwości tooestablish niektóre funkcje sieciowe obserwatorów agenta hello nieprawidłowe działanie lub stała się niedostępna. Aby uzyskać więcej informacji, zobacz hello [dokumentacji obserwatora sieciowego](https://review.docs.microsoft.com/en-us/azure/network-watcher/).

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
        "type": "NetworkWatcherAgentLinux",
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
| type | NetworkWatcherAgentLinux |
| typeHandlerVersion | 1.4 |

## <a name="template-deployment"></a>Wdrażanie na podstawie szablonu

Rozszerzenia maszyny Wirtualnej platformy Azure można wdrożyć przy użyciu szablonów usługi Azure Resource Manager. Podczas wdrażania szablonu usługi Azure Resource Manager hello toorun szablonu usługi Azure Resource Manager Agent monitora sieci rozszerzenia schematu JSON Hello szczegółowo opisane w poprzedniej sekcji hello w można.

## <a name="azure-cli-deployment"></a>Wdrożenia usługi Azure CLI

Hello Azure CLI może być używane toodeploy hello VM Agent monitora sieci rozszerzenia tooan istniejącej maszyny wirtualnej.

```azurecli
azure vm extension set myResourceGroup1 myVM1 NetworkWatcherAgentLinux Microsoft.Azure.NetworkWatcher 1.4
```

## <a name="troubleshooting-and-support"></a>Rozwiązywanie problemów i pomoc techniczna

### <a name="troubleshooting"></a>Rozwiązywanie problemów

Z hello portalu Azure i przy użyciu interfejsu wiersza polecenia Azure hello można pobrać danych o stanie hello wdrożeń rozszerzenia. Stan wdrożenia hello toosee rozszerzeń dla danej maszyny Wirtualnej, uruchom powitania po użyciu polecenia hello wiersza polecenia platformy Azure.

```azurecli
azure vm extension get myResourceGroup1 myVM1
```

Wykonanie rozszerzenia danych wyjściowych jest rejestrowane toofiles w hello następującego katalogu:

`
/var/log/azure/Microsoft.Azure.NetworkWatcher.NetworkWatcherAgentLinux/
`

### <a name="support"></a>Pomoc techniczna

Jeśli potrzebujesz więcej pomocy w dowolnym momencie, w tym artykule można zapoznaj się z dokumentacją obserwatora sieciowego toohello lub skontaktuj się z hello Azure ekspertów hello [fora MSDN Azure i przepełnienie stosu](https://azure.microsoft.com/en-us/support/forums/). Alternatywnie można pliku zdarzenia pomocy technicznej platformy Azure. Przejdź toohello [witrynę pomocy technicznej platformy Azure](https://azure.microsoft.com/en-us/support/options/) i wybierz Uzyskaj pomoc techniczną. Informacje o korzystaniu z platformy Azure obsługuje, przeczytaj hello [pomocy technicznej Microsoft Azure — często zadawane pytania](https://azure.microsoft.com/en-us/support/faq/).
