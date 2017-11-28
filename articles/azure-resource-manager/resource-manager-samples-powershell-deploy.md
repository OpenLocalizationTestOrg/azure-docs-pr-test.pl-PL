---
title: "aaaAzure przykładowy skrypt programu PowerShell — wdrażanie szablonu | Dokumentacja firmy Microsoft"
description: "Przykładowy skrypt do wdrażania szablonu usługi Azure Resource Manager."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: tomfitz
ms.openlocfilehash: 536b8ccecad4ed8a4c4a4139c6bf4600e2eb9405
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-manager-template-deployment---powershell-script"></a><span data-ttu-id="a2c8f-103">Wdrożenie szablonu usługi Resource Manager Azure — skrypt programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="a2c8f-103">Azure Resource Manager template deployment - PowerShell script</span></span>

<span data-ttu-id="a2c8f-104">Ten skrypt wdraża grupy zasobów tooa szablonu usługi Resource Manager w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="a2c8f-104">This script deploys a Resource Manager template tooa resource group in your subscription.</span></span>

[!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="a2c8f-105">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="a2c8f-105">Sample script</span></span>

```powershell
<#
 .SYNOPSIS
    Deploys a template tooAzure

 .DESCRIPTION
    Deploys an Azure Resource Manager template
#>

param (
    [Parameter(Mandatory)]
    #hello subscription id where hello template will be deployed.
    [string]$SubscriptionId,  

    [Parameter(Mandatory)]
    #hello resource group where hello template will be deployed. Can be hello name of an existing or a new resource group.
    [string]$ResourceGroupName, 

    #Optional, a resource group location. If specified, will try toocreate a new resource group in this location. If not specified, assumes resource group is existing.
    [string]$ResourceGroupLocation, 

    #hello deployment name.
    [Parameter(Mandatory)]
    [string]$DeploymentName,    

    #Path toohello template file. Defaults tootemplate.json.
    [string]$TemplateFilePath = "template.json",  

    #Path toohello parameters file. Defaults tooparameters.json. If file is not found, will prompt for parameter values based on template.
    [string]$ParametersFilePath = "parameters.json"
)

$ErrorActionPreference = "Stop"

# Login tooAzure and select subscription
Write-Output "Logging in"
Login-AzureRmAccount
Write-Output "Selecting subscription '$SubscriptionId'"
Select-AzureRmSubscription -SubscriptionID $SubscriptionId

# Create or check for existing resource group
$resourceGroup = Get-AzureRmResourceGroup -Name $ResourceGroupName -ErrorAction SilentlyContinue
if ( -not $ResourceGroup ) {
    Write-Output "Could not find resource group '$ResourceGroupName' - will create it"
    if ( -not $ResourceGroupLocation ) {
        $ResourceGroupLocation = Read-Host -Prompt 'Enter location for resource group'
    }
    Write-Output "Creating resource group '$ResourceGroupName' in location '$ResourceGroupLocation'"
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $resourceGroupLocation
}
else {
    Write-Output "Using existing resource group '$ResourceGroupName'"
}

# Start hello deployment
Write-Output "Starting deployment"
if ( Test-Path $ParametersFilePath ) {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $ResourceGroupName -TemplateFile $TemplateFilePath -TemplateParameterFile $ParametersFilePath
}
else {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $ResourceGroupName -TemplateFile $TemplateFilePath
}
``` 

## <a name="clean-up-deployment"></a><span data-ttu-id="a2c8f-106">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="a2c8f-106">Clean up deployment</span></span> 

<span data-ttu-id="a2c8f-107">Hello uruchom następujące polecenie, grupy zasobów hello tooremove i wszystkie jego zasoby.</span><span class="sxs-lookup"><span data-stu-id="a2c8f-107">Run hello following command tooremove hello resource group and all its resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="a2c8f-108">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="a2c8f-108">Script explanation</span></span>

<span data-ttu-id="a2c8f-109">Ten skrypt używa hello następujące polecenia toocreate hello wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="a2c8f-109">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="a2c8f-110">Każdy element w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="a2c8f-110">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="a2c8f-111">Polecenie</span><span class="sxs-lookup"><span data-stu-id="a2c8f-111">Command</span></span> | <span data-ttu-id="a2c8f-112">Uwagi</span><span class="sxs-lookup"><span data-stu-id="a2c8f-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a2c8f-113">Rejestr AzureRmResourceProvider</span><span class="sxs-lookup"><span data-stu-id="a2c8f-113">Register-AzureRmResourceProvider</span></span>](/powershell/module/azurerm.resources/register-azurermresourceprovider) | <span data-ttu-id="a2c8f-114">Rejestruje dostawcę zasobów, jego typy zasobów mogą być wdrożone tooyour subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="a2c8f-114">Registers a resource provider so its resource types can be deployed tooyour subscription.</span></span>  |
| [<span data-ttu-id="a2c8f-115">Get-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a2c8f-115">Get-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/get-azurermresourcegroup) | <span data-ttu-id="a2c8f-116">Pobiera grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="a2c8f-116">Gets resource groups.</span></span>  |
| [<span data-ttu-id="a2c8f-117">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a2c8f-117">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="a2c8f-118">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="a2c8f-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a2c8f-119">Nowe AzureRmResourceGroupDeployment</span><span class="sxs-lookup"><span data-stu-id="a2c8f-119">New-AzureRmResourceGroupDeployment</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) | <span data-ttu-id="a2c8f-120">Dodaje grupę zasobów tooa wdrożenia usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="a2c8f-120">Adds an Azure deployment tooa resource group.</span></span>  |
| [<span data-ttu-id="a2c8f-121">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a2c8f-121">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="a2c8f-122">Usuwa grupę zasobów i wszystkie zasoby zawarte w ciągu.</span><span class="sxs-lookup"><span data-stu-id="a2c8f-122">Removes a resource group and all resources contained within.</span></span> |



## <a name="next-steps"></a><span data-ttu-id="a2c8f-123">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a2c8f-123">Next steps</span></span>
* <span data-ttu-id="a2c8f-124">Wprowadzenie toodeploying szablonów, zobacz [wdrażanie zasobów przy użyciu szablonów usługi Resource Manager i programu Azure PowerShell](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="a2c8f-124">For an introduction toodeploying templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="a2c8f-125">Aby uzyskać informacje o wdrażaniu szablonu, który wymaga tokenu sygnatury dostępu Współdzielonego, zobacz [wdrażanie szablonu prywatnej przy użyciu tokenu sygnatury dostępu Współdzielonego](resource-manager-powershell-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="a2c8f-125">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>
* <span data-ttu-id="a2c8f-126">Parametry toodefine w szablonie, zobacz [tworzenia szablonów](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="a2c8f-126">toodefine parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="a2c8f-127">Aby uzyskać wskazówki dotyczące użycia tooeffectively Menedżera zasobów przedsiębiorstwa Zarządzaj subskrypcjami, zobacz [szkieletu Azure enterprise — ładu przetestowanego subskrypcji](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="a2c8f-127">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

