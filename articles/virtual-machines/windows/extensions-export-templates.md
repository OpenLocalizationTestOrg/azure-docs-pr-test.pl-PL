---
title: "aaaExporting grup zasobów Azure, która zawiera rozszerzenia maszyny Wirtualnej | Dokumentacja firmy Microsoft"
description: "Wyeksportować szablony Menedżera zasobów, które obejmują rozszerzenia maszyny wirtualnej."
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7f4e2ca6-f1c7-4f59-a2cc-8f63132de279
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 12/05/2016
ms.author: nepeters
ms.openlocfilehash: cdbc2030988a19fe68429e8733dc60536c264abf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="exporting-resource-groups-that-contain-vm-extensions"></a>Eksportowanie grupy zasobów, która zawiera rozszerzenia maszyny Wirtualnej

Grupy zasobów platformy Azure mogą być eksportowane do nowego szablonu usługi Resource Manager, które mogą być następnie wdrażane. Witaj procesu eksportu interpretuje istniejących zasobów i tworzy szablonu usługi Resource Manager która po wdrożeniu powoduje podobne grupy zasobów. Korzystając z opcji eksportu grupy zasobów hello przed grupę zasobów zawierającą rozszerzenia maszyny wirtualnej, kilka elementów potrzeby toobe uznawane za takich jak zgodność rozszerzenia i chronionych ustawień.

Szczegóły tego dokumentu, jak działa hello procesu eksportu grupy zasobów dotyczących rozszerzenia maszyny wirtualnej, łącznie z listą obsługiwanych rozszerzeń, a szczegóły dotyczące obsługi zabezpieczonych danych.

## <a name="supported-virtual-machine-extensions"></a>Rozszerzenia obsługiwanych maszyn wirtualnych

Dostępnych jest wiele rozszerzeń maszyny wirtualnej. Nie wszystkie rozszerzenia mogą być eksportowane do szablonu usługi Resource Manager za pomocą funkcji "Skrypt automatyzacji" hello. Jeśli rozszerzenie maszyny wirtualnej nie jest obsługiwana, musi on toobe ręcznie umieścić do wyeksportowanego szablonu hello.

Witaj następujących rozszerzeń można eksportować z funkcją skryptów automatyzacji hello.

| Wewnętrzny ||||
|---|---|---|---|
| Kopia zapasowa Acronis | Agent Datadog Windows | Stosowanie poprawek dla systemu Linux systemu operacyjnego | Migawki maszyny Wirtualnej w systemie Linux
| Kopia zapasowa Acronis systemu Linux | Rozszerzenie docker | Puppet Agent |
| Informacje o BG | Rozszerzenie DSC | Szczegółowe informacje o lokacji 24 x 7 Apm |
| Linux Agent BMC CTM | Dynatrace systemu Linux | 24 x 7 Linux serwera lokacji |
| BMC CTM agenta w systemie Windows | Dynatrace systemu Windows | Lokacja 24 x 7 systemu Windows Server |
| Chef klienta | HPE zabezpieczeń aplikacji Defender | Trend Micro DSA |
| Niestandardowego skryptu | IaaS ochrony przed złośliwym oprogramowaniem | Trend Micro DSA Linux |
| Rozszerzenie niestandardowego skryptu | Diagnostyka IaaS | Dostęp do maszyny Wirtualnej dla systemu Linux |
| Skryptu niestandardowego dla systemu Linux | Linux Chef klienta | Dostęp do maszyny Wirtualnej dla systemu Linux |
| Datadog agenta systemu Linux | Diagnostyka systemu Linux | Migawki maszyny Wirtualnej |

## <a name="export-hello-resource-group"></a>Eksportuj hello grupy zasobów

tooexport grupę zasobów do szablonu wielokrotnego użytku, pełną hello następujące kroki:

1. Zaloguj się toohello portalu Azure
2. W Menu centralnym hello kliknij polecenie grup zasobów
3. Wybierz z listy hello hello docelowa grupa zasobów
4. W bloku grupy zasobów powitania kliknij skryptu automatyzacji

![Eksportowanie szablonu](./media/extensions-export-templates/template-export.png)

Witaj skryptów automatyzacji Azure Resource Manager tworzy szablonu usługi Resource Manager, pliku parametrów i skrypty wdrażania przykładowe, takie jak środowiska PowerShell i interfejsu wiersza polecenia Azure. W tym momencie hello wyeksportowanego szablonu można pobrać za pomocą przycisku pobierania hello, dodany jako nowy szablon biblioteki toohello szablonu, lub ponownej instalacji przy użyciu hello wdrażanie przycisku.

## <a name="configure-protected-settings"></a>Skonfiguruj ustawienia chronionego

Wiele rozszerzeń maszyny wirtualnej platformy Azure obejmują konfiguracji chronionych ustawień, który szyfruje dane poufne, na przykład poświadczenia i parametry konfiguracji. Ustawienia chronionych nie są eksportowane z hello skryptów automatyzacji. Jeśli konieczne, chronionych ustawienia należy ponownie wstawić do hello toobe eksportowane szablonem.

### <a name="step-1---remove-template-parameter"></a>Krok 1 — Usuń parametr szablonu

Podczas tworzenia tooprovide powitalne grupy zasobów jest eksportowany, parametr jednego szablonu toohello wartość wyeksportowane ustawienia chronionych. Ten parametr może zostać usunięta. Parametr hello tooremove, przejrzyj listę parametrów hello i usunąć parametr hello, która wygląda podobnie przykład JSON toothis.

```json
"extensions_extensionname_protectedSettings": {
    "defaultValue": null,
    "type": "SecureObject"
}
```

### <a name="step-2---get-protected-settings-properties"></a>Krok 2 - Get chronione ustawienia właściwości

Ponieważ każdy chroniony ustawienie ma zestaw właściwości wymagane, listę tych właściwości muszą toobe zebrane. Każdy parametr hello chronionych ustawień konfiguracji można znaleźć w hello [schematu usługi Azure Resource Manager w witrynie GitHub](https://raw.githubusercontent.com/Azure/azure-resource-manager-schemas/master/schemas/2015-08-01/Microsoft.Compute.json). Ten schemat zawiera tylko zestawy parametrów hello rozszerzeń hello wymienione w sekcji Przegląd hello tego dokumentu. 

Z wewnątrz hello schematu repozytorium, wyszukaj rozszerzenie hello potrzebne, w tym przykładzie `IaaSDiagnostics`. Raz hello rozszerzenia `protectedSettings` obiektu została znaleziona, zanotuj każdego parametru. W przykładzie hello hello `IaasDiagnostic` hello rozszerzenia, wymagają parametry są `storageAccountName`, `storageAccountKey`, i `storageAccountEndPoint`.

```json
"protectedSettings": {
    "type": "object",
    "properties": {
        "storageAccountName": {
            "type": "string"
        },
        "storageAccountKey": {
            "type": "string"
        },
        "storageAccountEndPoint": {
            "type": "string"
        }
    },
    "required": [
        "storageAccountName",
        "storageAccountKey",
        "storageAccountEndPoint"
    ]
}
```

### <a name="step-3---re-create-hello-protected-configuration"></a>Krok 3 — odtworzyć konfiguracji hello chronione

Na hello wyeksportowanego szablonu, wyszukiwanie `protectedSettings` i Zastąp hello wyeksportowanego ustawiania chronionego obiektu nowy obejmującej hello wymagane rozszerzenie parametrów i wartości dla każdego z nich.

W przykładzie hello hello `IaasDiagnostic` rozszerzenia, nowej konfiguracji chronionych ustawienie hello będzie wyglądała hello poniższy przykład:

```json
"protectedSettings": {
    "storageAccountName": "[parameters('storageAccountName')]",
    "storageAccountKey": "[parameters('storageAccountKey')]",
    "storageAccountEndPoint": "https://core.windows.net"
}
```

Hello rozszerzeniem końcowym zasobów wygląda podobnie toohello poniższy przykład JSON:

```json
{
    "name": "Microsoft.Insights.VMDiagnosticsSettings",
    "type": "extensions",
    "location": "[resourceGroup().location]",
    "apiVersion": "[variables('apiVersion')]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "tags": {
        "displayName": "AzureDiagnostics"
    },
    "properties": {
        "publisher": "Microsoft.Azure.Diagnostics",
        "type": "IaaSDiagnostics",
        "typeHandlerVersion": "1.5",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "xmlCfg": "[base64(concat(variables('wadcfgxstart'), variables('wadmetricsresourceid'), variables('vmName'), variables('wadcfgxend')))]",
            "storageAccount": "[parameters('existingdiagnosticsStorageAccountName')]"
        },
        "protectedSettings": {
            "storageAccountName": "[parameters('storageAccountName')]",
            "storageAccountKey": "[parameters('storageAccountKey')]",
            "storageAccountEndPoint": "https://core.windows.net"
        }
    }
}
```

Jeśli przy użyciu wartości właściwości tooprovide parametrów szablonu, te czynności toobe utworzony. Podczas tworzenia parametrów szablonu dla chronionych ustawiania wartości, upewnij się, że hello toouse `SecureString` typ parametru, tak aby poufnych wartości są chronione. Aby uzyskać więcej informacji na temat używania parametrów, zobacz [szablonów Authoring Azure Resource Manager](../../resource-group-authoring-templates.md).

W przykładzie hello hello `IaasDiagnostic` rozszerzenia, hello następujące parametry zostałyby utworzone w sekcji parametrów hello hello szablonu usługi Resource Manager.

```json
"storageAccountName": {
    "defaultValue": null,
    "type": "SecureString"
},
"storageAccountKey": {
    "defaultValue": null,
    "type": "SecureString"
}
```

W tym momencie hello szablonu można wdrożyć przy użyciu dowolnej metody wdrażania szablonu.
