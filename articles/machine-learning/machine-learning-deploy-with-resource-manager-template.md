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
# <a name="deploy-machine-learning-workspace-using-azure-resource-manager"></a><span data-ttu-id="04b24-103">Wdrażanie obszaru roboczego usługi Machine Learning przy użyciu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="04b24-103">Deploy Machine Learning Workspace Using Azure Resource Manager</span></span>
## <a name="introduction"></a><span data-ttu-id="04b24-104">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="04b24-104">Introduction</span></span>
<span data-ttu-id="04b24-105">Za pomocą usługi Azure Resource Manager pozwala Szablon wdrożenia czasu, przekazując toodeploy sposób skalowalny połączona składniki z mechanizmu sprawdzania poprawności i spróbuj ponownie.</span><span class="sxs-lookup"><span data-stu-id="04b24-105">Using an Azure Resource Manager deployment template saves you time by giving you a scalable way toodeploy interconnected components with a validation and retry mechanism.</span></span> <span data-ttu-id="04b24-106">tooset zapasowej Azure maszyny Learning w obszary robocze, na przykład należy toofirst skonfigurować konto usługi Azure storage, a następnie wdrożyć obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="04b24-106">tooset up Azure Machine Learning Workspaces, for example, you need toofirst configure an Azure storage account and then deploy your workspace.</span></span> <span data-ttu-id="04b24-107">Wyobraź sobie zrobić to ręcznie setek obszarów roboczych.</span><span class="sxs-lookup"><span data-stu-id="04b24-107">Imagine doing this manually for hundreds of workspaces.</span></span> <span data-ttu-id="04b24-108">Alternatywą łatwiejsze jest toouse toodeploy szablonu usługi Azure Resource Manager obszar roboczy usługi Azure Machine Learning i wszystkie jego zależności.</span><span class="sxs-lookup"><span data-stu-id="04b24-108">An easier alternative is toouse an Azure Resource Manager template toodeploy an Azure Machine Learning Workspace and all its dependencies.</span></span> <span data-ttu-id="04b24-109">W tym artykule przeprowadza użytkownika przez proces ten krok.</span><span class="sxs-lookup"><span data-stu-id="04b24-109">This article takes you through this process step-by-step.</span></span> <span data-ttu-id="04b24-110">Aby uzyskać wszechstronne Omówienie usługi Azure Resource Manager, zobacz [Omówienie usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="04b24-110">For a great overview of Azure Resource Manager, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="step-by-step-create-a-machine-learning-workspace"></a><span data-ttu-id="04b24-111">Krok po kroku: tworzenie obszaru roboczego Machine Learning</span><span class="sxs-lookup"><span data-stu-id="04b24-111">Step-by-step: create a Machine Learning Workspace</span></span>
<span data-ttu-id="04b24-112">Firma Microsoft będzie utworzyć grupy zasobów platformy Azure, a następnie wdrożyć nowe konto magazynu Azure i nowy Azure Machine Learning obszar roboczy za pomocą szablonu usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="04b24-112">We will create an Azure resource group, then deploy a new Azure storage account and a new Azure Machine Learning Workspace using a Resource Manager template.</span></span> <span data-ttu-id="04b24-113">Po zakończeniu wdrażania hello firma Microsoft będzie wydrukować ważne informacje na temat obszarów roboczych hello, które zostały utworzone (hello klucza podstawowego, hello workspaceID i hello adresu URL toohello roboczego).</span><span class="sxs-lookup"><span data-stu-id="04b24-113">Once hello deployment is complete, we will print out important information about hello workspaces that were created (hello primary key, hello workspaceID, and hello URL toohello workspace).</span></span>

### <a name="create-an-azure-resource-manager-template"></a><span data-ttu-id="04b24-114">Tworzenie szablonu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="04b24-114">Create an Azure Resource Manager template</span></span>
<span data-ttu-id="04b24-115">Obszaru roboczego uczenia maszyny wymaga tooit magazynu Azure konta toostore hello połączonego zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="04b24-115">A Machine Learning Workspace requires an Azure storage account toostore hello dataset linked tooit.</span></span>
<span data-ttu-id="04b24-116">Hello następujący szablon używa hello nazwy grupy zasobów hello toogenerate nazwy konta magazynu hello i hello nazwa obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="04b24-116">hello following template uses hello name of hello resource group toogenerate hello storage account name and hello workspace name.</span></span>  <span data-ttu-id="04b24-117">Ponadto użyto nazwy konta magazynu hello jako właściwość podczas tworzenia obszaru roboczego hello.</span><span class="sxs-lookup"><span data-stu-id="04b24-117">It also uses hello storage account name as a property when creating hello workspace.</span></span>

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
<span data-ttu-id="04b24-118">Zapisz ten szablon jako plik mlworkspace.json pod c:\temp\.</span><span class="sxs-lookup"><span data-stu-id="04b24-118">Save this template as mlworkspace.json file under c:\temp\.</span></span>

### <a name="deploy-hello-resource-group-based-on-hello-template"></a><span data-ttu-id="04b24-119">Wdrażanie hello grupy zasobów, na podstawie szablonu hello</span><span class="sxs-lookup"><span data-stu-id="04b24-119">Deploy hello resource group, based on hello template</span></span>
* <span data-ttu-id="04b24-120">Otwórz program PowerShell</span><span class="sxs-lookup"><span data-stu-id="04b24-120">Open PowerShell</span></span>
* <span data-ttu-id="04b24-121">Instalowanie modułów dla usługi Azure Resource Manager i zarządzania usługą Azure</span><span class="sxs-lookup"><span data-stu-id="04b24-121">Install modules for Azure Resource Manager and Azure Service Management</span></span>  

```
# Install hello Azure Resource Manager modules from hello PowerShell Gallery (press “A”)
Install-Module AzureRM -Scope CurrentUser

# Install hello Azure Service Management modules from hello PowerShell Gallery (press “A”)
Install-Module Azure -Scope CurrentUser
```

   <span data-ttu-id="04b24-122">Te kroki, Pobierz i zainstaluj hello modułów niezbędne toocomplete hello pozostałe kroki.</span><span class="sxs-lookup"><span data-stu-id="04b24-122">These steps download and install hello modules necessary toocomplete hello remaining steps.</span></span> <span data-ttu-id="04b24-123">Wymagane tylko toobe wykonywane raz w środowisku hello, gdzie są wykonywane hello poleceń programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="04b24-123">This only needs toobe done once in hello environment where you are executing hello PowerShell commands.</span></span>   

* <span data-ttu-id="04b24-124">Uwierzytelnianie tooAzure</span><span class="sxs-lookup"><span data-stu-id="04b24-124">Authenticate tooAzure</span></span>  

```
# Authenticate (enter your credentials in hello pop-up window)
Add-AzureRmAccount
```
<span data-ttu-id="04b24-125">Ten krok wymaga toobe powtarzany w każdej sesji.</span><span class="sxs-lookup"><span data-stu-id="04b24-125">This step needs toobe repeated for each session.</span></span> <span data-ttu-id="04b24-126">Po uwierzytelnieniu powinna być wyświetlana informacji o subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="04b24-126">Once authenticated, your subscription information should be displayed.</span></span>

![Konto platformy Azure][1]

<span data-ttu-id="04b24-128">Teraz, gdy mamy tooAzure dostępu, można utworzyć grupy zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="04b24-128">Now that we have access tooAzure, we can create hello resource group.</span></span>

* <span data-ttu-id="04b24-129">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="04b24-129">Create a resource group</span></span>

```
$rg = New-AzureRmResourceGroup -Name "uniquenamerequired523" -Location "South Central US"
$rg
```

<span data-ttu-id="04b24-130">Sprawdź, czy grupa zasobów tego hello poprawnie zainicjować obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="04b24-130">Verify that hello resource group is correctly provisioned.</span></span> <span data-ttu-id="04b24-131">**ProvisioningState** powinien być "powiodło się."</span><span class="sxs-lookup"><span data-stu-id="04b24-131">**ProvisioningState** should be “Succeeded.”</span></span>
<span data-ttu-id="04b24-132">Nazwa grupy zasobów Hello jest używany przez toogenerate szablonu hello hello nazwy konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="04b24-132">hello resource group name is used by hello template toogenerate hello storage account name.</span></span> <span data-ttu-id="04b24-133">Nazwa konta magazynu Hello musi należeć do zakresu od 3 do 24 znaków i korzystać tylko cyfry i małe litery.</span><span class="sxs-lookup"><span data-stu-id="04b24-133">hello storage account name must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span></span>

![Grupa zasobów][2]

* <span data-ttu-id="04b24-135">Przy użyciu wdrożenia grupy zasobów hello, Wdróż nowy obszar roboczy Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="04b24-135">Using hello resource group deployment, deploy a new Machine Learning Workspace.</span></span>

```
# Create a Resource Group, TemplateFile is hello location of hello JSON template.
$rgd = New-AzureRmResourceGroupDeployment -Name "demo" -TemplateFile "C:\temp\mlworkspace.json" -ResourceGroupName $rg.ResourceGroupName
```

<span data-ttu-id="04b24-136">Po zakończeniu wdrażania hello jest proste tooaccess właściwości obszaru roboczego hello, wdrożone.</span><span class="sxs-lookup"><span data-stu-id="04b24-136">Once hello deployment is completed, it is straightforward tooaccess properties of hello workspace you deployed.</span></span> <span data-ttu-id="04b24-137">Na przykład można uzyskać dostępu do hello tokenu klucza podstawowego.</span><span class="sxs-lookup"><span data-stu-id="04b24-137">For example, you can access hello Primary Key Token.</span></span>

```
# Access Azure ML Workspace Token after its deployment.
$rgd.Outputs.mlWorkspaceToken.Value
```

<span data-ttu-id="04b24-138">Inny sposób tooretrieve tokenów z istniejącym obszarem roboczym jest hello toouse polecenie Invoke-AzureRmResourceAction.</span><span class="sxs-lookup"><span data-stu-id="04b24-138">Another way tooretrieve tokens of existing workspace is toouse hello Invoke-AzureRmResourceAction command.</span></span> <span data-ttu-id="04b24-139">Można na przykład listy tokenów podstawowych i pomocniczych hello wszystkich obszarów roboczych.</span><span class="sxs-lookup"><span data-stu-id="04b24-139">For example, you can list hello primary and secondary tokens of all workspaces.</span></span>

```  
# List hello primary and secondary tokens of all workspaces
Get-AzureRmResource |? { $_.ResourceType -Like "*MachineLearning/workspaces*"} |% { Invoke-AzureRmResourceAction -ResourceId $_.ResourceId -Action listworkspacekeys -Force}  
```
<span data-ttu-id="04b24-140">Po udostępnieniu hello obszaru roboczego można również zautomatyzować wiele zadań Azure Machine Learning Studio za pomocą hello [modułu programu PowerShell dla usługi Azure Machine Learning](http://aka.ms/amlps).</span><span class="sxs-lookup"><span data-stu-id="04b24-140">After hello workspace is provisioned, you can also automate many Azure Machine Learning Studio tasks using hello [PowerShell Module for Azure Machine Learning](http://aka.ms/amlps).</span></span>

## <a name="next-steps"></a><span data-ttu-id="04b24-141">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="04b24-141">Next Steps</span></span>
* <span data-ttu-id="04b24-142">Dowiedz się więcej o [authoring Azure Resource Manager szablony](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="04b24-142">Learn more about [authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> 
* <span data-ttu-id="04b24-143">Obejrzyj hello [repozytorium szablonów Szybki Start Azure](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="04b24-143">Have a look at hello [Azure Quickstart Templates Repository](https://github.com/Azure/azure-quickstart-templates).</span></span> 
* <span data-ttu-id="04b24-144">Obejrzyj ten film o [usługi Azure Resource Manager](https://channel9.msdn.com/Events/Ignite/2015/C9-39).</span><span class="sxs-lookup"><span data-stu-id="04b24-144">Watch this video about [Azure Resource Manager](https://channel9.msdn.com/Events/Ignite/2015/C9-39).</span></span> 

<!--Image references-->
[1]: ../media/machine-learning-deploy-with-resource-manager-template/azuresubscription.png
[2]: ../media/machine-learning-deploy-with-resource-manager-template/resourcegroupprovisioning.png


<!--Link references-->
