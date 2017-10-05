---
title: "Strukturę szablonu usługi Azure Resource Manager i składni | Dokumentacja firmy Microsoft"
description: "Opis struktury i właściwości szablonów usługi Azure Resource Manager za pomocą składni deklaratywnej JSON."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 19694cb4-d9ed-499a-a2cc-bcfc4922d7f5
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/14/2017
ms.author: tomfitz
ms.openlocfilehash: dc9b64062d7f68c83aa090eec96744819a5ca423
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="understand-the-structure-and-syntax-of-azure-resource-manager-templates"></a><span data-ttu-id="6a28c-103">Struktura i składni szablonów usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6a28c-103">Understand the structure and syntax of Azure Resource Manager templates</span></span>
<span data-ttu-id="6a28c-104">W tym temacie opisano strukturę szablonu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6a28c-104">This topic describes the structure of an Azure Resource Manager template.</span></span> <span data-ttu-id="6a28c-105">Stanowi różne sekcje szablonu i właściwości, które są dostępne w tych sekcjach.</span><span class="sxs-lookup"><span data-stu-id="6a28c-105">It presents the different sections of a template and the properties that are available in those sections.</span></span> <span data-ttu-id="6a28c-106">Szablon składa się z kodu JSON i wyrażeń, które służy do tworzenia wartości na potrzeby wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="6a28c-106">The template consists of JSON and expressions that you can use to construct values for your deployment.</span></span> <span data-ttu-id="6a28c-107">Samouczek krok po kroku dotyczące tworzenia szablonu, zobacz [Tworzenie pierwszego szablonu usługi Azure Resource Manager](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="6a28c-107">For a step-by-step tutorial on creating a template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>

## <a name="template-format"></a><span data-ttu-id="6a28c-108">Format szablonu</span><span class="sxs-lookup"><span data-stu-id="6a28c-108">Template format</span></span>
<span data-ttu-id="6a28c-109">W swojej najprostszej strukturze szablonu zawiera następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="6a28c-109">In its simplest structure, a template contains the following elements:</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "",
    "parameters": {  },
    "variables": {  },
    "resources": [  ],
    "outputs": {  }
}
```

| <span data-ttu-id="6a28c-110">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="6a28c-110">Element name</span></span> | <span data-ttu-id="6a28c-111">Wymagane</span><span class="sxs-lookup"><span data-stu-id="6a28c-111">Required</span></span> | <span data-ttu-id="6a28c-112">Opis</span><span class="sxs-lookup"><span data-stu-id="6a28c-112">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="6a28c-113">$schema</span><span class="sxs-lookup"><span data-stu-id="6a28c-113">$schema</span></span> |<span data-ttu-id="6a28c-114">Tak</span><span class="sxs-lookup"><span data-stu-id="6a28c-114">Yes</span></span> |<span data-ttu-id="6a28c-115">Lokalizacja pliku schematu JSON, który zawiera opis wersji języka szablonu.</span><span class="sxs-lookup"><span data-stu-id="6a28c-115">Location of the JSON schema file that describes the version of the template language.</span></span> <span data-ttu-id="6a28c-116">Użyj adres URL wyświetlany w poprzednim przykładzie.</span><span class="sxs-lookup"><span data-stu-id="6a28c-116">Use the URL shown in the preceding example.</span></span> |
| <span data-ttu-id="6a28c-117">contentVersion</span><span class="sxs-lookup"><span data-stu-id="6a28c-117">contentVersion</span></span> |<span data-ttu-id="6a28c-118">Tak</span><span class="sxs-lookup"><span data-stu-id="6a28c-118">Yes</span></span> |<span data-ttu-id="6a28c-119">Wersja szablonu (na przykład 1.0.0.0).</span><span class="sxs-lookup"><span data-stu-id="6a28c-119">Version of the template (such as 1.0.0.0).</span></span> <span data-ttu-id="6a28c-120">Musisz podać wartości dla tego elementu.</span><span class="sxs-lookup"><span data-stu-id="6a28c-120">You can provide any value for this element.</span></span> <span data-ttu-id="6a28c-121">Podczas wdrażania zasobów przy użyciu szablonu, ta wartość może służyć do upewnij się, że używany jest odpowiedniego szablonu.</span><span class="sxs-lookup"><span data-stu-id="6a28c-121">When deploying resources using the template, this value can be used to make sure that the right template is being used.</span></span> |
| <span data-ttu-id="6a28c-122">Parametry</span><span class="sxs-lookup"><span data-stu-id="6a28c-122">parameters</span></span> |<span data-ttu-id="6a28c-123">Nie</span><span class="sxs-lookup"><span data-stu-id="6a28c-123">No</span></span> |<span data-ttu-id="6a28c-124">Wartości, które są podane podczas wdrażania jest wykonywany w celu dostosowania wdrożenia zasobów.</span><span class="sxs-lookup"><span data-stu-id="6a28c-124">Values that are provided when deployment is executed to customize resource deployment.</span></span> |
| <span data-ttu-id="6a28c-125">zmienne</span><span class="sxs-lookup"><span data-stu-id="6a28c-125">variables</span></span> |<span data-ttu-id="6a28c-126">Nie</span><span class="sxs-lookup"><span data-stu-id="6a28c-126">No</span></span> |<span data-ttu-id="6a28c-127">Wartości, które są używane jako fragmenty JSON w szablonie, aby uprościć wyrażeń języka szablonu.</span><span class="sxs-lookup"><span data-stu-id="6a28c-127">Values that are used as JSON fragments in the template to simplify template language expressions.</span></span> |
| <span data-ttu-id="6a28c-128">Zasoby</span><span class="sxs-lookup"><span data-stu-id="6a28c-128">resources</span></span> |<span data-ttu-id="6a28c-129">Tak</span><span class="sxs-lookup"><span data-stu-id="6a28c-129">Yes</span></span> |<span data-ttu-id="6a28c-130">Typy zasobów, które są wdrożone lub zaktualizowane w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="6a28c-130">Resource types that are deployed or updated in a resource group.</span></span> |
| <span data-ttu-id="6a28c-131">dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="6a28c-131">outputs</span></span> |<span data-ttu-id="6a28c-132">Nie</span><span class="sxs-lookup"><span data-stu-id="6a28c-132">No</span></span> |<span data-ttu-id="6a28c-133">Wartości, które są zwracane po wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="6a28c-133">Values that are returned after deployment.</span></span> |

<span data-ttu-id="6a28c-134">Każdy element zawiera właściwości, które można ustawić.</span><span class="sxs-lookup"><span data-stu-id="6a28c-134">Each element contains properties you can set.</span></span> <span data-ttu-id="6a28c-135">Poniżej przedstawiono przykład zawierający pełnej składni szablonu:</span><span class="sxs-lookup"><span data-stu-id="6a28c-135">The following example contains the full syntax for a template:</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "",
    "parameters": {  
        "<parameter-name>" : {
            "type" : "<type-of-parameter-value>",
            "defaultValue": "<default-value-of-parameter>",
            "allowedValues": [ "<array-of-allowed-values>" ],
            "minValue": <minimum-value-for-int>,
            "maxValue": <maximum-value-for-int>,
            "minLength": <minimum-length-for-string-or-array>,
            "maxLength": <maximum-length-for-string-or-array-parameters>,
            "metadata": {
                "description": "<description-of-the parameter>" 
            }
        }
    },
    "variables": {  
        "<variable-name>": "<variable-value>",
        "<variable-name>": { 
            <variable-complex-type-value> 
        }
    },
    "resources": [
      {
          "condition": "<boolean-value-whether-to-deploy>",
          "apiVersion": "<api-version-of-resource>",
          "type": "<resource-provider-namespace/resource-type-name>",
          "name": "<name-of-the-resource>",
          "location": "<location-of-resource>",
          "tags": {
              "<tag-name1>": "<tag-value1>",
              "<tag-name2>": "<tag-value2>"
          },
          "comments": "<your-reference-notes>",
          "copy": {
              "name": "<name-of-copy-loop>",
              "count": "<number-of-iterations>",
              "mode": "<serial-or-parallel>",
              "batchSize": "<number-to-deploy-serially>"
          },
          "dependsOn": [
              "<array-of-related-resource-names>"
          ],
          "properties": {
              "<settings-for-the-resource>",
              "copy": [
                  {
                      "name": ,
                      "count": ,
                      "input": {}
                  }
              ]
          },
          "resources": [
              "<array-of-child-resources>"
          ]
      }
    ],
    "outputs": {
        "<outputName>" : {
            "type" : "<type-of-output-value>",
            "value": "<output-value-expression>"
        }
    }
}
```

<span data-ttu-id="6a28c-136">Omówione części szablonu bardziej szczegółowo w dalszej części tego tematu.</span><span class="sxs-lookup"><span data-stu-id="6a28c-136">We examine the sections of the template in greater detail later in this topic.</span></span>

## <a name="expressions-and-functions"></a><span data-ttu-id="6a28c-137">Wyrażeń i funkcji</span><span class="sxs-lookup"><span data-stu-id="6a28c-137">Expressions and functions</span></span>
<span data-ttu-id="6a28c-138">Podstawowa składnia szablonu jest JSON.</span><span class="sxs-lookup"><span data-stu-id="6a28c-138">The basic syntax of the template is JSON.</span></span> <span data-ttu-id="6a28c-139">Jednak wyrażeń i funkcji rozszerzyć dostępnych w szablonie wartości JSON.</span><span class="sxs-lookup"><span data-stu-id="6a28c-139">However, expressions and functions extend the JSON values available within the template.</span></span>  <span data-ttu-id="6a28c-140">Wyrażenia są zapisywane w literałach ciągu JSON, których pierwszy i ostatnie znaki są nawiasy: `[` i `]`odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="6a28c-140">Expressions are written within JSON string literals whose first and last characters are the brackets: `[` and `]`, respectively.</span></span> <span data-ttu-id="6a28c-141">Wartość wyrażenia jest oceniane podczas wdrażania szablonu.</span><span class="sxs-lookup"><span data-stu-id="6a28c-141">The value of the expression is evaluated when the template is deployed.</span></span> <span data-ttu-id="6a28c-142">Podczas zapisywania jako literału ciągu, wynik obliczania wyrażenia może być innego typu JSON, takich jak tablicy lub liczba całkowita, w zależności od rzeczywistej wyrażenia.</span><span class="sxs-lookup"><span data-stu-id="6a28c-142">While written as a string literal, the result of evaluating the expression can be of a different JSON type, such as an array or integer, depending on the actual expression.</span></span>  <span data-ttu-id="6a28c-143">Mieć literałem rozpoczynać nawiasu `[`, ale nie została ona interpretowana jako wyrażenie, Dodaj dodatkowe nawiasu zacząć ciąg z `[[`.</span><span class="sxs-lookup"><span data-stu-id="6a28c-143">To have a literal string start with a bracket `[`, but not have it interpreted as an expression, add an extra bracket to start the string with `[[`.</span></span>

<span data-ttu-id="6a28c-144">Zazwyczaj umożliwia wyrażenia funkcji wykonywać operacje związane z konfigurowaniem wdrażania.</span><span class="sxs-lookup"><span data-stu-id="6a28c-144">Typically, you use expressions with functions to perform operations for configuring the deployment.</span></span> <span data-ttu-id="6a28c-145">Po prostu, tak jak w języku JavaScript, wywołania funkcji są sformatowane jako `functionName(arg1,arg2,arg3)`.</span><span class="sxs-lookup"><span data-stu-id="6a28c-145">Just like in JavaScript, function calls are formatted as `functionName(arg1,arg2,arg3)`.</span></span> <span data-ttu-id="6a28c-146">Możesz odwoływać się do właściwości przy użyciu operatorów kropka i [Indeks].</span><span class="sxs-lookup"><span data-stu-id="6a28c-146">You reference properties by using the dot and [index] operators.</span></span>

<span data-ttu-id="6a28c-147">Poniższy przykład przedstawia użycie kilku funkcji podczas tworzenia wartości:</span><span class="sxs-lookup"><span data-stu-id="6a28c-147">The following example shows how to use several functions when constructing values:</span></span>

```json
"variables": {
    "location": "[resourceGroup().location]",
    "usernameAndPassword": "[concat(parameters('username'), ':', parameters('password'))]",
    "authorizationHeader": "[concat('Basic ', base64(variables('usernameAndPassword')))]"
}
```

<span data-ttu-id="6a28c-148">Aby uzyskać pełną listę funkcji szablonu, zobacz [funkcje szablonu usługi Azure Resource Manager](resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="6a28c-148">For the full list of template functions, see [Azure Resource Manager template functions](resource-group-template-functions.md).</span></span> 

## <a name="parameters"></a><span data-ttu-id="6a28c-149">Parametry</span><span class="sxs-lookup"><span data-stu-id="6a28c-149">Parameters</span></span>
<span data-ttu-id="6a28c-150">W sekcji Parametry szablonu można określić wartości, które można wprowadzić podczas wdrażania zasobów.</span><span class="sxs-lookup"><span data-stu-id="6a28c-150">In the parameters section of the template, you specify which values you can input when deploying the resources.</span></span> <span data-ttu-id="6a28c-151">Wartości tych parametrów umożliwiają dostosowanie wdrożenie, podając wartości, które są dostosowane określonym środowisku (na przykład deweloperów, testowego i produkcyjnego).</span><span class="sxs-lookup"><span data-stu-id="6a28c-151">These parameter values enable you to customize the deployment by providing values that are tailored for a particular environment (such as dev, test, and production).</span></span> <span data-ttu-id="6a28c-152">Nie musisz podać parametry w szablonie, ale bez parametrów szablonu będzie zawsze wdrażać te same zasoby z tej samej nazwy, lokalizacji i właściwości.</span><span class="sxs-lookup"><span data-stu-id="6a28c-152">You do not have to provide parameters in your template, but without parameters your template would always deploy the same resources with the same names, locations, and properties.</span></span>

<span data-ttu-id="6a28c-153">Definiuje parametry o następującej strukturze:</span><span class="sxs-lookup"><span data-stu-id="6a28c-153">You define parameters with the following structure:</span></span>

```json
"parameters": {
    "<parameter-name>" : {
        "type" : "<type-of-parameter-value>",
        "defaultValue": "<default-value-of-parameter>",
        "allowedValues": [ "<array-of-allowed-values>" ],
        "minValue": <minimum-value-for-int>,
        "maxValue": <maximum-value-for-int>,
        "minLength": <minimum-length-for-string-or-array>,
        "maxLength": <maximum-length-for-string-or-array-parameters>,
        "metadata": {
            "description": "<description-of-the parameter>" 
        }
    }
}
```

| <span data-ttu-id="6a28c-154">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="6a28c-154">Element name</span></span> | <span data-ttu-id="6a28c-155">Wymagane</span><span class="sxs-lookup"><span data-stu-id="6a28c-155">Required</span></span> | <span data-ttu-id="6a28c-156">Opis</span><span class="sxs-lookup"><span data-stu-id="6a28c-156">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="6a28c-157">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="6a28c-157">parameterName</span></span> |<span data-ttu-id="6a28c-158">Tak</span><span class="sxs-lookup"><span data-stu-id="6a28c-158">Yes</span></span> |<span data-ttu-id="6a28c-159">Nazwa parametru.</span><span class="sxs-lookup"><span data-stu-id="6a28c-159">Name of the parameter.</span></span> <span data-ttu-id="6a28c-160">Musi być prawidłowym identyfikatorem języka JavaScript.</span><span class="sxs-lookup"><span data-stu-id="6a28c-160">Must be a valid JavaScript identifier.</span></span> |
| <span data-ttu-id="6a28c-161">type</span><span class="sxs-lookup"><span data-stu-id="6a28c-161">type</span></span> |<span data-ttu-id="6a28c-162">Tak</span><span class="sxs-lookup"><span data-stu-id="6a28c-162">Yes</span></span> |<span data-ttu-id="6a28c-163">Typ wartości parametru.</span><span class="sxs-lookup"><span data-stu-id="6a28c-163">Type of the parameter value.</span></span> <span data-ttu-id="6a28c-164">Zobacz listę dozwolonych typów pod tą tabelą.</span><span class="sxs-lookup"><span data-stu-id="6a28c-164">See the list of allowed types after this table.</span></span> |
| <span data-ttu-id="6a28c-165">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="6a28c-165">defaultValue</span></span> |<span data-ttu-id="6a28c-166">Nie</span><span class="sxs-lookup"><span data-stu-id="6a28c-166">No</span></span> |<span data-ttu-id="6a28c-167">Wartość domyślna parametru, jeśli wartość nie zostanie podana dla parametru.</span><span class="sxs-lookup"><span data-stu-id="6a28c-167">Default value for the parameter, if no value is provided for the parameter.</span></span> |
| <span data-ttu-id="6a28c-168">allowedValues</span><span class="sxs-lookup"><span data-stu-id="6a28c-168">allowedValues</span></span> |<span data-ttu-id="6a28c-169">Nie</span><span class="sxs-lookup"><span data-stu-id="6a28c-169">No</span></span> |<span data-ttu-id="6a28c-170">Tablica dozwolonych wartości tego parametru upewnić się, że podano wartość prawej strony.</span><span class="sxs-lookup"><span data-stu-id="6a28c-170">Array of allowed values for the parameter to make sure that the right value is provided.</span></span> |
| <span data-ttu-id="6a28c-171">Wartość MinValue</span><span class="sxs-lookup"><span data-stu-id="6a28c-171">minValue</span></span> |<span data-ttu-id="6a28c-172">Nie</span><span class="sxs-lookup"><span data-stu-id="6a28c-172">No</span></span> |<span data-ttu-id="6a28c-173">Minimalna wartość parametrów typu int, ta wartość jest włącznie.</span><span class="sxs-lookup"><span data-stu-id="6a28c-173">The minimum value for int type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="6a28c-174">MaxValue</span><span class="sxs-lookup"><span data-stu-id="6a28c-174">maxValue</span></span> |<span data-ttu-id="6a28c-175">Nie</span><span class="sxs-lookup"><span data-stu-id="6a28c-175">No</span></span> |<span data-ttu-id="6a28c-176">Maksymalna wartość dla parametrów typu int, ta wartość jest włącznie.</span><span class="sxs-lookup"><span data-stu-id="6a28c-176">The maximum value for int type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="6a28c-177">Element minLength</span><span class="sxs-lookup"><span data-stu-id="6a28c-177">minLength</span></span> |<span data-ttu-id="6a28c-178">Nie</span><span class="sxs-lookup"><span data-stu-id="6a28c-178">No</span></span> |<span data-ttu-id="6a28c-179">Minimalna długość ciągu, secureString i parametrów typu tablicy, ta wartość jest włącznie.</span><span class="sxs-lookup"><span data-stu-id="6a28c-179">The minimum length for string, secureString, and array type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="6a28c-180">Element maxLength</span><span class="sxs-lookup"><span data-stu-id="6a28c-180">maxLength</span></span> |<span data-ttu-id="6a28c-181">Nie</span><span class="sxs-lookup"><span data-stu-id="6a28c-181">No</span></span> |<span data-ttu-id="6a28c-182">Maksymalna długość ciągu, secureString i parametrów typu tablicy, ta wartość jest włącznie.</span><span class="sxs-lookup"><span data-stu-id="6a28c-182">The maximum length for string, secureString, and array type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="6a28c-183">Opis elementu</span><span class="sxs-lookup"><span data-stu-id="6a28c-183">description</span></span> |<span data-ttu-id="6a28c-184">Nie</span><span class="sxs-lookup"><span data-stu-id="6a28c-184">No</span></span> |<span data-ttu-id="6a28c-185">Opis parametru, który będzie wyświetlany użytkownikom za pośrednictwem portalu.</span><span class="sxs-lookup"><span data-stu-id="6a28c-185">Description of the parameter that is displayed to users through the portal.</span></span> |

<span data-ttu-id="6a28c-186">Są dozwolonymi typami i wartości:</span><span class="sxs-lookup"><span data-stu-id="6a28c-186">The allowed types and values are:</span></span>

* <span data-ttu-id="6a28c-187">**ciąg**</span><span class="sxs-lookup"><span data-stu-id="6a28c-187">**string**</span></span>
* <span data-ttu-id="6a28c-188">**secureString**</span><span class="sxs-lookup"><span data-stu-id="6a28c-188">**secureString**</span></span>
* <span data-ttu-id="6a28c-189">**int**</span><span class="sxs-lookup"><span data-stu-id="6a28c-189">**int**</span></span>
* <span data-ttu-id="6a28c-190">**wartość logiczna**</span><span class="sxs-lookup"><span data-stu-id="6a28c-190">**bool**</span></span>
* <span data-ttu-id="6a28c-191">**obiekt**</span><span class="sxs-lookup"><span data-stu-id="6a28c-191">**object**</span></span> 
* <span data-ttu-id="6a28c-192">**secureObject**</span><span class="sxs-lookup"><span data-stu-id="6a28c-192">**secureObject**</span></span>
* <span data-ttu-id="6a28c-193">**Tablica**</span><span class="sxs-lookup"><span data-stu-id="6a28c-193">**array**</span></span>

<span data-ttu-id="6a28c-194">Aby określić parametr jako opcjonalne, należy podać właściwość defaultValue (może być ciągiem pustym).</span><span class="sxs-lookup"><span data-stu-id="6a28c-194">To specify a parameter as optional, provide a defaultValue (can be an empty string).</span></span> 

<span data-ttu-id="6a28c-195">Jeśli określono nazwę parametru w szablonie parametr w poleceniu, aby wdrożyć szablon jest zgodny, jest potencjalnych niejednoznaczności wartości podane przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6a28c-195">If you specify a parameter name in your template that matches a parameter in the command to deploy the template, there is potential ambiguity about the values you provide.</span></span> <span data-ttu-id="6a28c-196">Menedżer zasobów usuwa to pomyłka, dodając przyrostek **FromTemplate** do parametru szablonu.</span><span class="sxs-lookup"><span data-stu-id="6a28c-196">Resource Manager resolves this confusion by adding the postfix **FromTemplate** to the template parameter.</span></span> <span data-ttu-id="6a28c-197">Na przykład, jeśli zawiera parametr o nazwie **ResourceGroupName** w szablonie, powoduje konflikt z **ResourceGroupName** parametru w [AzureRmResourceGroupDeployment nowy](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6a28c-197">For example, if you include a parameter named **ResourceGroupName** in your template, it conflicts with the **ResourceGroupName** parameter in the [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet.</span></span> <span data-ttu-id="6a28c-198">Podczas wdrażania, monit o podanie wartości **ResourceGroupNameFromTemplate**.</span><span class="sxs-lookup"><span data-stu-id="6a28c-198">During deployment, you are prompted to provide a value for **ResourceGroupNameFromTemplate**.</span></span> <span data-ttu-id="6a28c-199">Ogólnie rzecz biorąc należy unikać to pomyłka nie nadawanie nazw parametrów o takiej samej nazwie jako parametry używane dla operacji wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="6a28c-199">In general, you should avoid this confusion by not naming parameters with the same name as parameters used for deployment operations.</span></span>

> [!NOTE]
> <span data-ttu-id="6a28c-200">Wszystkie hasła, klucze i innych informacji poufnych, należy użyć **secureString** typu.</span><span class="sxs-lookup"><span data-stu-id="6a28c-200">All passwords, keys, and other secrets should use the **secureString** type.</span></span> <span data-ttu-id="6a28c-201">W przypadku przekazania danych poufnych w obiekcie JSON, użyj **secureObject** typu.</span><span class="sxs-lookup"><span data-stu-id="6a28c-201">If you pass sensitive data in a JSON object, use the **secureObject** type.</span></span> <span data-ttu-id="6a28c-202">Nie można odczytać parametrów szablonu z typami secureString lub secureObject po wdrożeniu zasobów.</span><span class="sxs-lookup"><span data-stu-id="6a28c-202">Template parameters with secureString or secureObject types cannot be read after resource deployment.</span></span> 
> 
> <span data-ttu-id="6a28c-203">Na przykład następujący wpis w historii wdrożenia zawiera wartość dla ciągu lub obiektu, ale nie dla secureString i secureObject.</span><span class="sxs-lookup"><span data-stu-id="6a28c-203">For example, the following entry in the deployment history shows the value for a string and object but not for secureString and secureObject.</span></span>
>
> ![Pokaż wartości wdrożenia](./media/resource-group-authoring-templates/show-parameters.png)  
>

<span data-ttu-id="6a28c-205">Poniższy przykład przedstawia sposób definiowania parametrów:</span><span class="sxs-lookup"><span data-stu-id="6a28c-205">The following example shows how to define parameters:</span></span>

```json
"parameters": {
    "siteName": {
        "type": "string",
        "defaultValue": "[concat('site', uniqueString(resourceGroup().id))]"
    },
    "hostingPlanName": {
        "type": "string",
        "defaultValue": "[concat(parameters('siteName'),'-plan')]"
    },
    "skuName": {
        "type": "string",
        "defaultValue": "F1",
        "allowedValues": [
          "F1",
          "D1",
          "B1",
          "B2",
          "B3",
          "S1",
          "S2",
          "S3",
          "P1",
          "P2",
          "P3",
          "P4"
        ]
    },
    "skuCapacity": {
        "type": "int",
        "defaultValue": 1,
        "minValue": 1
    }
}
```

<span data-ttu-id="6a28c-206">Jak wartości parametrów wejściowych podczas wdrażania, zobacz [wdrażania aplikacji przy użyciu szablonu usługi Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="6a28c-206">For how to input the parameter values during deployment, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span> 

## <a name="variables"></a><span data-ttu-id="6a28c-207">Zmienne</span><span class="sxs-lookup"><span data-stu-id="6a28c-207">Variables</span></span>
<span data-ttu-id="6a28c-208">W sekcji variables można skonstruować wartości, które mogą być używane w szablonie.</span><span class="sxs-lookup"><span data-stu-id="6a28c-208">In the variables section, you construct values that can be used throughout your template.</span></span> <span data-ttu-id="6a28c-209">Nie trzeba zdefiniować zmienne, ale one często uprościć szablonu zmniejszając złożonych wyrażeń.</span><span class="sxs-lookup"><span data-stu-id="6a28c-209">You do not need to define variables, but they often simplify your template by reducing complex expressions.</span></span>

<span data-ttu-id="6a28c-210">Można zdefiniować zmienne o następującej strukturze:</span><span class="sxs-lookup"><span data-stu-id="6a28c-210">You define variables with the following structure:</span></span>

```json
"variables": {
    "<variable-name>": "<variable-value>",
    "<variable-name>": { 
        <variable-complex-type-value> 
    }
}
```

<span data-ttu-id="6a28c-211">Poniższy przykład przedstawia sposób zdefiniowania zmiennej, który jest tworzony z dwóch wartości parametrów:</span><span class="sxs-lookup"><span data-stu-id="6a28c-211">The following example shows how to define a variable that is constructed from two parameter values:</span></span>

```json
"variables": {
    "connectionString": "[concat('Name=', parameters('username'), ';Password=', parameters('password'))]"
}
```

<span data-ttu-id="6a28c-212">W kolejnym przykładzie pokazano zmiennej, która jest typem złożonym JSON i zmienne, które są tworzone na podstawie innych zmiennych:</span><span class="sxs-lookup"><span data-stu-id="6a28c-212">The next example shows a variable that is a complex JSON type, and variables that are constructed from other variables:</span></span>

```json
"parameters": {
    "environmentName": {
        "type": "string",
        "allowedValues": [
          "test",
          "prod"
        ]
    }
},
"variables": {
    "environmentSettings": {
        "test": {
            "instancesSize": "Small",
            "instancesCount": 1
        },
        "prod": {
            "instancesSize": "Large",
            "instancesCount": 4
        }
    },
    "currentEnvironmentSettings": "[variables('environmentSettings')[parameters('environmentName')]]",
    "instancesSize": "[variables('currentEnvironmentSettings').instancesSize]",
    "instancesCount": "[variables('currentEnvironmentSettings').instancesCount]"
}
```

## <a name="resources"></a><span data-ttu-id="6a28c-213">Zasoby</span><span class="sxs-lookup"><span data-stu-id="6a28c-213">Resources</span></span>
<span data-ttu-id="6a28c-214">W sekcji zasobów można zdefiniować zasoby, które są wdrożone lub aktualizowane.</span><span class="sxs-lookup"><span data-stu-id="6a28c-214">In the resources section, you define the resources that are deployed or updated.</span></span> <span data-ttu-id="6a28c-215">W tej sekcji można uzyskać skomplikowane, ponieważ należy zrozumieć typy, które jest wdrażany w celu zapewnienia właściwych wartości.</span><span class="sxs-lookup"><span data-stu-id="6a28c-215">This section can get complicated because you must understand the types you are deploying to provide the right values.</span></span> <span data-ttu-id="6a28c-216">Dla określonych zasobów wartości (apiVersion, typ i właściwości), które należy ustawić, zobacz [zdefiniować zasoby w szablonach usługi Azure Resource Manager](/azure/templates/).</span><span class="sxs-lookup"><span data-stu-id="6a28c-216">For the resource-specific values (apiVersion, type, and properties) that you need to set, see [Define resources in Azure Resource Manager templates](/azure/templates/).</span></span> 

<span data-ttu-id="6a28c-217">Można zdefiniować zasoby o następującej strukturze:</span><span class="sxs-lookup"><span data-stu-id="6a28c-217">You define resources with the following structure:</span></span>

```json
"resources": [
  {
      "condition": "<boolean-value-whether-to-deploy>",
      "apiVersion": "<api-version-of-resource>",
      "type": "<resource-provider-namespace/resource-type-name>",
      "name": "<name-of-the-resource>",
      "location": "<location-of-resource>",
      "tags": {
          "<tag-name1>": "<tag-value1>",
          "<tag-name2>": "<tag-value2>"
      },
      "comments": "<your-reference-notes>",
      "copy": {
          "name": "<name-of-copy-loop>",
          "count": "<number-of-iterations>",
          "mode": "<serial-or-parallel>",
          "batchSize": "<number-to-deploy-serially>"
      },
      "dependsOn": [
          "<array-of-related-resource-names>"
      ],
      "properties": {
          "<settings-for-the-resource>",
          "copy": [
              {
                  "name": ,
                  "count": ,
                  "input": {}
              }
          ]
      },
      "resources": [
          "<array-of-child-resources>"
      ]
  }
]
```

| <span data-ttu-id="6a28c-218">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="6a28c-218">Element name</span></span> | <span data-ttu-id="6a28c-219">Wymagane</span><span class="sxs-lookup"><span data-stu-id="6a28c-219">Required</span></span> | <span data-ttu-id="6a28c-220">Opis</span><span class="sxs-lookup"><span data-stu-id="6a28c-220">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="6a28c-221">Warunek</span><span class="sxs-lookup"><span data-stu-id="6a28c-221">condition</span></span> | <span data-ttu-id="6a28c-222">Nie</span><span class="sxs-lookup"><span data-stu-id="6a28c-222">No</span></span> | <span data-ttu-id="6a28c-223">Wartość logiczna wskazująca, czy zasób jest wdrażany.</span><span class="sxs-lookup"><span data-stu-id="6a28c-223">Boolean value that indicates whether the resource is deployed.</span></span> |
| <span data-ttu-id="6a28c-224">apiVersion</span><span class="sxs-lookup"><span data-stu-id="6a28c-224">apiVersion</span></span> |<span data-ttu-id="6a28c-225">Tak</span><span class="sxs-lookup"><span data-stu-id="6a28c-225">Yes</span></span> |<span data-ttu-id="6a28c-226">Wersja interfejsu API REST do użycia podczas tworzenia zasobu.</span><span class="sxs-lookup"><span data-stu-id="6a28c-226">Version of the REST API to use for creating the resource.</span></span> |
| <span data-ttu-id="6a28c-227">type</span><span class="sxs-lookup"><span data-stu-id="6a28c-227">type</span></span> |<span data-ttu-id="6a28c-228">Tak</span><span class="sxs-lookup"><span data-stu-id="6a28c-228">Yes</span></span> |<span data-ttu-id="6a28c-229">Typ zasobu.</span><span class="sxs-lookup"><span data-stu-id="6a28c-229">Type of the resource.</span></span> <span data-ttu-id="6a28c-230">Ta wartość jest kombinacją przestrzeń nazw dostawcy zasobów i typu zasobu (takich jak **magazyn.Microsoft/kontamagazynu**).</span><span class="sxs-lookup"><span data-stu-id="6a28c-230">This value is a combination of the namespace of the resource provider and the resource type (such as **Microsoft.Storage/storageAccounts**).</span></span> |
| <span data-ttu-id="6a28c-231">name</span><span class="sxs-lookup"><span data-stu-id="6a28c-231">name</span></span> |<span data-ttu-id="6a28c-232">Tak</span><span class="sxs-lookup"><span data-stu-id="6a28c-232">Yes</span></span> |<span data-ttu-id="6a28c-233">Nazwa zasobu.</span><span class="sxs-lookup"><span data-stu-id="6a28c-233">Name of the resource.</span></span> <span data-ttu-id="6a28c-234">Nazwa musi występować po zdefiniowane w RFC3986 ograniczenia składnika identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="6a28c-234">The name must follow URI component restrictions defined in RFC3986.</span></span> <span data-ttu-id="6a28c-235">Ponadto usług platformy Azure, które udostępniają poza strony zweryfikować nazwę, aby zapewnić, że nazwa zasobu nie jest próba podszywają się pod innego tożsamości.</span><span class="sxs-lookup"><span data-stu-id="6a28c-235">In addition, Azure services that expose the resource name to outside parties validate the name to make sure it is not an attempt to spoof another identity.</span></span> |
| <span data-ttu-id="6a28c-236">location</span><span class="sxs-lookup"><span data-stu-id="6a28c-236">location</span></span> |<span data-ttu-id="6a28c-237">Zmienia się</span><span class="sxs-lookup"><span data-stu-id="6a28c-237">Varies</span></span> |<span data-ttu-id="6a28c-238">Obsługiwane lokalizacje geograficzne podane zasobu.</span><span class="sxs-lookup"><span data-stu-id="6a28c-238">Supported geo-locations of the provided resource.</span></span> <span data-ttu-id="6a28c-239">Można wybrać dowolny z dostępnych lokalizacji, ale zazwyczaj warto wybrać, który znajduje się w pobliżu użytkowników.</span><span class="sxs-lookup"><span data-stu-id="6a28c-239">You can select any of the available locations, but typically it makes sense to pick one that is close to your users.</span></span> <span data-ttu-id="6a28c-240">Zazwyczaj również dobrym rozwiązaniem jest umieszczenie zasoby, które współdziałają ze sobą w tym samym regionie.</span><span class="sxs-lookup"><span data-stu-id="6a28c-240">Usually, it also makes sense to place resources that interact with each other in the same region.</span></span> <span data-ttu-id="6a28c-241">Większość typów zasobów wymaga lokalizacji, ale nie wymagają lokalizację niektórych typów (takich jak przypisanie roli).</span><span class="sxs-lookup"><span data-stu-id="6a28c-241">Most resource types require a location, but some types (such as a role assignment) do not require a location.</span></span> <span data-ttu-id="6a28c-242">Zobacz [Ustaw lokalizację zasobów w szablonach usługi Azure Resource Manager](resource-manager-template-location.md).</span><span class="sxs-lookup"><span data-stu-id="6a28c-242">See [Set resource location in Azure Resource Manager templates](resource-manager-template-location.md).</span></span> |
| <span data-ttu-id="6a28c-243">tags</span><span class="sxs-lookup"><span data-stu-id="6a28c-243">tags</span></span> |<span data-ttu-id="6a28c-244">Nie</span><span class="sxs-lookup"><span data-stu-id="6a28c-244">No</span></span> |<span data-ttu-id="6a28c-245">Tagi, które są skojarzone z zasobem.</span><span class="sxs-lookup"><span data-stu-id="6a28c-245">Tags that are associated with the resource.</span></span> <span data-ttu-id="6a28c-246">Zobacz [tagów zasobów w szablonach usługi Azure Resource Manager](resource-manager-template-tags.md).</span><span class="sxs-lookup"><span data-stu-id="6a28c-246">See [Tag resources in Azure Resource Manager templates](resource-manager-template-tags.md).</span></span> |
| <span data-ttu-id="6a28c-247">Komentarze</span><span class="sxs-lookup"><span data-stu-id="6a28c-247">comments</span></span> |<span data-ttu-id="6a28c-248">Nie</span><span class="sxs-lookup"><span data-stu-id="6a28c-248">No</span></span> |<span data-ttu-id="6a28c-249">Notatki za dokumentację zasobów w szablonie</span><span class="sxs-lookup"><span data-stu-id="6a28c-249">Your notes for documenting the resources in your template</span></span> |
| <span data-ttu-id="6a28c-250">Kopiuj</span><span class="sxs-lookup"><span data-stu-id="6a28c-250">copy</span></span> |<span data-ttu-id="6a28c-251">Nie</span><span class="sxs-lookup"><span data-stu-id="6a28c-251">No</span></span> |<span data-ttu-id="6a28c-252">Jeśli wymagane jest więcej niż jedno wystąpienie, liczba zasobów do utworzenia.</span><span class="sxs-lookup"><span data-stu-id="6a28c-252">If more than one instance is needed, the number of resources to create.</span></span> <span data-ttu-id="6a28c-253">Domyślnym trybem jest równoległe.</span><span class="sxs-lookup"><span data-stu-id="6a28c-253">The default mode is parallel.</span></span> <span data-ttu-id="6a28c-254">Określ tryb serial gdy nie ma wszystkich lub zasoby w celu wdrożenia w tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="6a28c-254">Specify serial mode when you do not want all or the resources to deploy at the same time.</span></span> <span data-ttu-id="6a28c-255">Aby uzyskać więcej informacji, zobacz [utworzyć wiele wystąpień zasobów usługi Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="6a28c-255">For more information, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span> |
| <span data-ttu-id="6a28c-256">dependsOn</span><span class="sxs-lookup"><span data-stu-id="6a28c-256">dependsOn</span></span> |<span data-ttu-id="6a28c-257">Nie</span><span class="sxs-lookup"><span data-stu-id="6a28c-257">No</span></span> |<span data-ttu-id="6a28c-258">Zasoby, które należy wdrożyć przed wdrożeniem tego zasobu.</span><span class="sxs-lookup"><span data-stu-id="6a28c-258">Resources that must be deployed before this resource is deployed.</span></span> <span data-ttu-id="6a28c-259">Menedżer zasobów ocenia zależności między zasobami i wdraża je w odpowiedniej kolejności.</span><span class="sxs-lookup"><span data-stu-id="6a28c-259">Resource Manager evaluates the dependencies between resources and deploys them in the correct order.</span></span> <span data-ttu-id="6a28c-260">Zasoby nie są zależne od siebie, są wdrożone równolegle.</span><span class="sxs-lookup"><span data-stu-id="6a28c-260">When resources are not dependent on each other, they are deployed in parallel.</span></span> <span data-ttu-id="6a28c-261">Wartość może być rozdzielaną przecinkami listą zasobu nazwy lub unikatowych identyfikatorów zasobów.</span><span class="sxs-lookup"><span data-stu-id="6a28c-261">The value can be a comma-separated list of a resource names or resource unique identifiers.</span></span> <span data-ttu-id="6a28c-262">Tylko listy zasobów, które są wdrażane w tym szablonie.</span><span class="sxs-lookup"><span data-stu-id="6a28c-262">Only list resources that are deployed in this template.</span></span> <span data-ttu-id="6a28c-263">Zasoby, które nie są zdefiniowane w tym szablonie musi już istnieć.</span><span class="sxs-lookup"><span data-stu-id="6a28c-263">Resources that are not defined in this template must already exist.</span></span> <span data-ttu-id="6a28c-264">Unikaj Dodawanie zależności niepotrzebne, jak mogą spowalniać wdrożenia i utworzyć zależności cykliczne.</span><span class="sxs-lookup"><span data-stu-id="6a28c-264">Avoid adding unnecessary dependencies as they can slow your deployment and create circular dependencies.</span></span> <span data-ttu-id="6a28c-265">Aby uzyskać wskazówki dotyczące zależności ustawienia, zobacz [Definiowanie zależności w szablonach usługi Azure Resource Manager](resource-group-define-dependencies.md).</span><span class="sxs-lookup"><span data-stu-id="6a28c-265">For guidance on setting dependencies, see [Defining dependencies in Azure Resource Manager templates](resource-group-define-dependencies.md).</span></span> |
| <span data-ttu-id="6a28c-266">properties</span><span class="sxs-lookup"><span data-stu-id="6a28c-266">properties</span></span> |<span data-ttu-id="6a28c-267">Nie</span><span class="sxs-lookup"><span data-stu-id="6a28c-267">No</span></span> |<span data-ttu-id="6a28c-268">Ustawienia konfiguracji określonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="6a28c-268">Resource-specific configuration settings.</span></span> <span data-ttu-id="6a28c-269">Wartości właściwości są takie same jak wartości podane w treści żądania dla operacji interfejsu API REST (metody PUT) do utworzenia zasobu.</span><span class="sxs-lookup"><span data-stu-id="6a28c-269">The values for the properties are the same as the values you provide in the request body for the REST API operation (PUT method) to create the resource.</span></span> <span data-ttu-id="6a28c-270">Można również określić tablicy kopiowania, aby utworzyć wiele wystąpień właściwości.</span><span class="sxs-lookup"><span data-stu-id="6a28c-270">You can also specify a copy array to create multiple instances of a property.</span></span> <span data-ttu-id="6a28c-271">Aby uzyskać więcej informacji, zobacz [utworzyć wiele wystąpień zasobów usługi Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="6a28c-271">For more information, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span> |
| <span data-ttu-id="6a28c-272">Zasoby</span><span class="sxs-lookup"><span data-stu-id="6a28c-272">resources</span></span> |<span data-ttu-id="6a28c-273">Nie</span><span class="sxs-lookup"><span data-stu-id="6a28c-273">No</span></span> |<span data-ttu-id="6a28c-274">Zasoby podrzędne, które zależą od zasobu został określony.</span><span class="sxs-lookup"><span data-stu-id="6a28c-274">Child resources that depend on the resource being defined.</span></span> <span data-ttu-id="6a28c-275">Podaj tylko typy zasobów, które są dozwolone w schemacie zasobu nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="6a28c-275">Only provide resource types that are permitted by the schema of the parent resource.</span></span> <span data-ttu-id="6a28c-276">Pełny typ zasobu podrzędnych obejmuje nadrzędny typ zasobu, takich jak **Microsoft.Web/sites/extensions**.</span><span class="sxs-lookup"><span data-stu-id="6a28c-276">The fully qualified type of the child resource includes the parent resource type, such as **Microsoft.Web/sites/extensions**.</span></span> <span data-ttu-id="6a28c-277">Zależność od zasobu nadrzędnego nie jest oznaczany.</span><span class="sxs-lookup"><span data-stu-id="6a28c-277">Dependency on the parent resource is not implied.</span></span> <span data-ttu-id="6a28c-278">Jawnie zdefiniuj tej zależności.</span><span class="sxs-lookup"><span data-stu-id="6a28c-278">You must explicitly define that dependency.</span></span> |

<span data-ttu-id="6a28c-279">Sekcja zasobów zawiera zasoby w celu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="6a28c-279">The resources section contains an array of the resources to deploy.</span></span> <span data-ttu-id="6a28c-280">W ramach każdego zasobu można również zdefiniować tablicę zasoby podrzędne.</span><span class="sxs-lookup"><span data-stu-id="6a28c-280">Within each resource, you can also define an array of child resources.</span></span> <span data-ttu-id="6a28c-281">W związku z tym sekcji zasobów można mieć struktury, takiej jak:</span><span class="sxs-lookup"><span data-stu-id="6a28c-281">Therefore, your resources section could have a structure like:</span></span>

```json
"resources": [
  {
      "name": "resourceA",
  },
  {
      "name": "resourceB",
      "resources": [
        {
            "name": "firstChildResourceB",
        },
        {   
            "name": "secondChildResourceB",
        }
      ]
  },
  {
      "name": "resourceC",
  }
]
```      

<span data-ttu-id="6a28c-282">Aby uzyskać więcej informacji na temat definiowania zasoby podrzędne, zobacz [Ustaw nazwę i typ zasobu podrzędnego w szablonie usługi Resource Manager](resource-manager-template-child-resource.md).</span><span class="sxs-lookup"><span data-stu-id="6a28c-282">For more information about defining child resources, see [Set name and type for child resource in Resource Manager template](resource-manager-template-child-resource.md).</span></span>

<span data-ttu-id="6a28c-283">**Warunku** element określa, czy zasób jest wdrażany.</span><span class="sxs-lookup"><span data-stu-id="6a28c-283">The **condition** element specifies whether the resource is deployed.</span></span> <span data-ttu-id="6a28c-284">Wartość dla tego elementu jest rozpoznawany jako PRAWDA lub FAŁSZ.</span><span class="sxs-lookup"><span data-stu-id="6a28c-284">The value for this element resolves to true or false.</span></span> <span data-ttu-id="6a28c-285">Na przykład aby określić, czy nowe konto magazynu jest wdrażany, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="6a28c-285">For example, to specify whether a new storage account is deployed, use:</span></span>

```json
{
    "condition": "[equals(parameters('newOrExisting'),'new')]",
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2017-06-01",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "[variables('storageAccountType')]"
    },
    "kind": "Storage",
    "properties": {}
}
```

<span data-ttu-id="6a28c-286">Na przykład za pomocą nowego lub istniejącego zasobu, zobacz [nowy lub istniejący szablon warunku](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span><span class="sxs-lookup"><span data-stu-id="6a28c-286">For an example of using a new or existing resource, see [New or existing condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span></span>

<span data-ttu-id="6a28c-287">Aby określić, czy maszyna wirtualna jest wdrażany za pomocą hasła lub klucza SSH, należy zdefiniować dwie wersje maszyny wirtualnej w szablonie i użyj **warunku** rozróżnianie użycia.</span><span class="sxs-lookup"><span data-stu-id="6a28c-287">To specify whether a virtual machine is deployed with a password or SSH key, define two versions of the virtual machine in your template and use **condition** to differentiate usage.</span></span> <span data-ttu-id="6a28c-288">Podaj parametr, który określa scenariusza wdrażania.</span><span class="sxs-lookup"><span data-stu-id="6a28c-288">Pass a parameter that specifies which scenario to deploy.</span></span>

```json
{
    "condition": "[equals(parameters('passwordOrSshKey'),'password')]",
    "apiVersion": "2016-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[concat(variables('vmName'),'password')]",
    "properties": {
        "osProfile": {
            "computerName": "[variables('vmName')]",
            "adminUsername": "[parameters('adminUsername')]",
            "adminPassword": "[parameters('adminPassword')]"
        },
        ...
    },
    ...
},
{
    "condition": "[equals(parameters('passwordOrSshKey'),'sshKey')]",
    "apiVersion": "2016-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[concat(variables('vmName'),'ssh')]",
    "properties": {
        "osProfile": {
            "linuxConfiguration": {
                "disablePasswordAuthentication": "true",
                "ssh": {
                    "publicKeys": [
                        {
                            "path": "[variables('sshKeyPath')]",
                            "keyData": "[parameters('adminSshKey')]"
                        }
                    ]
                }
            }
        },
        ...
    },
    ...
}
``` 

<span data-ttu-id="6a28c-289">Przykład wdrożenia maszyny wirtualnej za pomocą hasła lub klucza SSH, zobacz [nazwa użytkownika lub SSH szablonu warunku](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span><span class="sxs-lookup"><span data-stu-id="6a28c-289">For an example of using a password or SSH key to deploy virtual machine, see [Username or SSH condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span></span>

## <a name="outputs"></a><span data-ttu-id="6a28c-290">dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="6a28c-290">Outputs</span></span>
<span data-ttu-id="6a28c-291">W sekcji danych wyjściowych można określić wartości, które są zwracane z wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="6a28c-291">In the Outputs section, you specify values that are returned from deployment.</span></span> <span data-ttu-id="6a28c-292">Na przykład można zwrócić identyfikator URI do uzyskania dostępu do zasobu wdrożone.</span><span class="sxs-lookup"><span data-stu-id="6a28c-292">For example, you could return the URI to access a deployed resource.</span></span>

<span data-ttu-id="6a28c-293">W poniższym przykładzie przedstawiono struktura definicji danych wyjściowych:</span><span class="sxs-lookup"><span data-stu-id="6a28c-293">The following example shows the structure of an output definition:</span></span>

```json
"outputs": {
    "<outputName>" : {
        "type" : "<type-of-output-value>",
        "value": "<output-value-expression>"
    }
}
```

| <span data-ttu-id="6a28c-294">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="6a28c-294">Element name</span></span> | <span data-ttu-id="6a28c-295">Wymagane</span><span class="sxs-lookup"><span data-stu-id="6a28c-295">Required</span></span> | <span data-ttu-id="6a28c-296">Opis</span><span class="sxs-lookup"><span data-stu-id="6a28c-296">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="6a28c-297">outputName</span><span class="sxs-lookup"><span data-stu-id="6a28c-297">outputName</span></span> |<span data-ttu-id="6a28c-298">Tak</span><span class="sxs-lookup"><span data-stu-id="6a28c-298">Yes</span></span> |<span data-ttu-id="6a28c-299">Nazwa wartości danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="6a28c-299">Name of the output value.</span></span> <span data-ttu-id="6a28c-300">Musi być prawidłowym identyfikatorem języka JavaScript.</span><span class="sxs-lookup"><span data-stu-id="6a28c-300">Must be a valid JavaScript identifier.</span></span> |
| <span data-ttu-id="6a28c-301">type</span><span class="sxs-lookup"><span data-stu-id="6a28c-301">type</span></span> |<span data-ttu-id="6a28c-302">Tak</span><span class="sxs-lookup"><span data-stu-id="6a28c-302">Yes</span></span> |<span data-ttu-id="6a28c-303">Typ wartości danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="6a28c-303">Type of the output value.</span></span> <span data-ttu-id="6a28c-304">Dane wyjściowe wartości obsługuje te same typy tablic jako parametrów wejściowych szablonu.</span><span class="sxs-lookup"><span data-stu-id="6a28c-304">Output values support the same types as template input parameters.</span></span> |
| <span data-ttu-id="6a28c-305">wartość</span><span class="sxs-lookup"><span data-stu-id="6a28c-305">value</span></span> |<span data-ttu-id="6a28c-306">Tak</span><span class="sxs-lookup"><span data-stu-id="6a28c-306">Yes</span></span> |<span data-ttu-id="6a28c-307">Wyrażenia języka szablonu, który jest obliczany i zwracany, jako wartość wyjściowa.</span><span class="sxs-lookup"><span data-stu-id="6a28c-307">Template language expression that is evaluated and returned as output value.</span></span> |

<span data-ttu-id="6a28c-308">W poniższym przykładzie przedstawiono wartość, która jest zwracana w sekcji danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="6a28c-308">The following example shows a value that is returned in the Outputs section.</span></span>

```json
"outputs": {
    "siteUri" : {
        "type" : "string",
        "value": "[concat('http://',reference(resourceId('Microsoft.Web/sites', parameters('siteName'))).hostNames[0])]"
    }
}
```

<span data-ttu-id="6a28c-309">Aby uzyskać więcej informacji na temat pracy z danych wyjściowych, zobacz [udostępniania stanu w szablonach usługi Azure Resource Manager](best-practices-resource-manager-state.md).</span><span class="sxs-lookup"><span data-stu-id="6a28c-309">For more information about working with output, see [Sharing state in Azure Resource Manager templates](best-practices-resource-manager-state.md).</span></span>

## <a name="template-limits"></a><span data-ttu-id="6a28c-310">Limity szablonu</span><span class="sxs-lookup"><span data-stu-id="6a28c-310">Template limits</span></span>

<span data-ttu-id="6a28c-311">Limit rozmiaru szablon 1 MB, a każdy plik parametrów do 64 KB.</span><span class="sxs-lookup"><span data-stu-id="6a28c-311">Limit the size of your template to 1 MB, and each parameter file to 64 KB.</span></span> <span data-ttu-id="6a28c-312">Limit 1 MB jest stosowana do stanu końcowego szablonu zostanie rozwinięty definicje interakcyjnych zasobów i wartości zmiennych i parametrów.</span><span class="sxs-lookup"><span data-stu-id="6a28c-312">The 1-MB limit applies to the final state of the template after it has been expanded with iterative resource definitions, and values for variables and parameters.</span></span> 

<span data-ttu-id="6a28c-313">Możesz również są ograniczone do:</span><span class="sxs-lookup"><span data-stu-id="6a28c-313">You are also limited to:</span></span>

* <span data-ttu-id="6a28c-314">Parametry 256</span><span class="sxs-lookup"><span data-stu-id="6a28c-314">256 parameters</span></span>
* <span data-ttu-id="6a28c-315">zmienne 256</span><span class="sxs-lookup"><span data-stu-id="6a28c-315">256 variables</span></span>
* <span data-ttu-id="6a28c-316">800 zasoby (w tym liczba kopii)</span><span class="sxs-lookup"><span data-stu-id="6a28c-316">800 resources (including copy count)</span></span>
* <span data-ttu-id="6a28c-317">64 wartości danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="6a28c-317">64 output values</span></span>
* <span data-ttu-id="6a28c-318">24 576 znaków w wyrażeniu szablonu</span><span class="sxs-lookup"><span data-stu-id="6a28c-318">24,576 characters in a template expression</span></span>

<span data-ttu-id="6a28c-319">Niektóre limity szablonu może przekroczyć przy użyciu szablonu zagnieżdżonego.</span><span class="sxs-lookup"><span data-stu-id="6a28c-319">You can exceed some template limits by using a nested template.</span></span> <span data-ttu-id="6a28c-320">Aby uzyskać więcej informacji, zobacz [przy użyciu szablonów połączonych w przypadku wdrażania zasobów Azure](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="6a28c-320">For more information, see [Using linked templates when deploying Azure resources](resource-group-linked-templates.md).</span></span> <span data-ttu-id="6a28c-321">Aby zmniejszyć liczbę parametrów, zmiennych lub dane wyjściowe, można połączyć kilka wartości do obiektu.</span><span class="sxs-lookup"><span data-stu-id="6a28c-321">To reduce the number of parameters, variables, or outputs, you can combine several values into an object.</span></span> <span data-ttu-id="6a28c-322">Aby uzyskać więcej informacji, zobacz [obiektów jako parametry](resource-manager-objects-as-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="6a28c-322">For more information, see [Objects as parameters](resource-manager-objects-as-parameters.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6a28c-323">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6a28c-323">Next steps</span></span>
* <span data-ttu-id="6a28c-324">Aby wyświetlić pełną listę szablonów dla wielu różnych rozwiązań, zobacz [Szablony szybkiego startu platformy Azure](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="6a28c-324">To view complete templates for many different types of solutions, see the [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/).</span></span>
* <span data-ttu-id="6a28c-325">Aby uzyskać więcej informacji o funkcje, których można użyć z w ramach szablonu, zobacz [funkcje szablonów usługi Azure Resource Manager](resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="6a28c-325">For details about the functions you can use from within a template, see [Azure Resource Manager Template Functions](resource-group-template-functions.md).</span></span>
* <span data-ttu-id="6a28c-326">Aby połączyć wiele szablonów podczas wdrażania, zobacz [za pomocą szablonów połączonych z usługą Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="6a28c-326">To combine multiple templates during deployment, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="6a28c-327">Może być konieczne użycie zasobów, które istnieją w innej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="6a28c-327">You may need to use resources that exist within a different resource group.</span></span> <span data-ttu-id="6a28c-328">Ten scenariusz jest typowy podczas pracy z kontami magazynu lub sieci wirtualne, które są współdzielone przez wiele grup zasobów.</span><span class="sxs-lookup"><span data-stu-id="6a28c-328">This scenario is common when working with storage accounts or virtual networks that are shared across multiple resource groups.</span></span> <span data-ttu-id="6a28c-329">Aby uzyskać więcej informacji, zobacz [funkcja resourceId](resource-group-template-functions-resource.md#resourceid).</span><span class="sxs-lookup"><span data-stu-id="6a28c-329">For more information, see the [resourceId function](resource-group-template-functions-resource.md#resourceid).</span></span>
