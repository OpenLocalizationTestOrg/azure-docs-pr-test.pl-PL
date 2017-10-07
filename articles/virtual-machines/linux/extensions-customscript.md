---
title: "niestandardowych skryptów aaaRun na maszynach wirtualnych systemu Linux na platformie Azure | Dokumentacja firmy Microsoft"
description: "Automatyzowanie zadań konfiguracji maszyny Wirtualnej systemu Linux przy użyciu hello niestandardowe rozszerzenie skryptu"
services: virtual-machines-linux
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: cf17ab2b-8d7e-4078-b6df-955c6d5071c2
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: nepeters
ms.openlocfilehash: f2c273a5fbd4cd1695aea48fa4bd08e691511e5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-custom-script-extension-with-linux-virtual-machines"></a>Przy użyciu hello Azure niestandardowe rozszerzenie skryptu z maszyn wirtualnych systemu Linux
Witaj niestandardowe rozszerzenie skryptu pobiera i uruchamia skrypty na maszynach wirtualnych Azure. To rozszerzenie jest przydatne w przypadku konfiguracji wdrożenia post, instalacja oprogramowania lub dowolnej innej konfiguracji / zadanie zarządzania. Skrypty można pobrać z magazynu Azure lub inne dostępne miejsce w Internecie lub podane rozszerzenie toohello czas wykonywania. Hello rozszerzenia niestandardowego skryptu integruje się z szablonów usługi Azure Resource Manager i można również uruchomić przy użyciu hello wiersza polecenia platformy Azure, programu PowerShell, portalu Azure lub hello interfejsu API REST maszyny wirtualnej Azure.

Szczegóły tego dokumentu, jak toouse hello niestandardowe rozszerzenie skryptu z hello Azure CLI i szablonu usługi Azure Resource Manager, a także szczegółowe informacje, kroki w systemach Linux rozwiązywania problemów.

## <a name="extension-configuration"></a>Konfiguracja rozszerzenia
Hello niestandardowe rozszerzenie skryptu konfiguracji określa lokalizację i hello toobe polecenie Uruchom. Tej konfiguracji mogą być przechowywane w plikach konfiguracji określone w wierszu polecenia hello lub w szablonie usługi Azure Resource Manager. Poufne dane mogą być przechowywane w chronionej konfigurację, która zostaje zaszyfrowany i odszyfrowane tylko wewnątrz maszyny wirtualnej hello. Konfiguracja chronionych Hello jest użyteczna, gdy hello wykonanie polecenia zawiera klucze tajne, takie jak hasła.

### <a name="public-configuration"></a>Publiczna Konfiguracja
Schemat:

**Uwaga** — te nazwy właściwości jest uwzględniana wielkość liter. Użyj nazwy hello, jak pokazano poniżej tooavoid problemy z wdrażaniem.

* **commandToExecute**: (wymagane, string) hello tooexecute skryptu punktu wejścia
* **fileUris**: pobrać adresy URL hello toobe plików (opcjonalne, tablicy ciągów).
* **Sygnatura czasowa** (opcjonalne, liczba całkowita) Użyj tego pola tootrigger tylko Uruchom ponownie skrypt hello, zmieniając wartość tego pola.

```json
{
  "fileUris": ["<url>"],
  "commandToExecute": "<command-to-execute>"
}
```

### <a name="protected-configuration"></a>Konfiguracja chronionych
Schemat:

**Uwaga** — te nazwy właściwości jest uwzględniana wielkość liter. Użyj nazwy hello, jak pokazano poniżej tooavoid problemy z wdrażaniem.

* **commandToExecute**: (opcjonalne, ciąg) hello tooexecute skryptu punktu wejścia. Zamiast tego użyj tego pola, jeśli polecenie zawiera klucze tajne, takie jak hasła.
* **storageAccountName**: (opcjonalne, ciąg) hello nazwę konta magazynu. Jeśli określisz poświadczeń magazynu fileUris wszystkie muszą być adresami URL dla obiektów blob Azure.
* **storageAccountKey**: (opcjonalne, ciąg) hello klucz dostępu konta magazynu.

```json
{
  "commandToExecute": "<command-to-execute>",
  "storageAccountName": "<storage-account-name>",
  "storageAccountKey": "<storage-account-key>"
}
```

## <a name="azure-cli"></a>Interfejs wiersza polecenia platformy Azure
Używając hello Azure CLI toorun hello niestandardowe rozszerzenie skryptu, Utwórz plik konfiguracji lub pliki zawierające uri pliku hello minimalna i hello skryptu wykonywania polecenia.

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

Opcjonalnie hello ustawienia można określić w poleceniu hello jako ciąg w formacie JSON. Dzięki temu toobe konfiguracji hello określony podczas wykonywania i bez pliku osobną konfiguracją.

```azurecli
az vm extension set '
  --resource-group exttest `
  --vm-name exttest `
  --name customScript `
  --publisher Microsoft.Azure.Extensions `
  --settings '{"fileUris": ["https://raw.githubusercontent.com/neilpeterson/test-extension/master/test.sh"],"commandToExecute": "./test.sh"}'
```

### <a name="azure-cli-examples"></a>Przykłady Azure CLI

**Przykład 1** -publicznej konfiguracji z pliku skryptu.

```json
{
  "fileUris": ["https://raw.githubusercontent.com/neilpeterson/test-extension/master/test.sh"],
  "commandToExecute": "./test.sh"
}
```

Polecenia interfejsu wiersza polecenia platformy Azure:

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

**Przykład 2** -publicznej konfiguracji z żadnego pliku skryptu.

```json
{
  "commandToExecute": "apt-get -y update && apt-get install -y apache2"
}
```

Polecenia interfejsu wiersza polecenia platformy Azure:

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

**Przykład 3** — plik konfiguracji publicznego jest plik skryptu używany toospecify hello identyfikatora URI, a plik chroniony konfiguracji jest toobe polecenia hello używane toospecify wykonywane.

Plik konfiguracji publicznego:

```json
{
  "fileUris": ["https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"]
}
```

Plik chroniony konfiguracji:  

```json
{
  "commandToExecute": "./hello.sh <password>"
}
```

Polecenia interfejsu wiersza polecenia platformy Azure:

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json --protected-settings ./protected-config.json
```

## <a name="resource-manager-template"></a>Szablon usługi Resource Manager
Hello Azure niestandardowe rozszerzenie skryptu można uruchomić w czasie wdrażania maszyny wirtualnej przy użyciu szablonu usługi Resource Manager. toodo tak, Dodaj prawidłowo sformatowane JSON toohello wdrażania szablonu.

### <a name="resource-manager-examples"></a>Przykłady usługi Resource Manager
**Przykład 1** -publicznej konfiguracji.

```json
{
    "name": "scriptextensiondemo",
    "type": "extensions",
    "location": "[resourceGroup().location]",
    "apiVersion": "2015-06-15",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', parameters('scriptextensiondemoName'))]"
    ],
    "tags": {
        "displayName": "scriptextensiondemo"
    },
    "properties": {
        "publisher": "Microsoft.Azure.Extensions",
        "type": "CustomScript",
        "typeHandlerVersion": "2.0",
        "autoUpgradeMinorVersion": true,
      "settings": {
        "fileUris": [
          "https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"
        ],
        "commandToExecute": "sh hello.sh"
      }
    }
}
```

**Przykład 2** — wykonanie polecenia w chronionym konfiguracji.

```json
{
  "name": "config-app",
  "type": "extensions",
  "location": "[resourceGroup().location]",
  "apiVersion": "2015-06-15",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"
      ]              
    },
    "protectedSettings": {
      "commandToExecute": "sh hello.sh <password>"
    }
  }
}
```

Zobacz hello .net Core utworów muzycznych magazynu pokaz pełny przykład - [pokaz magazynu utworów muzycznych](https://github.com/neilpeterson/nepeters-azure-templates/tree/master/dotnet-core-music-linux-vm-sql-db).

## <a name="troubleshooting"></a>Rozwiązywanie problemów
Po uruchomieniu hello niestandardowe rozszerzenie skryptu skryptu hello jest tworzony lub pobrany do katalogu toohello podobne, poniższy przykład. dane wyjściowe polecenia Hello jest także zapisane w tym katalogu w `stdout` i `stderr` pliku.

```bash
/var/lib/waagent/custom-script/download/0/
```

Witaj rozszerzenie skryptu Azure tworzy dziennika, który można znaleźć tutaj.

```bash
/var/log/azure/custom-script/handler.log
```

Stan wykonywania Hello hello niestandardowe rozszerzenie skryptu można również pobrać z hello wiersza polecenia platformy Azure.

```azurecli
az vm extension list -g myResourceGroup --vm-name myVM
```

dane wyjściowe Hello wygląda hello następującego tekstu:

```azurecli
info:    Executing command vm extension get
+ Looking up hello VM "scripttst001"
data:    Publisher                   Name                                      Version  State
data:    --------------------------  ----------------------------------------  -------  ---------
data:    Microsoft.Azure.Extensions  CustomScript                              2.0      Succeeded
data:    Microsoft.OSTCExtensions    Microsoft.Insights.VMDiagnosticsSettings  2.3      Succeeded
info:    vm extension get command OK
```

## <a name="next-steps"></a>Następne kroki
Aby uzyskać informacje na inne rozszerzenia skryptu maszyny Wirtualnej, zobacz [omówienie rozszerzenie skryptu Azure dla systemu Linux](extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

