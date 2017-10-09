---
title: "aaaDeploy obszaru roboczego usługi Machine Learning z usługą Azure Resource Manager | Dokumentacja firmy Microsoft"
description: "Jak toodeploy obszaru roboczego dla usługi Azure Machine Learning przy użyciu szablonu usługi Azure Resource Manager"
services: machine-learning
documentationcenter: 
author: ahgyger
manager: haining
editor: garye
ms.assetid: 4955ac4d-ff99-4908-aa27-69b6bfcc8e85
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/15/2017
ms.author: ahgyger
ms.openlocfilehash: 308959825bcbd670f6ce9b6dc381be767f172357
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-machine-learning-workspace-using-azure-resource-manager"></a>Wdrażanie obszaru roboczego usługi Machine Learning przy użyciu usługi Azure Resource Manager
## <a name="introduction"></a>Wprowadzenie
Za pomocą usługi Azure Resource Manager pozwala Szablon wdrożenia czasu, przekazując toodeploy sposób skalowalny połączona składniki z mechanizmu sprawdzania poprawności i spróbuj ponownie. tooset zapasowej Azure maszyny Learning w obszary robocze, na przykład należy toofirst skonfigurować konto usługi Azure storage, a następnie wdrożyć obszaru roboczego. Wyobraź sobie zrobić to ręcznie setek obszarów roboczych. Alternatywą łatwiejsze jest toouse toodeploy szablonu usługi Azure Resource Manager obszar roboczy usługi Azure Machine Learning i wszystkie jego zależności. W tym artykule przeprowadza użytkownika przez proces ten krok. Aby uzyskać wszechstronne Omówienie usługi Azure Resource Manager, zobacz [Omówienie usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).

## <a name="step-by-step-create-a-machine-learning-workspace"></a>Krok po kroku: tworzenie obszaru roboczego Machine Learning
Firma Microsoft będzie utworzyć grupy zasobów platformy Azure, a następnie wdrożyć nowe konto magazynu Azure i nowy Azure Machine Learning obszar roboczy za pomocą szablonu usługi Resource Manager. Po zakończeniu wdrażania hello firma Microsoft będzie wydrukować ważne informacje na temat obszarów roboczych hello, które zostały utworzone (hello klucza podstawowego, hello workspaceID i hello adresu URL toohello roboczego).

### <a name="create-an-azure-resource-manager-template"></a>Tworzenie szablonu usługi Azure Resource Manager
Obszaru roboczego uczenia maszyny wymaga tooit magazynu Azure konta toostore hello połączonego zestawu danych.
Hello następujący szablon używa hello nazwy grupy zasobów hello toogenerate nazwy konta magazynu hello i hello nazwa obszaru roboczego.  Ponadto użyto nazwy konta magazynu hello jako właściwość podczas tworzenia obszaru roboczego hello.

```
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "variables": {
        "namePrefix": "[resourceGroup().name]",
        "location": "[resourceGroup().location]",
        "mlVersion": "2016-04-01",
        "stgVersion": "2015-06-15",
        "storageAccountName": "[concat(variables('namePrefix'),'stg')]",
        "mlWorkspaceName": "[concat(variables('namePrefix'),'mlwk')]",
        "mlResourceId": "[resourceId('Microsoft.MachineLearning/workspaces', variables('mlWorkspaceName'))]",
        "stgResourceId": "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]",
        "storageAccountType": "Standard_LRS"
    },
    "resources": [
        {
            "apiVersion": "[variables('stgVersion')]",
            "name": "[variables('storageAccountName')]",
            "type": "Microsoft.Storage/storageAccounts",
            "location": "[variables('location')]",
            "properties": {
                "accountType": "[variables('storageAccountType')]"
            }
        },
        {
            "apiVersion": "[variables('mlVersion')]",
            "type": "Microsoft.MachineLearning/workspaces",
            "name": "[variables('mlWorkspaceName')]",
            "location": "[variables('location')]",
            "dependsOn": ["[variables('stgResourceId')]"],
            "properties": {
                "UserStorageAccountId": "[variables('stgResourceId')]"
            }
        }
    ],
    "outputs": {
        "mlWorkspaceObject": {"type": "object", "value": "[reference(variables('mlResourceId'), variables('mlVersion'))]"},
        "mlWorkspaceToken": {"type": "string", "value": "[listWorkspaceKeys(variables('mlResourceId'), variables('mlVersion')).primaryToken]"},
        "mlWorkspaceWorkspaceID": {"type": "string", "value": "[reference(variables('mlResourceId'), variables('mlVersion')).WorkspaceId]"},
        "mlWorkspaceWorkspaceLink": {"type": "string", "value": "[concat('https://studio.azureml.net/Home/ViewWorkspace/', reference(variables('mlResourceId'), variables('mlVersion')).WorkspaceId)]"}
    }
}

```
Zapisz ten szablon jako plik mlworkspace.json pod c:\temp\.

### <a name="deploy-hello-resource-group-based-on-hello-template"></a>Wdrażanie hello grupy zasobów, na podstawie szablonu hello
* Otwórz program PowerShell
* Instalowanie modułów dla usługi Azure Resource Manager i zarządzania usługą Azure  

```
# Install hello Azure Resource Manager modules from hello PowerShell Gallery (press “A”)
Install-Module AzureRM -Scope CurrentUser

# Install hello Azure Service Management modules from hello PowerShell Gallery (press “A”)
Install-Module Azure -Scope CurrentUser
```

   Te kroki, Pobierz i zainstaluj hello modułów niezbędne toocomplete hello pozostałe kroki. Wymagane tylko toobe wykonywane raz w środowisku hello, gdzie są wykonywane hello poleceń programu PowerShell.   

* Uwierzytelnianie tooAzure  

```
# Authenticate (enter your credentials in hello pop-up window)
Add-AzureRmAccount
```
Ten krok wymaga toobe powtarzany w każdej sesji. Po uwierzytelnieniu powinna być wyświetlana informacji o subskrypcji.

![Konto platformy Azure][1]

Teraz, gdy mamy tooAzure dostępu, można utworzyć grupy zasobów hello.

* Tworzenie grupy zasobów

```
$rg = New-AzureRmResourceGroup -Name "uniquenamerequired523" -Location "South Central US"
$rg
```

Sprawdź, czy grupa zasobów tego hello poprawnie zainicjować obsługi administracyjnej. **ProvisioningState** powinien być "powiodło się."
Nazwa grupy zasobów Hello jest używany przez toogenerate szablonu hello hello nazwy konta magazynu. Nazwa konta magazynu Hello musi należeć do zakresu od 3 do 24 znaków i korzystać tylko cyfry i małe litery.

![Grupa zasobów][2]

* Przy użyciu wdrożenia grupy zasobów hello, Wdróż nowy obszar roboczy Machine Learning.

```
# Create a Resource Group, TemplateFile is hello location of hello JSON template.
$rgd = New-AzureRmResourceGroupDeployment -Name "demo" -TemplateFile "C:\temp\mlworkspace.json" -ResourceGroupName $rg.ResourceGroupName
```

Po zakończeniu wdrażania hello jest proste tooaccess właściwości obszaru roboczego hello, wdrożone. Na przykład można uzyskać dostępu do hello tokenu klucza podstawowego.

```
# Access Azure ML Workspace Token after its deployment.
$rgd.Outputs.mlWorkspaceToken.Value
```

Inny sposób tooretrieve tokenów z istniejącym obszarem roboczym jest hello toouse polecenie Invoke-AzureRmResourceAction. Można na przykład listy tokenów podstawowych i pomocniczych hello wszystkich obszarów roboczych.

```  
# List hello primary and secondary tokens of all workspaces
Get-AzureRmResource |? { $_.ResourceType -Like "*MachineLearning/workspaces*"} |% { Invoke-AzureRmResourceAction -ResourceId $_.ResourceId -Action listworkspacekeys -Force}  
```
Po udostępnieniu hello obszaru roboczego można również zautomatyzować wiele zadań Azure Machine Learning Studio za pomocą hello [modułu programu PowerShell dla usługi Azure Machine Learning](http://aka.ms/amlps).

## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o [authoring Azure Resource Manager szablony](../azure-resource-manager/resource-group-authoring-templates.md). 
* Obejrzyj hello [repozytorium szablonów Szybki Start Azure](https://github.com/Azure/azure-quickstart-templates). 
* Obejrzyj ten film o [usługi Azure Resource Manager](https://channel9.msdn.com/Events/Ignite/2015/C9-39). 

<!--Image references-->
[1]: ../media/machine-learning-deploy-with-resource-manager-template/azuresubscription.png
[2]: ../media/machine-learning-deploy-with-resource-manager-template/resourcegroupprovisioning.png


<!--Link references-->
