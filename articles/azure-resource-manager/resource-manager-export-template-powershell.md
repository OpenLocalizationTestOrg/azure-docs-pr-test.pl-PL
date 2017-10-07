---
title: "Szablon usługi Resource Manager aaaExport przy użyciu programu Azure PowerShell | Dokumentacja firmy Microsoft"
description: "Za pomocą usługi Azure Resource Manager i programu Azure PowerShell tooexport szablonu z grupą zasobów."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/01/2017
ms.author: tomfitz
ms.openlocfilehash: 9a239b7bce8209326c0e267a4d3d69f7014bdaed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="export-azure-resource-manager-templates-with-powershell"></a>Eksportowanie szablonów usługi Azure Resource Manager przy użyciu programu PowerShell

Menedżer zasobów pozwala tooexport szablonem usługi Resource Manager z istniejących zasobów w ramach subskrypcji. Możesz użyć tego toolearn wygenerowanego szablonu o hello szablonu składni lub tooautomate hello ponowne wdrożenie rozwiązania zgodnie z potrzebami.

Jest ważne toonote, że istnieją dwa różne sposoby tooexport szablonu:

* Można wyeksportować szablon rzeczywiste hello używany we wdrożeniu. Hello wyeksportowanego szablonu obejmuje wszystkie hello parametry i zmienne, dokładnie tak, jak znalazły się na oryginalnym szablonie hello. Takie podejście jest przydatne, gdy będziesz potrzebować tooretrieve szablonu.
* Można wyeksportować szablon, który reprezentuje bieżący stan hello hello grupy zasobów. Witaj wyeksportowanego szablonu nie jest oparta na dowolnego szablonu, który został użyty do wdrożenia. Zamiast tego tworzy szablon, który jest migawką hello grupy zasobów. Witaj wyeksportowanego szablonu ma wiele wartości stałe i prawdopodobnie nie jako wiele parametrów, jak zwykle należy zdefiniować. Takie podejście jest przydatne, gdy zmieniono hello grupy zasobów. Teraz należy grupy zasobów hello toocapture jako szablon.

W tym temacie opisano obie te metody.

## <a name="deploy-a-solution"></a>Wdrażanie rozwiązania

tooillustrate zarówno zbliża się do eksportowania szablonu, Zacznijmy poprzez wdrożenie rozwiązania tooyour subskrypcji. Jeśli masz już grupę zasobów w ramach subskrypcji, które mają tooexport, nie masz toodeploy tego rozwiązania. Jednak hello dalszej części tego artykułu odwołuje się szablon toohello dla tego rozwiązania. skrypt przykładowy Hello wdraża konta magazynu.

```powershell
New-AzureRmResourceGroup -Name ExampleGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup `
  -DeploymentName NewStorage
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json
```  

## <a name="save-template-from-deployment-history"></a>Zapisz szablon z historii wdrożenia

Można pobrać szablonu z historii wdrożenia przy użyciu hello [AzureRmResourceGroupDeploymentTemplate Zapisz](/powershell/module/azurerm.resources/save-azurermresourcegroupdeploymenttemplate) polecenia. następujące przykładowe zapisuje hello szablon, który wcześniej wdrażanie Hello:

```powershell
Save-AzureRmResourceGroupDeploymentTemplate -ResourceGroupName ExampleGroup -DeploymentName NewStorage
```

Zwraca lokalizację hello hello szablonu.

```powershell
Path
----
C:\Users\exampleuser\NewStorage.json
```

Otwórz plik hello i Zauważ, że jest ona hello dokładne szablon, który można użyć do wdrożenia. Witaj, parametry i zmienne odpowiada hello szablonu z serwisu GitHub. Tego szablonu można wdrożyć ponownie.

## <a name="export-resource-group-as-template"></a>Eksportowanie grupy zasobów jako szablon

Zamiast pobierania szablonu z historii wdrożenia hello, można pobrać szablonu, który reprezentuje hello bieżący stan grupy zasobów przy użyciu hello [Export-AzureRmResourceGroup](/powershell/module/azurerm.resources/export-azurermresourcegroup) polecenia. Użyj tego polecenia, gdy wprowadzono wiele zmian tooyour zasobów grupy, a nie istniejący szablon reprezentuje wszystkie zmiany hello.

```powershell
Export-AzureRmResourceGroup -ResourceGroupName ExampleGroup
```

Zwraca lokalizację hello hello szablonu.

```powershell
Path
----
C:\Users\exampleuser\ExampleGroup.json
```

Otwórz plik hello i zwróć uwagę, że jest inny niż szablon hello w serwisie GitHub. Zawiera różne parametry i żadnych zmiennych. Magazyn Hello jednostki SKU i lokalizacji są toovalues ustalony. Witaj poniższy przykład przedstawia hello wyeksportowanego szablonu, ale szablon ma nazwę parametru nieco inne:

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageAccounts_nf3mvst4nqb36standardsa_name": {
      "defaultValue": null,
      "type": "String"
    }
  },
  "variables": {},
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "sku": {
        "name": "Standard_LRS",
        "tier": "Standard"
      },
      "kind": "Storage",
      "name": "[parameters('storageAccounts_nf3mvst4nqb36standardsa_name')]",
      "apiVersion": "2016-01-01",
      "location": "southcentralus",
      "tags": {},
      "properties": {},
      "dependsOn": []
    }
  ]
}
```

Można ponownie wdrożyć tego szablonu, ale wymaga to odgadnięcie unikatową nazwę konta magazynu hello. Nazwa parametru Hello różni się nieznacznie.

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup `
  -TemplateFile C:\Users\exampleuser\ExampleGroup.json `
  -storageAccounts_nf3mvst4nqb36standardsa_name tfnewstorage0501
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
