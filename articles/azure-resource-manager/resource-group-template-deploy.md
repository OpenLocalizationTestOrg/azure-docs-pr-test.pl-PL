---
title: "aaaDeploy zasobów przy użyciu programu PowerShell i szablonu | Dokumentacja firmy Microsoft"
description: "Za pomocą usługi Azure Resource Manager i programu Azure PowerShell toodeploy tooAzure zasobów. zasoby Hello są definiowane w szablonie usługi Resource Manager."
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
ms.openlocfilehash: 41506811ba3c2ea5df6313db70978ade50f71161
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-powershell"></a><span data-ttu-id="ba397-104">Deploy resources with Resource Manager templates and Azure PowerShell (Wdrażanie zasobów za pomocą szablonów usługi Resource Manager i programu Azure PowerShell)</span><span class="sxs-lookup"><span data-stu-id="ba397-104">Deploy resources with Resource Manager templates and Azure PowerShell</span></span>

<span data-ttu-id="ba397-105">W tym temacie opisano sposób toouse programu Azure PowerShell z toodeploy szablonów usługi Resource Manager tooAzure Twojego zasobów.</span><span class="sxs-lookup"><span data-stu-id="ba397-105">This topic explains how toouse Azure PowerShell with Resource Manager templates toodeploy your resources tooAzure.</span></span> <span data-ttu-id="ba397-106">Jeśli nie jesteś znasz koncepcji hello wdrażania i zarządzania rozwiązań platformy Azure, zobacz [Omówienie usługi Azure Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ba397-106">If you are not familiar with hello concepts of deploying and managing your Azure solutions, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

<span data-ttu-id="ba397-107">Szablon usługi Resource Manager Hello wdrażania może być pliku lokalnego na komputerze lub plik znajdujący się w repozytorium, takich jak usługi GitHub.</span><span class="sxs-lookup"><span data-stu-id="ba397-107">hello Resource Manager template you deploy can either be a local file on your machine, or an external file that is located in a repository like GitHub.</span></span> <span data-ttu-id="ba397-108">Szablon Hello wdrożenia w tym artykule jest dostępny w hello [przykładowy szablon](#sample-template) sekcji lub jako [szablon konta magazynu w usłudze GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="ba397-108">hello template you deploy in this article is available in hello [Sample template](#sample-template) section, or as [storage account template in GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span></span>

[!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install.md)]

<a id="deploy-local-template" />

## <a name="deploy-a-template-from-your-local-machine"></a><span data-ttu-id="ba397-109">Wdrażanie szablonu z komputera lokalnego</span><span class="sxs-lookup"><span data-stu-id="ba397-109">Deploy a template from your local machine</span></span>

<span data-ttu-id="ba397-110">W przypadku wdrażania tooAzure zasobów, można:</span><span class="sxs-lookup"><span data-stu-id="ba397-110">When deploying resources tooAzure, you:</span></span>

1. <span data-ttu-id="ba397-111">Zaloguj się za tooyour konto platformy Azure</span><span class="sxs-lookup"><span data-stu-id="ba397-111">Log in tooyour Azure account</span></span>
2. <span data-ttu-id="ba397-112">Utwórz grupę zasobów, która służy jako kontener hello hello wdrożonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="ba397-112">Create a resource group that serves as hello container for hello deployed resources.</span></span> <span data-ttu-id="ba397-113">Nazwa Hello hello grupy zasobów może zawierać tylko znaki alfanumeryczne, kropki, podkreślenia, łączniki i nawiasy.</span><span class="sxs-lookup"><span data-stu-id="ba397-113">hello name of hello resource group can only include alphanumeric characters, periods, underscores, hyphens, and parenthesis.</span></span> <span data-ttu-id="ba397-114">Może okazać się too90 znaków.</span><span class="sxs-lookup"><span data-stu-id="ba397-114">It can be up too90 characters.</span></span> <span data-ttu-id="ba397-115">Nie może kończyć się kropką.</span><span class="sxs-lookup"><span data-stu-id="ba397-115">It cannot end in a period.</span></span>
3. <span data-ttu-id="ba397-116">Wdrażanie szablonu hello grupy zasobów toohello, który definiuje hello toocreate zasobów</span><span class="sxs-lookup"><span data-stu-id="ba397-116">Deploy toohello resource group hello template that defines hello resources toocreate</span></span>

<span data-ttu-id="ba397-117">Szablon może zawierać parametrów, które pozwalają toocustomize hello wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="ba397-117">A template can include parameters that enable you toocustomize hello deployment.</span></span> <span data-ttu-id="ba397-118">Na przykład można podać wartości dostosowanych określonym środowisku (na przykład deweloperów, testowego i produkcyjnego).</span><span class="sxs-lookup"><span data-stu-id="ba397-118">For example, you can provide values that are tailored for a particular environment (such as dev, test, and production).</span></span> <span data-ttu-id="ba397-119">Witaj przykładowy szablon definiuje parametru dla konta magazynu hello jednostki SKU.</span><span class="sxs-lookup"><span data-stu-id="ba397-119">hello sample template defines a parameter for hello storage account SKU.</span></span>

<span data-ttu-id="ba397-120">Witaj poniższy przykład tworzy grupę zasobów i wdraża szablonu z komputera lokalnego:</span><span class="sxs-lookup"><span data-stu-id="ba397-120">hello following example creates a resource group, and deploys a template from your local machine:</span></span>

```powershell
Login-AzureRmAccount
 
New-AzureRmResourceGroup -Name ExampleResourceGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

<span data-ttu-id="ba397-121">Witaj wdrożenia może zająć kilka minut toocomplete.</span><span class="sxs-lookup"><span data-stu-id="ba397-121">hello deployment can take a few minutes toocomplete.</span></span> <span data-ttu-id="ba397-122">Po zakończeniu zostanie wyświetlony komunikat zawierający wynik hello:</span><span class="sxs-lookup"><span data-stu-id="ba397-122">When it finishes, you see a message that includes hello result:</span></span>

```powershell
ProvisioningState       : Succeeded
```

## <a name="deploy-a-template-from-an-external-source"></a><span data-ttu-id="ba397-123">Wdrażanie szablonu z zewnętrznego źródła</span><span class="sxs-lookup"><span data-stu-id="ba397-123">Deploy a template from an external source</span></span>

<span data-ttu-id="ba397-124">Zamiast szablony Menedżera zasobów są przechowywane na komputerze lokalnym, możesz wybrać toostore je w lokalizacji zewnętrznej.</span><span class="sxs-lookup"><span data-stu-id="ba397-124">Instead of storing Resource Manager templates on your local machine, you may prefer toostore them in an external location.</span></span> <span data-ttu-id="ba397-125">Szablony można przechowywać w repozytorium kontroli źródła, (na przykład GitHub).</span><span class="sxs-lookup"><span data-stu-id="ba397-125">You can store templates in a source control repository (such as GitHub).</span></span> <span data-ttu-id="ba397-126">Lub przechowywać w koncie magazynu platformy Azure dla dostępu współdzielonego w Twojej organizacji.</span><span class="sxs-lookup"><span data-stu-id="ba397-126">Or, you can store them in an Azure storage account for shared access in your organization.</span></span>

<span data-ttu-id="ba397-127">toodeploy szablonu zewnętrznego, użyj hello **TemplateUri** parametru.</span><span class="sxs-lookup"><span data-stu-id="ba397-127">toodeploy an external template, use hello **TemplateUri** parameter.</span></span> <span data-ttu-id="ba397-128">Użyj hello identyfikatora URI w hello przykład toodeploy hello przykładowy szablon z usługi GitHub.</span><span class="sxs-lookup"><span data-stu-id="ba397-128">Use hello URI in hello example toodeploy hello sample template from GitHub.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -storageAccountType Standard_GRS
```

<span data-ttu-id="ba397-129">Witaj poprzednim przykładzie wymaga publicznie identyfikatora URI dla hello szablonu, który działa w przypadku większości scenariuszy, ponieważ szablon nie może zawierać dane poufne.</span><span class="sxs-lookup"><span data-stu-id="ba397-129">hello preceding example requires a publicly accessible URI for hello template, which works for most scenarios because your template should not include sensitive data.</span></span> <span data-ttu-id="ba397-130">Jeśli potrzebujesz toospecify poufne dane (takie jak hasło administratora), należy przekazać tę wartość jako parametr bezpieczne.</span><span class="sxs-lookup"><span data-stu-id="ba397-130">If you need toospecify sensitive data (like an admin password), pass that value as a secure parameter.</span></span> <span data-ttu-id="ba397-131">Jednak jeśli nie chcesz toobe Twojego szablonu publicznie, można chronić przez zapisanie jej w kontenerze prywatnego magazynu.</span><span class="sxs-lookup"><span data-stu-id="ba397-131">However, if you do not want your template toobe publicly accessible, you can protect it by storing it in a private storage container.</span></span> <span data-ttu-id="ba397-132">Aby uzyskać informacje o wdrażaniu szablonu, który wymaga tokenu sygnatury dostępu Współdzielonego dostępu współdzielonego, zobacz [wdrażanie szablonu prywatnej przy użyciu tokenu sygnatury dostępu Współdzielonego](resource-manager-powershell-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="ba397-132">For information about deploying a template that requires a shared access signature (SAS) token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>

## <a name="parameter-files"></a><span data-ttu-id="ba397-133">Pliki parametrów</span><span class="sxs-lookup"><span data-stu-id="ba397-133">Parameter files</span></span>

<span data-ttu-id="ba397-134">Zamiast przekazywanie parametrów jako wartości wbudowany w skrypcie, może być łatwiejsze toouse pliku JSON, który zawiera wartości parametrów hello.</span><span class="sxs-lookup"><span data-stu-id="ba397-134">Rather than passing parameters as inline values in your script, you may find it easier toouse a JSON file that contains hello parameter values.</span></span> <span data-ttu-id="ba397-135">plik parametrów Hello należy hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="ba397-135">hello parameter file must be in hello following format:</span></span>

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

<span data-ttu-id="ba397-136">Zwróć uwagę, że sekcja Parametry hello zawiera nazwę parametru pasującą hello parametrów zdefiniowanych w szablonie (storageAccountType).</span><span class="sxs-lookup"><span data-stu-id="ba397-136">Notice that hello parameters section includes a parameter name that matches hello parameter defined in your template (storageAccountType).</span></span> <span data-ttu-id="ba397-137">plik parametrów Hello zawiera wartość dla parametru hello.</span><span class="sxs-lookup"><span data-stu-id="ba397-137">hello parameter file contains a value for hello parameter.</span></span> <span data-ttu-id="ba397-138">Ta wartość jest automatycznie przekazywana toohello szablonu podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="ba397-138">This value is automatically passed toohello template during deployment.</span></span> <span data-ttu-id="ba397-139">Można utworzyć wiele plików parametru dla różnych scenariuszy wdrażania i przekaż plik odpowiedni parametr hello.</span><span class="sxs-lookup"><span data-stu-id="ba397-139">You can create multiple parameter files for different deployment scenarios, and then pass in hello appropriate parameter file.</span></span> 

<span data-ttu-id="ba397-140">Skopiuj hello poprzedzających przykład i zapisz go jako plik o nazwie `storage.parameters.json`.</span><span class="sxs-lookup"><span data-stu-id="ba397-140">Copy hello preceding example and save it as a file named `storage.parameters.json`.</span></span>

<span data-ttu-id="ba397-141">toopass pliku lokalnego parametrów użyj hello **TemplateParameterFile** parametru:</span><span class="sxs-lookup"><span data-stu-id="ba397-141">toopass a local parameter file, use hello **TemplateParameterFile** parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json `
  -TemplateParameterFile c:\MyTemplates\storage.parameters.json
```

<span data-ttu-id="ba397-142">toopass pliku parametrów zewnętrznego, użyj hello **TemplateParameterUri** parametru:</span><span class="sxs-lookup"><span data-stu-id="ba397-142">toopass an external parameter file, use hello **TemplateParameterUri** parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -TemplateParameterUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.parameters.json
```

<span data-ttu-id="ba397-143">Można użyć wbudowanej parametrów i lokalnego parametru plików w hello sam operacji wdrażania.</span><span class="sxs-lookup"><span data-stu-id="ba397-143">You can use inline parameters and a local parameter file in hello same deployment operation.</span></span> <span data-ttu-id="ba397-144">Na przykład możesz określić niektóre wartości w pliku parametrów lokalne powitania i dodać inne wbudowane wartości podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="ba397-144">For example, you can specify some values in hello local parameter file and add other values inline during deployment.</span></span> <span data-ttu-id="ba397-145">Podaj wartości dla parametru w pliku parametrów lokalne powitania i wbudowany, pierwszeństwo ma wartość wbudowanego hello.</span><span class="sxs-lookup"><span data-stu-id="ba397-145">If you provide values for a parameter in both hello local parameter file and inline, hello inline value takes precedence.</span></span>

<span data-ttu-id="ba397-146">Jednak użycie pliku parametrów zewnętrznych, nie można przekazać wartości innych albo wbudowanego lub z pliku lokalnego.</span><span class="sxs-lookup"><span data-stu-id="ba397-146">However, when you use an external parameter file, you cannot pass other values either inline or from a local file.</span></span> <span data-ttu-id="ba397-147">Po określeniu pliku parametrów hello **TemplateParameterUri** parametr, wszystkie parametry są ignorowane w wierszach.</span><span class="sxs-lookup"><span data-stu-id="ba397-147">When you specify a parameter file in hello **TemplateParameterUri** parameter, all inline parameters are ignored.</span></span> <span data-ttu-id="ba397-148">Podaj wszystkie wartości parametrów w pliku zewnętrznym hello.</span><span class="sxs-lookup"><span data-stu-id="ba397-148">Provide all parameter values in hello external file.</span></span> <span data-ttu-id="ba397-149">Jeśli szablon zawiera poufne wartość, która nie może zawierać w pliku parametrów hello, Dodaj magazyn kluczy tooa tej wartości lub dynamicznie Podaj wartości wszystkich parametrów w tekście.</span><span class="sxs-lookup"><span data-stu-id="ba397-149">If your template includes a sensitive value that you cannot include in hello parameter file, either add that value tooa key vault, or dynamically provide all parameter values inline.</span></span>

<span data-ttu-id="ba397-150">Jeśli szablon zawiera parametru z hello takie same nazwy co jeden z parametrów hello w hello polecenia programu PowerShell, programu PowerShell będzie zawierał parametr powitania od szablonu z przyrostek hello **FromTemplate**.</span><span class="sxs-lookup"><span data-stu-id="ba397-150">If your template includes a parameter with hello same name as one of hello parameters in hello PowerShell command, PowerShell presents hello parameter from your template with hello postfix **FromTemplate**.</span></span> <span data-ttu-id="ba397-151">Na przykład parametr o nazwie **ResourceGroupName** Twojego konflikty szablonu z hello **ResourceGroupName** parametru w hello [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment)polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ba397-151">For example, a parameter named **ResourceGroupName** in your template conflicts with hello **ResourceGroupName** parameter in hello [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet.</span></span> <span data-ttu-id="ba397-152">Jesteś tooprovide zostanie wyświetlony monit o wartości **ResourceGroupNameFromTemplate**.</span><span class="sxs-lookup"><span data-stu-id="ba397-152">You are prompted tooprovide a value for **ResourceGroupNameFromTemplate**.</span></span> <span data-ttu-id="ba397-153">Ogólnie rzecz biorąc należy unikać to pomyłka nie nadawanie nazw parametrów z hello takie same nazwy jako parametry używane dla operacji wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="ba397-153">In general, you should avoid this confusion by not naming parameters with hello same name as parameters used for deployment operations.</span></span>

## <a name="test-a-template-deployment"></a><span data-ttu-id="ba397-154">Testowanie wdrażania szablonu</span><span class="sxs-lookup"><span data-stu-id="ba397-154">Test a template deployment</span></span>

<span data-ttu-id="ba397-155">Użyj szablonu i parametru wartości bez faktycznie wdrażania żadnych zasobów tootest [AzureRmResourceGroupDeployment testu](/powershell/module/azurerm.resources/test-azurermresourcegroupdeployment).</span><span class="sxs-lookup"><span data-stu-id="ba397-155">tootest your template and parameter values without actually deploying any resources, use [Test-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/test-azurermresourcegroupdeployment).</span></span> 

```powershell
Test-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

<span data-ttu-id="ba397-156">Jeśli nie wykryto żadnych błędów, polecenie hello kończy działanie bez odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="ba397-156">If no errors are detected, hello command finishes without a response.</span></span> <span data-ttu-id="ba397-157">Jeśli zostanie wykryty błąd, hello polecenie zwróci komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="ba397-157">If an error is detected, hello command returns an error message.</span></span> <span data-ttu-id="ba397-158">Na przykład próba toopass nieprawidłową wartość dla konta magazynu hello jednostka SKU, zwraca hello następujący błąd:</span><span class="sxs-lookup"><span data-stu-id="ba397-158">For example, attempting toopass an incorrect value for hello storage account SKU, returns hello following error:</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName testgroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType badSku

Code    : InvalidTemplate
Message : Deployment template validation failed: 'hello provided value 'badSku' for hello template parameter 'storageAccountType'
          at line '15' and column '24' is not valid. hello parameter value is not part of hello allowed value(s):
          'Standard_LRS,Standard_ZRS,Standard_GRS,Standard_RAGRS,Premium_LRS'.'.
Details :
```

<span data-ttu-id="ba397-159">Jeśli szablon zawiera błąd składniowy, polecenie hello zwróci błąd wskazujący, że nie można przeanalizować hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="ba397-159">If your template has a syntax error, hello command returns an error indicating it could not parse hello template.</span></span> <span data-ttu-id="ba397-160">wiadomości powitania wskazuje numer wiersza hello i umieść je hello błąd analizy.</span><span class="sxs-lookup"><span data-stu-id="ba397-160">hello message indicates hello line number and position of hello parsing error.</span></span>

```powershell
Test-AzureRmResourceGroupDeployment : After parsing a value an unexpected character was encountered: 
  ". Path 'variables', line 31, position 3.
```

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

<span data-ttu-id="ba397-161">Tryb pełną toouse, użyj hello `Mode` parametru:</span><span class="sxs-lookup"><span data-stu-id="ba397-161">toouse complete mode, use hello `Mode` parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Mode Complete -Name ExampleDeployment `
  -ResourceGroupName ExampleResourceGroup -TemplateFile c:\MyTemplates\storage.json 
```

## <a name="sample-template"></a><span data-ttu-id="ba397-162">Przykładowy szablon</span><span class="sxs-lookup"><span data-stu-id="ba397-162">Sample template</span></span>

<span data-ttu-id="ba397-163">Witaj następujący szablon jest używany dla hello przykłady w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="ba397-163">hello following template is used for hello examples in this topic.</span></span> <span data-ttu-id="ba397-164">Skopiuj i zapisz go jako plik o nazwie storage.json.</span><span class="sxs-lookup"><span data-stu-id="ba397-164">Copy and save it as a file named storage.json.</span></span> <span data-ttu-id="ba397-165">toounderstand jak toocreate tego szablonu, zobacz [Tworzenie pierwszego szablonu usługi Azure Resource Manager](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="ba397-165">toounderstand how toocreate this template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>  

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

## <a name="next-steps"></a><span data-ttu-id="ba397-166">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ba397-166">Next steps</span></span>
* <span data-ttu-id="ba397-167">Przykłady Hello w tym artykule wdrażanie grupy zasobów tooa zasobów w ramach subskrypcji domyślne.</span><span class="sxs-lookup"><span data-stu-id="ba397-167">hello examples in this article deploy resources tooa resource group in your default subscription.</span></span> <span data-ttu-id="ba397-168">toouse inną subskrypcję, zobacz [zarządzać wieloma subskrypcjami platformy Azure](/powershell/azure/manage-subscriptions-azureps).</span><span class="sxs-lookup"><span data-stu-id="ba397-168">toouse a different subscription, see [Manage multiple Azure subscriptions](/powershell/azure/manage-subscriptions-azureps).</span></span>
* <span data-ttu-id="ba397-169">Zakończenie przykładowego skryptu, który wdraża szablonu, zobacz [skrypt wdrożenia szablonu usługi Resource Manager](resource-manager-samples-powershell-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="ba397-169">For a complete sample script that deploys a template, see [Resource Manager template deployment script](resource-manager-samples-powershell-deploy.md).</span></span>
* <span data-ttu-id="ba397-170">toounderstand toodefine parametry w szablonie, zobacz temat [zrozumieć hello struktury i składni szablonów usługi Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="ba397-170">toounderstand how toodefine parameters in your template, see [Understand hello structure and syntax of Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="ba397-171">Aby uzyskać wskazówki dotyczące rozwiązania typowych błędów wdrażania, zobacz [Rozwiąż typowe błędy wdrożenia usługi Azure z usługą Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="ba397-171">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="ba397-172">Aby uzyskać informacje o wdrażaniu szablonu, który wymaga tokenu sygnatury dostępu Współdzielonego, zobacz [wdrażanie szablonu prywatnej przy użyciu tokenu sygnatury dostępu Współdzielonego](resource-manager-powershell-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="ba397-172">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>
* <span data-ttu-id="ba397-173">Aby uzyskać wskazówki dotyczące użycia tooeffectively Menedżera zasobów przedsiębiorstwa Zarządzaj subskrypcjami, zobacz [szkieletu Azure enterprise — ładu przetestowanego subskrypcji](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="ba397-173">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

