---
title: "tooAzure zasobów aaaDeploy | Dokumentacja firmy Microsoft"
description: "Za pomocą programu Azure PowerShell lub interfejsu wiersza polecenia Azure tooAzure zasobów toodeploy. zasoby Hello są definiowane w szablonie usługi Resource Manager."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/16/2017
ms.author: tomfitz
ms.openlocfilehash: 0cd3f8ad45af1fb85c78899b56f6807d00b859f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-tooazure"></a>Wdrażanie tooAzure zasobów

W tym temacie przedstawiono sposób toodeploy tooyour zasobów subskrypcji platformy Azure. Możesz użyć programu Azure PowerShell lub interfejsu wiersza polecenia Azure toodeploy szablonu usługi Resource Manager, który definiuje infrastrukturę Twojego rozwiązania hello.

Aby tooconcepts wprowadzenie usługi Resource Manager, zobacz [Omówienie usługi Azure Resource Manager](resource-group-overview.md).

## <a name="steps-for-deployment"></a>Kroki wdrażania

W tym temacie założono wdrażasz hello [przykład magazynu szablonu](#example-storage-template) w tym temacie. Można użyć innego szablonu, ale hello parametry, które przekazujesz są inne niż to, co przedstawiono w tym temacie.

Po utworzeniu szablonu, hello ogólne kroki dotyczące wdrażania szablonu są:

1. Zaloguj się na koncie tooyour
2. Wybierz toouse subskrypcji hello (wymagane tylko jeśli masz wiele subskrypcji, i chcesz toouse, który nie jest hello domyślne subskrypcji)
3. Tworzenie grupy zasobów
4. Wdrażanie szablonu hello
5. Sprawdzenie stanu wdrożenia

Witaj poniższe sekcje pokazują, jak tooperform tych kroków [PowerShell](#powershell) lub [interfejsu wiersza polecenia Azure](#azure-cli).

## <a name="powershell"></a>PowerShell

1. tooinstall programu Azure PowerShell, zobacz [wprowadzenie do poleceń cmdlet programu Azure PowerShell](/powershell/azure/overview).

2. tooquickly wprowadzenie do wdrożenia, użyj następującego polecenia cmdlet hello:

  ```powershell
  Login-AzureRmAccount
  Set-AzureRmContext -SubscriptionID {subscription-id}

  New-AzureRmResourceGroup -Name ExampleGroup -Location "Central US"
  New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleGroup -TemplateFile c:\MyTemplates\azuredeploy.json 
  ```

  Witaj `Set-AzureRmContext` polecenia cmdlet jest potrzebne tylko wtedy, jeśli chcesz toouse subskrypcji innych niż domyślne subskrypcji. toosee wszystkie subskrypcje i ich identyfikatorów, należy użyć:

  ```powershell
  Get-AzureRmSubscription
  ```

3. Witaj wdrożenia może zająć kilka minut toocomplete. Po zakończeniu zostanie wyświetlony komunikat podobny do następującego:

  ```powershell
  DeploymentName          : ExampleDeployment
  CorrelationId           : 07b3b233-8367-4a0b-b9bc-7aa189065665
  ResourceGroupName       : ExampleGroup
  ProvisioningState       : Succeeded
  ...
  ```

4. toosee, które były zasobów konta grupy i magazynu wdrożone tooyour subskrypcji, użyj:

  ```powershell
  Get-AzureRmResourceGroup -Name ExampleGroup
  Find-AzureRmResource -ResourceGroupNameEquals ExampleGroup
  ```

5. Podczas wdrażania szablonu możesz określić parametry szablonu jako parametry programu PowerShell. Hello wcześniejszego przykładu nie zawiera żadnych parametrów szablonu, aby były używane wartości domyślne hello w szablonie hello. toodeploy magazynu innego konta i podaj wartości parametrów dla prefiksu nazwy hello magazynu i konto magazynu hello jednostka SKU, należy użyć:

  ```powershell
  New-AzureRmResourceGroupDeployment -Name ExampleDeployment2 -ResourceGroupName ExampleGroup -TemplateFile c:\MyTemplates\azuredeploy.json -storageNamePrefix "contoso" -storageSKU "Standard_GRS"
  ```

  Masz teraz dwa konta magazynu w grupie zasobów. 

## <a name="azure-cli"></a>Interfejs wiersza polecenia platformy Azure

1. tooinstall wiersza polecenia platformy Azure, zobacz [zainstalować Azure CLI 2.0](/cli/azure/install-az-cli2).

2. tooquickly wprowadzenie do wdrażania, użyj następującego polecenia hello:

  ```azurecli
  az login
  az account set --subscription {subscription-id}

  az group create --name ExampleGroup --location "Central US"
  az group deployment create --name ExampleDeployment --resource-group ExampleGroup --template-file c:\MyTemplates\azuredeploy.json
  ```

  Witaj `az account set` polecenia jest potrzebne tylko wtedy, jeśli chcesz toouse subskrypcji innych niż domyślne subskrypcji. toosee wszystkie subskrypcje i ich identyfikatorów, należy użyć:

  ```azurecli
  az account list
  ```

3. Witaj wdrożenia może zająć kilka minut toocomplete. Po zakończeniu zostanie wyświetlony komunikat podobny do następującego:

  ```azurecli
  "provisioningState": "Succeeded",
  ```

4. toosee, które były zasobów konta grupy i magazynu wdrożone tooyour subskrypcji, użyj:

  ```azurecli
  az group show --name ExampleGroup
  az resource list --resource-group ExampleGroup
  ```

5. Podczas wdrażania szablonu możesz określić parametry szablonu jako parametry programu PowerShell. Hello wcześniejszego przykładu nie zawiera żadnych parametrów szablonu, aby były używane wartości domyślne hello w szablonie hello. toodeploy magazynu innego konta i podaj wartości parametrów dla prefiksu nazwy hello magazynu i konto magazynu hello jednostka SKU, należy użyć:

  ```azurecli
  az group deployment create --name ExampleDeployment2 --resource-group ExampleGroup --template-file c:\MyTemplates\azuredeploy.json --parameters '{"storageNamePrefix":{"value":"contoso"},"storageSKU":{"value":"Standard_GRS"}}'
  ```

  Masz teraz dwa konta magazynu w grupie zasobów. 

## <a name="example-storage-template"></a>Przykładowy szablon magazynu

Użyj powitania po przykładowy szablon toodeploy subskrypcja tooyour konta magazynu:

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageNamePrefix": {
      "type": "string",
      "maxLength": 11,
      "defaultValue": "storage",
      "metadata": {
        "description": "hello value toouse for starting hello storage account name."
      }
    },
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
    }
  },
  "variables": {
    "storageName": "[concat(parameters('storageNamePrefix'), uniqueString(resourceGroup().id))]"
  },
  "resources": [
    {
      "name": "[variables('storageName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-05-01",
      "sku": {
        "name": "[parameters('storageSKU')]"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {
      }
    }
  ],
  "outputs": {  }
}
```

## <a name="next-steps"></a>Następne kroki

* Aby uzyskać szczegółowe informacje o korzystaniu z programu PowerShell toodeploy szablonów, zobacz [wdrażanie zasobów przy użyciu szablonów usługi Resource Manager i programu Azure PowerShell](/azure/azure-resource-manager/resource-group-template-deploy).
* Aby uzyskać szczegółowe informacje dotyczące korzystania z szablonów toodeploy wiersza polecenia platformy Azure, zobacz [wdrożenie zasobów z szablonami usługi Resource Manager i interfejsu wiersza polecenia Azure](/azure/azure-resource-manager/resource-group-template-deploy-cli).



