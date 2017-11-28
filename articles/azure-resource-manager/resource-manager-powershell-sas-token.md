---
title: "Wdrażanie szablonu platformy Azure z tokenu sygnatury dostępu Współdzielonego i programu PowerShell | Dokumentacja firmy Microsoft"
description: "Użyj usługi Azure Resource Manager i programu Azure PowerShell, aby wdrożyć zasobów na platformie Azure z szablonu, który jest chroniony za pomocą tokenu sygnatury dostępu Współdzielonego."
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
ms.openlocfilehash: 1e3cea027b599e2b1af1ced0fdf14e2cc8a0db82
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-private-resource-manager-template-with-sas-token-and-azure-powershell"></a><span data-ttu-id="71776-103">Wdrażanie prywatnej szablonu usługi Resource Manager z tokenu sygnatury dostępu Współdzielonego i programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="71776-103">Deploy private Resource Manager template with SAS token and Azure PowerShell</span></span>

<span data-ttu-id="71776-104">Gdy w szablonie znajduje się na koncie magazynu, można ograniczyć dostęp do szablonu, a także dostarczają token sygnatury dostępu Współdzielonego dostępu współdzielonego podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="71776-104">When your template resides in a storage account, you can restrict access to the template and provide a shared access signature (SAS) token during deployment.</span></span> <span data-ttu-id="71776-105">W tym temacie wyjaśniono, jak przy użyciu programu Azure PowerShell z szablonami usługi Resource Manager zapewnienie tokenu sygnatury dostępu Współdzielonego podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="71776-105">This topic explains how to use Azure PowerShell with Resource Manager templates to provide a SAS token during deployment.</span></span> 

## <a name="add-private-template-to-storage-account"></a><span data-ttu-id="71776-106">Dodaj szablon prywatnych do konta magazynu</span><span class="sxs-lookup"><span data-stu-id="71776-106">Add private template to storage account</span></span>

<span data-ttu-id="71776-107">Szablony można dodać do konta magazynu i link do ich podczas wdrażania z tokenem sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="71776-107">You can add your templates to a storage account and link to them during deployment with a SAS token.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="71776-108">Wykonując poniższe kroki, obiektu blob zawierającego szablon jest dostępny tylko dla właściciela konta.</span><span class="sxs-lookup"><span data-stu-id="71776-108">By following the steps below, the blob containing the template is accessible to only the account owner.</span></span> <span data-ttu-id="71776-109">Podczas tworzenia tokenu SAS obiektu blob obiektu blob jest jednak dostępne dla wszystkich użytkowników z tym identyfikatorem URI.</span><span class="sxs-lookup"><span data-stu-id="71776-109">However, when you create a SAS token for the blob, the blob is accessible to anyone with that URI.</span></span> <span data-ttu-id="71776-110">Jeśli inny użytkownik przechwytuje identyfikator URI, ten użytkownik jest w stanie uzyskać dostęp do szablonu.</span><span class="sxs-lookup"><span data-stu-id="71776-110">If another user intercepts the URI, that user is able to access the template.</span></span> <span data-ttu-id="71776-111">Za pomocą tokenu sygnatury dostępu Współdzielonego jest dobrym sposobem ograniczenia dostępu do szablonów, ale nie może zawierać dane poufne, takie jak hasła, bezpośrednio w szablonie.</span><span class="sxs-lookup"><span data-stu-id="71776-111">Using a SAS token is a good way of limiting access to your templates, but you should not include sensitive data like passwords directly in the template.</span></span>
> 
> 

<span data-ttu-id="71776-112">Poniższy przykład ustawia kontener konta magazynu prywatnych i przekazuje szablonu:</span><span class="sxs-lookup"><span data-stu-id="71776-112">The following example sets up a private storage account container and uploads a template:</span></span>
   
```powershell
# create a storage account for templates
New-AzureRmResourceGroup -Name ManageGroup -Location "South Central US"
New-AzureRmStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name} -Type Standard_LRS -Location "West US"
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name}

# create a container and upload template
New-AzureStorageContainer -Name templates -Permission Off
Set-AzureStorageBlobContent -Container templates -File c:\MyTemplates\storage.json
```

## <a name="provide-sas-token-during-deployment"></a><span data-ttu-id="71776-113">Podaj token sygnatury dostępu Współdzielonego podczas wdrażania</span><span class="sxs-lookup"><span data-stu-id="71776-113">Provide SAS token during deployment</span></span>
<span data-ttu-id="71776-114">Aby wdrożyć szablon prywatnych na koncie magazynu, wygenerowania tokenu sygnatury dostępu Współdzielonego i dołączyć go w identyfikatorze URI dla szablonu.</span><span class="sxs-lookup"><span data-stu-id="71776-114">To deploy a private template in a storage account, generate a SAS token and include it in the URI for the template.</span></span> <span data-ttu-id="71776-115">Ustawianie czasu wygaśnięcia poczekać na ukończenie wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="71776-115">Set the expiry time to allow enough time to complete the deployment.</span></span>
   
```powershell
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name}

# get the URI with the SAS token
$templateuri = New-AzureStorageBlobSASToken -Container templates -Blob storage.json -Permission r `
  -ExpiryTime (Get-Date).AddHours(2.0) -FullUri

# provide URI with SAS token during deployment
New-AzureRmResourceGroup -Name ExampleGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup -TemplateUri $templateuri
```

<span data-ttu-id="71776-116">Na przykład za pomocą tokenu sygnatury dostępu Współdzielonego przy użyciu szablonów połączonych, zobacz [za pomocą szablonów połączonych z usługą Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="71776-116">For an example of using a SAS token with linked templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="71776-117">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="71776-117">Next steps</span></span>
* <span data-ttu-id="71776-118">Aby obejrzeć wprowadzenie do wdrażania szablonów, zobacz [wdrażanie zasobów przy użyciu szablonów usługi Resource Manager i programu Azure PowerShell](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="71776-118">For an introduction to deploying templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="71776-119">Zakończenie przykładowego skryptu, który wdraża szablonu, zobacz [skryptu szablonu wdrażania Menedżera zasobów](resource-manager-samples-powershell-deploy.md)</span><span class="sxs-lookup"><span data-stu-id="71776-119">For a complete sample script that deploys a template, see [Deploy Resource Manager template script](resource-manager-samples-powershell-deploy.md)</span></span>
* <span data-ttu-id="71776-120">Aby określić parametry w szablonie, zobacz [tworzenia szablonów](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="71776-120">To define parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="71776-121">Aby uzyskać instrukcje dla przedsiębiorstw dotyczące użycia usługi Resource Manager w celu efektywnego zarządzania subskrypcjami, zobacz [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md) (Szkielet platformy Azure dla przedsiębiorstwa — narzucony nadzór subskrypcji).</span><span class="sxs-lookup"><span data-stu-id="71776-121">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

