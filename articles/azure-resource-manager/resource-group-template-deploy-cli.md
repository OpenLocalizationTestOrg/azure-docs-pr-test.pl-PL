---
title: "aaaDeploy zasobów przy użyciu wiersza polecenia platformy Azure i szablon | Dokumentacja firmy Microsoft"
description: "Za pomocą usługi Azure Resource Manager i interfejsu wiersza polecenia Azure toodeploy tooAzure zasobów. zasoby Hello są definiowane w szablonie usługi Resource Manager."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 493b7932-8d1e-4499-912c-26098282ec95
ms.service: azure-resource-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/31/2017
ms.author: tomfitz
ms.openlocfilehash: 9f8bb9a8720399390a407030d2d32bcd97d32f13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-cli"></a><span data-ttu-id="d0603-104">Deploy resources with Resource Manager templates and Azure CLI (Wdrażanie zasobów za pomocą szablonów usługi Resource Manager i interfejsu wiersza polecenia platformy Azure)</span><span class="sxs-lookup"><span data-stu-id="d0603-104">Deploy resources with Resource Manager templates and Azure CLI</span></span>

<span data-ttu-id="d0603-105">W tym temacie opisano sposób toouse 2.0 interfejsu wiersza polecenia platformy Azure z toodeploy szablonów usługi Resource Manager tooAzure Twojego zasobów.</span><span class="sxs-lookup"><span data-stu-id="d0603-105">This topic explains how toouse Azure CLI 2.0 with Resource Manager templates toodeploy your resources tooAzure.</span></span> <span data-ttu-id="d0603-106">Jeśli nie jesteś znasz koncepcji hello wdrażania i zarządzania rozwiązań platformy Azure, zobacz [Omówienie usługi Azure Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d0603-106">If you are not familiar with hello concepts of deploying and managing your Azure solutions, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>  

<span data-ttu-id="d0603-107">Szablon usługi Resource Manager Hello wdrażania może być pliku lokalnego na komputerze lub plik znajdujący się w repozytorium, takich jak usługi GitHub.</span><span class="sxs-lookup"><span data-stu-id="d0603-107">hello Resource Manager template you deploy can either be a local file on your machine, or an external file that is located in a repository like GitHub.</span></span> <span data-ttu-id="d0603-108">Szablon Hello wdrożenia w tym artykule jest dostępny w hello [przykładowy szablon](#sample-template) sekcji lub jako [szablon konta magazynu w usłudze GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="d0603-108">hello template you deploy in this article is available in hello [Sample template](#sample-template) section, or as a [storage account template in GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span></span>

[!INCLUDE [sample-cli-install](../../includes/sample-cli-install.md)]

<span data-ttu-id="d0603-109">Jeśli nie masz zainstalowanych wiersza polecenia platformy Azure, możesz użyć hello [powłoki chmury](#deploy-template-from-cloud-shell).</span><span class="sxs-lookup"><span data-stu-id="d0603-109">If you do not have Azure CLI installed, you can use hello [Cloud Shell](#deploy-template-from-cloud-shell).</span></span>

## <a name="deploy-local-template"></a><span data-ttu-id="d0603-110">Wdrażanie lokalnego szablonu</span><span class="sxs-lookup"><span data-stu-id="d0603-110">Deploy local template</span></span>

<span data-ttu-id="d0603-111">W przypadku wdrażania tooAzure zasobów, można:</span><span class="sxs-lookup"><span data-stu-id="d0603-111">When deploying resources tooAzure, you:</span></span>

1. <span data-ttu-id="d0603-112">Zaloguj się za tooyour konto platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d0603-112">Log in tooyour Azure account</span></span>
2. <span data-ttu-id="d0603-113">Utwórz grupę zasobów, która służy jako kontener hello hello wdrożonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="d0603-113">Create a resource group that serves as hello container for hello deployed resources.</span></span> <span data-ttu-id="d0603-114">Nazwa Hello hello grupy zasobów może zawierać tylko znaki alfanumeryczne, kropki, podkreślenia, łączniki i nawiasy.</span><span class="sxs-lookup"><span data-stu-id="d0603-114">hello name of hello resource group can only include alphanumeric characters, periods, underscores, hyphens, and parenthesis.</span></span> <span data-ttu-id="d0603-115">Może okazać się too90 znaków.</span><span class="sxs-lookup"><span data-stu-id="d0603-115">It can be up too90 characters.</span></span> <span data-ttu-id="d0603-116">Nie może kończyć się kropką.</span><span class="sxs-lookup"><span data-stu-id="d0603-116">It cannot end in a period.</span></span>
3. <span data-ttu-id="d0603-117">Wdrażanie szablonu hello grupy zasobów toohello, który definiuje hello toocreate zasobów</span><span class="sxs-lookup"><span data-stu-id="d0603-117">Deploy toohello resource group hello template that defines hello resources toocreate</span></span>

<span data-ttu-id="d0603-118">Szablon może zawierać parametrów, które pozwalają toocustomize hello wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="d0603-118">A template can include parameters that enable you toocustomize hello deployment.</span></span> <span data-ttu-id="d0603-119">Na przykład można podać wartości dostosowanych określonym środowisku (na przykład deweloperów, testowego i produkcyjnego).</span><span class="sxs-lookup"><span data-stu-id="d0603-119">For example, you can provide values that are tailored for a particular environment (such as dev, test, and production).</span></span> <span data-ttu-id="d0603-120">Witaj przykładowy szablon definiuje parametru dla konta magazynu hello jednostki SKU.</span><span class="sxs-lookup"><span data-stu-id="d0603-120">hello sample template defines a parameter for hello storage account SKU.</span></span> 

<span data-ttu-id="d0603-121">Witaj poniższy przykład tworzy grupę zasobów i wdraża szablonu z komputera lokalnego:</span><span class="sxs-lookup"><span data-stu-id="d0603-121">hello following example creates a resource group, and deploys a template from your local machine:</span></span>

```azurecli
az login

az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters storageAccountType=Standard_GRS
```

<span data-ttu-id="d0603-122">Witaj wdrożenia może zająć kilka minut toocomplete.</span><span class="sxs-lookup"><span data-stu-id="d0603-122">hello deployment can take a few minutes toocomplete.</span></span> <span data-ttu-id="d0603-123">Po zakończeniu zostanie wyświetlony komunikat zawierający wynik hello:</span><span class="sxs-lookup"><span data-stu-id="d0603-123">When it finishes, you see a message that includes hello result:</span></span>

```azurecli
"provisioningState": "Succeeded",
```

## <a name="deploy-external-template"></a><span data-ttu-id="d0603-124">Wdrażanie szablonu zewnętrznych</span><span class="sxs-lookup"><span data-stu-id="d0603-124">Deploy external template</span></span>

<span data-ttu-id="d0603-125">Zamiast szablony Menedżera zasobów są przechowywane na komputerze lokalnym, możesz wybrać toostore je w lokalizacji zewnętrznej.</span><span class="sxs-lookup"><span data-stu-id="d0603-125">Instead of storing Resource Manager templates on your local machine, you may prefer toostore them in an external location.</span></span> <span data-ttu-id="d0603-126">Szablony można przechowywać w repozytorium kontroli źródła, (na przykład GitHub).</span><span class="sxs-lookup"><span data-stu-id="d0603-126">You can store templates in a source control repository (such as GitHub).</span></span> <span data-ttu-id="d0603-127">Lub przechowywać w koncie magazynu platformy Azure dla dostępu współdzielonego w Twojej organizacji.</span><span class="sxs-lookup"><span data-stu-id="d0603-127">Or, you can store them in an Azure storage account for shared access in your organization.</span></span>

<span data-ttu-id="d0603-128">toodeploy szablonu zewnętrznego, użyj hello **szablon uri** parametru.</span><span class="sxs-lookup"><span data-stu-id="d0603-128">toodeploy an external template, use hello **template-uri** parameter.</span></span> <span data-ttu-id="d0603-129">Użyj hello identyfikatora URI w hello przykład toodeploy hello przykładowy szablon z usługi GitHub.</span><span class="sxs-lookup"><span data-stu-id="d0603-129">Use hello URI in hello example toodeploy hello sample template from GitHub.</span></span>
   
```azurecli
az login

az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json" \
    --parameters storageAccountType=Standard_GRS
```

<span data-ttu-id="d0603-130">Witaj poprzednim przykładzie wymaga publicznie identyfikatora URI dla hello szablonu, który działa w przypadku większości scenariuszy, ponieważ szablon nie może zawierać dane poufne.</span><span class="sxs-lookup"><span data-stu-id="d0603-130">hello preceding example requires a publicly accessible URI for hello template, which works for most scenarios because your template should not include sensitive data.</span></span> <span data-ttu-id="d0603-131">Jeśli potrzebujesz toospecify poufne dane (takie jak hasło administratora), należy przekazać tę wartość jako parametr bezpieczne.</span><span class="sxs-lookup"><span data-stu-id="d0603-131">If you need toospecify sensitive data (like an admin password), pass that value as a secure parameter.</span></span> <span data-ttu-id="d0603-132">Jednak jeśli nie chcesz toobe Twojego szablonu publicznie, można chronić przez zapisanie jej w kontenerze prywatnego magazynu.</span><span class="sxs-lookup"><span data-stu-id="d0603-132">However, if you do not want your template toobe publicly accessible, you can protect it by storing it in a private storage container.</span></span> <span data-ttu-id="d0603-133">Aby uzyskać informacje o wdrażaniu szablonu, który wymaga tokenu sygnatury dostępu Współdzielonego dostępu współdzielonego, zobacz [wdrażanie szablonu prywatnej przy użyciu tokenu sygnatury dostępu Współdzielonego](resource-manager-cli-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="d0603-133">For information about deploying a template that requires a shared access signature (SAS) token, see [Deploy private template with SAS token](resource-manager-cli-sas-token.md).</span></span>

## <a name="deploy-template-from-cloud-shell"></a><span data-ttu-id="d0603-134">Wdrażanie szablonu za pomocą usługi Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="d0603-134">Deploy template from Cloud Shell</span></span>

<span data-ttu-id="d0603-135">Można użyć [powłoki chmury](../cloud-shell/overview.md) toorun hello Azure CLI polecenia do wdrożenia szablonu.</span><span class="sxs-lookup"><span data-stu-id="d0603-135">You can use [Cloud Shell](../cloud-shell/overview.md) toorun hello Azure CLI commands for deploying your template.</span></span> <span data-ttu-id="d0603-136">Jednak należy najpierw załadować szablonu do udziału plików powitania dla powłoki chmury.</span><span class="sxs-lookup"><span data-stu-id="d0603-136">However, you must first load your template into hello file share for your Cloud Shell.</span></span> <span data-ttu-id="d0603-137">Jeśli nie używasz usługi Cloud Shell, zobacz [Overview of Azure Cloud Shell (Omówienie usługi Azure Cloud Shell)](../cloud-shell/overview.md), aby uzyskać informacje o jej konfigurowaniu.</span><span class="sxs-lookup"><span data-stu-id="d0603-137">If you have not used Cloud Shell, see [Overview of Azure Cloud Shell](../cloud-shell/overview.md) for information about setting it up.</span></span>

1. <span data-ttu-id="d0603-138">Zaloguj się za toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d0603-138">Log in toohello [Azure portal](https://portal.azure.com).</span></span>   

2. <span data-ttu-id="d0603-139">Wybierz swoją grupę zasobów usługi Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="d0603-139">Select your Cloud Shell resource group.</span></span> <span data-ttu-id="d0603-140">wzorzec nazwy Hello jest `cloud-shell-storage-<region>`.</span><span class="sxs-lookup"><span data-stu-id="d0603-140">hello name pattern is `cloud-shell-storage-<region>`.</span></span>

   ![Wybieranie grupy zasobów](./media/resource-group-template-deploy-cli/select-cs-resource-group.png)

3. <span data-ttu-id="d0603-142">Wybierz konto magazynu powitania dla powłoki chmury.</span><span class="sxs-lookup"><span data-stu-id="d0603-142">Select hello storage account for your Cloud Shell.</span></span>

   ![Wybieranie konta magazynu](./media/resource-group-template-deploy-cli/select-storage.png)

4. <span data-ttu-id="d0603-144">Wybierz pozycję **Pliki**.</span><span class="sxs-lookup"><span data-stu-id="d0603-144">Select **Files**.</span></span>

   ![Wybieranie pozycji Pliki](./media/resource-group-template-deploy-cli/select-files.png)

5. <span data-ttu-id="d0603-146">Wybierz udział plików powitania dla powłoki chmury.</span><span class="sxs-lookup"><span data-stu-id="d0603-146">Select hello file share for Cloud Shell.</span></span> <span data-ttu-id="d0603-147">wzorzec nazwy Hello jest `cs-<user>-<domain>-com-<uniqueGuid>`.</span><span class="sxs-lookup"><span data-stu-id="d0603-147">hello name pattern is `cs-<user>-<domain>-com-<uniqueGuid>`.</span></span>

   ![Wybieranie udziału plików](./media/resource-group-template-deploy-cli/select-file-share.png)

6. <span data-ttu-id="d0603-149">Wybierz pozycję **Dodaj katalog**.</span><span class="sxs-lookup"><span data-stu-id="d0603-149">Select **Add directory**.</span></span>

   ![Dodawanie katalogu](./media/resource-group-template-deploy-cli/select-add-directory.png)

7. <span data-ttu-id="d0603-151">Nadaj mu nazwę **templates** i wybierz przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="d0603-151">Name it **templates**, and select **Okay**.</span></span>

   ![Nadawanie nazwy katalogowi](./media/resource-group-template-deploy-cli/name-templates.png)

8. <span data-ttu-id="d0603-153">Wybierz swój nowy katalog.</span><span class="sxs-lookup"><span data-stu-id="d0603-153">Select your new directory.</span></span>

   ![Wybieranie katalogu](./media/resource-group-template-deploy-cli/select-templates.png)

9. <span data-ttu-id="d0603-155">Wybierz pozycję **Przekaż**.</span><span class="sxs-lookup"><span data-stu-id="d0603-155">Select **Upload**.</span></span>

   ![Wybieranie pozycji Przekaż](./media/resource-group-template-deploy-cli/select-upload.png)

10. <span data-ttu-id="d0603-157">Znajdź i przekaż swój szablon.</span><span class="sxs-lookup"><span data-stu-id="d0603-157">Find and upload your template.</span></span>

   ![Przekazywanie pliku](./media/resource-group-template-deploy-cli/upload-files.png)

11. <span data-ttu-id="d0603-159">Otwórz hello wiersza.</span><span class="sxs-lookup"><span data-stu-id="d0603-159">Open hello prompt.</span></span>

   ![Otwieranie usługi Cloud Shell](./media/resource-group-template-deploy-cli/start-cloud-shell.png)

12. <span data-ttu-id="d0603-161">Wprowadź następujące polecenia w hello powłoki chmury hello:</span><span class="sxs-lookup"><span data-stu-id="d0603-161">Enter hello following commands in hello Cloud Shell:</span></span>

   ```azurecli
   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json --parameters storageAccountType=Standard_GRS
   ```

## <a name="parameter-files"></a><span data-ttu-id="d0603-162">Pliki parametrów</span><span class="sxs-lookup"><span data-stu-id="d0603-162">Parameter files</span></span>

<span data-ttu-id="d0603-163">Zamiast przekazywanie parametrów jako wartości wbudowany w skrypcie, może być łatwiejsze toouse pliku JSON, który zawiera wartości parametrów hello.</span><span class="sxs-lookup"><span data-stu-id="d0603-163">Rather than passing parameters as inline values in your script, you may find it easier toouse a JSON file that contains hello parameter values.</span></span> <span data-ttu-id="d0603-164">plik parametrów Hello należy hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="d0603-164">hello parameter file must be in hello following format:</span></span>

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

<span data-ttu-id="d0603-165">Zwróć uwagę, że sekcja Parametry hello zawiera nazwę parametru pasującą hello parametrów zdefiniowanych w szablonie (storageAccountType).</span><span class="sxs-lookup"><span data-stu-id="d0603-165">Notice that hello parameters section includes a parameter name that matches hello parameter defined in your template (storageAccountType).</span></span> <span data-ttu-id="d0603-166">plik parametrów Hello zawiera wartość dla parametru hello.</span><span class="sxs-lookup"><span data-stu-id="d0603-166">hello parameter file contains a value for hello parameter.</span></span> <span data-ttu-id="d0603-167">Ta wartość jest automatycznie przekazywana toohello szablonu podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="d0603-167">This value is automatically passed toohello template during deployment.</span></span> <span data-ttu-id="d0603-168">Można utworzyć wiele plików parametru dla różnych scenariuszy wdrażania i przekaż plik odpowiedni parametr hello.</span><span class="sxs-lookup"><span data-stu-id="d0603-168">You can create multiple parameter files for different deployment scenarios, and then pass in hello appropriate parameter file.</span></span> 

<span data-ttu-id="d0603-169">Skopiuj hello poprzedzających przykład i zapisz go jako plik o nazwie `storage.parameters.json`.</span><span class="sxs-lookup"><span data-stu-id="d0603-169">Copy hello preceding example and save it as a file named `storage.parameters.json`.</span></span>

<span data-ttu-id="d0603-170">Użyj toopass pliku lokalnego parametru `@` toospecify lokalnego pliku o nazwie storage.parameters.json.</span><span class="sxs-lookup"><span data-stu-id="d0603-170">toopass a local parameter file, use `@` toospecify a local file named storage.parameters.json.</span></span>

```azurecli
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters @storage.parameters.json
```

## <a name="test-a-template-deployment"></a><span data-ttu-id="d0603-171">Testowanie wdrażania szablonu</span><span class="sxs-lookup"><span data-stu-id="d0603-171">Test a template deployment</span></span>

<span data-ttu-id="d0603-172">Użyj szablonu i parametru wartości bez faktycznie wdrażania żadnych zasobów tootest [zweryfikować wdrożenie grupy az](/cli/azure/group/deployment#validate).</span><span class="sxs-lookup"><span data-stu-id="d0603-172">tootest your template and parameter values without actually deploying any resources, use [az group deployment validate](/cli/azure/group/deployment#validate).</span></span> 

```azurecli
az group deployment validate \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters @storage.parameters.json
```

<span data-ttu-id="d0603-173">Jeśli nie wykryto żadnych błędów, hello polecenie zwraca informacji o wdrażaniu testu hello.</span><span class="sxs-lookup"><span data-stu-id="d0603-173">If no errors are detected, hello command returns information about hello test deployment.</span></span> <span data-ttu-id="d0603-174">W szczególności należy zauważyć, że hello **błąd** ma wartość null.</span><span class="sxs-lookup"><span data-stu-id="d0603-174">In particular, notice that hello **error** value is null.</span></span>

```azurecli
{
  "error": null,
  "properties": {
      ...
```

<span data-ttu-id="d0603-175">Jeśli zostanie wykryty błąd, hello polecenie zwróci komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="d0603-175">If an error is detected, hello command returns an error message.</span></span> <span data-ttu-id="d0603-176">Na przykład próba toopass nieprawidłową wartość dla konta magazynu hello jednostka SKU, zwraca hello następujący błąd:</span><span class="sxs-lookup"><span data-stu-id="d0603-176">For example, attempting toopass an incorrect value for hello storage account SKU, returns hello following error:</span></span>

```azurecli
{
  "error": {
    "code": "InvalidTemplate",
    "details": null,
    "message": "Deployment template validation failed: 'hello provided value 'badSKU' for hello template parameter 
      'storageAccountType' at line '13' and column '20' is not valid. hello parameter value is not part of hello allowed 
      value(s): 'Standard_LRS,Standard_ZRS,Standard_GRS,Standard_RAGRS,Premium_LRS'.'.",
    "target": null
  },
  "properties": null
}
```

<span data-ttu-id="d0603-177">Jeśli szablon zawiera błąd składniowy, polecenie hello zwróci błąd wskazujący, że nie można przeanalizować hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="d0603-177">If your template has a syntax error, hello command returns an error indicating it could not parse hello template.</span></span> <span data-ttu-id="d0603-178">wiadomości powitania wskazuje numer wiersza hello i umieść je hello błąd analizy.</span><span class="sxs-lookup"><span data-stu-id="d0603-178">hello message indicates hello line number and position of hello parsing error.</span></span>

```azurecli
{
  "error": {
    "code": "InvalidTemplate",
    "details": null,
    "message": "Deployment template parse failed: 'After parsing a value an unexpected character was encountered:
      \". Path 'variables', line 31, position 3.'.",
    "target": null
  },
  "properties": null
}
```

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

<span data-ttu-id="d0603-179">Tryb pełną toouse, użyj hello `mode` parametru:</span><span class="sxs-lookup"><span data-stu-id="d0603-179">toouse complete mode, use hello `mode` parameter:</span></span>

```azurecli
az group deployment create \
    --name ExampleDeployment \
    --mode Complete \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters storageAccountType=Standard_GRS
```

## <a name="sample-template"></a><span data-ttu-id="d0603-180">Przykładowy szablon</span><span class="sxs-lookup"><span data-stu-id="d0603-180">Sample template</span></span>

<span data-ttu-id="d0603-181">Witaj następujący szablon jest używany dla hello przykłady w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="d0603-181">hello following template is used for hello examples in this topic.</span></span> <span data-ttu-id="d0603-182">Skopiuj i zapisz go jako plik o nazwie storage.json.</span><span class="sxs-lookup"><span data-stu-id="d0603-182">Copy and save it as a file named storage.json.</span></span> <span data-ttu-id="d0603-183">toounderstand jak toocreate tego szablonu, zobacz [Tworzenie pierwszego szablonu usługi Azure Resource Manager](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="d0603-183">toounderstand how toocreate this template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>  

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

## <a name="next-steps"></a><span data-ttu-id="d0603-184">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d0603-184">Next steps</span></span>
* <span data-ttu-id="d0603-185">Przykłady Hello w tym artykule wdrażanie grupy zasobów tooa zasobów w ramach subskrypcji domyślne.</span><span class="sxs-lookup"><span data-stu-id="d0603-185">hello examples in this article deploy resources tooa resource group in your default subscription.</span></span> <span data-ttu-id="d0603-186">toouse inną subskrypcję, zobacz [zarządzać wieloma subskrypcjami platformy Azure](/cli/azure/manage-azure-subscriptions-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d0603-186">toouse a different subscription, see [Manage multiple Azure subscriptions](/cli/azure/manage-azure-subscriptions-azure-cli).</span></span>
* <span data-ttu-id="d0603-187">Zakończenie przykładowego skryptu, który wdraża szablonu, zobacz [skrypt wdrożenia szablonu usługi Resource Manager](resource-manager-samples-cli-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="d0603-187">For a complete sample script that deploys a template, see [Resource Manager template deployment script](resource-manager-samples-cli-deploy.md).</span></span>
* <span data-ttu-id="d0603-188">toounderstand toodefine parametry w szablonie, zobacz temat [zrozumieć hello struktury i składni szablonów usługi Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="d0603-188">toounderstand how toodefine parameters in your template, see [Understand hello structure and syntax of Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="d0603-189">Aby uzyskać wskazówki dotyczące rozwiązania typowych błędów wdrażania, zobacz [Rozwiąż typowe błędy wdrożenia usługi Azure z usługą Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="d0603-189">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="d0603-190">Aby uzyskać informacje o wdrażaniu szablonu, który wymaga tokenu sygnatury dostępu Współdzielonego, zobacz [wdrażanie szablonu prywatnej przy użyciu tokenu sygnatury dostępu Współdzielonego](resource-manager-cli-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="d0603-190">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-cli-sas-token.md).</span></span>
* <span data-ttu-id="d0603-191">Aby uzyskać wskazówki dotyczące użycia tooeffectively Menedżera zasobów przedsiębiorstwa Zarządzaj subskrypcjami, zobacz [szkieletu Azure enterprise — ładu przetestowanego subskrypcji](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="d0603-191">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
