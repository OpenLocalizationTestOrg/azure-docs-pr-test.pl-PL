---
title: "funkcje szablonu usługi Resource Manager aaaAzure — wdrożenia | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano toouse funkcje hello w usługi Azure Resource Manager szablonu tooretrieve informacje na temat wdrażania."
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
ms.date: 06/13/2017
ms.author: tomfitz
ms.openlocfilehash: 458c3f740504fdd6799ed24cc386219726737636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deployment-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="f6958-103">Funkcje wdrażania dla szablonów usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f6958-103">Deployment functions for Azure Resource Manager templates</span></span> 

<span data-ttu-id="f6958-104">Usługa Resource Manager zapewnia hello następujące funkcje do pobierania wartości z części szablonu hello i wartości wdrożenia toohello pokrewne:</span><span class="sxs-lookup"><span data-stu-id="f6958-104">Resource Manager provides hello following functions for getting values from sections of hello template and values related toohello deployment:</span></span>

* [<span data-ttu-id="f6958-105">wdrożenia</span><span class="sxs-lookup"><span data-stu-id="f6958-105">deployment</span></span>](#deployment)
* [<span data-ttu-id="f6958-106">Parametry</span><span class="sxs-lookup"><span data-stu-id="f6958-106">parameters</span></span>](#parameters)
* [<span data-ttu-id="f6958-107">zmienne</span><span class="sxs-lookup"><span data-stu-id="f6958-107">variables</span></span>](#variables)

<span data-ttu-id="f6958-108">wartości tooget z zasobów, grupy zasobów lub subskrypcji, zobacz [funkcji zasobów](resource-group-template-functions-resource.md).</span><span class="sxs-lookup"><span data-stu-id="f6958-108">tooget values from resources, resource groups, or subscriptions, see [Resource functions](resource-group-template-functions-resource.md).</span></span>

<a id="deployment" />

## <a name="deployment"></a><span data-ttu-id="f6958-109">wdrożenie</span><span class="sxs-lookup"><span data-stu-id="f6958-109">deployment</span></span>
`deployment()`

<span data-ttu-id="f6958-110">Zwraca informacje o hello bieżącej operacji wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="f6958-110">Returns information about hello current deployment operation.</span></span>

### <a name="return-value"></a><span data-ttu-id="f6958-111">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="f6958-111">Return value</span></span>

<span data-ttu-id="f6958-112">Ta funkcja zwraca obiekt hello, który jest przekazywany podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="f6958-112">This function returns hello object that is passed during deployment.</span></span> <span data-ttu-id="f6958-113">właściwości Hello w hello zwrócił obiekt się różnić w zależności od tego, czy hello obiektu wdrożenia jest przekazywany jako łącze lub obiekt w wierszu.</span><span class="sxs-lookup"><span data-stu-id="f6958-113">hello properties in hello returned object differ based on whether hello deployment object is passed as a link or as an in-line object.</span></span> <span data-ttu-id="f6958-114">Gdy obiektu wdrożenia hello jest przekazywany w zewnętrznych, takich jak przy użyciu hello **- TemplateFile** parametru w toopoint programu Azure PowerShell tooa pliku lokalnego, hello zwrócony obiekt ma hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="f6958-114">When hello deployment object is passed in-line, such as when using hello **-TemplateFile** parameter in Azure PowerShell toopoint tooa local file, hello returned object has hello following format:</span></span>

```json
{
    "name": "",
    "properties": {
        "template": {
            "$schema": "",
            "contentVersion": "",
            "parameters": {},
            "variables": {},
            "resources": [
            ],
            "outputs": {}
        },
        "parameters": {},
        "mode": "",
        "provisioningState": ""
    }
}
```

<span data-ttu-id="f6958-115">Gdy obiekt hello jest przekazywany jako łącze, takie jak kiedy hello przy użyciu **- TemplateUri** obiektu zdalnego tooa toopoint parametru hello obiekt jest zwracany w hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="f6958-115">When hello object is passed as a link, such as when using hello **-TemplateUri** parameter toopoint tooa remote object, hello object is returned in hello following format:</span></span> 

```json
{
    "name": "",
    "properties": {
        "templateLink": {
            "uri": ""
        },
        "template": {
            "$schema": "",
            "contentVersion": "",
            "parameters": {},
            "variables": {},
            "resources": [],
            "outputs": {}
        },
        "parameters": {},
        "mode": "",
        "provisioningState": ""
    }
}
```

### <a name="remarks"></a><span data-ttu-id="f6958-116">Uwagi</span><span class="sxs-lookup"><span data-stu-id="f6958-116">Remarks</span></span>

<span data-ttu-id="f6958-117">Można użyć szablonu tooanother toolink deployment() opartego na powitania URI szablonu nadrzędnego hello.</span><span class="sxs-lookup"><span data-stu-id="f6958-117">You can use deployment() toolink tooanother template based on hello URI of hello parent template.</span></span>

```json
"variables": {  
    "sharedTemplateUrl": "[uri(deployment().properties.templateLink.uri, 'shared-resources.json')]"  
}
```  

### <a name="example"></a><span data-ttu-id="f6958-118">Przykład</span><span class="sxs-lookup"><span data-stu-id="f6958-118">Example</span></span>

<span data-ttu-id="f6958-119">Witaj poniższy przykład zwraca obiekt wdrożenia hello:</span><span class="sxs-lookup"><span data-stu-id="f6958-119">hello following example returns hello deployment object:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[deployment()]",
            "type" : "object"
        }
    }
}
```

<span data-ttu-id="f6958-120">Witaj poprzednim przykładzie zwraca hello następującego obiektu:</span><span class="sxs-lookup"><span data-stu-id="f6958-120">hello preceding example returns hello following object:</span></span>

```json
{
  "name": "deployment",
  "properties": {
    "template": {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "resources": [],
      "outputs": {
        "subscriptionOutput": {
          "type": "Object",
          "value": "[deployment()]"
        }
      }
    },
    "parameters": {},
    "mode": "Incremental",
    "provisioningState": "Accepted"
  }
}
```

<a id="parameters" />

## <a name="parameters"></a><span data-ttu-id="f6958-121">parameters</span><span class="sxs-lookup"><span data-stu-id="f6958-121">parameters</span></span>
`parameters(parameterName)`

<span data-ttu-id="f6958-122">Zwraca wartość parametru.</span><span class="sxs-lookup"><span data-stu-id="f6958-122">Returns a parameter value.</span></span> <span data-ttu-id="f6958-123">Witaj określona nazwa parametru musi być zdefiniowany w sekcji parametrów hello hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="f6958-123">hello specified parameter name must be defined in hello parameters section of hello template.</span></span>

### <a name="parameters"></a><span data-ttu-id="f6958-124">Parametry</span><span class="sxs-lookup"><span data-stu-id="f6958-124">Parameters</span></span>

| <span data-ttu-id="f6958-125">Parametr</span><span class="sxs-lookup"><span data-stu-id="f6958-125">Parameter</span></span> | <span data-ttu-id="f6958-126">Wymagane</span><span class="sxs-lookup"><span data-stu-id="f6958-126">Required</span></span> | <span data-ttu-id="f6958-127">Typ</span><span class="sxs-lookup"><span data-stu-id="f6958-127">Type</span></span> | <span data-ttu-id="f6958-128">Opis</span><span class="sxs-lookup"><span data-stu-id="f6958-128">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="f6958-129">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="f6958-129">parameterName</span></span> |<span data-ttu-id="f6958-130">Tak</span><span class="sxs-lookup"><span data-stu-id="f6958-130">Yes</span></span> |<span data-ttu-id="f6958-131">Ciąg</span><span class="sxs-lookup"><span data-stu-id="f6958-131">string</span></span> |<span data-ttu-id="f6958-132">Nazwa Hello hello tooreturn parametru.</span><span class="sxs-lookup"><span data-stu-id="f6958-132">hello name of hello parameter tooreturn.</span></span> |

### <a name="return-value"></a><span data-ttu-id="f6958-133">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="f6958-133">Return value</span></span>

<span data-ttu-id="f6958-134">wartość Hello hello określony parametr.</span><span class="sxs-lookup"><span data-stu-id="f6958-134">hello value of hello specified parameter.</span></span>

### <a name="remarks"></a><span data-ttu-id="f6958-135">Uwagi</span><span class="sxs-lookup"><span data-stu-id="f6958-135">Remarks</span></span>

<span data-ttu-id="f6958-136">Należy zwykle użyć wartości zasobów tooset parametrów.</span><span class="sxs-lookup"><span data-stu-id="f6958-136">Typically, you use parameters tooset resource values.</span></span> <span data-ttu-id="f6958-137">Witaj poniższy przykład przedstawia hello nazwa witryny sieci web toohello wartość parametru w podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="f6958-137">hello following example sets hello name of web site toohello parameter value passed in during deployment.</span></span>

```json
"parameters": { 
  "siteName": {
      "type": "string"
  }
},
"resources": [
   {
      "apiVersion": "2016-08-01",
      "name": "[parameters('siteName')]",
      "type": "Microsoft.Web/Sites",
      ...
   }
]
```

### <a name="example"></a><span data-ttu-id="f6958-138">Przykład</span><span class="sxs-lookup"><span data-stu-id="f6958-138">Example</span></span>

<span data-ttu-id="f6958-139">Witaj poniższym przykładzie pokazano uproszczony Użyj hello parametrów funkcji.</span><span class="sxs-lookup"><span data-stu-id="f6958-139">hello following example shows a simplified use of hello parameters function.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringParameter": {
            "type" : "string",
            "defaultValue": "option 1"
        },
        "intParameter": {
            "type": "int",
            "defaultValue": 1
        },
        "objectParameter": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b"}
        },
        "arrayParameter": {
            "type": "array",
            "defaultValue": [1, 2, 3]
        },
        "crossParameter": {
            "type": "string",
            "defaultValue": "[parameters('stringParameter')]"
        }
    },
    "variables": {},
    "resources": [],
    "outputs": {
        "stringOutput": {
            "value": "[parameters('stringParameter')]",
            "type" : "string"
        },
        "intOutput": {
            "value": "[parameters('intParameter')]",
            "type" : "int"
        },
        "objectOutput": {
            "value": "[parameters('objectParameter')]",
            "type" : "object"
        },
        "arrayOutput": {
            "value": "[parameters('arrayParameter')]",
            "type" : "array"
        },
        "crossOutput": {
            "value": "[parameters('crossParameter')]",
            "type" : "string"
        }
    }
}
```

<span data-ttu-id="f6958-140">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="f6958-140">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="f6958-141">Nazwa</span><span class="sxs-lookup"><span data-stu-id="f6958-141">Name</span></span> | <span data-ttu-id="f6958-142">Typ</span><span class="sxs-lookup"><span data-stu-id="f6958-142">Type</span></span> | <span data-ttu-id="f6958-143">Wartość</span><span class="sxs-lookup"><span data-stu-id="f6958-143">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="f6958-144">stringOutput</span><span class="sxs-lookup"><span data-stu-id="f6958-144">stringOutput</span></span> | <span data-ttu-id="f6958-145">Ciąg</span><span class="sxs-lookup"><span data-stu-id="f6958-145">String</span></span> | <span data-ttu-id="f6958-146">Opcja 1</span><span class="sxs-lookup"><span data-stu-id="f6958-146">option 1</span></span> |
| <span data-ttu-id="f6958-147">intOutput</span><span class="sxs-lookup"><span data-stu-id="f6958-147">intOutput</span></span> | <span data-ttu-id="f6958-148">int</span><span class="sxs-lookup"><span data-stu-id="f6958-148">Int</span></span> | <span data-ttu-id="f6958-149">1</span><span class="sxs-lookup"><span data-stu-id="f6958-149">1</span></span> |
| <span data-ttu-id="f6958-150">objectOutput</span><span class="sxs-lookup"><span data-stu-id="f6958-150">objectOutput</span></span> | <span data-ttu-id="f6958-151">Obiekt</span><span class="sxs-lookup"><span data-stu-id="f6958-151">Object</span></span> | <span data-ttu-id="f6958-152">{"jeden": "", "2": "b"}</span><span class="sxs-lookup"><span data-stu-id="f6958-152">{"one": "a", "two": "b"}</span></span> |
| <span data-ttu-id="f6958-153">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="f6958-153">arrayOutput</span></span> | <span data-ttu-id="f6958-154">Tablica</span><span class="sxs-lookup"><span data-stu-id="f6958-154">Array</span></span> | <span data-ttu-id="f6958-155">[1, 2, 3]</span><span class="sxs-lookup"><span data-stu-id="f6958-155">[1, 2, 3]</span></span> |
| <span data-ttu-id="f6958-156">crossOutput</span><span class="sxs-lookup"><span data-stu-id="f6958-156">crossOutput</span></span> | <span data-ttu-id="f6958-157">Ciąg</span><span class="sxs-lookup"><span data-stu-id="f6958-157">String</span></span> | <span data-ttu-id="f6958-158">Opcja 1</span><span class="sxs-lookup"><span data-stu-id="f6958-158">option 1</span></span> |

<a id="variables" />

## <a name="variables"></a><span data-ttu-id="f6958-159">zmienne</span><span class="sxs-lookup"><span data-stu-id="f6958-159">variables</span></span>
`variables(variableName)`

<span data-ttu-id="f6958-160">Zwraca hello wartość zmiennej.</span><span class="sxs-lookup"><span data-stu-id="f6958-160">Returns hello value of variable.</span></span> <span data-ttu-id="f6958-161">Określona nazwa zmiennej Hello muszą być zdefiniowane w sekcji zmiennych hello hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="f6958-161">hello specified variable name must be defined in hello variables section of hello template.</span></span>

### <a name="parameters"></a><span data-ttu-id="f6958-162">Parametry</span><span class="sxs-lookup"><span data-stu-id="f6958-162">Parameters</span></span>

| <span data-ttu-id="f6958-163">Parametr</span><span class="sxs-lookup"><span data-stu-id="f6958-163">Parameter</span></span> | <span data-ttu-id="f6958-164">Wymagane</span><span class="sxs-lookup"><span data-stu-id="f6958-164">Required</span></span> | <span data-ttu-id="f6958-165">Typ</span><span class="sxs-lookup"><span data-stu-id="f6958-165">Type</span></span> | <span data-ttu-id="f6958-166">Opis</span><span class="sxs-lookup"><span data-stu-id="f6958-166">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="f6958-167">nazwa_zmiennej</span><span class="sxs-lookup"><span data-stu-id="f6958-167">variableName</span></span> |<span data-ttu-id="f6958-168">Tak</span><span class="sxs-lookup"><span data-stu-id="f6958-168">Yes</span></span> |<span data-ttu-id="f6958-169">Ciąg</span><span class="sxs-lookup"><span data-stu-id="f6958-169">String</span></span> |<span data-ttu-id="f6958-170">Nazwa Hello hello tooreturn zmiennej.</span><span class="sxs-lookup"><span data-stu-id="f6958-170">hello name of hello variable tooreturn.</span></span> |

### <a name="return-value"></a><span data-ttu-id="f6958-171">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="f6958-171">Return value</span></span>

<span data-ttu-id="f6958-172">wartość Hello hello określonej zmiennej.</span><span class="sxs-lookup"><span data-stu-id="f6958-172">hello value of hello specified variable.</span></span>

### <a name="remarks"></a><span data-ttu-id="f6958-173">Uwagi</span><span class="sxs-lookup"><span data-stu-id="f6958-173">Remarks</span></span>

<span data-ttu-id="f6958-174">Należy zwykle użyć, toosimplify zmiennych szablonu tworząc wartości złożonych tylko raz.</span><span class="sxs-lookup"><span data-stu-id="f6958-174">Typically, you use variables toosimplify your template by constructing complex values only once.</span></span> <span data-ttu-id="f6958-175">Witaj poniższy przykład tworzy unikatową nazwę konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="f6958-175">hello following example constructs a unique name for a storage account.</span></span>

```json
"variables": {
    "storageName": "[concat('storage', uniqueString(resourceGroup().id))]"
},
"resources": [
    {
        "type": "Microsoft.Storage/storageAccounts",
        "name": "[variables('storageName')]",
        ...
    },
    {
        "type": "Microsoft.Compute/virtualMachines",
        "dependsOn": [
            "[variables('storageName')]"
        ],
        ...
    }
],
```

### <a name="example"></a><span data-ttu-id="f6958-176">Przykład</span><span class="sxs-lookup"><span data-stu-id="f6958-176">Example</span></span>

<span data-ttu-id="f6958-177">Szablon przykład Hello zwraca różne wartości zmiennej.</span><span class="sxs-lookup"><span data-stu-id="f6958-177">hello example template returns different variable values.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {},
    "variables": {
        "var1": "myVariable",
        "var2": [ 1,2,3,4 ],
        "var3": "[ variables('var1') ]",
        "var4": {
            "property1": "value1",
            "property2": "value2"
        }
    },
    "resources": [],
    "outputs": {
        "exampleOutput1": {
            "value": "[variables('var1')]",
            "type" : "string"
        },
        "exampleOutput2": {
            "value": "[variables('var2')]",
            "type" : "array"
        },
        "exampleOutput3": {
            "value": "[variables('var3')]",
            "type" : "string"
        },
        "exampleOutput4": {
            "value": "[variables('var4')]",
            "type" : "object"
        }
    }
}
```

<span data-ttu-id="f6958-178">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="f6958-178">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="f6958-179">Nazwa</span><span class="sxs-lookup"><span data-stu-id="f6958-179">Name</span></span> | <span data-ttu-id="f6958-180">Typ</span><span class="sxs-lookup"><span data-stu-id="f6958-180">Type</span></span> | <span data-ttu-id="f6958-181">Wartość</span><span class="sxs-lookup"><span data-stu-id="f6958-181">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="f6958-182">exampleOutput1</span><span class="sxs-lookup"><span data-stu-id="f6958-182">exampleOutput1</span></span> | <span data-ttu-id="f6958-183">Ciąg</span><span class="sxs-lookup"><span data-stu-id="f6958-183">String</span></span> | <span data-ttu-id="f6958-184">myVariable</span><span class="sxs-lookup"><span data-stu-id="f6958-184">myVariable</span></span> |
| <span data-ttu-id="f6958-185">exampleOutput2</span><span class="sxs-lookup"><span data-stu-id="f6958-185">exampleOutput2</span></span> | <span data-ttu-id="f6958-186">Tablica</span><span class="sxs-lookup"><span data-stu-id="f6958-186">Array</span></span> | <span data-ttu-id="f6958-187">[1, 2, 3, 4]</span><span class="sxs-lookup"><span data-stu-id="f6958-187">[1, 2, 3, 4]</span></span> |
| <span data-ttu-id="f6958-188">exampleOutput3</span><span class="sxs-lookup"><span data-stu-id="f6958-188">exampleOutput3</span></span> | <span data-ttu-id="f6958-189">Ciąg</span><span class="sxs-lookup"><span data-stu-id="f6958-189">String</span></span> | <span data-ttu-id="f6958-190">myVariable</span><span class="sxs-lookup"><span data-stu-id="f6958-190">myVariable</span></span> |
| <span data-ttu-id="f6958-191">exampleOutput4</span><span class="sxs-lookup"><span data-stu-id="f6958-191">exampleOutput4</span></span> |  <span data-ttu-id="f6958-192">Obiekt</span><span class="sxs-lookup"><span data-stu-id="f6958-192">Object</span></span> | <span data-ttu-id="f6958-193">{"właściwości property1": "wartość1", "property2": "wartość2"}</span><span class="sxs-lookup"><span data-stu-id="f6958-193">{"property1": "value1", "property2": "value2"}</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f6958-194">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f6958-194">Next steps</span></span>
* <span data-ttu-id="f6958-195">Aby uzyskać opis hello części szablonu usługi Azure Resource Manager, zobacz [szablonów Authoring Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="f6958-195">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="f6958-196">Zobacz wielu szablonów toomerge [za pomocą szablonów połączonych z usługą Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="f6958-196">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="f6958-197">tooiterate określoną liczbę razy podczas tworzenia typu zasobu, zobacz [utworzyć wiele wystąpień zasobów usługi Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="f6958-197">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="f6958-198">toosee toodeploy hello szablonu po utworzeniu, zobacz [wdrażania aplikacji przy użyciu szablonu usługi Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="f6958-198">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

