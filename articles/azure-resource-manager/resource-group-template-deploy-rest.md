---
title: "aaaDeploy zasobów przy użyciu interfejsu API REST i szablon | Dokumentacja firmy Microsoft"
description: "Za pomocą usługi Azure Resource Manager i interfejsu REST API usługi Resource Manager toodeploy tooAzure zasobów. zasoby Hello są definiowane w szablonie usługi Resource Manager."
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
ms.openlocfilehash: 347ad3bdb604429e7291297d448688204af69b46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-resource-manager-rest-api"></a><span data-ttu-id="39b94-104">Deploy resources with Resource Manager templates and Resource Manager REST API (Wdrażanie zasobów za pomocą szablonów usługi Resource Manager i interfejsu API REST usługi Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="39b94-104">Deploy resources with Resource Manager templates and Resource Manager REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="39b94-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="39b94-105">PowerShell</span></span>](resource-group-template-deploy.md)
> * [<span data-ttu-id="39b94-106">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="39b94-106">Azure CLI</span></span>](resource-group-template-deploy-cli.md)
> * [<span data-ttu-id="39b94-107">Portal</span><span class="sxs-lookup"><span data-stu-id="39b94-107">Portal</span></span>](resource-group-template-deploy-portal.md)
> * [<span data-ttu-id="39b94-108">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="39b94-108">REST API</span></span>](resource-group-template-deploy-rest.md)
> 
> 

<span data-ttu-id="39b94-109">W tym artykule opisano, jak toouse hello interfejsu REST API usługi Resource Manager z toodeploy szablonów usługi Resource Manager tooAzure Twojego zasobów.</span><span class="sxs-lookup"><span data-stu-id="39b94-109">This article explains how toouse hello Resource Manager REST API with Resource Manager templates toodeploy your resources tooAzure.</span></span>  

> [!TIP]
> <span data-ttu-id="39b94-110">Aby uzyskać pomoc dotyczącą debugowania — błąd podczas wdrażania zobacz:</span><span class="sxs-lookup"><span data-stu-id="39b94-110">For help with debugging an error during deployment, see:</span></span>
> 
> * <span data-ttu-id="39b94-111">[Wyświetl operacje wdrażania](resource-manager-deployment-operations.md) toolearn uzyskiwanie informacje ułatwiające rozwiązywanie problemów z błędu</span><span class="sxs-lookup"><span data-stu-id="39b94-111">[View deployment operations](resource-manager-deployment-operations.md) toolearn about getting information that helps you troubleshoot your error</span></span>
> * <span data-ttu-id="39b94-112">[Rozwiąż typowe błędy podczas wdrażania tooAzure zasobów z usługi Azure Resource Manager](resource-manager-common-deployment-errors.md) toolearn jak tooresolve typowe błędy wdrażania</span><span class="sxs-lookup"><span data-stu-id="39b94-112">[Troubleshoot common errors when deploying resources tooAzure with Azure Resource Manager](resource-manager-common-deployment-errors.md) toolearn how tooresolve common deployment errors</span></span>
> 
> 

<span data-ttu-id="39b94-113">Szablon może być lokalny plik lub pliku zewnętrznego, który jest dostępny za pomocą identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="39b94-113">Your template can be either a local file or an external file that is available through a URI.</span></span> <span data-ttu-id="39b94-114">Gdy w szablonie znajduje się na koncie magazynu, można ograniczyć dostęp toohello szablonu, a także dostarczają token sygnatury dostępu Współdzielonego dostępu współdzielonego podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="39b94-114">When your template resides in a storage account, you can restrict access toohello template and provide a shared access signature (SAS) token during deployment.</span></span>

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

## <a name="deploy-with-hello-rest-api"></a><span data-ttu-id="39b94-115">Wdrażanie z hello interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="39b94-115">Deploy with hello REST API</span></span>
1. <span data-ttu-id="39b94-116">Ustaw [wspólnych parametrów i nagłówki](https://docs.microsoft.com/rest/api/index), łącznie z tokenami uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="39b94-116">Set [common parameters and headers](https://docs.microsoft.com/rest/api/index), including authentication tokens.</span></span>
2. <span data-ttu-id="39b94-117">Jeśli nie masz istniejącej grupy zasobów, należy utworzyć grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="39b94-117">If you do not have an existing resource group, create a resource group.</span></span> <span data-ttu-id="39b94-118">Podaj Twojego Identyfikatora subskrypcji, nazwę hello hello nowe, lokalizacji i grupy zasobów potrzebnym do rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="39b94-118">Provide your subscription ID, hello name of hello new resource group, and location that you need for your solution.</span></span> <span data-ttu-id="39b94-119">Aby uzyskać więcej informacji, zobacz [Utwórz grupę zasobów](https://docs.microsoft.com/rest/api/resources/resourcegroups#ResourceGroups_CreateOrUpdate).</span><span class="sxs-lookup"><span data-stu-id="39b94-119">For more information, see [Create a resource group](https://docs.microsoft.com/rest/api/resources/resourcegroups#ResourceGroups_CreateOrUpdate).</span></span>
   
        PUT https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>?api-version=2015-01-01
          <common headers>
          {
            "location": "West US",
            "tags": {
               "tagname1": "tagvalue1"
            }
          }
3. <span data-ttu-id="39b94-120">Sprawdzanie poprawności wdrożenia przed wykonaniem ją, uruchamiając hello [weryfikowanie wdrożenia szablonu](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Validate) operacji.</span><span class="sxs-lookup"><span data-stu-id="39b94-120">Validate your deployment before executing it by running hello [Validate a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Validate) operation.</span></span> <span data-ttu-id="39b94-121">Podczas testowania wdrożenia hello, należy podać parametry, dokładnie tak jak w przypadku wykonywania hello wdrożenia (pokazano w następnym kroku hello).</span><span class="sxs-lookup"><span data-stu-id="39b94-121">When testing hello deployment, provide parameters exactly as you would when executing hello deployment (shown in hello next step).</span></span>
4. <span data-ttu-id="39b94-122">Tworzenie wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="39b94-122">Create a deployment.</span></span> <span data-ttu-id="39b94-123">Podaj identyfikator subskrypcji, hello nazwę grupy zasobów hello nazwa hello hello wdrożenia i szablon tooyour łącza.</span><span class="sxs-lookup"><span data-stu-id="39b94-123">Provide your subscription ID, hello name of hello resource group, hello name of hello deployment, and a link tooyour template.</span></span> <span data-ttu-id="39b94-124">Informacji o pliku szablonu hello znajduje się w temacie [pliku parametrów](#parameter-file).</span><span class="sxs-lookup"><span data-stu-id="39b94-124">For information about hello template file, see [Parameter file](#parameter-file).</span></span> <span data-ttu-id="39b94-125">Aby uzyskać więcej informacji na temat toocreate interfejsu API REST hello grupę zasobów, zobacz [Utwórz wdrożenie szablonu](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_CreateOrUpdate).</span><span class="sxs-lookup"><span data-stu-id="39b94-125">For more information about hello REST API toocreate a resource group, see [Create a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_CreateOrUpdate).</span></span> <span data-ttu-id="39b94-126">Powiadomienie hello **tryb** ustawiono zbyt**przyrostowe**.</span><span class="sxs-lookup"><span data-stu-id="39b94-126">Notice hello **mode** is set too**Incremental**.</span></span> <span data-ttu-id="39b94-127">Ustaw toorun ukończenia wdrożenia, **tryb** za**Complete**.</span><span class="sxs-lookup"><span data-stu-id="39b94-127">toorun a complete deployment, set **mode** too**Complete**.</span></span> <span data-ttu-id="39b94-128">Należy zachować ostrożność podczas w trybie hello pełne, jak mogą przypadkowo usunięte zasoby, które nie znajdują się w szablonie.</span><span class="sxs-lookup"><span data-stu-id="39b94-128">Be careful when using hello complete mode as you can inadvertently delete resources that are not in your template.</span></span>
   
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
   
      <span data-ttu-id="39b94-129">Toolog zawartości odpowiedzi i żądania zawartości, należy włączyć **debugSetting** w żądaniu hello.</span><span class="sxs-lookup"><span data-stu-id="39b94-129">If you want toolog response content, request content, or both, include **debugSetting** in hello request.</span></span>
   
        "debugSetting": {
          "detailLevel": "requestContent, responseContent"
        }
   
      <span data-ttu-id="39b94-130">Można skonfigurować sieci toouse konta magazynu tokenu sygnatury dostępu Współdzielonego dostępu współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="39b94-130">You can set up your storage account toouse a shared access signature (SAS) token.</span></span> <span data-ttu-id="39b94-131">Aby uzyskać więcej informacji, zobacz [Delegowanie dostępu z sygnaturą dostępu współdzielonego](https://docs.microsoft.com/rest/api/storageservices/delegating-access-with-a-shared-access-signature).</span><span class="sxs-lookup"><span data-stu-id="39b94-131">For more information, see [Delegating Access with a Shared Access Signature](https://docs.microsoft.com/rest/api/storageservices/delegating-access-with-a-shared-access-signature).</span></span>
5. <span data-ttu-id="39b94-132">Pobierz stan hello hello szablonu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="39b94-132">Get hello status of hello template deployment.</span></span> <span data-ttu-id="39b94-133">Aby uzyskać więcej informacji, zobacz [uzyskać informacje na temat wdrażania szablonu](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get).</span><span class="sxs-lookup"><span data-stu-id="39b94-133">For more information, see [Get information about a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get).</span></span>
   
          GET https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>/providers/Microsoft.Resources/deployments/<YourDeploymentName>?api-version=2015-01-01
           <common headers>

## <a name="parameter-file"></a><span data-ttu-id="39b94-134">Plik parametrów</span><span class="sxs-lookup"><span data-stu-id="39b94-134">Parameter file</span></span>

[!INCLUDE [resource-manager-parameter-file](../../includes/resource-manager-parameter-file.md)]

## <a name="next-steps"></a><span data-ttu-id="39b94-135">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="39b94-135">Next steps</span></span>
* <span data-ttu-id="39b94-136">toolearn dotyczące obsługi operacji asynchronicznych REST, zobacz [śledzić operacje asynchroniczne Azure](resource-manager-async-operations.md).</span><span class="sxs-lookup"><span data-stu-id="39b94-136">toolearn about handling asynchronous REST operations, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>
* <span data-ttu-id="39b94-137">Na przykład wdrażania zasobów za pomocą biblioteki klienta .NET hello zobacz [wdrażanie zasobów przy użyciu bibliotek .NET oraz szablonu](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="39b94-137">For an example of deploying resources through hello .NET client library, see [Deploy resources using .NET libraries and a template](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="39b94-138">Parametry toodefine w szablonie, zobacz [tworzenia szablonów](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="39b94-138">toodefine parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="39b94-139">Aby uzyskać wskazówki dotyczące wdrażania środowiska toodifferent rozwiązania, zobacz [środowisk projektowania i testowania na platformie Microsoft Azure](solution-dev-test-environments.md).</span><span class="sxs-lookup"><span data-stu-id="39b94-139">For guidance on deploying your solution toodifferent environments, see [Development and test environments in Microsoft Azure](solution-dev-test-environments.md).</span></span>
* <span data-ttu-id="39b94-140">Aby uzyskać wskazówki dotyczące użycia tooeffectively Menedżera zasobów przedsiębiorstwa Zarządzaj subskrypcjami, zobacz [szkieletu Azure enterprise — ładu przetestowanego subskrypcji](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="39b94-140">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

