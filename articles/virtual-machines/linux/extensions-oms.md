---
title: aaaOMS rozszerzenia maszyny wirtualnej platformy Azure dla systemu Linux | Dokumentacja firmy Microsoft
description: "Wdróż agenta pakietu OMS hello na maszynie wirtualnej systemu Linux przy użyciu rozszerzenia maszyny wirtualnej."
services: virtual-machines-linux
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c7bbf210-7d71-4a37-ba47-9c74567a9ea6
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: nepeters
ms.openlocfilehash: 0fc8003d1fae6c043eef18ae78d12f9304b70832
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="oms-virtual-machine-extension-for-linux"></a>Rozszerzenie maszyny wirtualnej OMS dla systemu Linux

## <a name="overview"></a>Omówienie

Operations Management Suite (OMS) zapewnia możliwości korygowania monitorowania, alertów i alertów w chmurze i lokalnych zasobów. Witaj Agent pakietu OMS rozszerzenie maszyny wirtualnej dla systemu Linux publikowania i obsługiwane przez firmę Microsoft. rozszerzenie Hello instaluje agenta pakietu OMS hello na maszynach wirtualnych platformy Azure i rejestrowania maszyn wirtualnych w istniejącym obszarem roboczym pakietu OMS. Hello szczegóły tego dokumentu obsługuje platform, konfiguracji i opcji wdrażania hello OMS rozszerzenie maszyny wirtualnej systemu Linux.

## <a name="prerequisites"></a>Wymagania wstępne

### <a name="operating-system"></a>System operacyjny

Witaj Agent pakietu OMS rozszerzenia mogą być uruchamiane na tych dystrybucje systemu Linux.

| Dystrybucja | Wersja |
|---|---|
| CentOS Linux | 5, 6 i 7 |
| Oracle Linux | 5, 6 i 7 |
| Red Hat Enterprise Linux Server | 5, 6 i 7 |
| Debian GNU/Linux | 6, 7 i 8 |
| Ubuntu | 12.04 LTS, 14.04 LTS, 15.04, 15.10, 16.04 LTS |
| SUSE Linux Enterprise Server | 11 i 12 |

### <a name="internet-connectivity"></a>Łączność z Internetem

Hello Agent pakietu OMS rozszerzenia dla systemu Linux wymaga tego hello docelowej maszyny wirtualnej jest połączonych toohello internet. 

## <a name="extension-schema"></a>Rozszerzenie schematu

Hello następujące JSON zawiera schemat hello hello rozszerzenia Agent pakietu OMS. rozszerzenie Hello wymaga hello klucz identyfikator i obszaru roboczego obszaru roboczego z hello docelowym obszarem roboczym pakietu OMS; te wartości można znaleźć w portalu OMS hello. Ponieważ klucz obszaru roboczego hello powinny być traktowane jako poufne dane, powinny być przechowywane w chronionej konfiguracji. Danych ustawieniem rozszerzenia chronione maszyny Wirtualnej Azure jest szyfrowany i odszyfrowane tylko na powitania docelowej maszyny wirtualnej. Należy pamiętać, że **workspaceId** i **workspaceKey** jest rozróżniana wielkość liter.

```json
{
  "type": "extensions",
  "name": "OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

### <a name="property-values"></a>Wartości właściwości

| Nazwa | Wartość / przykład |
| ---- | ---- |
| apiVersion | 2015-06-15 |
| Wydawcy | Microsoft.EnterpriseCloud.Monitoring |
| type | OmsAgentForLinux |
| typeHandlerVersion | 1.4 |
| workspaceId (np.) | 6f680a37-00c6-41c7-a93f-1437e3462574 |
| workspaceKey (np.) | z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI + rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ == |


## <a name="template-deployment"></a>Wdrażanie na podstawie szablonu

Rozszerzenia maszyny Wirtualnej platformy Azure można wdrożyć przy użyciu szablonów usługi Azure Resource Manager. Szablony są idealne w przypadku wdrażania maszyn wirtualnych, które wymagają konfiguracji wdrożenia post, takich jak tooOMS dołączania. Przykładowy szablon usługi Resource Manager zawierający rozszerzenia maszyny Wirtualnej agenta pakietu OMS hello znajduje się na powitania [Azure Szybki Start galerii](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-ubuntu-vm). 

Hello JSON konfiguracji dla rozszerzenia maszyny wirtualnej można zagnieżdżona hello zasobu maszyny wirtualnej lub umieszczane na główny hello lub najwyższego poziomu szablonu usługi Resource Manager JSON. umieszczanie Hello hello JSON konfiguracji dotyczy wartości hello hello nazwy zasobów i typu. Aby uzyskać więcej informacji, zobacz [Ustaw nazwę i typ zasoby podrzędne](../../azure-resource-manager/resource-manager-template-child-resource.md). 

Witaj poniższym przykładzie przyjęto założenie, że rozszerzenie OMS hello jest zagnieżdżona hello zasobu maszyny wirtualnej. Podczas zagnieżdżania hello rozszerzenia zasobu, hello JSON jest umieszczany w hello `"resources": []` obiektu hello maszyny wirtualnej.

```json
{
  "type": "extensions",
  "name": "OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

Podczas umieszczania hello rozszerzenia JSON w głównym hello hello szablonu, hello Nazwa zasobu zawiera maszynę wirtualną nadrzędnej toohello odwołania, a typ hello odzwierciedla hello zagnieżdżonych konfiguracji.  

```json
{
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "name": "<parentVmResource>/OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

## <a name="azure-cli-deployment"></a>Wdrożenia usługi Azure CLI

Hello wiersza polecenia platformy Azure mogą być używane toodeploy hello VM Agent pakietu OMS rozszerzenia tooan istniejącej maszyny wirtualnej. Zamień na powitania OMS klucz i identyfikator pakietu OMS od obszar roboczy OMS. 

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name OmsAgentForLinux \
  --publisher Microsoft.EnterpriseCloud.Monitoring \
  --version 1.4 --protected-settings '{"workspaceKey": "omskey"}' \
  --settings '{"workspaceId": "omsid"}'
```

## <a name="troubleshoot-and-support"></a>Rozwiązywanie problemów i obsługa techniczna

### <a name="troubleshoot"></a>Rozwiązywanie problemów

Z hello portalu Azure i przy użyciu interfejsu wiersza polecenia Azure hello można pobrać danych o stanie hello wdrożeń rozszerzenia. Stan wdrożenia hello toosee rozszerzeń dla danej maszyny Wirtualnej, uruchom powitania po użyciu polecenia hello wiersza polecenia platformy Azure.

```azurecli
az vm extension list --resource-group myResourceGroup --vm-name myVM -o table
```

Wykonanie rozszerzenia danych wyjściowych jest rejestrowane toohello następującego pliku:

```
/opt/microsoft/omsagent/bin/stdout
```

### <a name="error-codes-and-their-meanings"></a>Kody błędów i ich znaczenie

| Kod błędu: | Znaczenie | Możliwe działania |
| :---: | --- | --- |
| 10 | Maszyna wirtualna jest już połączony tooan obszarem roboczym pakietu OMS | tooconnect hello wirtualna toohello roboczym określonej w schemacie rozszerzenia hello, ustaw stopOnMultipleConnections toofalse w ustawieniach publiczny lub Usuń tę właściwość. Tej maszyny Wirtualnej pobiera rozliczane po dla każdego obszaru roboczego jest połączony. |
| 11 | Nieprawidłowy konfiguracji podano toohello rozszerzenia | Wykonaj hello poprzedzających tooset przykłady wszystkich wartości właściwości niezbędne do wdrożenia. |
| 12 | Menedżer pakietów dpkg Hello jest zablokowany. | Upewnij się, wszystkie dpkg operacje aktualizacji na komputerze hello zostało ukończone, a następnie spróbuj ponownie. |
| 20 | Włącz o nazwie przedwcześnie | [Witaj aktualizacji agenta systemu Linux Azure](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) toohello najnowszej dostępnej wersji. |
| 51 | To rozszerzenie nie jest obsługiwany w systemie operacji hello maszyny Wirtualnej | |
| 55 | Nie można połączyć z usługą Microsoft Operations Management Suite toohello | Sprawdź, czy hello system ma dostęp do Internetu lub że podano prawidłowy serwer proxy HTTP. Ponadto sprawdź poprawność hello identyfikator hello obszaru roboczego. |

Dodatkowe informacje dotyczące rozwiązywania problemów można znaleźć na powitania [przewodnik rozwiązywania problemów OMS agenta dla Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Troubleshooting.md#).

### <a name="support"></a>Pomoc techniczna

Jeśli potrzebujesz więcej pomocy w dowolnym momencie, w tym artykule, możesz skontaktować się hello Azure ekspertów hello [fora MSDN Azure i przepełnienie stosu](https://azure.microsoft.com/en-us/support/forums/). Alternatywnie można pliku zdarzenia pomocy technicznej platformy Azure. Przejdź toohello [witrynę pomocy technicznej platformy Azure](https://azure.microsoft.com/en-us/support/options/) i wybierz Uzyskaj pomoc techniczną. Informacje o korzystaniu z platformy Azure obsługuje, przeczytaj hello [pomocy technicznej Microsoft Azure — często zadawane pytania](https://azure.microsoft.com/en-us/support/faq/).
