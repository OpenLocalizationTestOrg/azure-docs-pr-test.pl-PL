---
title: "aaaDeploy szablonu platformy Azure z tokenu sygnatury dostępu Współdzielonego i programu PowerShell | Dokumentacja firmy Microsoft"
description: "Usługi Azure Resource Manager i programu Azure PowerShell tooAzure zasobów toodeploy z szablonu, który jest chroniony za pomocą tokenu sygnatury dostępu Współdzielonego."
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
ms.openlocfilehash: b95e096591d6213f8ef79235c8cd85705c4b79ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-private-resource-manager-template-with-sas-token-and-azure-powershell"></a><span data-ttu-id="cdcc3-103">Wdrażanie prywatnej szablonu usługi Resource Manager z tokenu sygnatury dostępu Współdzielonego i programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="cdcc3-103">Deploy private Resource Manager template with SAS token and Azure PowerShell</span></span>

<span data-ttu-id="cdcc3-104">Gdy w szablonie znajduje się na koncie magazynu, można ograniczyć dostęp toohello szablonu, a także dostarczają token sygnatury dostępu Współdzielonego dostępu współdzielonego podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="cdcc3-104">When your template resides in a storage account, you can restrict access toohello template and provide a shared access signature (SAS) token during deployment.</span></span> <span data-ttu-id="cdcc3-105">W tym temacie opisano sposób toouse programu Azure PowerShell z tooprovide szablonów usługi Resource Manager tokenu sygnatury dostępu Współdzielonego, podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="cdcc3-105">This topic explains how toouse Azure PowerShell with Resource Manager templates tooprovide a SAS token during deployment.</span></span> 

## <a name="add-private-template-toostorage-account"></a><span data-ttu-id="cdcc3-106">Dodaj konto toostorage prywatnej szablonu</span><span class="sxs-lookup"><span data-stu-id="cdcc3-106">Add private template toostorage account</span></span>

<span data-ttu-id="cdcc3-107">Można dodać konta magazynu tooa szablony, a następnie połącz toothem podczas wdrażania z tokenem sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="cdcc3-107">You can add your templates tooa storage account and link toothem during deployment with a SAS token.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cdcc3-108">Wykonując poniższe kroki hello hello obiektu blob zawierającego szablon hello jest właściciela konta hello tooonly dostępny.</span><span class="sxs-lookup"><span data-stu-id="cdcc3-108">By following hello steps below, hello blob containing hello template is accessible tooonly hello account owner.</span></span> <span data-ttu-id="cdcc3-109">Podczas tworzenia tokenu SAS obiektu blob hello hello obiektu blob jest jednak dostępne tooanyone z tym identyfikatorem URI.</span><span class="sxs-lookup"><span data-stu-id="cdcc3-109">However, when you create a SAS token for hello blob, hello blob is accessible tooanyone with that URI.</span></span> <span data-ttu-id="cdcc3-110">Inny użytkownik przechwytuje hello identyfikatora URI, który jest możliwe tooaccess hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="cdcc3-110">If another user intercepts hello URI, that user is able tooaccess hello template.</span></span> <span data-ttu-id="cdcc3-111">Za pomocą tokenu sygnatury dostępu Współdzielonego jest dobrym sposobem ograniczenia dostępu tooyour szablonów, ale nie może zawierać dane poufne, takie jak hasła, bezpośrednio w szablonie hello.</span><span class="sxs-lookup"><span data-stu-id="cdcc3-111">Using a SAS token is a good way of limiting access tooyour templates, but you should not include sensitive data like passwords directly in hello template.</span></span>
> 
> 

<span data-ttu-id="cdcc3-112">Witaj poniższy przykład ustawia kontener konta magazynu prywatnych i przekazuje szablonu:</span><span class="sxs-lookup"><span data-stu-id="cdcc3-112">hello following example sets up a private storage account container and uploads a template:</span></span>
   
```powershell
# create a storage account for templates
New-AzureRmResourceGroup -Name ManageGroup -Location "South Central US"
New-AzureRmStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name} -Type Standard_LRS -Location "West US"
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name}

# create a container and upload template
New-AzureStorageContainer -Name templates -Permission Off
Set-AzureStorageBlobContent -Container templates -File c:\MyTemplates\storage.json
```

## <a name="provide-sas-token-during-deployment"></a><span data-ttu-id="cdcc3-113">Podaj token sygnatury dostępu Współdzielonego podczas wdrażania</span><span class="sxs-lookup"><span data-stu-id="cdcc3-113">Provide SAS token during deployment</span></span>
<span data-ttu-id="cdcc3-114">toodeploy prywatnej szablonu na koncie magazynu wygenerowania tokenu sygnatury dostępu Współdzielonego i uwzględnić go w hello URI hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="cdcc3-114">toodeploy a private template in a storage account, generate a SAS token and include it in hello URI for hello template.</span></span> <span data-ttu-id="cdcc3-115">Ustaw tooallow czas wygaśnięcia hello wdrożenia hello toocomplete wystarczająco dużo czasu.</span><span class="sxs-lookup"><span data-stu-id="cdcc3-115">Set hello expiry time tooallow enough time toocomplete hello deployment.</span></span>
   
```powershell
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name}

# get hello URI with hello SAS token
$templateuri = New-AzureStorageBlobSASToken -Container templates -Blob storage.json -Permission r `
  -ExpiryTime (Get-Date).AddHours(2.0) -FullUri

# provide URI with SAS token during deployment
New-AzureRmResourceGroup -Name ExampleGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup -TemplateUri $templateuri
```

<span data-ttu-id="cdcc3-116">Na przykład za pomocą tokenu sygnatury dostępu Współdzielonego przy użyciu szablonów połączonych, zobacz [za pomocą szablonów połączonych z usługą Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="cdcc3-116">For an example of using a SAS token with linked templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="cdcc3-117">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cdcc3-117">Next steps</span></span>
* <span data-ttu-id="cdcc3-118">Wprowadzenie toodeploying szablonów, zobacz [wdrażanie zasobów przy użyciu szablonów usługi Resource Manager i programu Azure PowerShell](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="cdcc3-118">For an introduction toodeploying templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="cdcc3-119">Zakończenie przykładowego skryptu, który wdraża szablonu, zobacz [skryptu szablonu wdrażania Menedżera zasobów](resource-manager-samples-powershell-deploy.md)</span><span class="sxs-lookup"><span data-stu-id="cdcc3-119">For a complete sample script that deploys a template, see [Deploy Resource Manager template script](resource-manager-samples-powershell-deploy.md)</span></span>
* <span data-ttu-id="cdcc3-120">Parametry toodefine w szablonie, zobacz [tworzenia szablonów](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="cdcc3-120">toodefine parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="cdcc3-121">Aby uzyskać wskazówki dotyczące użycia tooeffectively Menedżera zasobów przedsiębiorstwa Zarządzaj subskrypcjami, zobacz [szkieletu Azure enterprise — ładu przetestowanego subskrypcji](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="cdcc3-121">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

