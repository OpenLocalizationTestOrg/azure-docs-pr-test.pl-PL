---
title: "aaaDeploy zasobów przy użyciu programu PowerShell i szablonu | Dokumentacja firmy Microsoft"
description: "Za pomocą usługi Azure Resource Manager i programu Azure PowerShell toodeploy tooAzure zasobów. zasoby Hello są definiowane w szablonie usługi Resource Manager."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 55903f35-6c16-4c6d-bf52-dbf365605c3f
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 41506811ba3c2ea5df6313db70978ade50f71161
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-powershell"></a>Deploy resources with Resource Manager templates and Azure PowerShell (Wdrażanie zasobów za pomocą szablonów usługi Resource Manager i programu Azure PowerShell)

W tym temacie opisano sposób toouse programu Azure PowerShell z toodeploy szablonów usługi Resource Manager tooAzure Twojego zasobów. Jeśli nie jesteś znasz koncepcji hello wdrażania i zarządzania rozwiązań platformy Azure, zobacz [Omówienie usługi Azure Resource Manager](resource-group-overview.md).

Szablon usługi Resource Manager Hello wdrażania może być pliku lokalnego na komputerze lub plik znajdujący się w repozytorium, takich jak usługi GitHub. Szablon Hello wdrożenia w tym artykule jest dostępny w hello [przykładowy szablon](#sample-template) sekcji lub jako [szablon konta magazynu w usłudze GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).

[!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install.md)]

<a id="deploy-local-template" />

## <a name="deploy-a-template-from-your-local-machine"></a>Wdrażanie szablonu z komputera lokalnego

W przypadku wdrażania tooAzure zasobów, można:

1. Zaloguj się za tooyour konto platformy Azure
2. Utwórz grupę zasobów, która służy jako kontener hello hello wdrożonych zasobów. Nazwa Hello hello grupy zasobów może zawierać tylko znaki alfanumeryczne, kropki, podkreślenia, łączniki i nawiasy. Może okazać się too90 znaków. Nie może kończyć się kropką.
3. Wdrażanie szablonu hello grupy zasobów toohello, który definiuje hello toocreate zasobów

Szablon może zawierać parametrów, które pozwalają toocustomize hello wdrożenia. Na przykład można podać wartości dostosowanych określonym środowisku (na przykład deweloperów, testowego i produkcyjnego). Witaj przykładowy szablon definiuje parametru dla konta magazynu hello jednostki SKU.

Witaj poniższy przykład tworzy grupę zasobów i wdraża szablonu z komputera lokalnego:

```powershell
Login-AzureRmAccount
 
New-AzureRmResourceGroup -Name ExampleResourceGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

Witaj wdrożenia może zająć kilka minut toocomplete. Po zakończeniu zostanie wyświetlony komunikat zawierający wynik hello:

```powershell
ProvisioningState       : Succeeded
```

## <a name="deploy-a-template-from-an-external-source"></a>Wdrażanie szablonu z zewnętrznego źródła

Zamiast szablony Menedżera zasobów są przechowywane na komputerze lokalnym, możesz wybrać toostore je w lokalizacji zewnętrznej. Szablony można przechowywać w repozytorium kontroli źródła, (na przykład GitHub). Lub przechowywać w koncie magazynu platformy Azure dla dostępu współdzielonego w Twojej organizacji.

toodeploy szablonu zewnętrznego, użyj hello **TemplateUri** parametru. Użyj hello identyfikatora URI w hello przykład toodeploy hello przykładowy szablon z usługi GitHub.

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -storageAccountType Standard_GRS
```

Witaj poprzednim przykładzie wymaga publicznie identyfikatora URI dla hello szablonu, który działa w przypadku większości scenariuszy, ponieważ szablon nie może zawierać dane poufne. Jeśli potrzebujesz toospecify poufne dane (takie jak hasło administratora), należy przekazać tę wartość jako parametr bezpieczne. Jednak jeśli nie chcesz toobe Twojego szablonu publicznie, można chronić przez zapisanie jej w kontenerze prywatnego magazynu. Aby uzyskać informacje o wdrażaniu szablonu, który wymaga tokenu sygnatury dostępu Współdzielonego dostępu współdzielonego, zobacz [wdrażanie szablonu prywatnej przy użyciu tokenu sygnatury dostępu Współdzielonego](resource-manager-powershell-sas-token.md).

## <a name="parameter-files"></a>Pliki parametrów

Zamiast przekazywanie parametrów jako wartości wbudowany w skrypcie, może być łatwiejsze toouse pliku JSON, który zawiera wartości parametrów hello. plik parametrów Hello należy hello następującego formatu:

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
     "storageAccountType": {
         "value": "Standard_GRS"
     }
  }
}
```

Zwróć uwagę, że sekcja Parametry hello zawiera nazwę parametru pasującą hello parametrów zdefiniowanych w szablonie (storageAccountType). plik parametrów Hello zawiera wartość dla parametru hello. Ta wartość jest automatycznie przekazywana toohello szablonu podczas wdrażania. Można utworzyć wiele plików parametru dla różnych scenariuszy wdrażania i przekaż plik odpowiedni parametr hello. 

Skopiuj hello poprzedzających przykład i zapisz go jako plik o nazwie `storage.parameters.json`.

toopass pliku lokalnego parametrów użyj hello **TemplateParameterFile** parametru:

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json `
  -TemplateParameterFile c:\MyTemplates\storage.parameters.json
```

toopass pliku parametrów zewnętrznego, użyj hello **TemplateParameterUri** parametru:

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -TemplateParameterUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.parameters.json
```

Można użyć wbudowanej parametrów i lokalnego parametru plików w hello sam operacji wdrażania. Na przykład możesz określić niektóre wartości w pliku parametrów lokalne powitania i dodać inne wbudowane wartości podczas wdrażania. Podaj wartości dla parametru w pliku parametrów lokalne powitania i wbudowany, pierwszeństwo ma wartość wbudowanego hello.

Jednak użycie pliku parametrów zewnętrznych, nie można przekazać wartości innych albo wbudowanego lub z pliku lokalnego. Po określeniu pliku parametrów hello **TemplateParameterUri** parametr, wszystkie parametry są ignorowane w wierszach. Podaj wszystkie wartości parametrów w pliku zewnętrznym hello. Jeśli szablon zawiera poufne wartość, która nie może zawierać w pliku parametrów hello, Dodaj magazyn kluczy tooa tej wartości lub dynamicznie Podaj wartości wszystkich parametrów w tekście.

Jeśli szablon zawiera parametru z hello takie same nazwy co jeden z parametrów hello w hello polecenia programu PowerShell, programu PowerShell będzie zawierał parametr powitania od szablonu z przyrostek hello **FromTemplate**. Na przykład parametr o nazwie **ResourceGroupName** Twojego konflikty szablonu z hello **ResourceGroupName** parametru w hello [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment)polecenia cmdlet. Jesteś tooprovide zostanie wyświetlony monit o wartości **ResourceGroupNameFromTemplate**. Ogólnie rzecz biorąc należy unikać to pomyłka nie nadawanie nazw parametrów z hello takie same nazwy jako parametry używane dla operacji wdrożenia.

## <a name="test-a-template-deployment"></a>Testowanie wdrażania szablonu

Użyj szablonu i parametru wartości bez faktycznie wdrażania żadnych zasobów tootest [AzureRmResourceGroupDeployment testu](/powershell/module/azurerm.resources/test-azurermresourcegroupdeployment). 

```powershell
Test-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

Jeśli nie wykryto żadnych błędów, polecenie hello kończy działanie bez odpowiedzi. Jeśli zostanie wykryty błąd, hello polecenie zwróci komunikat o błędzie. Na przykład próba toopass nieprawidłową wartość dla konta magazynu hello jednostka SKU, zwraca hello następujący błąd:

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName testgroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType badSku

Code    : InvalidTemplate
Message : Deployment template validation failed: 'hello provided value 'badSku' for hello template parameter 'storageAccountType'
          at line '15' and column '24' is not valid. hello parameter value is not part of hello allowed value(s):
          'Standard_LRS,Standard_ZRS,Standard_GRS,Standard_RAGRS,Premium_LRS'.'.
Details :
```

Jeśli szablon zawiera błąd składniowy, polecenie hello zwróci błąd wskazujący, że nie można przeanalizować hello szablonu. wiadomości powitania wskazuje numer wiersza hello i umieść je hello błąd analizy.

```powershell
Test-AzureRmResourceGroupDeployment : After parsing a value an unexpected character was encountered: 
  ". Path 'variables', line 31, position 3.
```

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

Tryb pełną toouse, użyj hello `Mode` parametru:

```powershell
New-AzureRmResourceGroupDeployment -Mode Complete -Name ExampleDeployment `
  -ResourceGroupName ExampleResourceGroup -TemplateFile c:\MyTemplates\storage.json 
```

## <a name="sample-template"></a>Przykładowy szablon

Witaj następujący szablon jest używany dla hello przykłady w tym temacie. Skopiuj i zapisz go jako plik o nazwie storage.json. toounderstand jak toocreate tego szablonu, zobacz [Tworzenie pierwszego szablonu usługi Azure Resource Manager](resource-manager-create-first-template.md).  

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageAccountType": {
      "type": "string",
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS",
        "Premium_LRS"
      ],
      "metadata": {
        "description": "Storage Account type"
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "2016-01-01",
      "location": "[resourceGroup().location]",
      "sku": {
          "name": "[parameters('storageAccountType')]"
      },
      "kind": "Storage", 
      "properties": {
      }
    }
  ],
  "outputs": {
      "storageAccountName": {
          "type": "string",
          "value": "[variables('storageAccountName')]"
      }
  }
}
```

## <a name="next-steps"></a>Następne kroki
* Przykłady Hello w tym artykule wdrażanie grupy zasobów tooa zasobów w ramach subskrypcji domyślne. toouse inną subskrypcję, zobacz [zarządzać wieloma subskrypcjami platformy Azure](/powershell/azure/manage-subscriptions-azureps).
* Zakończenie przykładowego skryptu, który wdraża szablonu, zobacz [skrypt wdrożenia szablonu usługi Resource Manager](resource-manager-samples-powershell-deploy.md).
* toounderstand toodefine parametry w szablonie, zobacz temat [zrozumieć hello struktury i składni szablonów usługi Azure Resource Manager](resource-group-authoring-templates.md).
* Aby uzyskać wskazówki dotyczące rozwiązania typowych błędów wdrażania, zobacz [Rozwiąż typowe błędy wdrożenia usługi Azure z usługą Azure Resource Manager](resource-manager-common-deployment-errors.md).
* Aby uzyskać informacje o wdrażaniu szablonu, który wymaga tokenu sygnatury dostępu Współdzielonego, zobacz [wdrażanie szablonu prywatnej przy użyciu tokenu sygnatury dostępu Współdzielonego](resource-manager-powershell-sas-token.md).
* Aby uzyskać wskazówki dotyczące użycia tooeffectively Menedżera zasobów przedsiębiorstwa Zarządzaj subskrypcjami, zobacz [szkieletu Azure enterprise — ładu przetestowanego subskrypcji](resource-manager-subscription-governance.md).

