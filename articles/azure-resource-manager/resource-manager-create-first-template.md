---
title: "aaaCreate pierwszego szablonu usługi Azure Resource Manager | Dokumentacja firmy Microsoft"
description: "Toocreating przewodnik krok po kroku pierwszego szablonu usługi Azure Resource Manager. Przedstawiono sposób toouse hello odwołanie do szablonu dla szablonu hello toocreate konta magazynu."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 07/27/2017
ms.topic: get-started-article
ms.author: tomfitz
ms.openlocfilehash: 92e6d6bb7094fe0e4537ee080704967862804bdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-your-first-azure-resource-manager-template"></a>Tworzenie i wdrażanie pierwszego szablonu usługi Azure Resource Manager
Ten temat przeprowadzi Cię przez kroki tworzenia szablonu usługi Azure Resource Manager pierwszy hello. Szablony Menedżera zasobów są pliki w formacie JSON określające zasoby hello potrzebne toodeploy dla rozwiązania. toounderstand hello pojęć związanych z wdrażania i zarządzania nimi rozwiązań platformy Azure, zobacz [Omówienie usługi Azure Resource Manager](resource-group-overview.md). Jeśli korzystasz z istniejących zasobów i chcesz tooget szablonu dla tych zasobów, zobacz [Eksportowanie szablonu usługi Azure Resource Manager z istniejących zasobów](resource-manager-export-template.md).

toocreate i popraw szablonów, należy edytora JSON. [Visual Studio Code](https://code.visualstudio.com/) to lekki edytor kodu typu open-source dla wielu platform. Zdecydowanie zalecamy używanie programu Visual Studio Code do tworzenia szablonów usługi Resource Manager. W tym temacie założono, że używasz programu VS Code. Jeśli jednak masz inny edytor plików JSON (np. program Visual Studio), możesz użyć tego edytora.

## <a name="prerequisites"></a>Wymagania wstępne

* Program Visual Studio Code. W razie potrzeby zainstaluj go ze strony [https://code.visualstudio.com/](https://code.visualstudio.com/).
* Subskrypcja platformy Azure. Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).

## <a name="create-template"></a>Tworzenie szablonu

Zacznijmy prostego szablonu, który wdraża subskrypcja tooyour konta magazynu.

1. Wybierz pozycję **Plik** > **Nowy plik**. 

   ![Nowy plik](./media/resource-manager-create-first-template/new-file.png)

2. Skopiuj i Wklej powitania po składni JSON do pliku:

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

   Nazwy kont magazynu ma kilka ograniczeń, które były tooset trudne. Nazwa Hello musi należeć do zakresu od 3 do 24 znaków długości, użyj tylko cyfry i małe litery i musi być unikatowa. Witaj poprzedniego szablon używa hello [uniqueString](resource-group-template-functions-string.md#uniquestring) funkcji toogenerate wartość skrótu. toogive ten skrót wartości jeden, co oznacza, dodaje prefiks hello *magazynu*. 

3. Zapisz ten plik jako **azuredeploy.json** tooa folderu lokalnego.

   ![Zapisywanie szablonu](./media/resource-manager-create-first-template/save-template.png)

## <a name="deploy-template"></a>Wdrażanie szablonu

Możesz są gotowe toodeploy tego szablonu. Możesz użyć programu PowerShell lub interfejsu wiersza polecenia Azure toocreate grupę zasobów. Następnie można wdrożyć grupę zasobów toothat konta magazynu.

* Dla programu PowerShell Użyj poniższych poleceń z hello folderu zawierającego szablon hello hello:

   ```powershell
   Login-AzureRmAccount
   
   New-AzureRmResourceGroup -Name examplegroup -Location "South Central US"
   New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json
   ```

* W przypadku instalacji lokalnej z wiersza polecenia platformy Azure Użyj poniższych poleceń z hello folderu zawierającego szablon hello hello:

   ```azurecli
   az login

   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file azuredeploy.json
   ```

Po zakończeniu wdrażania, Twoje konto magazynu istnieje w grupie zasobów hello.

## <a name="deploy-template-from-cloud-shell"></a>Wdrażanie szablonu za pomocą usługi Cloud Shell

Można użyć [powłoki chmury](../cloud-shell/overview.md) toorun hello Azure CLI polecenia do wdrożenia szablonu. Jednak należy najpierw załadować szablonu do udziału plików powitania dla powłoki chmury. Jeśli nie używasz usługi Cloud Shell, zobacz [Overview of Azure Cloud Shell (Omówienie usługi Azure Cloud Shell)](../cloud-shell/overview.md), aby uzyskać informacje o jej konfigurowaniu.

1. Zaloguj się za toohello [portalu Azure](https://portal.azure.com).   

2. Wybierz swoją grupę zasobów usługi Cloud Shell. wzorzec nazwy Hello jest `cloud-shell-storage-<region>`.

   ![Wybieranie grupy zasobów](./media/resource-manager-create-first-template/select-cs-resource-group.png)

3. Wybierz konto magazynu powitania dla powłoki chmury.

   ![Wybieranie konta magazynu](./media/resource-manager-create-first-template/select-storage.png)

4. Wybierz pozycję **Pliki**.

   ![Wybieranie pozycji Pliki](./media/resource-manager-create-first-template/select-files.png)

5. Wybierz udział plików powitania dla powłoki chmury. wzorzec nazwy Hello jest `cs-<user>-<domain>-com-<uniqueGuid>`.

   ![Wybieranie udziału plików](./media/resource-manager-create-first-template/select-file-share.png)

6. Wybierz pozycję **Dodaj katalog**.

   ![Dodawanie katalogu](./media/resource-manager-create-first-template/select-add-directory.png)

7. Nadaj mu nazwę **templates** i wybierz przycisk **OK**.

   ![Nadawanie nazwy katalogowi](./media/resource-manager-create-first-template/name-templates.png)

8. Wybierz swój nowy katalog.

   ![Wybieranie katalogu](./media/resource-manager-create-first-template/select-templates.png)

9. Wybierz pozycję **Przekaż**.

   ![Wybieranie pozycji Przekaż](./media/resource-manager-create-first-template/select-upload.png)

10. Znajdź i przekaż swój szablon.

   ![Przekazywanie pliku](./media/resource-manager-create-first-template/upload-files.png)

11. Otwórz hello wiersza.

   ![Otwieranie usługi Cloud Shell](./media/resource-manager-create-first-template/start-cloud-shell.png)

12. Wprowadź następujące polecenia w hello powłoki chmury hello:

   ```azurecli
   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json
   ```

Po zakończeniu wdrażania, Twoje konto magazynu istnieje w grupie zasobów hello.

## <a name="customize-hello-template"></a>Dostosowywanie szablonu hello

Szablon Hello działa prawidłowo, ale nie jest elastyczny. Magazyn lokalnie nadmiarowy tooSouth środkowe stany USA zawsze wdrażania. Nazwa Hello jest zawsze *magazynu* następuje wartość skrótu. tooenable przy użyciu szablonu powitania dla różnych scenariuszy, Dodaj parametry toohello szablon.

Witaj poniższy przykład przedstawia sekcji parameters hello dwa parametry. pierwszy parametr Hello `storageSKU` pozwala typu hello toospecify nadmiarowości. Ogranicza wartości hello, które można przekazać toovalues, które są prawidłowe dla konta magazynu. Określa też wartość domyślną. Witaj drugi parametr `storageNamePrefix` jest zestaw tooallow maksymalnie 11 znaków. Określa on wartość domyślną.

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
      "description": "hello type of replication toouse for hello storage account."
    }
  },
  "storageNamePrefix": {
    "type": "string",
    "maxLength": 11,
    "defaultValue": "storage",
    "metadata": {
      "description": "hello value toouse for starting hello storage account name. Use only lowercase letters and numbers."
    }
  }
},
```

W sekcji variables hello dodać zmienną o nazwie `storageName`. Łączy wartość prefiks hello z hello parametrów i wartości skrótu z hello [uniqueString](resource-group-template-functions-string.md#uniquestring) funkcji. Używa hello [toLower](resource-group-template-functions-string.md#tolower) funkcji tooconvert wszystkie toolowercase znaków.

```json
"variables": {
  "storageName": "[concat(toLower(parameters('storageNamePrefix')), uniqueString(resourceGroup().id))]"
},
```

toouse te nowe wartości dla konta magazynu, Zmień definicję zasobu hello:

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

Zwróć uwagę, że hello nazwy konta magazynu hello ma teraz wartość zmiennej toohello, który został dodany. Nazwa jednostki SKU Hello ustawiono wartość toohello hello parametru. Lokalizacja Hello jest ustawiana hello tej samej lokalizacji co hello grupy zasobów.

Zapisz plik. 

Po wykonaniu czynności hello w tym artykule szablonu teraz wygląda następująco:

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
        "description": "hello type of replication toouse for hello storage account."
      }
    },   
    "storageNamePrefix": {
      "type": "string",
      "maxLength": 11,
      "defaultValue": "storage",
      "metadata": {
        "description": "hello value toouse for starting hello storage account name. Use only lowercase letters and numbers."
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

Należy ponownie wdrożyć szablon hello o różnych wartościach.

W przypadku programu PowerShell użyj polecenia:

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json -storageNamePrefix newstore -storageSKU Standard_RAGRS
```

W przypadku interfejsu wiersza polecenia platformy Azure użyj polecenia:

```azurecli
az group deployment create --resource-group examplegroup --template-file azuredeploy.json --parameters storageSKU=Standard_RAGRS storageNamePrefix=newstore
```

W przypadku hello powłoki chmury przekazać udziału plików toohello zmienionego szablonu. Zastąp istniejący plik hello. Następnie należy użyć następującego polecenia hello:

```azurecli
az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json --parameters storageSKU=Standard_RAGRS storageNamePrefix=newstore
```

## <a name="clean-up-resources"></a>Oczyszczanie zasobów

Gdy nie są już potrzebne, należy wyczyścić zasoby hello, wdrożonej przez usunięcie hello grupy zasobów.

W przypadku programu PowerShell użyj polecenia:

```powershell
Remove-AzureRmResourceGroup -Name examplegroup
```

W przypadku interfejsu wiersza polecenia platformy Azure użyj polecenia:

```azurecli
az group delete --name examplegroup
```

## <a name="next-steps"></a>Następne kroki
* toolearn więcej informacji na temat struktury hello szablonu, zobacz [szablonów Authoring Azure Resource Manager](resource-group-authoring-templates.md).
* toolearn hello właściwości konta magazynu, zobacz [odwołania do szablonu kont magazynu](/azure/templates/microsoft.storage/storageaccounts).
* Szablony pełną tooview do różnych rozwiązań, zobacz hello [szablonów Szybki Start Azure](https://azure.microsoft.com/documentation/templates/).
