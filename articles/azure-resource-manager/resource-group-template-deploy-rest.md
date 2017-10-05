---
title: "Wdrażanie zasobów przy użyciu interfejsu API REST i szablon | Dokumentacja firmy Microsoft"
description: "Użyj Menedżera zasobów Azure i interfejsu REST API usługi Resource Manager wdrażania zasobów na platformie Azure. Zasoby są zdefiniowane w szablonie usługi Resource Manager."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 1d8fbd4c-78b0-425b-ba76-f2b7fd260b45
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/10/2017
ms.author: tomfitz
ms.openlocfilehash: 46856a25fb57bb2c5a3c1aeae13c11655e1a58a5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-resource-manager-rest-api"></a><span data-ttu-id="5a7f7-104">Deploy resources with Resource Manager templates and Resource Manager REST API (Wdrażanie zasobów za pomocą szablonów usługi Resource Manager i interfejsu API REST usługi Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="5a7f7-104">Deploy resources with Resource Manager templates and Resource Manager REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5a7f7-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5a7f7-105">PowerShell</span></span>](resource-group-template-deploy.md)
> * [<span data-ttu-id="5a7f7-106">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="5a7f7-106">Azure CLI</span></span>](resource-group-template-deploy-cli.md)
> * [<span data-ttu-id="5a7f7-107">Portal</span><span class="sxs-lookup"><span data-stu-id="5a7f7-107">Portal</span></span>](resource-group-template-deploy-portal.md)
> * [<span data-ttu-id="5a7f7-108">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="5a7f7-108">REST API</span></span>](resource-group-template-deploy-rest.md)
> 
> 

<span data-ttu-id="5a7f7-109">W tym artykule wyjaśniono, jak wdrażanie zasobów na platformie Azure za pomocą interfejsu REST API usługi Resource Manager z szablonami usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5a7f7-109">This article explains how to use the Resource Manager REST API with Resource Manager templates to deploy your resources to Azure.</span></span>  

> [!TIP]
> <span data-ttu-id="5a7f7-110">Aby uzyskać pomoc dotyczącą debugowania — błąd podczas wdrażania zobacz:</span><span class="sxs-lookup"><span data-stu-id="5a7f7-110">For help with debugging an error during deployment, see:</span></span>
> 
> * <span data-ttu-id="5a7f7-111">[Wyświetl operacje wdrażania](resource-manager-deployment-operations.md) Aby dowiedzieć się o wprowadzenie informacje ułatwiające rozwiązywania problemów dotyczących błędu</span><span class="sxs-lookup"><span data-stu-id="5a7f7-111">[View deployment operations](resource-manager-deployment-operations.md) to learn about getting information that helps you troubleshoot your error</span></span>
> * <span data-ttu-id="5a7f7-112">[Rozwiąż typowe błędy podczas wdrażania zasobów na platformie Azure za pomocą Menedżera zasobów Azure](resource-manager-common-deployment-errors.md) Aby dowiedzieć się, jak rozwiązać typowe błędy wdrażania</span><span class="sxs-lookup"><span data-stu-id="5a7f7-112">[Troubleshoot common errors when deploying resources to Azure with Azure Resource Manager](resource-manager-common-deployment-errors.md) to learn how to resolve common deployment errors</span></span>
> 
> 

<span data-ttu-id="5a7f7-113">Szablon może być lokalny plik lub pliku zewnętrznego, który jest dostępny za pomocą identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="5a7f7-113">Your template can be either a local file or an external file that is available through a URI.</span></span> <span data-ttu-id="5a7f7-114">Gdy w szablonie znajduje się na koncie magazynu, można ograniczyć dostęp do szablonu, a także dostarczają token sygnatury dostępu Współdzielonego dostępu współdzielonego podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="5a7f7-114">When your template resides in a storage account, you can restrict access to the template and provide a shared access signature (SAS) token during deployment.</span></span>

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

## <a name="deploy-with-the-rest-api"></a><span data-ttu-id="5a7f7-115">Rozmieszczanie za pomocą interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="5a7f7-115">Deploy with the REST API</span></span>
1. <span data-ttu-id="5a7f7-116">Ustaw [wspólnych parametrów i nagłówki](https://docs.microsoft.com/rest/api/index), łącznie z tokenami uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="5a7f7-116">Set [common parameters and headers](https://docs.microsoft.com/rest/api/index), including authentication tokens.</span></span>
2. <span data-ttu-id="5a7f7-117">Jeśli nie masz istniejącej grupy zasobów, należy utworzyć grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="5a7f7-117">If you do not have an existing resource group, create a resource group.</span></span> <span data-ttu-id="5a7f7-118">Podaj identyfikator subskrypcji, nazwę nowej grupy zasobów i lokalizacji, która należy do rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="5a7f7-118">Provide your subscription ID, the name of the new resource group, and location that you need for your solution.</span></span> <span data-ttu-id="5a7f7-119">Aby uzyskać więcej informacji, zobacz [Utwórz grupę zasobów](https://docs.microsoft.com/rest/api/resources/resourcegroups#ResourceGroups_CreateOrUpdate).</span><span class="sxs-lookup"><span data-stu-id="5a7f7-119">For more information, see [Create a resource group](https://docs.microsoft.com/rest/api/resources/resourcegroups#ResourceGroups_CreateOrUpdate).</span></span>
   
        PUT https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>?api-version=2015-01-01
          <common headers>
          {
            "location": "West US",
            "tags": {
               "tagname1": "tagvalue1"
            }
          }
3. <span data-ttu-id="5a7f7-120">Sprawdzanie poprawności wdrożenia przed wykonaniem ją, uruchamiając [weryfikowanie wdrożenia szablonu](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Validate) operacji.</span><span class="sxs-lookup"><span data-stu-id="5a7f7-120">Validate your deployment before executing it by running the [Validate a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Validate) operation.</span></span> <span data-ttu-id="5a7f7-121">Podczas testowania wdrożenia, należy podać parametry, dokładnie tak jak w przypadku wykonywania wdrożenia (pokazano w następnym kroku).</span><span class="sxs-lookup"><span data-stu-id="5a7f7-121">When testing the deployment, provide parameters exactly as you would when executing the deployment (shown in the next step).</span></span>
4. <span data-ttu-id="5a7f7-122">Tworzenie wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="5a7f7-122">Create a deployment.</span></span> <span data-ttu-id="5a7f7-123">Podaj identyfikator subskrypcji, nazwę grupy zasobów, nazwę wdrożenia i łącza do szablonu.</span><span class="sxs-lookup"><span data-stu-id="5a7f7-123">Provide your subscription ID, the name of the resource group, the name of the deployment, and a link to your template.</span></span> <span data-ttu-id="5a7f7-124">Aby uzyskać informacje o pliku szablonu, zobacz [pliku parametrów](#parameter-file).</span><span class="sxs-lookup"><span data-stu-id="5a7f7-124">For information about the template file, see [Parameter file](#parameter-file).</span></span> <span data-ttu-id="5a7f7-125">Aby uzyskać więcej informacji na temat interfejsu API REST, aby utworzyć grupę zasobów, zobacz [Utwórz wdrożenie szablonu](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_CreateOrUpdate).</span><span class="sxs-lookup"><span data-stu-id="5a7f7-125">For more information about the REST API to create a resource group, see [Create a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_CreateOrUpdate).</span></span> <span data-ttu-id="5a7f7-126">Powiadomienie **tryb** ustawiono **przyrostowe**.</span><span class="sxs-lookup"><span data-stu-id="5a7f7-126">Notice the **mode** is set to **Incremental**.</span></span> <span data-ttu-id="5a7f7-127">Uruchamiania ukończenia wdrożenia, należy ustawić **tryb** do **Complete**.</span><span class="sxs-lookup"><span data-stu-id="5a7f7-127">To run a complete deployment, set **mode** to **Complete**.</span></span> <span data-ttu-id="5a7f7-128">Należy zachować ostrożność podczas korzystania z trybu pełne, jak może przypadkowo usunięte zasoby, które nie znajdują się w szablonie.</span><span class="sxs-lookup"><span data-stu-id="5a7f7-128">Be careful when using the complete mode as you can inadvertently delete resources that are not in your template.</span></span>
   
        PUT https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>/providers/Microsoft.Resources/deployments/<YourDeploymentName>?api-version=2015-01-01
          <common headers>
          {
            "properties": {
              "templateLink": {
                "uri": "http://mystorageaccount.blob.core.windows.net/templates/template.json",
                "contentVersion": "1.0.0.0"
              },
              "mode": "Incremental",
              "parametersLink": {
                "uri": "http://mystorageaccount.blob.core.windows.net/templates/parameters.json",
                "contentVersion": "1.0.0.0"
              }
            }
          }
   
      <span data-ttu-id="5a7f7-129">Do rejestrowania zawartości odpowiedzi i żądania zawartości, należy włączyć **debugSetting** w żądaniu.</span><span class="sxs-lookup"><span data-stu-id="5a7f7-129">If you want to log response content, request content, or both, include **debugSetting** in the request.</span></span>
   
        "debugSetting": {
          "detailLevel": "requestContent, responseContent"
        }
   
      <span data-ttu-id="5a7f7-130">Aby użyć tokenu sygnatury dostępu Współdzielonego dostępu współdzielonego, można skonfigurować konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="5a7f7-130">You can set up your storage account to use a shared access signature (SAS) token.</span></span> <span data-ttu-id="5a7f7-131">Aby uzyskać więcej informacji, zobacz [Delegowanie dostępu z sygnaturą dostępu współdzielonego](https://docs.microsoft.com/rest/api/storageservices/delegating-access-with-a-shared-access-signature).</span><span class="sxs-lookup"><span data-stu-id="5a7f7-131">For more information, see [Delegating Access with a Shared Access Signature](https://docs.microsoft.com/rest/api/storageservices/delegating-access-with-a-shared-access-signature).</span></span>
5. <span data-ttu-id="5a7f7-132">Pobieranie stanu wdrażania szablonu.</span><span class="sxs-lookup"><span data-stu-id="5a7f7-132">Get the status of the template deployment.</span></span> <span data-ttu-id="5a7f7-133">Aby uzyskać więcej informacji, zobacz [uzyskać informacje na temat wdrażania szablonu](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get).</span><span class="sxs-lookup"><span data-stu-id="5a7f7-133">For more information, see [Get information about a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get).</span></span>
   
          GET https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>/providers/Microsoft.Resources/deployments/<YourDeploymentName>?api-version=2015-01-01
           <common headers>

## <a name="parameter-file"></a><span data-ttu-id="5a7f7-134">Plik parametrów</span><span class="sxs-lookup"><span data-stu-id="5a7f7-134">Parameter file</span></span>

[!INCLUDE [resource-manager-parameter-file](../../includes/resource-manager-parameter-file.md)]

## <a name="next-steps"></a><span data-ttu-id="5a7f7-135">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5a7f7-135">Next steps</span></span>
* <span data-ttu-id="5a7f7-136">Informacje na temat obsługi operacji asynchronicznych REST, zobacz [śledzić operacje asynchroniczne Azure](resource-manager-async-operations.md).</span><span class="sxs-lookup"><span data-stu-id="5a7f7-136">To learn about handling asynchronous REST operations, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>
* <span data-ttu-id="5a7f7-137">Na przykład wdrażania zasobów za pomocą biblioteki klienta .NET, zobacz [wdrażanie zasobów przy użyciu bibliotek .NET oraz szablonu](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5a7f7-137">For an example of deploying resources through the .NET client library, see [Deploy resources using .NET libraries and a template](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="5a7f7-138">Aby określić parametry w szablonie, zobacz [tworzenia szablonów](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="5a7f7-138">To define parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="5a7f7-139">Aby uzyskać wskazówki dotyczące wdrażania rozwiązania w różnych środowiskach, zobacz [Development and test environments in Microsoft Azure](solution-dev-test-environments.md) (Środowiska projektowe i testowe na platformie Microsoft Azure).</span><span class="sxs-lookup"><span data-stu-id="5a7f7-139">For guidance on deploying your solution to different environments, see [Development and test environments in Microsoft Azure](solution-dev-test-environments.md).</span></span>
* <span data-ttu-id="5a7f7-140">Aby uzyskać instrukcje dla przedsiębiorstw dotyczące użycia usługi Resource Manager w celu efektywnego zarządzania subskrypcjami, zobacz [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md) (Szkielet platformy Azure dla przedsiębiorstwa — narzucony nadzór subskrypcji).</span><span class="sxs-lookup"><span data-stu-id="5a7f7-140">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

