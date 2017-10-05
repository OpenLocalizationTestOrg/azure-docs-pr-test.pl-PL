---
title: "Wdrażanie zasobów przy użyciu programu PowerShell i szablonu | Dokumentacja firmy Microsoft"
description: "Użyj usługi Azure Resource Manager i programu Azure PowerShell, aby wdrożyć zasobów na platformie Azure. Zasoby są zdefiniowane w szablonie usługi Resource Manager."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 55903f35-6c16-4c6d-bf52-dbf365605c3f
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 5f395abf8ebdfbac18fd17d8183b392673e280ec
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-powershell"></a><span data-ttu-id="d9404-104">Deploy resources with Resource Manager templates and Azure PowerShell (Wdrażanie zasobów za pomocą szablonów usługi Resource Manager i programu Azure PowerShell)</span><span class="sxs-lookup"><span data-stu-id="d9404-104">Deploy resources with Resource Manager templates and Azure PowerShell</span></span>

<span data-ttu-id="d9404-105">W tym temacie wyjaśniono, jak wdrażanie zasobów na platformie Azure przy użyciu programu Azure PowerShell z szablonami usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d9404-105">This topic explains how to use Azure PowerShell with Resource Manager templates to deploy your resources to Azure.</span></span> <span data-ttu-id="d9404-106">Jeśli nie jesteś znasz koncepcji wdrażania i zarządzania rozwiązań platformy Azure, zobacz [Omówienie usługi Azure Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d9404-106">If you are not familiar with the concepts of deploying and managing your Azure solutions, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

<span data-ttu-id="d9404-107">Szablon usługi Resource Manager wdrażania może być pliku lokalnego na komputerze lub plik znajdujący się w repozytorium, takich jak usługi GitHub.</span><span class="sxs-lookup"><span data-stu-id="d9404-107">The Resource Manager template you deploy can either be a local file on your machine, or an external file that is located in a repository like GitHub.</span></span> <span data-ttu-id="d9404-108">Szablon wdrożenia w tym artykule jest dostępny w [przykładowy szablon](#sample-template) sekcji lub jako [szablon konta magazynu w usłudze GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="d9404-108">The template you deploy in this article is available in the [Sample template](#sample-template) section, or as [storage account template in GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span></span>

[!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install.md)]

<a id="deploy-local-template" />

## <a name="deploy-a-template-from-your-local-machine"></a><span data-ttu-id="d9404-109">Wdrażanie szablonu z komputera lokalnego</span><span class="sxs-lookup"><span data-stu-id="d9404-109">Deploy a template from your local machine</span></span>

<span data-ttu-id="d9404-110">W przypadku wdrażania zasobów na platformie Azure, możesz:</span><span class="sxs-lookup"><span data-stu-id="d9404-110">When deploying resources to Azure, you:</span></span>

1. <span data-ttu-id="d9404-111">Zaloguj się do konta platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d9404-111">Log in to your Azure account</span></span>
2. <span data-ttu-id="d9404-112">Utwórz grupę zasobów, która służy jako kontener dla wdrożonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="d9404-112">Create a resource group that serves as the container for the deployed resources.</span></span> <span data-ttu-id="d9404-113">Nazwa grupy zasobów może zawierać tylko znaki alfanumeryczne, kropki, podkreślenia, łączniki i nawiasy.</span><span class="sxs-lookup"><span data-stu-id="d9404-113">The name of the resource group can only include alphanumeric characters, periods, underscores, hyphens, and parenthesis.</span></span> <span data-ttu-id="d9404-114">Można go do 90 znaków.</span><span class="sxs-lookup"><span data-stu-id="d9404-114">It can be up to 90 characters.</span></span> <span data-ttu-id="d9404-115">Nie może kończyć się kropką.</span><span class="sxs-lookup"><span data-stu-id="d9404-115">It cannot end in a period.</span></span>
3. <span data-ttu-id="d9404-116">Wdrożyć szablon, który definiuje zasoby do utworzenia grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="d9404-116">Deploy to the resource group the template that defines the resources to create</span></span>

<span data-ttu-id="d9404-117">Szablon może zawierać parametrów, które umożliwiają dostosowanie wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="d9404-117">A template can include parameters that enable you to customize the deployment.</span></span> <span data-ttu-id="d9404-118">Na przykład można podać wartości dostosowanych określonym środowisku (na przykład deweloperów, testowego i produkcyjnego).</span><span class="sxs-lookup"><span data-stu-id="d9404-118">For example, you can provide values that are tailored for a particular environment (such as dev, test, and production).</span></span> <span data-ttu-id="d9404-119">Przykładowy szablon definiuje parametru dla konta magazynu wersji.</span><span class="sxs-lookup"><span data-stu-id="d9404-119">The sample template defines a parameter for the storage account SKU.</span></span>

<span data-ttu-id="d9404-120">Poniższy przykład tworzy grupę zasobów, a następnie wdraża szablonu z komputera lokalnego:</span><span class="sxs-lookup"><span data-stu-id="d9404-120">The following example creates a resource group, and deploys a template from your local machine:</span></span>

```powershell
Login-AzureRmAccount
 
New-AzureRmResourceGroup -Name ExampleResourceGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

<span data-ttu-id="d9404-121">Wdrożenie może potrwać kilka minut.</span><span class="sxs-lookup"><span data-stu-id="d9404-121">The deployment can take a few minutes to complete.</span></span> <span data-ttu-id="d9404-122">Po zakończeniu zostanie wyświetlony komunikat zawierający wynik:</span><span class="sxs-lookup"><span data-stu-id="d9404-122">When it finishes, you see a message that includes the result:</span></span>

```powershell
ProvisioningState       : Succeeded
```

## <a name="deploy-a-template-from-an-external-source"></a><span data-ttu-id="d9404-123">Wdrażanie szablonu z zewnętrznego źródła</span><span class="sxs-lookup"><span data-stu-id="d9404-123">Deploy a template from an external source</span></span>

<span data-ttu-id="d9404-124">Zamiast szablony Menedżera zasobów są przechowywane na komputerze lokalnym, można przechowywać je w lokalizacji zewnętrznej.</span><span class="sxs-lookup"><span data-stu-id="d9404-124">Instead of storing Resource Manager templates on your local machine, you may prefer to store them in an external location.</span></span> <span data-ttu-id="d9404-125">Szablony można przechowywać w repozytorium kontroli źródła, (na przykład GitHub).</span><span class="sxs-lookup"><span data-stu-id="d9404-125">You can store templates in a source control repository (such as GitHub).</span></span> <span data-ttu-id="d9404-126">Lub przechowywać w koncie magazynu platformy Azure dla dostępu współdzielonego w Twojej organizacji.</span><span class="sxs-lookup"><span data-stu-id="d9404-126">Or, you can store them in an Azure storage account for shared access in your organization.</span></span>

<span data-ttu-id="d9404-127">Aby wdrożyć szablon zewnętrznego, użyj **TemplateUri** parametru.</span><span class="sxs-lookup"><span data-stu-id="d9404-127">To deploy an external template, use the **TemplateUri** parameter.</span></span> <span data-ttu-id="d9404-128">Użyj identyfikatora URI w przykładzie, aby wdrożyć przykładowy szablon z usługi GitHub.</span><span class="sxs-lookup"><span data-stu-id="d9404-128">Use the URI in the example to deploy the sample template from GitHub.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -storageAccountType Standard_GRS
```

<span data-ttu-id="d9404-129">Powyższy przykład wymaga publicznie identyfikatora URI dla szablonu, który działa w przypadku większości scenariuszy, ponieważ szablon nie może zawierać dane poufne.</span><span class="sxs-lookup"><span data-stu-id="d9404-129">The preceding example requires a publicly accessible URI for the template, which works for most scenarios because your template should not include sensitive data.</span></span> <span data-ttu-id="d9404-130">Jeśli trzeba określić poufne dane (takie jak hasło administratora), należy przekazać tę wartość jako parametr bezpieczne.</span><span class="sxs-lookup"><span data-stu-id="d9404-130">If you need to specify sensitive data (like an admin password), pass that value as a secure parameter.</span></span> <span data-ttu-id="d9404-131">Jednak jeśli nie chcesz, aby szablon był publicznie dostępny, można chronić przez zapisanie jej w kontenerze prywatnego magazynu.</span><span class="sxs-lookup"><span data-stu-id="d9404-131">However, if you do not want your template to be publicly accessible, you can protect it by storing it in a private storage container.</span></span> <span data-ttu-id="d9404-132">Aby uzyskać informacje o wdrażaniu szablonu, który wymaga tokenu sygnatury dostępu Współdzielonego dostępu współdzielonego, zobacz [wdrażanie szablonu prywatnej przy użyciu tokenu sygnatury dostępu Współdzielonego](resource-manager-powershell-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="d9404-132">For information about deploying a template that requires a shared access signature (SAS) token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>

## <a name="parameter-files"></a><span data-ttu-id="d9404-133">Pliki parametrów</span><span class="sxs-lookup"><span data-stu-id="d9404-133">Parameter files</span></span>

<span data-ttu-id="d9404-134">Zamiast przekazywanie parametrów jako wartości wbudowany w skrypcie, może okazać łatwiejsze w pliku JSON, który zawiera wartości parametrów.</span><span class="sxs-lookup"><span data-stu-id="d9404-134">Rather than passing parameters as inline values in your script, you may find it easier to use a JSON file that contains the parameter values.</span></span> <span data-ttu-id="d9404-135">Plik parametru musi być w następującym formacie:</span><span class="sxs-lookup"><span data-stu-id="d9404-135">The parameter file must be in the following format:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
     "storageAccountType": {
         "value": "Standard_GRS"
     }
  }
}
```

<span data-ttu-id="d9404-136">Zwróć uwagę, że w sekcji parametrów zawiera nazwę parametru, która odpowiada parametrowi zdefiniowanych w szablonie (storageAccountType).</span><span class="sxs-lookup"><span data-stu-id="d9404-136">Notice that the parameters section includes a parameter name that matches the parameter defined in your template (storageAccountType).</span></span> <span data-ttu-id="d9404-137">Plik parametrów zawiera wartość dla parametru.</span><span class="sxs-lookup"><span data-stu-id="d9404-137">The parameter file contains a value for the parameter.</span></span> <span data-ttu-id="d9404-138">Ta wartość jest automatycznie przekazywane do szablonu podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="d9404-138">This value is automatically passed to the template during deployment.</span></span> <span data-ttu-id="d9404-139">Można utworzyć wiele plików parametru dla różnych scenariuszy wdrażania i przekaż plik odpowiedni parametr.</span><span class="sxs-lookup"><span data-stu-id="d9404-139">You can create multiple parameter files for different deployment scenarios, and then pass in the appropriate parameter file.</span></span> 

<span data-ttu-id="d9404-140">Skopiuj poprzedniego przykładu i zapisz go jako plik o nazwie `storage.parameters.json`.</span><span class="sxs-lookup"><span data-stu-id="d9404-140">Copy the preceding example and save it as a file named `storage.parameters.json`.</span></span>

<span data-ttu-id="d9404-141">Aby przekazać pliku lokalnego parametrów, należy użyć **TemplateParameterFile** parametru:</span><span class="sxs-lookup"><span data-stu-id="d9404-141">To pass a local parameter file, use the **TemplateParameterFile** parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json `
  -TemplateParameterFile c:\MyTemplates\storage.parameters.json
```

<span data-ttu-id="d9404-142">Aby przekazać plik parametrów zewnętrznego, użyj **TemplateParameterUri** parametru:</span><span class="sxs-lookup"><span data-stu-id="d9404-142">To pass an external parameter file, use the **TemplateParameterUri** parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -TemplateParameterUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.parameters.json
```

<span data-ttu-id="d9404-143">Można użyć wbudowanej parametrów i pliku parametrów lokalne w tej samej operacji wdrażania.</span><span class="sxs-lookup"><span data-stu-id="d9404-143">You can use inline parameters and a local parameter file in the same deployment operation.</span></span> <span data-ttu-id="d9404-144">Na przykład możesz określić niektóre wartości w pliku lokalnym parametru i dodać inne wbudowane wartości podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="d9404-144">For example, you can specify some values in the local parameter file and add other values inline during deployment.</span></span> <span data-ttu-id="d9404-145">Podaj wartości dla parametru w pliku lokalnym parametrów i wbudowany, pierwszeństwo ma wartość wbudowanego.</span><span class="sxs-lookup"><span data-stu-id="d9404-145">If you provide values for a parameter in both the local parameter file and inline, the inline value takes precedence.</span></span>

<span data-ttu-id="d9404-146">Jednak użycie pliku parametrów zewnętrznych, nie można przekazać wartości innych albo wbudowanego lub z pliku lokalnego.</span><span class="sxs-lookup"><span data-stu-id="d9404-146">However, when you use an external parameter file, you cannot pass other values either inline or from a local file.</span></span> <span data-ttu-id="d9404-147">Po określeniu pliku parametrów w **TemplateParameterUri** parametr, wszystkie parametry są ignorowane w wierszach.</span><span class="sxs-lookup"><span data-stu-id="d9404-147">When you specify a parameter file in the **TemplateParameterUri** parameter, all inline parameters are ignored.</span></span> <span data-ttu-id="d9404-148">Podaj wszystkie wartości parametrów w pliku zewnętrznym.</span><span class="sxs-lookup"><span data-stu-id="d9404-148">Provide all parameter values in the external file.</span></span> <span data-ttu-id="d9404-149">Jeśli szablon zawiera poufne wartość, która w pliku parametrów nie można uwzględnić, Dodaj tę wartość do magazynu kluczy lub dynamicznie Podaj wartości wszystkich parametrów w tekście.</span><span class="sxs-lookup"><span data-stu-id="d9404-149">If your template includes a sensitive value that you cannot include in the parameter file, either add that value to a key vault, or dynamically provide all parameter values inline.</span></span>

<span data-ttu-id="d9404-150">Jeśli szablon zawiera parametru o takiej samej nazwie jak jeden z parametrów polecenia programu PowerShell, programu PowerShell będzie zawierał z przyrostek parametru z szablonu **FromTemplate**.</span><span class="sxs-lookup"><span data-stu-id="d9404-150">If your template includes a parameter with the same name as one of the parameters in the PowerShell command, PowerShell presents the parameter from your template with the postfix **FromTemplate**.</span></span> <span data-ttu-id="d9404-151">Na przykład parametr o nazwie **ResourceGroupName** Twojego konflikty szablonu z **ResourceGroupName** parametru w [AzureRmResourceGroupDeployment nowy](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d9404-151">For example, a parameter named **ResourceGroupName** in your template conflicts with the **ResourceGroupName** parameter in the [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet.</span></span> <span data-ttu-id="d9404-152">Zostanie wyświetlony monit o podać wartości **ResourceGroupNameFromTemplate**.</span><span class="sxs-lookup"><span data-stu-id="d9404-152">You are prompted to provide a value for **ResourceGroupNameFromTemplate**.</span></span> <span data-ttu-id="d9404-153">Ogólnie rzecz biorąc należy unikać to pomyłka nie nadawanie nazw parametrów o takiej samej nazwie jako parametry używane dla operacji wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="d9404-153">In general, you should avoid this confusion by not naming parameters with the same name as parameters used for deployment operations.</span></span>

## <a name="test-a-template-deployment"></a><span data-ttu-id="d9404-154">Testowanie wdrażania szablonu</span><span class="sxs-lookup"><span data-stu-id="d9404-154">Test a template deployment</span></span>

<span data-ttu-id="d9404-155">Aby przetestować z szablonu i wartości parametrów bez faktycznie wdrażania zasobów, wpisz [AzureRmResourceGroupDeployment testu](/powershell/module/azurerm.resources/test-azurermresourcegroupdeployment).</span><span class="sxs-lookup"><span data-stu-id="d9404-155">To test your template and parameter values without actually deploying any resources, use [Test-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/test-azurermresourcegroupdeployment).</span></span> 

```powershell
Test-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

<span data-ttu-id="d9404-156">Jeśli nie wykryto żadnych błędów, polecenie kończy działanie bez odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="d9404-156">If no errors are detected, the command finishes without a response.</span></span> <span data-ttu-id="d9404-157">Jeśli zostanie wykryty błąd, polecenie zwróci komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="d9404-157">If an error is detected, the command returns an error message.</span></span> <span data-ttu-id="d9404-158">Na przykład próba przekazania nieprawidłową wartość dla konta magazynu jednostka SKU, zwraca następujący błąd:</span><span class="sxs-lookup"><span data-stu-id="d9404-158">For example, attempting to pass an incorrect value for the storage account SKU, returns the following error:</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName testgroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType badSku

Code    : InvalidTemplate
Message : Deployment template validation failed: 'The provided value 'badSku' for the template parameter 'storageAccountType'
          at line '15' and column '24' is not valid. The parameter value is not part of the allowed value(s):
          'Standard_LRS,Standard_ZRS,Standard_GRS,Standard_RAGRS,Premium_LRS'.'.
Details :
```

<span data-ttu-id="d9404-159">Jeśli szablon zawiera błąd składniowy, polecenie zwróci błąd wskazujący, że nie można przetworzyć szablonu.</span><span class="sxs-lookup"><span data-stu-id="d9404-159">If your template has a syntax error, the command returns an error indicating it could not parse the template.</span></span> <span data-ttu-id="d9404-160">Komunikat wskazuje numer wiersza i umieść je błąd analizy.</span><span class="sxs-lookup"><span data-stu-id="d9404-160">The message indicates the line number and position of the parsing error.</span></span>

```powershell
Test-AzureRmResourceGroupDeployment : After parsing a value an unexpected character was encountered: 
  ". Path 'variables', line 31, position 3.
```

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

<span data-ttu-id="d9404-161">Aby użyć trybu pełną, użyj `Mode` parametru:</span><span class="sxs-lookup"><span data-stu-id="d9404-161">To use complete mode, use the `Mode` parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Mode Complete -Name ExampleDeployment `
  -ResourceGroupName ExampleResourceGroup -TemplateFile c:\MyTemplates\storage.json 
```

## <a name="sample-template"></a><span data-ttu-id="d9404-162">Przykładowy szablon</span><span class="sxs-lookup"><span data-stu-id="d9404-162">Sample template</span></span>

<span data-ttu-id="d9404-163">Następujący szablon jest używany w przykładach w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="d9404-163">The following template is used for the examples in this topic.</span></span> <span data-ttu-id="d9404-164">Skopiuj i zapisz go jako plik o nazwie storage.json.</span><span class="sxs-lookup"><span data-stu-id="d9404-164">Copy and save it as a file named storage.json.</span></span> <span data-ttu-id="d9404-165">Aby poznać sposobu tworzenia tego szablonu, zobacz [Tworzenie pierwszego szablonu usługi Azure Resource Manager](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="d9404-165">To understand how to create this template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>  

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageAccountType": {
      "type": "string",
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS",
        "Premium_LRS"
      ],
      "metadata": {
        "description": "Storage Account type"
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "2016-01-01",
      "location": "[resourceGroup().location]",
      "sku": {
          "name": "[parameters('storageAccountType')]"
      },
      "kind": "Storage", 
      "properties": {
      }
    }
  ],
  "outputs": {
      "storageAccountName": {
          "type": "string",
          "value": "[variables('storageAccountName')]"
      }
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="d9404-166">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d9404-166">Next steps</span></span>
* <span data-ttu-id="d9404-167">Przykłady w tym artykule wdrożenie zasobów do grupy zasobów w ramach subskrypcji domyślne.</span><span class="sxs-lookup"><span data-stu-id="d9404-167">The examples in this article deploy resources to a resource group in your default subscription.</span></span> <span data-ttu-id="d9404-168">Aby użyć innej subskrypcji, zobacz [zarządzać wieloma subskrypcjami platformy Azure](/powershell/azure/manage-subscriptions-azureps).</span><span class="sxs-lookup"><span data-stu-id="d9404-168">To use a different subscription, see [Manage multiple Azure subscriptions](/powershell/azure/manage-subscriptions-azureps).</span></span>
* <span data-ttu-id="d9404-169">Zakończenie przykładowego skryptu, który wdraża szablonu, zobacz [skrypt wdrożenia szablonu usługi Resource Manager](resource-manager-samples-powershell-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="d9404-169">For a complete sample script that deploys a template, see [Resource Manager template deployment script](resource-manager-samples-powershell-deploy.md).</span></span>
* <span data-ttu-id="d9404-170">Aby poznać sposób definiowania parametry w szablonie, zobacz [poznać strukturę i składni szablonów usługi Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="d9404-170">To understand how to define parameters in your template, see [Understand the structure and syntax of Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="d9404-171">Aby uzyskać wskazówki dotyczące rozwiązania typowych błędów wdrażania, zobacz [Rozwiąż typowe błędy wdrożenia usługi Azure z usługą Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="d9404-171">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="d9404-172">Aby uzyskać informacje o wdrażaniu szablonu, który wymaga tokenu sygnatury dostępu Współdzielonego, zobacz [wdrażanie szablonu prywatnej przy użyciu tokenu sygnatury dostępu Współdzielonego](resource-manager-powershell-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="d9404-172">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>
* <span data-ttu-id="d9404-173">Aby uzyskać instrukcje dla przedsiębiorstw dotyczące użycia usługi Resource Manager w celu efektywnego zarządzania subskrypcjami, zobacz [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md) (Szkielet platformy Azure dla przedsiębiorstwa — narzucony nadzór subskrypcji).</span><span class="sxs-lookup"><span data-stu-id="d9404-173">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

