---
title: "Wdrażanie szablonu platformy Azure z tokenu sygnatury dostępu Współdzielonego i interfejsu wiersza polecenia Azure | Dokumentacja firmy Microsoft"
description: "Użyj usługi Azure Resource Manager i interfejsu wiersza polecenia Azure, aby wdrożyć zasobów na platformie Azure z szablonu, który jest chroniony za pomocą tokenu sygnatury dostępu Współdzielonego."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/31/2017
ms.author: tomfitz
ms.openlocfilehash: 22387aadd8f53a65efb76a29a9403c46a2c25954
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-private-resource-manager-template-with-sas-token-and-azure-cli"></a><span data-ttu-id="12530-103">Wdrażanie prywatnej szablonu usługi Resource Manager z tokenu sygnatury dostępu Współdzielonego i wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="12530-103">Deploy private Resource Manager template with SAS token and Azure CLI</span></span>

<span data-ttu-id="12530-104">Gdy w szablonie znajduje się na koncie magazynu, można ograniczyć dostęp do szablonu, a także dostarczają token sygnatury dostępu Współdzielonego dostępu współdzielonego podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="12530-104">When your template resides in a storage account, you can restrict access to the template and provide a shared access signature (SAS) token during deployment.</span></span> <span data-ttu-id="12530-105">W tym temacie wyjaśniono, jak przy użyciu programu Azure PowerShell z szablonami usługi Resource Manager zapewnienie tokenu sygnatury dostępu Współdzielonego podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="12530-105">This topic explains how to use Azure PowerShell with Resource Manager templates to provide a SAS token during deployment.</span></span> 

## <a name="add-private-template-to-storage-account"></a><span data-ttu-id="12530-106">Dodaj szablon prywatnych do konta magazynu</span><span class="sxs-lookup"><span data-stu-id="12530-106">Add private template to storage account</span></span>

<span data-ttu-id="12530-107">Szablony można dodać do konta magazynu i link do ich podczas wdrażania z tokenem sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="12530-107">You can add your templates to a storage account and link to them during deployment with a SAS token.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="12530-108">Wykonując poniższe kroki, obiektu blob zawierającego szablon jest dostępny tylko dla właściciela konta.</span><span class="sxs-lookup"><span data-stu-id="12530-108">By following the steps below, the blob containing the template is accessible to only the account owner.</span></span> <span data-ttu-id="12530-109">Podczas tworzenia tokenu SAS obiektu blob obiektu blob jest jednak dostępne dla wszystkich użytkowników z tym identyfikatorem URI.</span><span class="sxs-lookup"><span data-stu-id="12530-109">However, when you create a SAS token for the blob, the blob is accessible to anyone with that URI.</span></span> <span data-ttu-id="12530-110">Jeśli inny użytkownik przechwytuje identyfikator URI, ten użytkownik jest w stanie uzyskać dostęp do szablonu.</span><span class="sxs-lookup"><span data-stu-id="12530-110">If another user intercepts the URI, that user is able to access the template.</span></span> <span data-ttu-id="12530-111">Za pomocą tokenu sygnatury dostępu Współdzielonego jest dobrym sposobem ograniczenia dostępu do szablonów, ale nie może zawierać dane poufne, takie jak hasła, bezpośrednio w szablonie.</span><span class="sxs-lookup"><span data-stu-id="12530-111">Using a SAS token is a good way of limiting access to your templates, but you should not include sensitive data like passwords directly in the template.</span></span>
> 
> 

<span data-ttu-id="12530-112">Poniższy przykład ustawia kontener konta magazynu prywatnych i przekazuje szablonu:</span><span class="sxs-lookup"><span data-stu-id="12530-112">The following example sets up a private storage account container and uploads a template:</span></span>
   
```azurecli
az group create --name "ManageGroup" --location "South Central US"
az storage account create \
    --resource-group ManageGroup \
    --location "South Central US" \
    --sku Standard_LRS \
    --kind Storage \
    --name {your-unique-name}
connection=$(az storage account show-connection-string \
    --resource-group ManageGroup \
    --name {your-unique-name} \
    --query connectionString)
az storage container create \
    --name templates \
    --public-access Off \
    --connection-string $connection
az storage blob upload \
    --container-name templates \
    --file vmlinux.json \
    --name vmlinux.json \
    --connection-string $connection
```

### <a name="provide-sas-token-during-deployment"></a><span data-ttu-id="12530-113">Podaj token sygnatury dostępu Współdzielonego podczas wdrażania</span><span class="sxs-lookup"><span data-stu-id="12530-113">Provide SAS token during deployment</span></span>
<span data-ttu-id="12530-114">Aby wdrożyć szablon prywatnych na koncie magazynu, wygenerowania tokenu sygnatury dostępu Współdzielonego i dołączyć go w identyfikatorze URI dla szablonu.</span><span class="sxs-lookup"><span data-stu-id="12530-114">To deploy a private template in a storage account, generate a SAS token and include it in the URI for the template.</span></span> <span data-ttu-id="12530-115">Ustawianie czasu wygaśnięcia poczekać na ukończenie wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="12530-115">Set the expiry time to allow enough time to complete the deployment.</span></span>
   
```azurecli
expiretime=$(date -u -d '30 minutes' +%Y-%m-%dT%H:%MZ)
connection=$(az storage account show-connection-string \
    --resource-group ManageGroup \
    --name {your-unique-name} \
    --query connectionString)
token=$(az storage blob generate-sas \
    --container-name templates \
    --name vmlinux.json \
    --expiry $expiretime \
    --permissions r \
    --output tsv \
    --connection-string $connection)
url=$(az storage blob url \
    --container-name templates \
    --name vmlinux.json \
    --output tsv \
    --connection-string $connection)
az group deployment create --resource-group ExampleGroup --template-uri $url?$token
```

<span data-ttu-id="12530-116">Na przykład za pomocą tokenu sygnatury dostępu Współdzielonego przy użyciu szablonów połączonych, zobacz [za pomocą szablonów połączonych z usługą Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="12530-116">For an example of using a SAS token with linked templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="12530-117">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="12530-117">Next steps</span></span>
* <span data-ttu-id="12530-118">Aby obejrzeć wprowadzenie do wdrażania szablonów, zobacz [wdrażanie zasobów przy użyciu szablonów usługi Resource Manager i programu Azure PowerShell](resource-group-template-deploy-cli.md).</span><span class="sxs-lookup"><span data-stu-id="12530-118">For an introduction to deploying templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy-cli.md).</span></span>
* <span data-ttu-id="12530-119">Zakończenie przykładowego skryptu, który wdraża szablonu, zobacz [skryptu szablonu wdrażania Menedżera zasobów](resource-manager-samples-cli-deploy.md)</span><span class="sxs-lookup"><span data-stu-id="12530-119">For a complete sample script that deploys a template, see [Deploy Resource Manager template script](resource-manager-samples-cli-deploy.md)</span></span>
* <span data-ttu-id="12530-120">Aby określić parametry w szablonie, zobacz [tworzenia szablonów](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="12530-120">To define parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="12530-121">Aby uzyskać instrukcje dla przedsiębiorstw dotyczące użycia usługi Resource Manager w celu efektywnego zarządzania subskrypcjami, zobacz [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md) (Szkielet platformy Azure dla przedsiębiorstwa — narzucony nadzór subskrypcji).</span><span class="sxs-lookup"><span data-stu-id="12530-121">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
