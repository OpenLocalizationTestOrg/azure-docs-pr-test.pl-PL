---
title: "Wdrażanie obszaru roboczego usługi Machine Learning z usługą Azure Resource Manager | Dokumentacja firmy Microsoft"
description: "Jak wdrożyć obszaru roboczego dla usługi Azure Machine Learning przy użyciu szablonu usługi Azure Resource Manager"
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
ms.openlocfilehash: 9e37780428b0867da63987ec4f7f843a8abeb907
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-machine-learning-workspace-using-azure-resource-manager"></a><span data-ttu-id="c1c7e-103">Wdrażanie obszaru roboczego usługi Machine Learning przy użyciu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c1c7e-103">Deploy Machine Learning Workspace Using Azure Resource Manager</span></span>
## <a name="introduction"></a><span data-ttu-id="c1c7e-104">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="c1c7e-104">Introduction</span></span>
<span data-ttu-id="c1c7e-105">Za pomocą usługi Azure Resource Manager Szablon wdrożenia zapisuje czas, zapewniając skalowalne sposób wdrażania składników połączonych ze sprawdzaniem poprawności, a następnie spróbuj ponownie mechanizmu.</span><span class="sxs-lookup"><span data-stu-id="c1c7e-105">Using an Azure Resource Manager deployment template saves you time by giving you a scalable way to deploy interconnected components with a validation and retry mechanism.</span></span> <span data-ttu-id="c1c7e-106">Aby konfigurowanie obszarów roboczych do programu Azure Machine Learning, na przykład, należy najpierw skonfigurować konto usługi Azure storage, a następnie wdrożyć obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="c1c7e-106">To set up Azure Machine Learning Workspaces, for example, you need to first configure an Azure storage account and then deploy your workspace.</span></span> <span data-ttu-id="c1c7e-107">Wyobraź sobie zrobić to ręcznie setek obszarów roboczych.</span><span class="sxs-lookup"><span data-stu-id="c1c7e-107">Imagine doing this manually for hundreds of workspaces.</span></span> <span data-ttu-id="c1c7e-108">Łatwiejsze zamiast jest szablon usługi Azure Resource Manager umożliwia wdrażanie obszar roboczy usługi Azure Machine Learning i jego zależności.</span><span class="sxs-lookup"><span data-stu-id="c1c7e-108">An easier alternative is to use an Azure Resource Manager template to deploy an Azure Machine Learning Workspace and all its dependencies.</span></span> <span data-ttu-id="c1c7e-109">W tym artykule przeprowadza użytkownika przez proces ten krok.</span><span class="sxs-lookup"><span data-stu-id="c1c7e-109">This article takes you through this process step-by-step.</span></span> <span data-ttu-id="c1c7e-110">Aby uzyskać wszechstronne Omówienie usługi Azure Resource Manager, zobacz [Omówienie usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c1c7e-110">For a great overview of Azure Resource Manager, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="step-by-step-create-a-machine-learning-workspace"></a><span data-ttu-id="c1c7e-111">Krok po kroku: tworzenie obszaru roboczego Machine Learning</span><span class="sxs-lookup"><span data-stu-id="c1c7e-111">Step-by-step: create a Machine Learning Workspace</span></span>
<span data-ttu-id="c1c7e-112">Firma Microsoft będzie utworzyć grupy zasobów platformy Azure, a następnie wdrożyć nowe konto magazynu Azure i nowy Azure Machine Learning obszar roboczy za pomocą szablonu usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c1c7e-112">We will create an Azure resource group, then deploy a new Azure storage account and a new Azure Machine Learning Workspace using a Resource Manager template.</span></span> <span data-ttu-id="c1c7e-113">Po zakończeniu wdrażania, firma Microsoft będzie drukować ważne informacje na temat obszarów roboczych, które zostały utworzone (klucz podstawowy, workspaceID i adres URL do obszaru roboczego).</span><span class="sxs-lookup"><span data-stu-id="c1c7e-113">Once the deployment is complete, we will print out important information about the workspaces that were created (the primary key, the workspaceID, and the URL to the workspace).</span></span>

### <a name="create-an-azure-resource-manager-template"></a><span data-ttu-id="c1c7e-114">Tworzenie szablonu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c1c7e-114">Create an Azure Resource Manager template</span></span>
<span data-ttu-id="c1c7e-115">Obszaru roboczego uczenia maszyny wymaga konta magazynu Azure do przechowywania zestawu danych z nim połączone.</span><span class="sxs-lookup"><span data-stu-id="c1c7e-115">A Machine Learning Workspace requires an Azure storage account to store the dataset linked to it.</span></span>
<span data-ttu-id="c1c7e-116">Następujący szablon użyje nazwy grupy zasobów można wygenerować nazwy konta magazynu i nazwa obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="c1c7e-116">The following template uses the name of the resource group to generate the storage account name and the workspace name.</span></span>  <span data-ttu-id="c1c7e-117">Ponadto użyto nazwy konta magazynu jako właściwość podczas tworzenia obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="c1c7e-117">It also uses the storage account name as a property when creating the workspace.</span></span>

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
<span data-ttu-id="c1c7e-118">Zapisz ten szablon jako plik mlworkspace.json pod c:\temp\.</span><span class="sxs-lookup"><span data-stu-id="c1c7e-118">Save this template as mlworkspace.json file under c:\temp\.</span></span>

### <a name="deploy-the-resource-group-based-on-the-template"></a><span data-ttu-id="c1c7e-119">Wdrożenie grupy zasobów, na podstawie szablonu</span><span class="sxs-lookup"><span data-stu-id="c1c7e-119">Deploy the resource group, based on the template</span></span>
* <span data-ttu-id="c1c7e-120">Otwórz program PowerShell</span><span class="sxs-lookup"><span data-stu-id="c1c7e-120">Open PowerShell</span></span>
* <span data-ttu-id="c1c7e-121">Instalowanie modułów dla usługi Azure Resource Manager i zarządzania usługą Azure</span><span class="sxs-lookup"><span data-stu-id="c1c7e-121">Install modules for Azure Resource Manager and Azure Service Management</span></span>  

```
# Install the Azure Resource Manager modules from the PowerShell Gallery (press “A”)
Install-Module AzureRM -Scope CurrentUser

# Install the Azure Service Management modules from the PowerShell Gallery (press “A”)
Install-Module Azure -Scope CurrentUser
```

   <span data-ttu-id="c1c7e-122">Te kroki, Pobierz i zainstaluj moduły, które należy wykonać pozostałe etapy.</span><span class="sxs-lookup"><span data-stu-id="c1c7e-122">These steps download and install the modules necessary to complete the remaining steps.</span></span> <span data-ttu-id="c1c7e-123">To tylko musi odbywać się raz w środowisku, w którym są wykonywane poleceń programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c1c7e-123">This only needs to be done once in the environment where you are executing the PowerShell commands.</span></span>   

* <span data-ttu-id="c1c7e-124">Uwierzytelnianie na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="c1c7e-124">Authenticate to Azure</span></span>  

```
# Authenticate (enter your credentials in the pop-up window)
Add-AzureRmAccount
```
<span data-ttu-id="c1c7e-125">Ten krok należy powtórzyć dla każdej sesji.</span><span class="sxs-lookup"><span data-stu-id="c1c7e-125">This step needs to be repeated for each session.</span></span> <span data-ttu-id="c1c7e-126">Po uwierzytelnieniu powinna być wyświetlana informacji o subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="c1c7e-126">Once authenticated, your subscription information should be displayed.</span></span>

![Konto platformy Azure][1]

<span data-ttu-id="c1c7e-128">Teraz, gdy będziemy mieć dostęp do platformy Azure, można utworzyć grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="c1c7e-128">Now that we have access to Azure, we can create the resource group.</span></span>

* <span data-ttu-id="c1c7e-129">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="c1c7e-129">Create a resource group</span></span>

```
$rg = New-AzureRmResourceGroup -Name "uniquenamerequired523" -Location "South Central US"
$rg
```

<span data-ttu-id="c1c7e-130">Upewnij się, że grupa zasobów jest poprawnie zainicjowane.</span><span class="sxs-lookup"><span data-stu-id="c1c7e-130">Verify that the resource group is correctly provisioned.</span></span> <span data-ttu-id="c1c7e-131">**ProvisioningState** powinien być "powiodło się."</span><span class="sxs-lookup"><span data-stu-id="c1c7e-131">**ProvisioningState** should be “Succeeded.”</span></span>
<span data-ttu-id="c1c7e-132">Nazwa grupy zasobów jest używany przez szablon można wygenerować nazwy konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="c1c7e-132">The resource group name is used by the template to generate the storage account name.</span></span> <span data-ttu-id="c1c7e-133">Nazwa konta magazynu musi należeć do zakresu od 3 do 24 znaków i korzystać tylko cyfry i małe litery.</span><span class="sxs-lookup"><span data-stu-id="c1c7e-133">The storage account name must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span></span>

![Grupa zasobów][2]

* <span data-ttu-id="c1c7e-135">Przy użyciu wdrożenia grupy zasobów, Wdróż nowy obszar roboczy Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="c1c7e-135">Using the resource group deployment, deploy a new Machine Learning Workspace.</span></span>

```
# Create a Resource Group, TemplateFile is the location of the JSON template.
$rgd = New-AzureRmResourceGroupDeployment -Name "demo" -TemplateFile "C:\temp\mlworkspace.json" -ResourceGroupName $rg.ResourceGroupName
```

<span data-ttu-id="c1c7e-136">Po zakończeniu wdrożenia jest prosta do dostępu do właściwości obszaru roboczego wdrożone.</span><span class="sxs-lookup"><span data-stu-id="c1c7e-136">Once the deployment is completed, it is straightforward to access properties of the workspace you deployed.</span></span> <span data-ttu-id="c1c7e-137">Na przykład możesz uzyskać dostęp podstawowego tokenu klucza.</span><span class="sxs-lookup"><span data-stu-id="c1c7e-137">For example, you can access the Primary Key Token.</span></span>

```
# Access Azure ML Workspace Token after its deployment.
$rgd.Outputs.mlWorkspaceToken.Value
```

<span data-ttu-id="c1c7e-138">Innym sposobem na pobranie tokenów z istniejącym obszarem roboczym jest Użyj polecenia Invoke-AzureRmResourceAction.</span><span class="sxs-lookup"><span data-stu-id="c1c7e-138">Another way to retrieve tokens of existing workspace is to use the Invoke-AzureRmResourceAction command.</span></span> <span data-ttu-id="c1c7e-139">Na przykład można wyświetlić listę głównych i dodatkowych tokenów wszystkich obszarów roboczych.</span><span class="sxs-lookup"><span data-stu-id="c1c7e-139">For example, you can list the primary and secondary tokens of all workspaces.</span></span>

```  
# List the primary and secondary tokens of all workspaces
Get-AzureRmResource |? { $_.ResourceType -Like "*MachineLearning/workspaces*"} |% { Invoke-AzureRmResourceAction -ResourceId $_.ResourceId -Action listworkspacekeys -Force}  
```
<span data-ttu-id="c1c7e-140">Po udostępnieniu obszaru roboczego można również zautomatyzować wiele zadań Azure Machine Learning Studio za pomocą [modułu programu PowerShell dla usługi Azure Machine Learning](http://aka.ms/amlps).</span><span class="sxs-lookup"><span data-stu-id="c1c7e-140">After the workspace is provisioned, you can also automate many Azure Machine Learning Studio tasks using the [PowerShell Module for Azure Machine Learning](http://aka.ms/amlps).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c1c7e-141">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c1c7e-141">Next Steps</span></span>
* <span data-ttu-id="c1c7e-142">Dowiedz się więcej o [authoring Azure Resource Manager szablony](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="c1c7e-142">Learn more about [authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> 
* <span data-ttu-id="c1c7e-143">Obejrzyj [repozytorium szablonów Szybki Start Azure](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="c1c7e-143">Have a look at the [Azure Quickstart Templates Repository](https://github.com/Azure/azure-quickstart-templates).</span></span> 
* <span data-ttu-id="c1c7e-144">Obejrzyj ten film o [usługi Azure Resource Manager](https://channel9.msdn.com/Events/Ignite/2015/C9-39).</span><span class="sxs-lookup"><span data-stu-id="c1c7e-144">Watch this video about [Azure Resource Manager](https://channel9.msdn.com/Events/Ignite/2015/C9-39).</span></span> 

<!--Image references-->
[1]: ../media/machine-learning-deploy-with-resource-manager-template/azuresubscription.png
[2]: ../media/machine-learning-deploy-with-resource-manager-template/resourcegroupprovisioning.png


<!--Link references-->
