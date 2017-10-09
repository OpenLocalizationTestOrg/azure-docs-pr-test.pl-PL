---
title: "aaaExport szablonu usługi Resource Manager z wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "Za pomocą usługi Azure Resource Manager i interfejsu wiersza polecenia Azure tooexport szablonu z grupą zasobów."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/01/2017
ms.author: tomfitz
ms.openlocfilehash: 2d44a0a6e9717504d4c2a01254d826679b381f22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="export-azure-resource-manager-templates-with-azure-cli"></a>Eksportowanie szablonów usługi Azure Resource Manager z wiersza polecenia platformy Azure

Menedżer zasobów pozwala tooexport szablonem usługi Resource Manager z istniejących zasobów w ramach subskrypcji. Możesz użyć tego toolearn wygenerowanego szablonu o hello szablonu składni lub tooautomate hello ponowne wdrożenie rozwiązania zgodnie z potrzebami.

Jest ważne toonote, że istnieją dwa różne sposoby tooexport szablonu:

* Można wyeksportować szablon rzeczywiste hello używany we wdrożeniu. Hello wyeksportowanego szablonu obejmuje wszystkie hello parametry i zmienne, dokładnie tak, jak znalazły się na oryginalnym szablonie hello. Takie podejście jest przydatne, gdy będziesz potrzebować tooretrieve szablonu.
* Można wyeksportować szablon, który reprezentuje bieżący stan hello hello grupy zasobów. Witaj wyeksportowanego szablonu nie jest oparta na dowolnego szablonu, który został użyty do wdrożenia. Zamiast tego tworzy szablon, który jest migawką hello grupy zasobów. Witaj wyeksportowanego szablonu ma wiele wartości stałe i prawdopodobnie nie jako wiele parametrów, jak zwykle należy zdefiniować. Takie podejście jest przydatne, gdy zmieniono hello grupy zasobów. Teraz należy grupy zasobów hello toocapture jako szablon.

W tym temacie opisano obie te metody.

## <a name="deploy-a-solution"></a>Wdrażanie rozwiązania

tooillustrate zarówno zbliża się do eksportowania szablonu, Zacznijmy poprzez wdrożenie rozwiązania tooyour subskrypcji. Jeśli masz już grupę zasobów w ramach subskrypcji, które mają tooexport, nie masz toodeploy tego rozwiązania. Jednak hello dalszej części tego artykułu odwołuje się szablon toohello dla tego rozwiązania. skrypt przykładowy Hello wdraża konta magazynu.

```azurecli
az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name NewStorage \
    --resource-group ExampleGroup \
    --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json" \
```  

## <a name="save-template-from-deployment-history"></a>Zapisz szablon z historii wdrożenia

Można pobrać szablonu z historii wdrożenia przy użyciu hello [eksportowanie wdrożenia grupy az](/cli/azure/group/deployment#export) polecenia. następujące przykładowe zapisuje hello szablon, który wcześniej wdrażanie Hello:

```azurecli
az group deployment export --name NewStorage --resource-group ExampleGroup
```

Zwraca hello szablonu. Skopiuj hello JSON i Zapisz jako plik. Zwróć uwagę, jest hello dokładne szablon, który można użyć do wdrożenia. Witaj, parametry i zmienne odpowiada hello szablonu z serwisu GitHub. Tego szablonu można wdrożyć ponownie.


## <a name="export-resource-group-as-template"></a>Eksportowanie grupy zasobów jako szablon

Zamiast pobierania szablonu z historii wdrożenia hello, można pobrać szablonu, który reprezentuje hello bieżący stan grupy zasobów przy użyciu hello [eksportowanie grupy az](/cli/azure/group#export) polecenia. Użyj tego polecenia, gdy wprowadzono wiele zmian tooyour zasobów grupy, a nie istniejący szablon reprezentuje wszystkie zmiany hello.

```azurecli
az group export --name ExampleGroup
```

Zwraca hello szablonu. Skopiuj hello JSON i Zapisz jako plik. Należy zauważyć, że różni się od szablonu hello w serwisie GitHub. Zawiera różne parametry i żadnych zmiennych. Magazyn Hello jednostki SKU i lokalizacji są toovalues ustalony. Witaj poniższy przykład przedstawia hello wyeksportowanego szablonu, ale szablon ma nazwę parametru nieco inne:

```json
{
  "parameters": {
    "storageAccounts_mcyzaljiv7qncstandardsa_name": {
      "type": "String",
      "defaultValue": null
    }
  },
  "variables": {},
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "resources": [
    {
      "tags": {},
      "dependsOn": [],
      "apiVersion": "2016-01-01",
      "sku": {
        "name": "Standard_LRS",
        "tier": "Standard"
      },
      "kind": "Storage",
      "type": "Microsoft.Storage/storageAccounts",
      "location": "centralus",
      "name": "[parameters('storageAccounts_mcyzaljiv7qncstandardsa_name')]",
      "properties": {}
    }
  ],
  "contentVersion": "1.0.0.0"
}
```

Można ponownie wdrożyć tego szablonu, ale wymaga to odgadnięcie unikatową nazwę konta magazynu hello. Nazwa parametru Hello różni się nieznacznie.

```azurecli
az group deployment create --name NewStorage --resource-group ExampleGroup \
  --template-file examplegroup.json \
  --parameters "{\"storageAccounts_mcyzaljiv7qncstandardsa_name\":{\"value\":\"tfstore0501\"}}"
```

## <a name="customize-exported-template"></a>Dostosowywanie wyeksportowanego szablonu

Toomake tego szablonu można modyfikować jej toouse łatwiejsze i bardziej elastyczne. tooallow więcej lokalizacje, zmień hello lokalizacji właściwości toouse hello tej samej lokalizacji co hello grupy zasobów:

```json
"location": "[resourceGroup().location]",
```

tooavoid o tooguess uniques nazwę konta magazynu, Usuń parametr hello nazwy konta magazynu hello. Dodaj parametr sufiks nazwy magazynu oraz Magazyn wersji:

```json
"parameters": {
    "storageSuffix": {
      "type": "string",
      "defaultValue": "standardsa"
    },
    "storageAccountType": {
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS"
      ],
      "type": "string",
      "metadata": {
        "description": "Storage Account type"
      }
    }
},
```

Dodaj zmienną, który konstruuje hello nazwy konta magazynu z funkcją uniqueString hello:

```json
"variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
```

Ustaw nazwę hello zmiennej toohello konta magazynu hello:

```json
"name": "[variables('storageAccountName')]",
```

Ustaw parametr toohello SKU hello:

```json
"sku": {
    "name": "[parameters('storageAccountType')]",
    "tier": "Standard"
},
```

Twój szablon wygląda teraz następująco:

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageSuffix": {
      "type": "string",
      "defaultValue": "standardsa"
    },
    "storageAccountType": {
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS"
      ],
      "type": "string",
      "metadata": {
        "description": "Storage Account type"
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), parameters('storageSuffix'))]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "sku": {
        "name": "[parameters('storageAccountType')]",
        "tier": "Standard"
      },
      "kind": "Storage",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "2016-01-01",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {},
      "dependsOn": []
    }
  ]
}
```

Należy ponownie wdrożyć hello zmodyfikowany szablon.

## <a name="next-steps"></a>Następne kroki
* Aby dowiedzieć się, jak za pomocą portalu tooexport hello szablonu, zobacz [Eksportowanie szablonu usługi Azure Resource Manager z istniejących zasobów](resource-manager-export-template.md).
* Parametry toodefine w szablonie, zobacz [tworzenia szablonów](resource-group-authoring-templates.md#parameters).
* Aby uzyskać wskazówki dotyczące rozwiązania typowych błędów wdrażania, zobacz [Rozwiąż typowe błędy wdrożenia usługi Azure z usługą Azure Resource Manager](resource-manager-common-deployment-errors.md).