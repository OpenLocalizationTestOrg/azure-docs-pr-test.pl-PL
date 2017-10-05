---
title: "Tworzenie pierwszego szablonu usługi Azure Resource Manager | Microsoft Docs"
description: "Przewodnik krok po kroku dotyczący tworzenia pierwszego szablonu usługi Azure Resource Manager. Przewodnik pokazuje sposób użycia odwołania do szablonu dla konta magazynu w celu utworzenia szablonu."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 07/27/2017
ms.topic: get-started-article
ms.author: tomfitz
ms.openlocfilehash: 49086b51e2db1aebed45746306ae14b6f1feb631
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-deploy-your-first-azure-resource-manager-template"></a><span data-ttu-id="63dd5-104">Tworzenie i wdrażanie pierwszego szablonu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="63dd5-104">Create and deploy your first Azure Resource Manager template</span></span>
<span data-ttu-id="63dd5-105">W tym temacie szczegółowo omówiono kroki tworzenia pierwszego szablonu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="63dd5-105">This topic walks you through the steps of creating your first Azure Resource Manager template.</span></span> <span data-ttu-id="63dd5-106">Szablony usługi Resource Manager są plikami JSON definiującymi zasoby, które należy wdrożyć dla danego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="63dd5-106">Resource Manager templates are JSON files that define the resources you need to deploy for your solution.</span></span> <span data-ttu-id="63dd5-107">Aby zrozumieć pojęcia związane z wdrażaniem rozwiązań platformy Azure i zarządzaniem nimi, zobacz [Usługa Azure Resource Manager — omówienie](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="63dd5-107">To understand the concepts associated with deploying and managing your Azure solutions, see [Azure Resource Manager overview](resource-group-overview.md).</span></span> <span data-ttu-id="63dd5-108">Jeśli masz istniejące zasoby i chcesz uzyskać szablon dla tych zasobów, zobacz [Eksportowanie szablonu usługi Azure Resource Manager z istniejących zasobów](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="63dd5-108">If you have existing resources and want to get a template for those resources, see [Export an Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>

<span data-ttu-id="63dd5-109">Aby utworzyć i sprawdzić szablony, potrzebujesz edytora plików JSON.</span><span class="sxs-lookup"><span data-stu-id="63dd5-109">To create and revise templates, you need a JSON editor.</span></span> <span data-ttu-id="63dd5-110">[Visual Studio Code](https://code.visualstudio.com/) to lekki edytor kodu typu open-source dla wielu platform.</span><span class="sxs-lookup"><span data-stu-id="63dd5-110">[Visual Studio Code](https://code.visualstudio.com/) is a lightweight, open-source, cross-platform code editor.</span></span> <span data-ttu-id="63dd5-111">Zdecydowanie zalecamy używanie programu Visual Studio Code do tworzenia szablonów usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="63dd5-111">We strongly recommend using Visual Studio Code for creating Resource Manager templates.</span></span> <span data-ttu-id="63dd5-112">W tym temacie założono, że używasz programu VS Code. Jeśli jednak masz inny edytor plików JSON (np. program Visual Studio), możesz użyć tego edytora.</span><span class="sxs-lookup"><span data-stu-id="63dd5-112">This topic assumes you are using VS Code; however, if you have another JSON editor (like Visual Studio), you can use that editor.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="63dd5-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="63dd5-113">Prerequisites</span></span>

* <span data-ttu-id="63dd5-114">Program Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="63dd5-114">Visual Studio Code.</span></span> <span data-ttu-id="63dd5-115">W razie potrzeby zainstaluj go ze strony [https://code.visualstudio.com/](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="63dd5-115">If needed, install it from [https://code.visualstudio.com/](https://code.visualstudio.com/).</span></span>
* <span data-ttu-id="63dd5-116">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="63dd5-116">An Azure subscription.</span></span> <span data-ttu-id="63dd5-117">Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="63dd5-117">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="create-template"></a><span data-ttu-id="63dd5-118">Tworzenie szablonu</span><span class="sxs-lookup"><span data-stu-id="63dd5-118">Create template</span></span>

<span data-ttu-id="63dd5-119">Zacznijmy od prostego szablonu, który wdraża konto magazynu w Twojej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="63dd5-119">Let's start with a simple template that deploys a storage account to your subscription.</span></span>

1. <span data-ttu-id="63dd5-120">Wybierz pozycję **Plik** > **Nowy plik**.</span><span class="sxs-lookup"><span data-stu-id="63dd5-120">Select **File** > **New File**.</span></span> 

   ![Nowy plik](./media/resource-manager-create-first-template/new-file.png)

2. <span data-ttu-id="63dd5-122">Skopiuj i wklej następującą składnię JSON do pliku:</span><span class="sxs-lookup"><span data-stu-id="63dd5-122">Copy and paste the following JSON syntax into your file:</span></span>

   ```json
   {
     "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
     "contentVersion": "1.0.0.0",
     "parameters": {
     },
     "variables": {
     },
     "resources": [
       {
         "name": "[concat('storage', uniqueString(resourceGroup().id))]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "sku": {
           "name": "Standard_LRS"
         },
         "kind": "Storage",
         "location": "South Central US",
         "tags": {},
         "properties": {}
       }
     ],
     "outputs": {  }
   }
   ```

   <span data-ttu-id="63dd5-123">Nazwy kont magazynu podlegają kilku ograniczeniom, które utrudniają ich skonfigurowanie.</span><span class="sxs-lookup"><span data-stu-id="63dd5-123">Storage account names have several restrictions that make them difficult to set.</span></span> <span data-ttu-id="63dd5-124">Nazwa musi mieć od 3 do 24 znaków długości, zawierać wyłącznie cyfry i małe litery oraz musi być unikatowa.</span><span class="sxs-lookup"><span data-stu-id="63dd5-124">The name must be between 3 and 24 characters in length, use only numbers and lower-case letters, and be unique.</span></span> <span data-ttu-id="63dd5-125">Powyższy szablon używa funkcji [uniqueString](resource-group-template-functions-string.md#uniquestring) do generowania wartości skrótu.</span><span class="sxs-lookup"><span data-stu-id="63dd5-125">The preceding template uses the [uniqueString](resource-group-template-functions-string.md#uniquestring) function to generate a hash value.</span></span> <span data-ttu-id="63dd5-126">Aby nadać więcej znaczenia tej wartości skrótu, dodawany jest prefiks *storage*.</span><span class="sxs-lookup"><span data-stu-id="63dd5-126">To give this hash value more meaning, it adds the prefix *storage*.</span></span> 

3. <span data-ttu-id="63dd5-127">Zapisz ten plik pod nazwą **azuredeploy.json** w folderze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="63dd5-127">Save this file as **azuredeploy.json** to a local folder.</span></span>

   ![Zapisywanie szablonu](./media/resource-manager-create-first-template/save-template.png)

## <a name="deploy-template"></a><span data-ttu-id="63dd5-129">Wdrażanie szablonu</span><span class="sxs-lookup"><span data-stu-id="63dd5-129">Deploy template</span></span>

<span data-ttu-id="63dd5-130">Wszystko jest teraz gotowe do wdrożenia tego szablonu.</span><span class="sxs-lookup"><span data-stu-id="63dd5-130">You are ready to deploy this template.</span></span> <span data-ttu-id="63dd5-131">Użyjesz programu PowerShell lub interfejsu wiersza polecenia platformy Azure, aby utworzyć grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="63dd5-131">You use either PowerShell or Azure CLI to create a resource group.</span></span> <span data-ttu-id="63dd5-132">Następnie wdrożysz konto magazynu w tej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="63dd5-132">Then, you deploy a storage account to that resource group.</span></span>

* <span data-ttu-id="63dd5-133">W przypadku programu PowerShell użyj następujących poleceń z poziomu folderu zawierającego szablon:</span><span class="sxs-lookup"><span data-stu-id="63dd5-133">For PowerShell, use the following commands from the folder containing the template:</span></span>

   ```powershell
   Login-AzureRmAccount
   
   New-AzureRmResourceGroup -Name examplegroup -Location "South Central US"
   New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json
   ```

* <span data-ttu-id="63dd5-134">W przypadku lokalnej instalacji interfejsu wiersza polecenia platformy Azure użyj następujących poleceń z poziomu folderu zawierającego szablon:</span><span class="sxs-lookup"><span data-stu-id="63dd5-134">For a local installation of Azure CLI, use the following commands from the folder containing the template:</span></span>

   ```azurecli
   az login

   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file azuredeploy.json
   ```

<span data-ttu-id="63dd5-135">Po zakończeniu wdrażania Twoje konto magazynu będzie istnieć w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="63dd5-135">When deployment finishes, your storage account exists in the resource group.</span></span>

## <a name="deploy-template-from-cloud-shell"></a><span data-ttu-id="63dd5-136">Wdrażanie szablonu za pomocą usługi Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="63dd5-136">Deploy template from Cloud Shell</span></span>

<span data-ttu-id="63dd5-137">Do uruchamiania poleceń interfejsu wiersza polecenia platformy Azure w celu wdrożenia szablonu możesz użyć usługi [Cloud Shell](../cloud-shell/overview.md).</span><span class="sxs-lookup"><span data-stu-id="63dd5-137">You can use [Cloud Shell](../cloud-shell/overview.md) to run the Azure CLI commands for deploying your template.</span></span> <span data-ttu-id="63dd5-138">Jednak musisz najpierw załadować swój szablon do udziału plików dla usługi Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="63dd5-138">However, you must first load your template into the file share for your Cloud Shell.</span></span> <span data-ttu-id="63dd5-139">Jeśli nie używasz usługi Cloud Shell, zobacz [Overview of Azure Cloud Shell (Omówienie usługi Azure Cloud Shell)](../cloud-shell/overview.md), aby uzyskać informacje o jej konfigurowaniu.</span><span class="sxs-lookup"><span data-stu-id="63dd5-139">If you have not used Cloud Shell, see [Overview of Azure Cloud Shell](../cloud-shell/overview.md) for information about setting it up.</span></span>

1. <span data-ttu-id="63dd5-140">Zaloguj się do witryny [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="63dd5-140">Log in to the [Azure portal](https://portal.azure.com).</span></span>   

2. <span data-ttu-id="63dd5-141">Wybierz swoją grupę zasobów usługi Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="63dd5-141">Select your Cloud Shell resource group.</span></span> <span data-ttu-id="63dd5-142">Wzorzec nazwy to `cloud-shell-storage-<region>`.</span><span class="sxs-lookup"><span data-stu-id="63dd5-142">The name pattern is `cloud-shell-storage-<region>`.</span></span>

   ![Wybieranie grupy zasobów](./media/resource-manager-create-first-template/select-cs-resource-group.png)

3. <span data-ttu-id="63dd5-144">Wybierz konto magazynu dla usługi Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="63dd5-144">Select the storage account for your Cloud Shell.</span></span>

   ![Wybieranie konta magazynu](./media/resource-manager-create-first-template/select-storage.png)

4. <span data-ttu-id="63dd5-146">Wybierz pozycję **Pliki**.</span><span class="sxs-lookup"><span data-stu-id="63dd5-146">Select **Files**.</span></span>

   ![Wybieranie pozycji Pliki](./media/resource-manager-create-first-template/select-files.png)

5. <span data-ttu-id="63dd5-148">Wybierz udział plików dla usługi Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="63dd5-148">Select the file share for Cloud Shell.</span></span> <span data-ttu-id="63dd5-149">Wzorzec nazwy to `cs-<user>-<domain>-com-<uniqueGuid>`.</span><span class="sxs-lookup"><span data-stu-id="63dd5-149">The name pattern is `cs-<user>-<domain>-com-<uniqueGuid>`.</span></span>

   ![Wybieranie udziału plików](./media/resource-manager-create-first-template/select-file-share.png)

6. <span data-ttu-id="63dd5-151">Wybierz pozycję **Dodaj katalog**.</span><span class="sxs-lookup"><span data-stu-id="63dd5-151">Select **Add directory**.</span></span>

   ![Dodawanie katalogu](./media/resource-manager-create-first-template/select-add-directory.png)

7. <span data-ttu-id="63dd5-153">Nadaj mu nazwę **templates** i wybierz przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="63dd5-153">Name it **templates**, and select **Okay**.</span></span>

   ![Nadawanie nazwy katalogowi](./media/resource-manager-create-first-template/name-templates.png)

8. <span data-ttu-id="63dd5-155">Wybierz swój nowy katalog.</span><span class="sxs-lookup"><span data-stu-id="63dd5-155">Select your new directory.</span></span>

   ![Wybieranie katalogu](./media/resource-manager-create-first-template/select-templates.png)

9. <span data-ttu-id="63dd5-157">Wybierz pozycję **Przekaż**.</span><span class="sxs-lookup"><span data-stu-id="63dd5-157">Select **Upload**.</span></span>

   ![Wybieranie pozycji Przekaż](./media/resource-manager-create-first-template/select-upload.png)

10. <span data-ttu-id="63dd5-159">Znajdź i przekaż swój szablon.</span><span class="sxs-lookup"><span data-stu-id="63dd5-159">Find and upload your template.</span></span>

   ![Przekazywanie pliku](./media/resource-manager-create-first-template/upload-files.png)

11. <span data-ttu-id="63dd5-161">Otwórz wiersz polecenia.</span><span class="sxs-lookup"><span data-stu-id="63dd5-161">Open the prompt.</span></span>

   ![Otwieranie usługi Cloud Shell](./media/resource-manager-create-first-template/start-cloud-shell.png)

12. <span data-ttu-id="63dd5-163">Wprowadź następujące polecenia w usłudze Cloud Shell:</span><span class="sxs-lookup"><span data-stu-id="63dd5-163">Enter the following commands in the Cloud Shell:</span></span>

   ```azurecli
   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json
   ```

<span data-ttu-id="63dd5-164">Po zakończeniu wdrażania Twoje konto magazynu będzie istnieć w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="63dd5-164">When deployment finishes, your storage account exists in the resource group.</span></span>

## <a name="customize-the-template"></a><span data-ttu-id="63dd5-165">Dostosowywanie szablonu</span><span class="sxs-lookup"><span data-stu-id="63dd5-165">Customize the template</span></span>

<span data-ttu-id="63dd5-166">Szablon działa prawidłowo, ale nie jest elastyczny.</span><span class="sxs-lookup"><span data-stu-id="63dd5-166">The template works fine, but it is not flexible.</span></span> <span data-ttu-id="63dd5-167">Zawsze wdraża magazyn lokalnie nadmiarowy w regionie Południowo-środkowe stany USA.</span><span class="sxs-lookup"><span data-stu-id="63dd5-167">It always deploys a locally redundant storage to South Central US.</span></span> <span data-ttu-id="63dd5-168">Nazwą jest zawsze *storage*, po której znajduje się wartość skrótu.</span><span class="sxs-lookup"><span data-stu-id="63dd5-168">The name is always *storage* followed by a hash value.</span></span> <span data-ttu-id="63dd5-169">Aby umożliwić używanie szablonu w różnych scenariuszach, dodaj do niego parametry.</span><span class="sxs-lookup"><span data-stu-id="63dd5-169">To enable using the template for different scenarios, add parameters to the template.</span></span>

<span data-ttu-id="63dd5-170">W poniższym przykładzie przedstawiono sekcję parametrów z dwoma parametrami.</span><span class="sxs-lookup"><span data-stu-id="63dd5-170">The following example shows the parameters section with two parameters.</span></span> <span data-ttu-id="63dd5-171">Pierwszy parametr, `storageSKU`, umożliwia określenie typu nadmiarowości.</span><span class="sxs-lookup"><span data-stu-id="63dd5-171">The first parameter `storageSKU` enables you to specify the type of redundancy.</span></span> <span data-ttu-id="63dd5-172">Ogranicza on wartości, które można przekazać, do wartości, które są prawidłowe dla konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="63dd5-172">It limits the values you can pass in to values that are valid for a storage account.</span></span> <span data-ttu-id="63dd5-173">Określa też wartość domyślną.</span><span class="sxs-lookup"><span data-stu-id="63dd5-173">It also specifies a default value.</span></span> <span data-ttu-id="63dd5-174">Drugi parametr, `storageNamePrefix`, jest ustawiony tak, że zezwala na maksymalnie 11 znaków.</span><span class="sxs-lookup"><span data-stu-id="63dd5-174">The second parameter `storageNamePrefix` is set to allow a maximum of 11 characters.</span></span> <span data-ttu-id="63dd5-175">Określa on wartość domyślną.</span><span class="sxs-lookup"><span data-stu-id="63dd5-175">It specifies a default value.</span></span>

```json
"parameters": {
  "storageSKU": {
    "type": "string",
    "allowedValues": [
      "Standard_LRS",
      "Standard_ZRS",
      "Standard_GRS",
      "Standard_RAGRS",
      "Premium_LRS"
    ],
    "defaultValue": "Standard_LRS",
    "metadata": {
      "description": "The type of replication to use for the storage account."
    }
  },
  "storageNamePrefix": {
    "type": "string",
    "maxLength": 11,
    "defaultValue": "storage",
    "metadata": {
      "description": "The value to use for starting the storage account name. Use only lowercase letters and numbers."
    }
  }
},
```

<span data-ttu-id="63dd5-176">W sekcji zmiennych dodaj zmienną o nazwie `storageName`.</span><span class="sxs-lookup"><span data-stu-id="63dd5-176">In the variables section, add a variable named `storageName`.</span></span> <span data-ttu-id="63dd5-177">Łączy ona wartość prefiksu z parametrów i wartość skrótu z funkcji [uniqueString](resource-group-template-functions-string.md#uniquestring).</span><span class="sxs-lookup"><span data-stu-id="63dd5-177">It combines the prefix value from the parameters and a hash value from the [uniqueString](resource-group-template-functions-string.md#uniquestring) function.</span></span> <span data-ttu-id="63dd5-178">Używa ona funkcji [toLower](resource-group-template-functions-string.md#tolower) w celu konwersji wszystkich liter na małe.</span><span class="sxs-lookup"><span data-stu-id="63dd5-178">It uses the [toLower](resource-group-template-functions-string.md#tolower) function to convert all characters to lowercase.</span></span>

```json
"variables": {
  "storageName": "[concat(toLower(parameters('storageNamePrefix')), uniqueString(resourceGroup().id))]"
},
```

<span data-ttu-id="63dd5-179">Aby użyć tych nowych wartości konta magazynu, zmień definicję zasobu:</span><span class="sxs-lookup"><span data-stu-id="63dd5-179">To use these new values for your storage account, change the resource definition:</span></span>

```json
"resources": [
  {
    "name": "[variables('storageName')]",
    "type": "Microsoft.Storage/storageAccounts",
    "apiVersion": "2016-01-01",
    "sku": {
      "name": "[parameters('storageSKU')]"
    },
    "kind": "Storage",
    "location": "[resourceGroup().location]",
    "tags": {},
    "properties": {}
  }
],
```

<span data-ttu-id="63dd5-180">Zauważ, że nazwa konta magazynu jest teraz ustawiona na dodaną przez Ciebie zmienną.</span><span class="sxs-lookup"><span data-stu-id="63dd5-180">Notice that the name of the storage account is now set to the variable that you added.</span></span> <span data-ttu-id="63dd5-181">Nazwa jednostki SKU ma ustawioną wartość parametru.</span><span class="sxs-lookup"><span data-stu-id="63dd5-181">The SKU name is set to the value of the parameter.</span></span> <span data-ttu-id="63dd5-182">Lokalizacja jest ustawiona na tę samą lokalizację co grupa zasobów.</span><span class="sxs-lookup"><span data-stu-id="63dd5-182">The location is set the same location as the resource group.</span></span>

<span data-ttu-id="63dd5-183">Zapisz plik.</span><span class="sxs-lookup"><span data-stu-id="63dd5-183">Save your file.</span></span> 

<span data-ttu-id="63dd5-184">Po wykonaniu tych kroków z tego artykułu szablon wygląda teraz następująco:</span><span class="sxs-lookup"><span data-stu-id="63dd5-184">After completing the steps in this article, your template now looks like:</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageSKU": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_ZRS",
        "Standard_GRS",
        "Standard_RAGRS",
        "Premium_LRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "The type of replication to use for the storage account."
      }
    },   
    "storageNamePrefix": {
      "type": "string",
      "maxLength": 11,
      "defaultValue": "storage",
      "metadata": {
        "description": "The value to use for starting the storage account name. Use only lowercase letters and numbers."
      }
    }
  },
  "variables": {
    "storageName": "[concat(toLower(parameters('storageNamePrefix')), uniqueString(resourceGroup().id))]"
  },
  "resources": [
    {
      "name": "[variables('storageName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-01-01",
      "sku": {
        "name": "[parameters('storageSKU')]"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {}
    }
  ],
  "outputs": {  }
}
```

## <a name="redeploy-template"></a><span data-ttu-id="63dd5-185">Ponowne wdrażanie szablonu</span><span class="sxs-lookup"><span data-stu-id="63dd5-185">Redeploy template</span></span>

<span data-ttu-id="63dd5-186">Ponownie wdróż szablon z innymi wartościami.</span><span class="sxs-lookup"><span data-stu-id="63dd5-186">Redeploy the template with different values.</span></span>

<span data-ttu-id="63dd5-187">W przypadku programu PowerShell użyj polecenia:</span><span class="sxs-lookup"><span data-stu-id="63dd5-187">For PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json -storageNamePrefix newstore -storageSKU Standard_RAGRS
```

<span data-ttu-id="63dd5-188">W przypadku interfejsu wiersza polecenia platformy Azure użyj polecenia:</span><span class="sxs-lookup"><span data-stu-id="63dd5-188">For Azure CLI, use:</span></span>

```azurecli
az group deployment create --resource-group examplegroup --template-file azuredeploy.json --parameters storageSKU=Standard_RAGRS storageNamePrefix=newstore
```

<span data-ttu-id="63dd5-189">W przypadku usługi Cloud Shell przekaż zmieniony szablon do udziału plików.</span><span class="sxs-lookup"><span data-stu-id="63dd5-189">For the Cloud Shell, upload your changed template to the file share.</span></span> <span data-ttu-id="63dd5-190">Zastąp istniejący plik.</span><span class="sxs-lookup"><span data-stu-id="63dd5-190">Overwrite the existing file.</span></span> <span data-ttu-id="63dd5-191">Następnie użyj poniższego polecenia:</span><span class="sxs-lookup"><span data-stu-id="63dd5-191">Then, use the following command:</span></span>

```azurecli
az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json --parameters storageSKU=Standard_RAGRS storageNamePrefix=newstore
```

## <a name="clean-up-resources"></a><span data-ttu-id="63dd5-192">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="63dd5-192">Clean up resources</span></span>

<span data-ttu-id="63dd5-193">Gdy nie będą już potrzebne, wyczyść wdrożone zasoby, usuwając grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="63dd5-193">When no longer needed, clean up the resources you deployed by deleting the resource group.</span></span>

<span data-ttu-id="63dd5-194">W przypadku programu PowerShell użyj polecenia:</span><span class="sxs-lookup"><span data-stu-id="63dd5-194">For PowerShell, use:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name examplegroup
```

<span data-ttu-id="63dd5-195">W przypadku interfejsu wiersza polecenia platformy Azure użyj polecenia:</span><span class="sxs-lookup"><span data-stu-id="63dd5-195">For Azure CLI, use:</span></span>

```azurecli
az group delete --name examplegroup
```

## <a name="next-steps"></a><span data-ttu-id="63dd5-196">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="63dd5-196">Next steps</span></span>
* <span data-ttu-id="63dd5-197">Aby uzyskać więcej informacji o strukturze szablonu, zobacz [Tworzenie szablonów usługi Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="63dd5-197">To learn more about the structure of a template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="63dd5-198">Aby poznać właściwości konta magazynu, zobacz [dokumentację szablonu kont magazynu](/azure/templates/microsoft.storage/storageaccounts).</span><span class="sxs-lookup"><span data-stu-id="63dd5-198">To learn about the properties for a storage account, see [storage accounts template reference](/azure/templates/microsoft.storage/storageaccounts).</span></span>
* <span data-ttu-id="63dd5-199">Aby wyświetlić pełną listę szablonów dla wielu różnych rozwiązań, zobacz [Szablony szybkiego startu platformy Azure](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="63dd5-199">To view complete templates for many different types of solutions, see the [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/).</span></span>
