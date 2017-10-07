---
title: "grupy zasobów toomultiple zasobów Azure aaaDeploy | Dokumentacja firmy Microsoft"
description: "Pokazuje, jak tootarget więcej niż jeden zasób Azure grupy podczas wdrażania."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/15/2017
ms.author: tomfitz
ms.openlocfilehash: 93a39a26e0ca18dfcb5c6e8de95c38a64186d6de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-azure-resources-toomore-than-one-resource-group"></a>Wdrażanie zasobów Azure toomore niż jednej grupy zasobów

Zazwyczaj jest wdrażany, wszystkie zasoby hello w grupie pojedynczy zasób tooa szablonu. Istnieją jednak sytuacji, gdy mają razem toodeploy zestaw zasobów, ale umieścić je w różnych grupach zasobów. Na przykład można toodeploy hello kopii zapasowej maszyny wirtualnej dla usługi Azure Site Recovery tooa oddzielnej grupie zasobów i lokalizacji. Menedżer zasobów pozwala toouse zagnieżdżone szablony tootarget różnych grup zasobów niż grupa zasobów hello używane hello nadrzędnego szablonu.

Grupa zasobów Hello jest hello cyklu życia kontener dla aplikacji hello i jego kolekcji zasobów. Utwórz grupę zasobów hello poza hello szablonu, a następnie określ tootarget grupy zasobów hello podczas wdrażania. Wprowadzenie tooresource grup, zobacz [Omówienie usługi Azure Resource Manager](resource-group-overview.md).

## <a name="example-template"></a>Przykład szablonu

tootarget różnych zasobów, w przypadku użycia szablonu zagnieżdżonych lub połączonych podczas wdrażania. Witaj `Microsoft.Resources/deployments` udostępnia typ zasobu `resourceGroup` parametr, który umożliwia toospecify innej grupie zasobów dla hello zagnieżdżone wdrożenia. Wszystkie grupy zasobów hello muszą istnieć przed uruchomieniem hello wdrożenia. Witaj poniższy przykład wdraża dwóch kont magazynu — w grupie zasobów hello określony podczas wdrażania, a druga w grupie zasobów o nazwie `crossResourceGroupDeployment`:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "StorageAccountName1": {
            "type": "string"
        },
        "StorageAccountName2": {
            "type": "string"
        }
    },
    "variables": {},
    "resources": [
        {
            "apiVersion": "2017-05-10",
            "name": "nestedTemplate",
            "type": "Microsoft.Resources/deployments",
            "resourceGroup": "crossResourceGroupDeployment",
            "properties": {
                "mode": "Incremental",
                "template": {
                    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
                    "contentVersion": "1.0.0.0",
                    "parameters": {},
                    "variables": {},
                    "resources": [
                        {
                            "type": "Microsoft.Storage/storageAccounts",
                            "name": "[parameters('StorageAccountName2')]",
                            "apiVersion": "2015-06-15",
                            "location": "West US",
                            "properties": {
                                "accountType": "Standard_LRS"
                            }
                        }
                    ]
                },
                "parameters": {}
            }
        },
        {
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[parameters('StorageAccountName1')]",
            "apiVersion": "2015-06-15",
            "location": "West US",
            "properties": {
                "accountType": "Standard_LRS"
            }
        }
    ]
}
```

Jeśli ustawisz `resourceGroup` toohello Nazwa grupy zasobów, która nie istnieje, wdrożenie hello kończy się niepowodzeniem. Jeśli nie zostanie określona wartość `resourceGroup`, Menedżer zasobów używa hello nadrzędnej grupy zasobów.  

## <a name="deploy-hello-template"></a>Wdrażanie szablonu hello

toodeploy hello przykładowy szablon, można użyć portalu hello, programu Azure PowerShell lub wiersza polecenia platformy Azure. Dla programu Azure PowerShell lub interfejsu wiersza polecenia Azure należy użyć wersji z maja 2017 lub nowszego. Przykłady Hello założono zapisany szablon hello lokalnie jako plik o nazwie **crossrgdeployment.json**.

Dla środowiska PowerShell:

```powershell
Login-AzureRmAccount

New-AzureRmResourceGroup -Name mainResourceGroup -Location "South Central US"
New-AzureRmResourceGroup -Name crossResourceGroupDeployment -Location "Central US"
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName mainResourceGroup `
  -TemplateFile c:\MyTemplates\crossrgdeployment.json
```

Dla platformy Azure interfejsu wiersza polecenia:

```azurecli
az login

az group create --name mainResourceGroup --location "South Central US"
az group create --name crossResourceGroupDeployment --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group mainResourceGroup \
    --template-file crossrgdeployment.json
```

Po zakończeniu wdrażania, zobacz się dwie grupy zasobów. Każda grupa zasobów zawiera konta magazynu.

## <a name="use-resourcegroup-function"></a>Funkcja resourceGroup()

Dla wielu wdrożenia grupy zasobów, hello [funkcja resouceGroup()](resource-group-template-functions-resource.md#resourcegroup) jest rozpoznawana inaczej w zależności od określania hello zagnieżdżonego szablonu. 

Po osadzeniu jeden szablon w innym szablonie resouceGroup() w szablonie zagnieżdżonym hello rozpoznaje toohello nadrzędnej grupy zasobów. Osadzony szablon używa hello następującego formatu:

```json
"apiVersion": "2017-05-10",
"name": "embeddedTemplate",
"type": "Microsoft.Resources/deployments",
"resourceGroup": "crossResourceGroupDeployment",
"properties": {
    "mode": "Incremental",
    "template": {
        ...
        resourceGroup() refers tooparent resource group
    }
}
```

Gdy łącze tooa oddzielnego szablonu, resouceGroup() w szablonie połączonego hello rozpoznaje toohello zagnieżdżonych zasobów grupy. Połączone szablon używa hello następującego formatu:

```json
"apiVersion": "2017-05-10",
"name": "linkedTemplate",
"type": "Microsoft.Resources/deployments",
"resourceGroup": "crossResourceGroupDeployment",
"properties": {
    "mode": "Incremental",
    "templateLink": {
        ...
        resourceGroup() in linked template refers toolinked resource group
    }
}
```

## <a name="next-steps"></a>Następne kroki

* toounderstand toodefine parametry w szablonie, zobacz temat [zrozumieć hello struktury i składni szablonów usługi Azure Resource Manager](resource-group-authoring-templates.md).
* Aby uzyskać wskazówki dotyczące rozwiązania typowych błędów wdrażania, zobacz [Rozwiąż typowe błędy wdrożenia usługi Azure z usługą Azure Resource Manager](resource-manager-common-deployment-errors.md).
* Aby uzyskać informacje o wdrażaniu szablonu, który wymaga tokenu sygnatury dostępu Współdzielonego, zobacz [wdrażanie szablonu prywatnej przy użyciu tokenu sygnatury dostępu Współdzielonego](resource-manager-powershell-sas-token.md).
