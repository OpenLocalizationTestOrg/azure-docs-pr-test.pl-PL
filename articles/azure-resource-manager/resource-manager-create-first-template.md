---
title: "aaaCreate pierwszego szablonu usługi Azure Resource Manager | Dokumentacja firmy Microsoft"
description: "Toocreating przewodnik krok po kroku pierwszego szablonu usługi Azure Resource Manager. Przedstawiono sposób toouse hello odwołanie do szablonu dla szablonu hello toocreate konta magazynu."
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
ms.openlocfilehash: 92e6d6bb7094fe0e4537ee080704967862804bdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-your-first-azure-resource-manager-template"></a><span data-ttu-id="97534-104">Tworzenie i wdrażanie pierwszego szablonu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="97534-104">Create and deploy your first Azure Resource Manager template</span></span>
<span data-ttu-id="97534-105">Ten temat przeprowadzi Cię przez kroki tworzenia szablonu usługi Azure Resource Manager pierwszy hello.</span><span class="sxs-lookup"><span data-stu-id="97534-105">This topic walks you through hello steps of creating your first Azure Resource Manager template.</span></span> <span data-ttu-id="97534-106">Szablony Menedżera zasobów są pliki w formacie JSON określające zasoby hello potrzebne toodeploy dla rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="97534-106">Resource Manager templates are JSON files that define hello resources you need toodeploy for your solution.</span></span> <span data-ttu-id="97534-107">toounderstand hello pojęć związanych z wdrażania i zarządzania nimi rozwiązań platformy Azure, zobacz [Omówienie usługi Azure Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="97534-107">toounderstand hello concepts associated with deploying and managing your Azure solutions, see [Azure Resource Manager overview](resource-group-overview.md).</span></span> <span data-ttu-id="97534-108">Jeśli korzystasz z istniejących zasobów i chcesz tooget szablonu dla tych zasobów, zobacz [Eksportowanie szablonu usługi Azure Resource Manager z istniejących zasobów](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="97534-108">If you have existing resources and want tooget a template for those resources, see [Export an Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>

<span data-ttu-id="97534-109">toocreate i popraw szablonów, należy edytora JSON.</span><span class="sxs-lookup"><span data-stu-id="97534-109">toocreate and revise templates, you need a JSON editor.</span></span> <span data-ttu-id="97534-110">[Visual Studio Code](https://code.visualstudio.com/) to lekki edytor kodu typu open-source dla wielu platform.</span><span class="sxs-lookup"><span data-stu-id="97534-110">[Visual Studio Code](https://code.visualstudio.com/) is a lightweight, open-source, cross-platform code editor.</span></span> <span data-ttu-id="97534-111">Zdecydowanie zalecamy używanie programu Visual Studio Code do tworzenia szablonów usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="97534-111">We strongly recommend using Visual Studio Code for creating Resource Manager templates.</span></span> <span data-ttu-id="97534-112">W tym temacie założono, że używasz programu VS Code. Jeśli jednak masz inny edytor plików JSON (np. program Visual Studio), możesz użyć tego edytora.</span><span class="sxs-lookup"><span data-stu-id="97534-112">This topic assumes you are using VS Code; however, if you have another JSON editor (like Visual Studio), you can use that editor.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="97534-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="97534-113">Prerequisites</span></span>

* <span data-ttu-id="97534-114">Program Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="97534-114">Visual Studio Code.</span></span> <span data-ttu-id="97534-115">W razie potrzeby zainstaluj go ze strony [https://code.visualstudio.com/](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="97534-115">If needed, install it from [https://code.visualstudio.com/](https://code.visualstudio.com/).</span></span>
* <span data-ttu-id="97534-116">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="97534-116">An Azure subscription.</span></span> <span data-ttu-id="97534-117">Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="97534-117">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="create-template"></a><span data-ttu-id="97534-118">Tworzenie szablonu</span><span class="sxs-lookup"><span data-stu-id="97534-118">Create template</span></span>

<span data-ttu-id="97534-119">Zacznijmy prostego szablonu, który wdraża subskrypcja tooyour konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="97534-119">Let's start with a simple template that deploys a storage account tooyour subscription.</span></span>

1. <span data-ttu-id="97534-120">Wybierz pozycję **Plik** > **Nowy plik**.</span><span class="sxs-lookup"><span data-stu-id="97534-120">Select **File** > **New File**.</span></span> 

   ![Nowy plik](./media/resource-manager-create-first-template/new-file.png)

2. <span data-ttu-id="97534-122">Skopiuj i Wklej powitania po składni JSON do pliku:</span><span class="sxs-lookup"><span data-stu-id="97534-122">Copy and paste hello following JSON syntax into your file:</span></span>

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

   <span data-ttu-id="97534-123">Nazwy kont magazynu ma kilka ograniczeń, które były tooset trudne.</span><span class="sxs-lookup"><span data-stu-id="97534-123">Storage account names have several restrictions that make them difficult tooset.</span></span> <span data-ttu-id="97534-124">Nazwa Hello musi należeć do zakresu od 3 do 24 znaków długości, użyj tylko cyfry i małe litery i musi być unikatowa.</span><span class="sxs-lookup"><span data-stu-id="97534-124">hello name must be between 3 and 24 characters in length, use only numbers and lower-case letters, and be unique.</span></span> <span data-ttu-id="97534-125">Witaj poprzedniego szablon używa hello [uniqueString](resource-group-template-functions-string.md#uniquestring) funkcji toogenerate wartość skrótu.</span><span class="sxs-lookup"><span data-stu-id="97534-125">hello preceding template uses hello [uniqueString](resource-group-template-functions-string.md#uniquestring) function toogenerate a hash value.</span></span> <span data-ttu-id="97534-126">toogive ten skrót wartości jeden, co oznacza, dodaje prefiks hello *magazynu*.</span><span class="sxs-lookup"><span data-stu-id="97534-126">toogive this hash value more meaning, it adds hello prefix *storage*.</span></span> 

3. <span data-ttu-id="97534-127">Zapisz ten plik jako **azuredeploy.json** tooa folderu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="97534-127">Save this file as **azuredeploy.json** tooa local folder.</span></span>

   ![Zapisywanie szablonu](./media/resource-manager-create-first-template/save-template.png)

## <a name="deploy-template"></a><span data-ttu-id="97534-129">Wdrażanie szablonu</span><span class="sxs-lookup"><span data-stu-id="97534-129">Deploy template</span></span>

<span data-ttu-id="97534-130">Możesz są gotowe toodeploy tego szablonu.</span><span class="sxs-lookup"><span data-stu-id="97534-130">You are ready toodeploy this template.</span></span> <span data-ttu-id="97534-131">Możesz użyć programu PowerShell lub interfejsu wiersza polecenia Azure toocreate grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="97534-131">You use either PowerShell or Azure CLI toocreate a resource group.</span></span> <span data-ttu-id="97534-132">Następnie można wdrożyć grupę zasobów toothat konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="97534-132">Then, you deploy a storage account toothat resource group.</span></span>

* <span data-ttu-id="97534-133">Dla programu PowerShell Użyj poniższych poleceń z hello folderu zawierającego szablon hello hello:</span><span class="sxs-lookup"><span data-stu-id="97534-133">For PowerShell, use hello following commands from hello folder containing hello template:</span></span>

   ```powershell
   Login-AzureRmAccount
   
   New-AzureRmResourceGroup -Name examplegroup -Location "South Central US"
   New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json
   ```

* <span data-ttu-id="97534-134">W przypadku instalacji lokalnej z wiersza polecenia platformy Azure Użyj poniższych poleceń z hello folderu zawierającego szablon hello hello:</span><span class="sxs-lookup"><span data-stu-id="97534-134">For a local installation of Azure CLI, use hello following commands from hello folder containing hello template:</span></span>

   ```azurecli
   az login

   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file azuredeploy.json
   ```

<span data-ttu-id="97534-135">Po zakończeniu wdrażania, Twoje konto magazynu istnieje w grupie zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="97534-135">When deployment finishes, your storage account exists in hello resource group.</span></span>

## <a name="deploy-template-from-cloud-shell"></a><span data-ttu-id="97534-136">Wdrażanie szablonu za pomocą usługi Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="97534-136">Deploy template from Cloud Shell</span></span>

<span data-ttu-id="97534-137">Można użyć [powłoki chmury](../cloud-shell/overview.md) toorun hello Azure CLI polecenia do wdrożenia szablonu.</span><span class="sxs-lookup"><span data-stu-id="97534-137">You can use [Cloud Shell](../cloud-shell/overview.md) toorun hello Azure CLI commands for deploying your template.</span></span> <span data-ttu-id="97534-138">Jednak należy najpierw załadować szablonu do udziału plików powitania dla powłoki chmury.</span><span class="sxs-lookup"><span data-stu-id="97534-138">However, you must first load your template into hello file share for your Cloud Shell.</span></span> <span data-ttu-id="97534-139">Jeśli nie używasz usługi Cloud Shell, zobacz [Overview of Azure Cloud Shell (Omówienie usługi Azure Cloud Shell)](../cloud-shell/overview.md), aby uzyskać informacje o jej konfigurowaniu.</span><span class="sxs-lookup"><span data-stu-id="97534-139">If you have not used Cloud Shell, see [Overview of Azure Cloud Shell](../cloud-shell/overview.md) for information about setting it up.</span></span>

1. <span data-ttu-id="97534-140">Zaloguj się za toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="97534-140">Log in toohello [Azure portal](https://portal.azure.com).</span></span>   

2. <span data-ttu-id="97534-141">Wybierz swoją grupę zasobów usługi Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="97534-141">Select your Cloud Shell resource group.</span></span> <span data-ttu-id="97534-142">wzorzec nazwy Hello jest `cloud-shell-storage-<region>`.</span><span class="sxs-lookup"><span data-stu-id="97534-142">hello name pattern is `cloud-shell-storage-<region>`.</span></span>

   ![Wybieranie grupy zasobów](./media/resource-manager-create-first-template/select-cs-resource-group.png)

3. <span data-ttu-id="97534-144">Wybierz konto magazynu powitania dla powłoki chmury.</span><span class="sxs-lookup"><span data-stu-id="97534-144">Select hello storage account for your Cloud Shell.</span></span>

   ![Wybieranie konta magazynu](./media/resource-manager-create-first-template/select-storage.png)

4. <span data-ttu-id="97534-146">Wybierz pozycję **Pliki**.</span><span class="sxs-lookup"><span data-stu-id="97534-146">Select **Files**.</span></span>

   ![Wybieranie pozycji Pliki](./media/resource-manager-create-first-template/select-files.png)

5. <span data-ttu-id="97534-148">Wybierz udział plików powitania dla powłoki chmury.</span><span class="sxs-lookup"><span data-stu-id="97534-148">Select hello file share for Cloud Shell.</span></span> <span data-ttu-id="97534-149">wzorzec nazwy Hello jest `cs-<user>-<domain>-com-<uniqueGuid>`.</span><span class="sxs-lookup"><span data-stu-id="97534-149">hello name pattern is `cs-<user>-<domain>-com-<uniqueGuid>`.</span></span>

   ![Wybieranie udziału plików](./media/resource-manager-create-first-template/select-file-share.png)

6. <span data-ttu-id="97534-151">Wybierz pozycję **Dodaj katalog**.</span><span class="sxs-lookup"><span data-stu-id="97534-151">Select **Add directory**.</span></span>

   ![Dodawanie katalogu](./media/resource-manager-create-first-template/select-add-directory.png)

7. <span data-ttu-id="97534-153">Nadaj mu nazwę **templates** i wybierz przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="97534-153">Name it **templates**, and select **Okay**.</span></span>

   ![Nadawanie nazwy katalogowi](./media/resource-manager-create-first-template/name-templates.png)

8. <span data-ttu-id="97534-155">Wybierz swój nowy katalog.</span><span class="sxs-lookup"><span data-stu-id="97534-155">Select your new directory.</span></span>

   ![Wybieranie katalogu](./media/resource-manager-create-first-template/select-templates.png)

9. <span data-ttu-id="97534-157">Wybierz pozycję **Przekaż**.</span><span class="sxs-lookup"><span data-stu-id="97534-157">Select **Upload**.</span></span>

   ![Wybieranie pozycji Przekaż](./media/resource-manager-create-first-template/select-upload.png)

10. <span data-ttu-id="97534-159">Znajdź i przekaż swój szablon.</span><span class="sxs-lookup"><span data-stu-id="97534-159">Find and upload your template.</span></span>

   ![Przekazywanie pliku](./media/resource-manager-create-first-template/upload-files.png)

11. <span data-ttu-id="97534-161">Otwórz hello wiersza.</span><span class="sxs-lookup"><span data-stu-id="97534-161">Open hello prompt.</span></span>

   ![Otwieranie usługi Cloud Shell](./media/resource-manager-create-first-template/start-cloud-shell.png)

12. <span data-ttu-id="97534-163">Wprowadź następujące polecenia w hello powłoki chmury hello:</span><span class="sxs-lookup"><span data-stu-id="97534-163">Enter hello following commands in hello Cloud Shell:</span></span>

   ```azurecli
   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json
   ```

<span data-ttu-id="97534-164">Po zakończeniu wdrażania, Twoje konto magazynu istnieje w grupie zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="97534-164">When deployment finishes, your storage account exists in hello resource group.</span></span>

## <a name="customize-hello-template"></a><span data-ttu-id="97534-165">Dostosowywanie szablonu hello</span><span class="sxs-lookup"><span data-stu-id="97534-165">Customize hello template</span></span>

<span data-ttu-id="97534-166">Szablon Hello działa prawidłowo, ale nie jest elastyczny.</span><span class="sxs-lookup"><span data-stu-id="97534-166">hello template works fine, but it is not flexible.</span></span> <span data-ttu-id="97534-167">Magazyn lokalnie nadmiarowy tooSouth środkowe stany USA zawsze wdrażania.</span><span class="sxs-lookup"><span data-stu-id="97534-167">It always deploys a locally redundant storage tooSouth Central US.</span></span> <span data-ttu-id="97534-168">Nazwa Hello jest zawsze *magazynu* następuje wartość skrótu.</span><span class="sxs-lookup"><span data-stu-id="97534-168">hello name is always *storage* followed by a hash value.</span></span> <span data-ttu-id="97534-169">tooenable przy użyciu szablonu powitania dla różnych scenariuszy, Dodaj parametry toohello szablon.</span><span class="sxs-lookup"><span data-stu-id="97534-169">tooenable using hello template for different scenarios, add parameters toohello template.</span></span>

<span data-ttu-id="97534-170">Witaj poniższy przykład przedstawia sekcji parameters hello dwa parametry.</span><span class="sxs-lookup"><span data-stu-id="97534-170">hello following example shows hello parameters section with two parameters.</span></span> <span data-ttu-id="97534-171">pierwszy parametr Hello `storageSKU` pozwala typu hello toospecify nadmiarowości.</span><span class="sxs-lookup"><span data-stu-id="97534-171">hello first parameter `storageSKU` enables you toospecify hello type of redundancy.</span></span> <span data-ttu-id="97534-172">Ogranicza wartości hello, które można przekazać toovalues, które są prawidłowe dla konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="97534-172">It limits hello values you can pass in toovalues that are valid for a storage account.</span></span> <span data-ttu-id="97534-173">Określa też wartość domyślną.</span><span class="sxs-lookup"><span data-stu-id="97534-173">It also specifies a default value.</span></span> <span data-ttu-id="97534-174">Witaj drugi parametr `storageNamePrefix` jest zestaw tooallow maksymalnie 11 znaków.</span><span class="sxs-lookup"><span data-stu-id="97534-174">hello second parameter `storageNamePrefix` is set tooallow a maximum of 11 characters.</span></span> <span data-ttu-id="97534-175">Określa on wartość domyślną.</span><span class="sxs-lookup"><span data-stu-id="97534-175">It specifies a default value.</span></span>

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
      "description": "hello type of replication toouse for hello storage account."
    }
  },
  "storageNamePrefix": {
    "type": "string",
    "maxLength": 11,
    "defaultValue": "storage",
    "metadata": {
      "description": "hello value toouse for starting hello storage account name. Use only lowercase letters and numbers."
    }
  }
},
```

<span data-ttu-id="97534-176">W sekcji variables hello dodać zmienną o nazwie `storageName`.</span><span class="sxs-lookup"><span data-stu-id="97534-176">In hello variables section, add a variable named `storageName`.</span></span> <span data-ttu-id="97534-177">Łączy wartość prefiks hello z hello parametrów i wartości skrótu z hello [uniqueString](resource-group-template-functions-string.md#uniquestring) funkcji.</span><span class="sxs-lookup"><span data-stu-id="97534-177">It combines hello prefix value from hello parameters and a hash value from hello [uniqueString](resource-group-template-functions-string.md#uniquestring) function.</span></span> <span data-ttu-id="97534-178">Używa hello [toLower](resource-group-template-functions-string.md#tolower) funkcji tooconvert wszystkie toolowercase znaków.</span><span class="sxs-lookup"><span data-stu-id="97534-178">It uses hello [toLower](resource-group-template-functions-string.md#tolower) function tooconvert all characters toolowercase.</span></span>

```json
"variables": {
  "storageName": "[concat(toLower(parameters('storageNamePrefix')), uniqueString(resourceGroup().id))]"
},
```

<span data-ttu-id="97534-179">toouse te nowe wartości dla konta magazynu, Zmień definicję zasobu hello:</span><span class="sxs-lookup"><span data-stu-id="97534-179">toouse these new values for your storage account, change hello resource definition:</span></span>

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

<span data-ttu-id="97534-180">Zwróć uwagę, że hello nazwy konta magazynu hello ma teraz wartość zmiennej toohello, który został dodany.</span><span class="sxs-lookup"><span data-stu-id="97534-180">Notice that hello name of hello storage account is now set toohello variable that you added.</span></span> <span data-ttu-id="97534-181">Nazwa jednostki SKU Hello ustawiono wartość toohello hello parametru.</span><span class="sxs-lookup"><span data-stu-id="97534-181">hello SKU name is set toohello value of hello parameter.</span></span> <span data-ttu-id="97534-182">Lokalizacja Hello jest ustawiana hello tej samej lokalizacji co hello grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="97534-182">hello location is set hello same location as hello resource group.</span></span>

<span data-ttu-id="97534-183">Zapisz plik.</span><span class="sxs-lookup"><span data-stu-id="97534-183">Save your file.</span></span> 

<span data-ttu-id="97534-184">Po wykonaniu czynności hello w tym artykule szablonu teraz wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="97534-184">After completing hello steps in this article, your template now looks like:</span></span>

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
        "description": "hello type of replication toouse for hello storage account."
      }
    },   
    "storageNamePrefix": {
      "type": "string",
      "maxLength": 11,
      "defaultValue": "storage",
      "metadata": {
        "description": "hello value toouse for starting hello storage account name. Use only lowercase letters and numbers."
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

## <a name="redeploy-template"></a><span data-ttu-id="97534-185">Ponowne wdrażanie szablonu</span><span class="sxs-lookup"><span data-stu-id="97534-185">Redeploy template</span></span>

<span data-ttu-id="97534-186">Należy ponownie wdrożyć szablon hello o różnych wartościach.</span><span class="sxs-lookup"><span data-stu-id="97534-186">Redeploy hello template with different values.</span></span>

<span data-ttu-id="97534-187">W przypadku programu PowerShell użyj polecenia:</span><span class="sxs-lookup"><span data-stu-id="97534-187">For PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json -storageNamePrefix newstore -storageSKU Standard_RAGRS
```

<span data-ttu-id="97534-188">W przypadku interfejsu wiersza polecenia platformy Azure użyj polecenia:</span><span class="sxs-lookup"><span data-stu-id="97534-188">For Azure CLI, use:</span></span>

```azurecli
az group deployment create --resource-group examplegroup --template-file azuredeploy.json --parameters storageSKU=Standard_RAGRS storageNamePrefix=newstore
```

<span data-ttu-id="97534-189">W przypadku hello powłoki chmury przekazać udziału plików toohello zmienionego szablonu.</span><span class="sxs-lookup"><span data-stu-id="97534-189">For hello Cloud Shell, upload your changed template toohello file share.</span></span> <span data-ttu-id="97534-190">Zastąp istniejący plik hello.</span><span class="sxs-lookup"><span data-stu-id="97534-190">Overwrite hello existing file.</span></span> <span data-ttu-id="97534-191">Następnie należy użyć następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="97534-191">Then, use hello following command:</span></span>

```azurecli
az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json --parameters storageSKU=Standard_RAGRS storageNamePrefix=newstore
```

## <a name="clean-up-resources"></a><span data-ttu-id="97534-192">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="97534-192">Clean up resources</span></span>

<span data-ttu-id="97534-193">Gdy nie są już potrzebne, należy wyczyścić zasoby hello, wdrożonej przez usunięcie hello grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="97534-193">When no longer needed, clean up hello resources you deployed by deleting hello resource group.</span></span>

<span data-ttu-id="97534-194">W przypadku programu PowerShell użyj polecenia:</span><span class="sxs-lookup"><span data-stu-id="97534-194">For PowerShell, use:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name examplegroup
```

<span data-ttu-id="97534-195">W przypadku interfejsu wiersza polecenia platformy Azure użyj polecenia:</span><span class="sxs-lookup"><span data-stu-id="97534-195">For Azure CLI, use:</span></span>

```azurecli
az group delete --name examplegroup
```

## <a name="next-steps"></a><span data-ttu-id="97534-196">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="97534-196">Next steps</span></span>
* <span data-ttu-id="97534-197">toolearn więcej informacji na temat struktury hello szablonu, zobacz [szablonów Authoring Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="97534-197">toolearn more about hello structure of a template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="97534-198">toolearn hello właściwości konta magazynu, zobacz [odwołania do szablonu kont magazynu](/azure/templates/microsoft.storage/storageaccounts).</span><span class="sxs-lookup"><span data-stu-id="97534-198">toolearn about hello properties for a storage account, see [storage accounts template reference](/azure/templates/microsoft.storage/storageaccounts).</span></span>
* <span data-ttu-id="97534-199">Szablony pełną tooview do różnych rozwiązań, zobacz hello [szablonów Szybki Start Azure](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="97534-199">tooview complete templates for many different types of solutions, see hello [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/).</span></span>
