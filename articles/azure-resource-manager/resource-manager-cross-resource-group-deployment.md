---
title: "Wdrażanie zasobów platformy Azure do wielu grup zasobów | Dokumentacja firmy Microsoft"
description: "Pokazuje, jak docelowy kilku grup zasobów platformy Azure podczas wdrażania."
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
ms.openlocfilehash: d8b041213b269775175a810e585103d3c538557f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-azure-resources-to-more-than-one-resource-group"></a><span data-ttu-id="0dc97-103">Wdrażanie zasobów platformy Azure do więcej niż jednej grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="0dc97-103">Deploy Azure resources to more than one resource group</span></span>

<span data-ttu-id="0dc97-104">Zazwyczaj jest wdrażany, wszystkie zasoby w szablonie do pojedynczej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="0dc97-104">Typically, you deploy all the resources in your template to a single resource group.</span></span> <span data-ttu-id="0dc97-105">Istnieją jednak scenariuszy, w której chcesz wdrożyć razem zestaw zasobów, ale umieścić je w różnych grupach zasobów.</span><span class="sxs-lookup"><span data-stu-id="0dc97-105">However, there are scenarios where you want to deploy a set of resources together but place them in different resource groups.</span></span> <span data-ttu-id="0dc97-106">Na przykład możesz wdrażanie kopii zapasowej maszyny wirtualnej dla usługi Azure Site Recovery na oddzielnej grupie zasobów i lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="0dc97-106">For example, you may want to deploy the backup virtual machine for Azure Site Recovery to a separate resource group and location.</span></span> <span data-ttu-id="0dc97-107">Menedżer zasobów pozwala na użycie zagnieżdżone szablony pod kątem różnych grup zasobów niż grupa zasobów używany do szablonu nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="0dc97-107">Resource Manager enables you to use nested templates to target different resource groups than the resource group used for the parent template.</span></span>

<span data-ttu-id="0dc97-108">Grupa zasobów to kontener cyklem życia aplikacji i jej kolekcji zasobów.</span><span class="sxs-lookup"><span data-stu-id="0dc97-108">The resource group is the lifecycle container for the application and its collection of resources.</span></span> <span data-ttu-id="0dc97-109">Utwórz grupę zasobów poza szablon i określ grupę zasobów do docelowego podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="0dc97-109">You create the resource group outside of the template, and specify the resource group to target during deployment.</span></span> <span data-ttu-id="0dc97-110">Aby obejrzeć wprowadzenie do grup zasobów, zobacz [Omówienie usługi Azure Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0dc97-110">For an introduction to resource groups, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

## <a name="example-template"></a><span data-ttu-id="0dc97-111">Przykład szablonu</span><span class="sxs-lookup"><span data-stu-id="0dc97-111">Example template</span></span>

<span data-ttu-id="0dc97-112">Aby inny zasób docelowy, należy użyć szablonu zagnieżdżonych lub połączonych podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="0dc97-112">To target a different resource, you must use a nested or linked template during deployment.</span></span> <span data-ttu-id="0dc97-113">`Microsoft.Resources/deployments` Udostępnia typ zasobu `resourceGroup` parametr, który umożliwia określenie innej grupie zasobów dla wdrożenia zagnieżdżonego.</span><span class="sxs-lookup"><span data-stu-id="0dc97-113">The `Microsoft.Resources/deployments` resource type provides a `resourceGroup` parameter that enables you to specify a different resource group for the nested deployment.</span></span> <span data-ttu-id="0dc97-114">Wszystkie grupy zasobów musi istnieć przed uruchomieniem wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="0dc97-114">All the resource groups must exist before running the deployment.</span></span> <span data-ttu-id="0dc97-115">Poniższy przykład wdraża dwóch kont magazynu — w grupie zasobów określony podczas wdrażania, a druga w grupie zasobów o nazwie `crossResourceGroupDeployment`:</span><span class="sxs-lookup"><span data-stu-id="0dc97-115">The following example deploys two storage accounts - one in the resource group specified during deployment, and one in a resource group named `crossResourceGroupDeployment`:</span></span>

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

<span data-ttu-id="0dc97-116">Jeśli ustawisz `resourceGroup` Nazwa grupy zasobów, która nie istnieje, wdrożenie zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="0dc97-116">If you set `resourceGroup` to the name of a resource group that does not exist, the deployment fails.</span></span> <span data-ttu-id="0dc97-117">Jeśli nie zostanie określona wartość `resourceGroup`, Resource Manager korzysta z nadrzędnej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="0dc97-117">If you do not provide a value for `resourceGroup`, Resource Manager uses the parent resource group.</span></span>  

## <a name="deploy-the-template"></a><span data-ttu-id="0dc97-118">Wdrożenie szablonu</span><span class="sxs-lookup"><span data-stu-id="0dc97-118">Deploy the template</span></span>

<span data-ttu-id="0dc97-119">Aby wdrożyć szablon przykładzie, można użyć portalu, programu Azure PowerShell lub wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0dc97-119">To deploy the example template, you can use the portal, Azure PowerShell, or Azure CLI.</span></span> <span data-ttu-id="0dc97-120">Dla programu Azure PowerShell lub interfejsu wiersza polecenia Azure należy użyć wersji z maja 2017 lub nowszego.</span><span class="sxs-lookup"><span data-stu-id="0dc97-120">For Azure PowerShell or Azure CLI, you must use a release from May 2017 or later.</span></span> <span data-ttu-id="0dc97-121">Przykłady założono zapisany szablon lokalnie jako plik o nazwie **crossrgdeployment.json**.</span><span class="sxs-lookup"><span data-stu-id="0dc97-121">The examples assume you have saved the template locally as a file named **crossrgdeployment.json**.</span></span>

<span data-ttu-id="0dc97-122">Dla środowiska PowerShell:</span><span class="sxs-lookup"><span data-stu-id="0dc97-122">For PowerShell:</span></span>

```powershell
Login-AzureRmAccount

New-AzureRmResourceGroup -Name mainResourceGroup -Location "South Central US"
New-AzureRmResourceGroup -Name crossResourceGroupDeployment -Location "Central US"
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName mainResourceGroup `
  -TemplateFile c:\MyTemplates\crossrgdeployment.json
```

<span data-ttu-id="0dc97-123">Dla platformy Azure interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="0dc97-123">For Azure CLI:</span></span>

```azurecli
az login

az group create --name mainResourceGroup --location "South Central US"
az group create --name crossResourceGroupDeployment --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group mainResourceGroup \
    --template-file crossrgdeployment.json
```

<span data-ttu-id="0dc97-124">Po zakończeniu wdrażania, zobacz się dwie grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="0dc97-124">After deployment completes, you see two resource groups.</span></span> <span data-ttu-id="0dc97-125">Każda grupa zasobów zawiera konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="0dc97-125">Each resource group contains a storage account.</span></span>

## <a name="use-resourcegroup-function"></a><span data-ttu-id="0dc97-126">Funkcja resourceGroup()</span><span class="sxs-lookup"><span data-stu-id="0dc97-126">Use resourceGroup() function</span></span>

<span data-ttu-id="0dc97-127">Dla wielu wdrożenia grupy zasobów, [funkcja resouceGroup()](resource-group-template-functions-resource.md#resourcegroup) jest rozpoznawana inaczej w zależności od określania szablon zagnieżdżony.</span><span class="sxs-lookup"><span data-stu-id="0dc97-127">For cross resource group deployments, the [resouceGroup() function](resource-group-template-functions-resource.md#resourcegroup) resolves differently based on how you specify the nested template.</span></span> 

<span data-ttu-id="0dc97-128">Po osadzeniu jeden szablon w innym szablonie resouceGroup() w szablonie zagnieżdżonym rozpoznaje w nadrzędnej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="0dc97-128">If you embed one template within another template, resouceGroup() in the nested template resolves to the parent resource group.</span></span> <span data-ttu-id="0dc97-129">Osadzony szablonu używany następujący format:</span><span class="sxs-lookup"><span data-stu-id="0dc97-129">An embedded template uses the following format:</span></span>

```json
"apiVersion": "2017-05-10",
"name": "embeddedTemplate",
"type": "Microsoft.Resources/deployments",
"resourceGroup": "crossResourceGroupDeployment",
"properties": {
    "mode": "Incremental",
    "template": {
        ...
        resourceGroup() refers to parent resource group
    }
}
```

<span data-ttu-id="0dc97-130">Jeśli możesz połączyć się z oddzielnych szablonu, resouceGroup() w szablonie połączonego rozpoznawany jako grupa zasobów zagnieżdżonych.</span><span class="sxs-lookup"><span data-stu-id="0dc97-130">If you link to a separate template, resouceGroup() in the linked template resolves to the nested resource group.</span></span> <span data-ttu-id="0dc97-131">Połączone szablonu używany następujący format:</span><span class="sxs-lookup"><span data-stu-id="0dc97-131">A linked template uses the following format:</span></span>

```json
"apiVersion": "2017-05-10",
"name": "linkedTemplate",
"type": "Microsoft.Resources/deployments",
"resourceGroup": "crossResourceGroupDeployment",
"properties": {
    "mode": "Incremental",
    "templateLink": {
        ...
        resourceGroup() in linked template refers to linked resource group
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="0dc97-132">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0dc97-132">Next steps</span></span>

* <span data-ttu-id="0dc97-133">Aby poznać sposób definiowania parametry w szablonie, zobacz [poznać strukturę i składni szablonów usługi Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="0dc97-133">To understand how to define parameters in your template, see [Understand the structure and syntax of Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="0dc97-134">Aby uzyskać wskazówki dotyczące rozwiązania typowych błędów wdrażania, zobacz [Rozwiąż typowe błędy wdrożenia usługi Azure z usługą Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="0dc97-134">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="0dc97-135">Aby uzyskać informacje o wdrażaniu szablonu, który wymaga tokenu sygnatury dostępu Współdzielonego, zobacz [wdrażanie szablonu prywatnej przy użyciu tokenu sygnatury dostępu Współdzielonego](resource-manager-powershell-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="0dc97-135">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>
