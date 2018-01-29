---
title: "Tworzenie pierwszego szablonu usługi Azure Resource Manager | Microsoft Docs"
description: "Przewodnik krok po kroku dotyczący tworzenia pierwszego szablonu usługi Azure Resource Manager. Przewodnik pokazuje sposób użycia odwołania do szablonu dla konta magazynu w celu utworzenia szablonu."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 10/02/2017
ms.topic: get-started-article
ms.author: tomfitz
ms.openlocfilehash: 7d20469aaf2dfdd7a5f3650983b59152de837837
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="create-and-deploy-your-first-azure-resource-manager-template"></a>Tworzenie i wdrażanie pierwszego szablonu usługi Azure Resource Manager
W tym temacie szczegółowo omówiono kroki tworzenia pierwszego szablonu usługi Azure Resource Manager. Szablony usługi Resource Manager są plikami JSON definiującymi zasoby, które należy wdrożyć dla danego rozwiązania. Aby zrozumieć pojęcia związane z wdrażaniem rozwiązań platformy Azure i zarządzaniem nimi, zobacz [Usługa Azure Resource Manager — omówienie](resource-group-overview.md). Jeśli masz istniejące zasoby i chcesz uzyskać szablon dla tych zasobów, zobacz [Eksportowanie szablonu usługi Azure Resource Manager z istniejących zasobów](resource-manager-export-template.md).

Aby utworzyć i sprawdzić szablony, potrzebujesz edytora plików JSON. [Visual Studio Code](https://code.visualstudio.com/) to lekki edytor kodu typu open-source dla wielu platform. Zdecydowanie zalecamy używanie programu Visual Studio Code do tworzenia szablonów usługi Resource Manager. W tym artykule założono, że używasz programu VS Code. Jeśli jednak masz inny edytor plików JSON (np. program Visual Studio), możesz użyć tego edytora.

## <a name="prerequisites"></a>Wymagania wstępne

* Program Visual Studio Code. W razie potrzeby zainstaluj go ze strony [https://code.visualstudio.com/](https://code.visualstudio.com/).
* Subskrypcja platformy Azure. Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).

## <a name="create-template"></a>Tworzenie szablonu

Zacznijmy od prostego szablonu, który wdraża konto magazynu w Twojej subskrypcji.

1. Wybierz pozycję **Plik** > **Nowy plik**. 

   ![Nowy plik](./media/resource-manager-create-first-template/new-file.png)

2. Skopiuj i wklej następującą składnię JSON do pliku:

   ```json
   {
     "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
     "contentVersion": "1.0.0.0",
     "parameters": {
     },
     "variables": {
     },
     "resources": [
       {
         "name": "[concat('storage', uniqueString(resourceGroup().id))]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "sku": {
           "name": "Standard_LRS"
         },
         "kind": "Storage",
         "location": "South Central US",
         "tags": {},
         "properties": {}
       }
     ],
     "outputs": {  }
   }
   ```

   Nazwy kont magazynu podlegają kilku ograniczeniom, które utrudniają ich skonfigurowanie. Nazwa musi mieć od 3 do 24 znaków długości, zawierać wyłącznie cyfry i małe litery oraz musi być unikatowa. Powyższy szablon używa funkcji [uniqueString](resource-group-template-functions-string.md#uniquestring) do generowania wartości skrótu. Aby nadać więcej znaczenia tej wartości skrótu, dodawany jest prefiks *storage*. 

3. Zapisz ten plik pod nazwą **azuredeploy.json** w folderze lokalnym.

   ![Zapisywanie szablonu](./media/resource-manager-create-first-template/save-template.png)

## <a name="deploy-template"></a>Wdrażanie szablonu

Wszystko jest teraz gotowe do wdrożenia tego szablonu. Użyjesz programu PowerShell lub interfejsu wiersza polecenia platformy Azure, aby utworzyć grupę zasobów. Następnie wdrożysz konto magazynu w tej grupie zasobów.

* W przypadku programu PowerShell użyj następujących poleceń z poziomu folderu zawierającego szablon:

   ```powershell
   Login-AzureRmAccount
   
   New-AzureRmResourceGroup -Name examplegroup -Location "South Central US"
   New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json
   ```

* W przypadku lokalnej instalacji interfejsu wiersza polecenia platformy Azure użyj następujących poleceń z poziomu folderu zawierającego szablon:

   ```azurecli
   az login

   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file azuredeploy.json
   ```

Po zakończeniu wdrażania Twoje konto magazynu będzie istnieć w grupie zasobów.

[!INCLUDE [resource-manager-cloud-shell-deploy.md](../../includes/resource-manager-cloud-shell-deploy.md)]

Dla wiersza polecenia platformy Azure użyj następujących poleceń:

```azurecli-interactive
az group create --name examplegroup --location "South Central US"
az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json
```

Program PowerShell jest obecnie dostępny w usłudze Cloud Shell jako wersja zapoznawcza. Dla programu PowerShell użyj następujących poleceń:

```powershell
New-AzureRmResourceGroup -Name examplegroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile $home\CloudDrive\templates\azuredeploy.json
```

Po zakończeniu wdrażania Twoje konto magazynu będzie istnieć w grupie zasobów.

## <a name="customize-the-template"></a>Dostosowywanie szablonu

Szablon działa prawidłowo, ale nie jest elastyczny. Zawsze wdraża magazyn lokalnie nadmiarowy w regionie Południowo-środkowe stany USA. Nazwą jest zawsze *storage*, po której znajduje się wartość skrótu. Aby umożliwić używanie szablonu w różnych scenariuszach, dodaj do niego parametry.

W poniższym przykładzie przedstawiono sekcję parametrów z dwoma parametrami. Pierwszy parametr, `storageSKU`, umożliwia określenie typu nadmiarowości. Ogranicza on wartości, które można przekazać, do wartości, które są prawidłowe dla konta magazynu. Określa też wartość domyślną. Drugi parametr, `storageNamePrefix`, jest ustawiony tak, że zezwala na maksymalnie 11 znaków. Określa on wartość domyślną.

```json
"parameters": {
  "storageSKU": {
    "type": "string",
    "allowedValues": [
      "Standard_LRS",
      "Standard_ZRS",
      "Standard_GRS",
      "Standard_RAGRS",
      "Premium_LRS"
    ],
    "defaultValue": "Standard_LRS",
    "metadata": {
      "description": "The type of replication to use for the storage account."
    }
  },
  "storageNamePrefix": {
    "type": "string",
    "maxLength": 11,
    "defaultValue": "storage",
    "metadata": {
      "description": "The value to use for starting the storage account name. Use only lowercase letters and numbers."
    }
  }
},
```

W sekcji zmiennych dodaj zmienną o nazwie `storageName`. Łączy ona wartość prefiksu z parametrów i wartość skrótu z funkcji [uniqueString](resource-group-template-functions-string.md#uniquestring). Używa ona funkcji [toLower](resource-group-template-functions-string.md#tolower) w celu konwersji wszystkich liter na małe.

```json
"variables": {
  "storageName": "[concat(toLower(parameters('storageNamePrefix')), uniqueString(resourceGroup().id))]"
},
```

Aby użyć tych nowych wartości konta magazynu, zmień definicję zasobu:

```json
"resources": [
  {
    "name": "[variables('storageName')]",
    "type": "Microsoft.Storage/storageAccounts",
    "apiVersion": "2016-01-01",
    "sku": {
      "name": "[parameters('storageSKU')]"
    },
    "kind": "Storage",
    "location": "[resourceGroup().location]",
    "tags": {},
    "properties": {}
  }
],
```

Zauważ, że nazwa konta magazynu jest teraz ustawiona na dodaną przez Ciebie zmienną. Nazwa jednostki SKU ma ustawioną wartość parametru. Lokalizacja jest ustawiona na tę samą lokalizację co grupa zasobów.

Zapisz plik. 

Twój szablon wygląda teraz następująco:

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageSKU": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_ZRS",
        "Standard_GRS",
        "Standard_RAGRS",
        "Premium_LRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "The type of replication to use for the storage account."
      }
    },   
    "storageNamePrefix": {
      "type": "string",
      "maxLength": 11,
      "defaultValue": "storage",
      "metadata": {
        "description": "The value to use for starting the storage account name. Use only lowercase letters and numbers."
      }
    }
  },
  "variables": {
    "storageName": "[concat(toLower(parameters('storageNamePrefix')), uniqueString(resourceGroup().id))]"
  },
  "resources": [
    {
      "name": "[variables('storageName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-01-01",
      "sku": {
        "name": "[parameters('storageSKU')]"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {}
    }
  ],
  "outputs": {  }
}
```

## <a name="redeploy-template"></a>Ponowne wdrażanie szablonu

Ponownie wdróż szablon z innymi wartościami.

W przypadku programu PowerShell użyj polecenia:

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json -storageNamePrefix newstore -storageSKU Standard_RAGRS
```

W przypadku interfejsu wiersza polecenia platformy Azure użyj polecenia:

```azurecli
az group deployment create --resource-group examplegroup --template-file azuredeploy.json --parameters storageSKU=Standard_RAGRS storageNamePrefix=newstore
```

W przypadku usługi Cloud Shell przekaż zmieniony szablon do udziału plików. Zastąp istniejący plik. Następnie użyj poniższego polecenia:

```azurecli
az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json --parameters storageSKU=Standard_RAGRS storageNamePrefix=newstore
```

## <a name="use-autocomplete"></a>Korzystanie z autouzupełniania

Do tej pory praca z szablonem składała się tylko z kopiowania i wklejania elementów JSON z tego artykułu. Jednak podczas tworzenia własnych szablonów chcesz znaleźć i określić właściwości i wartości, które są dostępne dla danego typu zasobu. Program VS Code odczytuje schemat dla typu zasobu i sugeruje właściwości oraz wartości. Aby wyświetlić funkcję autouzupełniania, przejdź do elementu właściwości szablonu i dodaj nowy wiersz. Wpisz znak cudzysłowu i zwróć uwagę, że program VS Code natychmiast sugeruje nazwy dostępne w elemencie właściwości.

![Wyświetlanie dostępnych właściwości](./media/resource-manager-create-first-template/show-properties.png)

Wybierz element **encryption**. Wpisz dwukropek (:), a program VS Code zasugeruje dodanie nowego obiektu.

![Dodawanie obiektu](./media/resource-manager-create-first-template/add-object.png)

Naciśnij klawisz Tab lub Enter, aby dodać obiekt.

Ponownie wpisz znak cudzysłowu, a następnie zobacz, że teraz program VS Code sugeruje właściwości, które są dostępne dla elementu encryption.

![Wyświetlanie właściwości elementu encryption](./media/resource-manager-create-first-template/show-encryption-properties.png)

Wybierz element **services** i kontynuuj dodawanie wartości na podstawie rozszerzeń programu VS Code, dopóki nie uzyskasz tego:

```json
"properties": {
    "encryption":{
        "services":{
            "blob":{
              "enabled":true
            }
        }
    }
}
```

Włączono szyfrowanie obiektów blob dla konta magazynu. Jednak program VS Code wykrył problem. Zauważ, że dla elementu encryption istnieje ostrzeżenie.

![Ostrzeżenie dla elementu encryption](./media/resource-manager-create-first-template/encryption-warning.png)

Aby zobaczyć ostrzeżenie, zatrzymaj wskaźnik myszy nad zieloną linią.

![Brakująca właściwość](./media/resource-manager-create-first-template/missing-property.png)

Zobaczysz, że element encryption wymaga właściwości keySource. Dodaj przecinek po obiekcie services i dodaj właściwość keySource. Program VS Code sugeruje **"Microsoft.Storage"** jako prawidłową wartość. Po zakończeniu element właściwości wygląda następująco:

```json
"properties": {
    "encryption":{
        "services":{
            "blob":{
              "enabled":true
            }
        },
        "keySource":"Microsoft.Storage"
    }
}
```

Ostateczny szablon wygląda tak:

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageSKU": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_ZRS",
        "Standard_GRS",
        "Standard_RAGRS",
        "Premium_LRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "The type of replication to use for the storage account."
      }
    },   
    "storageNamePrefix": {
      "type": "string",
      "maxLength": 11,
      "defaultValue": "storage",
      "metadata": {
        "description": "The value to use for starting the storage account name. Use only lowercase letters and numbers."
      }
    }
  },
  "variables": {
    "storageName": "[concat(toLower(parameters('storageNamePrefix')), uniqueString(resourceGroup().id))]"
  },
  "resources": [
    {
      "name": "[variables('storageName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-01-01",
      "sku": {
        "name": "[parameters('storageSKU')]"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {
        "encryption":{
          "services":{
            "blob":{
              "enabled":true
            }
          },
          "keySource":"Microsoft.Storage"
        }
      }
    }
  ],
  "outputs": {}
}
```

## <a name="deploy-encrypted-storage"></a>Wdrażanie zaszyfrowanego magazynu

Ponownie wdróż szablon i podaj nazwę nowego konta magazynu.

W przypadku programu PowerShell użyj polecenia:

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json -storageNamePrefix storesecure
```

W przypadku interfejsu wiersza polecenia platformy Azure użyj polecenia:

```azurecli
az group deployment create --resource-group examplegroup --template-file azuredeploy.json --parameters storageNamePrefix=storesecure
```

W przypadku usługi Cloud Shell przekaż zmieniony szablon do udziału plików. Zastąp istniejący plik. Następnie użyj poniższego polecenia:

```azurecli
az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json --parameters storageNamePrefix=storesecure
```

## <a name="clean-up-resources"></a>Oczyszczanie zasobów

Gdy nie będą już potrzebne, wyczyść wdrożone zasoby, usuwając grupę zasobów.

W przypadku programu PowerShell użyj polecenia:

```powershell
Remove-AzureRmResourceGroup -Name examplegroup
```

W przypadku interfejsu wiersza polecenia platformy Azure użyj polecenia:

```azurecli
az group delete --name examplegroup
```

## <a name="next-steps"></a>Następne kroki
* Aby uzyskać większą pomoc przy opracowywaniu szablonów, możesz zainstalować rozszerzenie programu VS Code. Aby uzyskać więcej informacji, zobacz [Tworzenie szablonów usługi Azure Resource Manager przy użyciu rozszerzenia programu Visual Studio Code](resource-manager-vscode-extension.md)
* Aby uzyskać więcej informacji o strukturze szablonu, zobacz [Tworzenie szablonów usługi Azure Resource Manager](resource-group-authoring-templates.md).
* Aby poznać właściwości konta magazynu, zobacz [dokumentację szablonu kont magazynu](/azure/templates/microsoft.storage/storageaccounts).
* Aby wyświetlić pełną listę szablonów dla wielu różnych rozwiązań, zobacz [Szablony szybkiego startu platformy Azure](https://azure.microsoft.com/documentation/templates/).
