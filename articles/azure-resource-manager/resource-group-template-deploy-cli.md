---
title: "aaaDeploy zasobów przy użyciu wiersza polecenia platformy Azure i szablon | Dokumentacja firmy Microsoft"
description: "Za pomocą usługi Azure Resource Manager i interfejsu wiersza polecenia Azure toodeploy tooAzure zasobów. zasoby Hello są definiowane w szablonie usługi Resource Manager."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 493b7932-8d1e-4499-912c-26098282ec95
ms.service: azure-resource-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/31/2017
ms.author: tomfitz
ms.openlocfilehash: 9f8bb9a8720399390a407030d2d32bcd97d32f13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-cli"></a>Deploy resources with Resource Manager templates and Azure CLI (Wdrażanie zasobów za pomocą szablonów usługi Resource Manager i interfejsu wiersza polecenia platformy Azure)

W tym temacie opisano sposób toouse 2.0 interfejsu wiersza polecenia platformy Azure z toodeploy szablonów usługi Resource Manager tooAzure Twojego zasobów. Jeśli nie jesteś znasz koncepcji hello wdrażania i zarządzania rozwiązań platformy Azure, zobacz [Omówienie usługi Azure Resource Manager](resource-group-overview.md).  

Szablon usługi Resource Manager Hello wdrażania może być pliku lokalnego na komputerze lub plik znajdujący się w repozytorium, takich jak usługi GitHub. Szablon Hello wdrożenia w tym artykule jest dostępny w hello [przykładowy szablon](#sample-template) sekcji lub jako [szablon konta magazynu w usłudze GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).

[!INCLUDE [sample-cli-install](../../includes/sample-cli-install.md)]

Jeśli nie masz zainstalowanych wiersza polecenia platformy Azure, możesz użyć hello [powłoki chmury](#deploy-template-from-cloud-shell).

## <a name="deploy-local-template"></a>Wdrażanie lokalnego szablonu

W przypadku wdrażania tooAzure zasobów, można:

1. Zaloguj się za tooyour konto platformy Azure
2. Utwórz grupę zasobów, która służy jako kontener hello hello wdrożonych zasobów. Nazwa Hello hello grupy zasobów może zawierać tylko znaki alfanumeryczne, kropki, podkreślenia, łączniki i nawiasy. Może okazać się too90 znaków. Nie może kończyć się kropką.
3. Wdrażanie szablonu hello grupy zasobów toohello, który definiuje hello toocreate zasobów

Szablon może zawierać parametrów, które pozwalają toocustomize hello wdrożenia. Na przykład można podać wartości dostosowanych określonym środowisku (na przykład deweloperów, testowego i produkcyjnego). Witaj przykładowy szablon definiuje parametru dla konta magazynu hello jednostki SKU. 

Witaj poniższy przykład tworzy grupę zasobów i wdraża szablonu z komputera lokalnego:

```azurecli
az login

az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters storageAccountType=Standard_GRS
```

Witaj wdrożenia może zająć kilka minut toocomplete. Po zakończeniu zostanie wyświetlony komunikat zawierający wynik hello:

```azurecli
"provisioningState": "Succeeded",
```

## <a name="deploy-external-template"></a>Wdrażanie szablonu zewnętrznych

Zamiast szablony Menedżera zasobów są przechowywane na komputerze lokalnym, możesz wybrać toostore je w lokalizacji zewnętrznej. Szablony można przechowywać w repozytorium kontroli źródła, (na przykład GitHub). Lub przechowywać w koncie magazynu platformy Azure dla dostępu współdzielonego w Twojej organizacji.

toodeploy szablonu zewnętrznego, użyj hello **szablon uri** parametru. Użyj hello identyfikatora URI w hello przykład toodeploy hello przykładowy szablon z usługi GitHub.
   
```azurecli
az login

az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json" \
    --parameters storageAccountType=Standard_GRS
```

Witaj poprzednim przykładzie wymaga publicznie identyfikatora URI dla hello szablonu, który działa w przypadku większości scenariuszy, ponieważ szablon nie może zawierać dane poufne. Jeśli potrzebujesz toospecify poufne dane (takie jak hasło administratora), należy przekazać tę wartość jako parametr bezpieczne. Jednak jeśli nie chcesz toobe Twojego szablonu publicznie, można chronić przez zapisanie jej w kontenerze prywatnego magazynu. Aby uzyskać informacje o wdrażaniu szablonu, który wymaga tokenu sygnatury dostępu Współdzielonego dostępu współdzielonego, zobacz [wdrażanie szablonu prywatnej przy użyciu tokenu sygnatury dostępu Współdzielonego](resource-manager-cli-sas-token.md).

## <a name="deploy-template-from-cloud-shell"></a>Wdrażanie szablonu za pomocą usługi Cloud Shell

Można użyć [powłoki chmury](../cloud-shell/overview.md) toorun hello Azure CLI polecenia do wdrożenia szablonu. Jednak należy najpierw załadować szablonu do udziału plików powitania dla powłoki chmury. Jeśli nie używasz usługi Cloud Shell, zobacz [Overview of Azure Cloud Shell (Omówienie usługi Azure Cloud Shell)](../cloud-shell/overview.md), aby uzyskać informacje o jej konfigurowaniu.

1. Zaloguj się za toohello [portalu Azure](https://portal.azure.com).   

2. Wybierz swoją grupę zasobów usługi Cloud Shell. wzorzec nazwy Hello jest `cloud-shell-storage-<region>`.

   ![Wybieranie grupy zasobów](./media/resource-group-template-deploy-cli/select-cs-resource-group.png)

3. Wybierz konto magazynu powitania dla powłoki chmury.

   ![Wybieranie konta magazynu](./media/resource-group-template-deploy-cli/select-storage.png)

4. Wybierz pozycję **Pliki**.

   ![Wybieranie pozycji Pliki](./media/resource-group-template-deploy-cli/select-files.png)

5. Wybierz udział plików powitania dla powłoki chmury. wzorzec nazwy Hello jest `cs-<user>-<domain>-com-<uniqueGuid>`.

   ![Wybieranie udziału plików](./media/resource-group-template-deploy-cli/select-file-share.png)

6. Wybierz pozycję **Dodaj katalog**.

   ![Dodawanie katalogu](./media/resource-group-template-deploy-cli/select-add-directory.png)

7. Nadaj mu nazwę **templates** i wybierz przycisk **OK**.

   ![Nadawanie nazwy katalogowi](./media/resource-group-template-deploy-cli/name-templates.png)

8. Wybierz swój nowy katalog.

   ![Wybieranie katalogu](./media/resource-group-template-deploy-cli/select-templates.png)

9. Wybierz pozycję **Przekaż**.

   ![Wybieranie pozycji Przekaż](./media/resource-group-template-deploy-cli/select-upload.png)

10. Znajdź i przekaż swój szablon.

   ![Przekazywanie pliku](./media/resource-group-template-deploy-cli/upload-files.png)

11. Otwórz hello wiersza.

   ![Otwieranie usługi Cloud Shell](./media/resource-group-template-deploy-cli/start-cloud-shell.png)

12. Wprowadź następujące polecenia w hello powłoki chmury hello:

   ```azurecli
   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json --parameters storageAccountType=Standard_GRS
   ```

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

Użyj toopass pliku lokalnego parametru `@` toospecify lokalnego pliku o nazwie storage.parameters.json.

```azurecli
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters @storage.parameters.json
```

## <a name="test-a-template-deployment"></a>Testowanie wdrażania szablonu

Użyj szablonu i parametru wartości bez faktycznie wdrażania żadnych zasobów tootest [zweryfikować wdrożenie grupy az](/cli/azure/group/deployment#validate). 

```azurecli
az group deployment validate \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters @storage.parameters.json
```

Jeśli nie wykryto żadnych błędów, hello polecenie zwraca informacji o wdrażaniu testu hello. W szczególności należy zauważyć, że hello **błąd** ma wartość null.

```azurecli
{
  "error": null,
  "properties": {
      ...
```

Jeśli zostanie wykryty błąd, hello polecenie zwróci komunikat o błędzie. Na przykład próba toopass nieprawidłową wartość dla konta magazynu hello jednostka SKU, zwraca hello następujący błąd:

```azurecli
{
  "error": {
    "code": "InvalidTemplate",
    "details": null,
    "message": "Deployment template validation failed: 'hello provided value 'badSKU' for hello template parameter 
      'storageAccountType' at line '13' and column '20' is not valid. hello parameter value is not part of hello allowed 
      value(s): 'Standard_LRS,Standard_ZRS,Standard_GRS,Standard_RAGRS,Premium_LRS'.'.",
    "target": null
  },
  "properties": null
}
```

Jeśli szablon zawiera błąd składniowy, polecenie hello zwróci błąd wskazujący, że nie można przeanalizować hello szablonu. wiadomości powitania wskazuje numer wiersza hello i umieść je hello błąd analizy.

```azurecli
{
  "error": {
    "code": "InvalidTemplate",
    "details": null,
    "message": "Deployment template parse failed: 'After parsing a value an unexpected character was encountered:
      \". Path 'variables', line 31, position 3.'.",
    "target": null
  },
  "properties": null
}
```

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

Tryb pełną toouse, użyj hello `mode` parametru:

```azurecli
az group deployment create \
    --name ExampleDeployment \
    --mode Complete \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters storageAccountType=Standard_GRS
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
* Przykłady Hello w tym artykule wdrażanie grupy zasobów tooa zasobów w ramach subskrypcji domyślne. toouse inną subskrypcję, zobacz [zarządzać wieloma subskrypcjami platformy Azure](/cli/azure/manage-azure-subscriptions-azure-cli).
* Zakończenie przykładowego skryptu, który wdraża szablonu, zobacz [skrypt wdrożenia szablonu usługi Resource Manager](resource-manager-samples-cli-deploy.md).
* toounderstand toodefine parametry w szablonie, zobacz temat [zrozumieć hello struktury i składni szablonów usługi Azure Resource Manager](resource-group-authoring-templates.md).
* Aby uzyskać wskazówki dotyczące rozwiązania typowych błędów wdrażania, zobacz [Rozwiąż typowe błędy wdrożenia usługi Azure z usługą Azure Resource Manager](resource-manager-common-deployment-errors.md).
* Aby uzyskać informacje o wdrażaniu szablonu, który wymaga tokenu sygnatury dostępu Współdzielonego, zobacz [wdrażanie szablonu prywatnej przy użyciu tokenu sygnatury dostępu Współdzielonego](resource-manager-cli-sas-token.md).
* Aby uzyskać wskazówki dotyczące użycia tooeffectively Menedżera zasobów przedsiębiorstwa Zarządzaj subskrypcjami, zobacz [szkieletu Azure enterprise — ładu przetestowanego subskrypcji](resource-manager-subscription-governance.md).
