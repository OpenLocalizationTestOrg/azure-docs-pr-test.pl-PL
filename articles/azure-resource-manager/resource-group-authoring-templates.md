---
title: "Menedżer zasobów aaaAzure struktury szablonu i składni | Dokumentacja firmy Microsoft"
description: "Opis hello struktury i właściwości szablonów usługi Azure Resource Manager za pomocą składni deklaratywnej JSON."
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
ms.openlocfilehash: b0709852f8777c91cc1704d6bca16257a017d515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="understand-hello-structure-and-syntax-of-azure-resource-manager-templates"></a><span data-ttu-id="f82f6-103">Struktura hello i składni szablonów usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f82f6-103">Understand hello structure and syntax of Azure Resource Manager templates</span></span>
<span data-ttu-id="f82f6-104">W tym temacie opisano strukturę hello szablonu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f82f6-104">This topic describes hello structure of an Azure Resource Manager template.</span></span> <span data-ttu-id="f82f6-105">Stanowi hello różnych części szablonu i hello właściwości, które są dostępne w tych sekcjach.</span><span class="sxs-lookup"><span data-stu-id="f82f6-105">It presents hello different sections of a template and hello properties that are available in those sections.</span></span> <span data-ttu-id="f82f6-106">Szablon Hello składa się z kodu JSON i wyrażeń, że możesz użyć wartości tooconstruct dla danego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="f82f6-106">hello template consists of JSON and expressions that you can use tooconstruct values for your deployment.</span></span> <span data-ttu-id="f82f6-107">Samouczek krok po kroku dotyczące tworzenia szablonu, zobacz [Tworzenie pierwszego szablonu usługi Azure Resource Manager](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="f82f6-107">For a step-by-step tutorial on creating a template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>

## <a name="template-format"></a><span data-ttu-id="f82f6-108">Format szablonu</span><span class="sxs-lookup"><span data-stu-id="f82f6-108">Template format</span></span>
<span data-ttu-id="f82f6-109">W swojej najprostszej struktury szablonu zawiera hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="f82f6-109">In its simplest structure, a template contains hello following elements:</span></span>

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

| <span data-ttu-id="f82f6-110">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="f82f6-110">Element name</span></span> | <span data-ttu-id="f82f6-111">Wymagane</span><span class="sxs-lookup"><span data-stu-id="f82f6-111">Required</span></span> | <span data-ttu-id="f82f6-112">Opis</span><span class="sxs-lookup"><span data-stu-id="f82f6-112">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="f82f6-113">$schema</span><span class="sxs-lookup"><span data-stu-id="f82f6-113">$schema</span></span> |<span data-ttu-id="f82f6-114">Tak</span><span class="sxs-lookup"><span data-stu-id="f82f6-114">Yes</span></span> |<span data-ttu-id="f82f6-115">Lokalizacja pliku hello schematu JSON, który zawiera opis wersji hello hello języka szablonu.</span><span class="sxs-lookup"><span data-stu-id="f82f6-115">Location of hello JSON schema file that describes hello version of hello template language.</span></span> <span data-ttu-id="f82f6-116">Użyj adresu URL hello pokazano hello poprzedzających przykład.</span><span class="sxs-lookup"><span data-stu-id="f82f6-116">Use hello URL shown in hello preceding example.</span></span> |
| <span data-ttu-id="f82f6-117">contentVersion</span><span class="sxs-lookup"><span data-stu-id="f82f6-117">contentVersion</span></span> |<span data-ttu-id="f82f6-118">Tak</span><span class="sxs-lookup"><span data-stu-id="f82f6-118">Yes</span></span> |<span data-ttu-id="f82f6-119">Wersja szablonu hello (na przykład 1.0.0.0).</span><span class="sxs-lookup"><span data-stu-id="f82f6-119">Version of hello template (such as 1.0.0.0).</span></span> <span data-ttu-id="f82f6-120">Musisz podać wartości dla tego elementu.</span><span class="sxs-lookup"><span data-stu-id="f82f6-120">You can provide any value for this element.</span></span> <span data-ttu-id="f82f6-121">W przypadku wdrażania zasobów przy użyciu szablonu hello, ta wartość może być używane toomake się, że ten szablon prawo hello jest używany.</span><span class="sxs-lookup"><span data-stu-id="f82f6-121">When deploying resources using hello template, this value can be used toomake sure that hello right template is being used.</span></span> |
| <span data-ttu-id="f82f6-122">parameters</span><span class="sxs-lookup"><span data-stu-id="f82f6-122">parameters</span></span> |<span data-ttu-id="f82f6-123">Nie</span><span class="sxs-lookup"><span data-stu-id="f82f6-123">No</span></span> |<span data-ttu-id="f82f6-124">Wartości, które są dostarczane, gdy wdrożenie jest wykonywane toocustomize zasobu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="f82f6-124">Values that are provided when deployment is executed toocustomize resource deployment.</span></span> |
| <span data-ttu-id="f82f6-125">zmienne</span><span class="sxs-lookup"><span data-stu-id="f82f6-125">variables</span></span> |<span data-ttu-id="f82f6-126">Nie</span><span class="sxs-lookup"><span data-stu-id="f82f6-126">No</span></span> |<span data-ttu-id="f82f6-127">Wartości, które są używane jako fragmenty JSON w wyrażeń języka szablonu hello szablonu toosimplify.</span><span class="sxs-lookup"><span data-stu-id="f82f6-127">Values that are used as JSON fragments in hello template toosimplify template language expressions.</span></span> |
| <span data-ttu-id="f82f6-128">Zasoby</span><span class="sxs-lookup"><span data-stu-id="f82f6-128">resources</span></span> |<span data-ttu-id="f82f6-129">Tak</span><span class="sxs-lookup"><span data-stu-id="f82f6-129">Yes</span></span> |<span data-ttu-id="f82f6-130">Typy zasobów, które są wdrożone lub zaktualizowane w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="f82f6-130">Resource types that are deployed or updated in a resource group.</span></span> |
| <span data-ttu-id="f82f6-131">dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="f82f6-131">outputs</span></span> |<span data-ttu-id="f82f6-132">Nie</span><span class="sxs-lookup"><span data-stu-id="f82f6-132">No</span></span> |<span data-ttu-id="f82f6-133">Wartości, które są zwracane po wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="f82f6-133">Values that are returned after deployment.</span></span> |

<span data-ttu-id="f82f6-134">Każdy element zawiera właściwości, które można ustawić.</span><span class="sxs-lookup"><span data-stu-id="f82f6-134">Each element contains properties you can set.</span></span> <span data-ttu-id="f82f6-135">Poniższy przykład Hello zawiera hello pełnej składni szablonu:</span><span class="sxs-lookup"><span data-stu-id="f82f6-135">hello following example contains hello full syntax for a template:</span></span>

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
                "description": "<description-of-hello parameter>" 
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

<span data-ttu-id="f82f6-136">Omówione hello części szablonu hello bardziej szczegółowo w dalszej części tego tematu.</span><span class="sxs-lookup"><span data-stu-id="f82f6-136">We examine hello sections of hello template in greater detail later in this topic.</span></span>

## <a name="expressions-and-functions"></a><span data-ttu-id="f82f6-137">Wyrażeń i funkcji</span><span class="sxs-lookup"><span data-stu-id="f82f6-137">Expressions and functions</span></span>
<span data-ttu-id="f82f6-138">Podstawowa składnia Hello szablonu hello jest JSON.</span><span class="sxs-lookup"><span data-stu-id="f82f6-138">hello basic syntax of hello template is JSON.</span></span> <span data-ttu-id="f82f6-139">Jednak wartości JSON hello dostępnych w szablonie hello rozszerzyć wyrażeń i funkcji.</span><span class="sxs-lookup"><span data-stu-id="f82f6-139">However, expressions and functions extend hello JSON values available within hello template.</span></span>  <span data-ttu-id="f82f6-140">Wyrażenia są zapisywane w literałach ciągu JSON, których pierwszy i ostatnie znaki to nawiasy hello: `[` i `]`odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="f82f6-140">Expressions are written within JSON string literals whose first and last characters are hello brackets: `[` and `]`, respectively.</span></span> <span data-ttu-id="f82f6-141">Hello wartość wyrażenia hello jest oceniane podczas wdrażania szablonu hello.</span><span class="sxs-lookup"><span data-stu-id="f82f6-141">hello value of hello expression is evaluated when hello template is deployed.</span></span> <span data-ttu-id="f82f6-142">Gdy zapisywane jako literału ciągu, hello wynikiem obliczenia wyrażenia hello może mieć innego typu JSON, takich jak tablicy lub liczba całkowita, w zależności od hello rzeczywistego wyrażenia.</span><span class="sxs-lookup"><span data-stu-id="f82f6-142">While written as a string literal, hello result of evaluating hello expression can be of a different JSON type, such as an array or integer, depending on hello actual expression.</span></span>  <span data-ttu-id="f82f6-143">toohave literałem rozpoczynać nawiasu `[`, ale nie została ona interpretowana jako wyrażenie, Dodaj ciąg hello nawiasu dodatkowe toostart z `[[`.</span><span class="sxs-lookup"><span data-stu-id="f82f6-143">toohave a literal string start with a bracket `[`, but not have it interpreted as an expression, add an extra bracket toostart hello string with `[[`.</span></span>

<span data-ttu-id="f82f6-144">Zwykle Użyj wyrażenia z operacjami tooperform funkcje związane z konfigurowaniem wdrażania hello.</span><span class="sxs-lookup"><span data-stu-id="f82f6-144">Typically, you use expressions with functions tooperform operations for configuring hello deployment.</span></span> <span data-ttu-id="f82f6-145">Po prostu, tak jak w języku JavaScript, wywołania funkcji są sformatowane jako `functionName(arg1,arg2,arg3)`.</span><span class="sxs-lookup"><span data-stu-id="f82f6-145">Just like in JavaScript, function calls are formatted as `functionName(arg1,arg2,arg3)`.</span></span> <span data-ttu-id="f82f6-146">Możesz odwoływać się do właściwości przy użyciu operatorów hello kropka i [Indeks].</span><span class="sxs-lookup"><span data-stu-id="f82f6-146">You reference properties by using hello dot and [index] operators.</span></span>

<span data-ttu-id="f82f6-147">Witaj poniższy przykład pokazuje, jak toouse kilka funkcji podczas tworzenia wartości:</span><span class="sxs-lookup"><span data-stu-id="f82f6-147">hello following example shows how toouse several functions when constructing values:</span></span>

```json
"variables": {
    "location": "[resourceGroup().location]",
    "usernameAndPassword": "[concat(parameters('username'), ':', parameters('password'))]",
    "authorizationHeader": "[concat('Basic ', base64(variables('usernameAndPassword')))]"
}
```

<span data-ttu-id="f82f6-148">Witaj pełną listę funkcji szablonu, zobacz [funkcje szablonu usługi Azure Resource Manager](resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="f82f6-148">For hello full list of template functions, see [Azure Resource Manager template functions](resource-group-template-functions.md).</span></span> 

## <a name="parameters"></a><span data-ttu-id="f82f6-149">Parametry</span><span class="sxs-lookup"><span data-stu-id="f82f6-149">Parameters</span></span>
<span data-ttu-id="f82f6-150">W sekcji parametrów hello hello szablonu należy określić wartości, które można wprowadzić w przypadku wdrażania hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="f82f6-150">In hello parameters section of hello template, you specify which values you can input when deploying hello resources.</span></span> <span data-ttu-id="f82f6-151">Wartości tych parametrów Włącz toocustomize hello wdrożenia, podając wartości, które są dostosowane określonym środowisku (na przykład deweloperów, testowego i produkcyjnego).</span><span class="sxs-lookup"><span data-stu-id="f82f6-151">These parameter values enable you toocustomize hello deployment by providing values that are tailored for a particular environment (such as dev, test, and production).</span></span> <span data-ttu-id="f82f6-152">Nie masz tooprovide parametry w szablonie, ale bez parametrów szablonu będzie zawsze wdrażać hello hello tyle samo zasobów o tej samej nazwy, lokalizacji i właściwości.</span><span class="sxs-lookup"><span data-stu-id="f82f6-152">You do not have tooprovide parameters in your template, but without parameters your template would always deploy hello same resources with hello same names, locations, and properties.</span></span>

<span data-ttu-id="f82f6-153">Definiuje parametry z następującej struktury hello:</span><span class="sxs-lookup"><span data-stu-id="f82f6-153">You define parameters with hello following structure:</span></span>

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
            "description": "<description-of-hello parameter>" 
        }
    }
}
```

| <span data-ttu-id="f82f6-154">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="f82f6-154">Element name</span></span> | <span data-ttu-id="f82f6-155">Wymagane</span><span class="sxs-lookup"><span data-stu-id="f82f6-155">Required</span></span> | <span data-ttu-id="f82f6-156">Opis</span><span class="sxs-lookup"><span data-stu-id="f82f6-156">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="f82f6-157">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="f82f6-157">parameterName</span></span> |<span data-ttu-id="f82f6-158">Tak</span><span class="sxs-lookup"><span data-stu-id="f82f6-158">Yes</span></span> |<span data-ttu-id="f82f6-159">Nazwa parametru hello.</span><span class="sxs-lookup"><span data-stu-id="f82f6-159">Name of hello parameter.</span></span> <span data-ttu-id="f82f6-160">Musi być prawidłowym identyfikatorem języka JavaScript.</span><span class="sxs-lookup"><span data-stu-id="f82f6-160">Must be a valid JavaScript identifier.</span></span> |
| <span data-ttu-id="f82f6-161">type</span><span class="sxs-lookup"><span data-stu-id="f82f6-161">type</span></span> |<span data-ttu-id="f82f6-162">Tak</span><span class="sxs-lookup"><span data-stu-id="f82f6-162">Yes</span></span> |<span data-ttu-id="f82f6-163">Typ wartości parametru hello.</span><span class="sxs-lookup"><span data-stu-id="f82f6-163">Type of hello parameter value.</span></span> <span data-ttu-id="f82f6-164">Lista hello dozwolonymi typami pod tą tabelą.</span><span class="sxs-lookup"><span data-stu-id="f82f6-164">See hello list of allowed types after this table.</span></span> |
| <span data-ttu-id="f82f6-165">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="f82f6-165">defaultValue</span></span> |<span data-ttu-id="f82f6-166">Nie</span><span class="sxs-lookup"><span data-stu-id="f82f6-166">No</span></span> |<span data-ttu-id="f82f6-167">Wartość domyślna parametru hello, jeśli wartość nie zostanie podana dla parametru hello.</span><span class="sxs-lookup"><span data-stu-id="f82f6-167">Default value for hello parameter, if no value is provided for hello parameter.</span></span> |
| <span data-ttu-id="f82f6-168">allowedValues</span><span class="sxs-lookup"><span data-stu-id="f82f6-168">allowedValues</span></span> |<span data-ttu-id="f82f6-169">Nie</span><span class="sxs-lookup"><span data-stu-id="f82f6-169">No</span></span> |<span data-ttu-id="f82f6-170">Tablica toomake parametru hello się upewnić, że wartość prawej strony hello jest dozwolonych wartości.</span><span class="sxs-lookup"><span data-stu-id="f82f6-170">Array of allowed values for hello parameter toomake sure that hello right value is provided.</span></span> |
| <span data-ttu-id="f82f6-171">Wartość MinValue</span><span class="sxs-lookup"><span data-stu-id="f82f6-171">minValue</span></span> |<span data-ttu-id="f82f6-172">Nie</span><span class="sxs-lookup"><span data-stu-id="f82f6-172">No</span></span> |<span data-ttu-id="f82f6-173">Witaj minimalną wartość parametrów typu int, ta wartość jest włącznie.</span><span class="sxs-lookup"><span data-stu-id="f82f6-173">hello minimum value for int type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="f82f6-174">MaxValue</span><span class="sxs-lookup"><span data-stu-id="f82f6-174">maxValue</span></span> |<span data-ttu-id="f82f6-175">Nie</span><span class="sxs-lookup"><span data-stu-id="f82f6-175">No</span></span> |<span data-ttu-id="f82f6-176">Witaj maksymalną wartość parametrów typu int, ta wartość jest włącznie.</span><span class="sxs-lookup"><span data-stu-id="f82f6-176">hello maximum value for int type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="f82f6-177">Element minLength</span><span class="sxs-lookup"><span data-stu-id="f82f6-177">minLength</span></span> |<span data-ttu-id="f82f6-178">Nie</span><span class="sxs-lookup"><span data-stu-id="f82f6-178">No</span></span> |<span data-ttu-id="f82f6-179">Witaj minimalną długość ciągu, secureString i parametrów typu tablicy, ta wartość jest włącznie.</span><span class="sxs-lookup"><span data-stu-id="f82f6-179">hello minimum length for string, secureString, and array type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="f82f6-180">Element maxLength</span><span class="sxs-lookup"><span data-stu-id="f82f6-180">maxLength</span></span> |<span data-ttu-id="f82f6-181">Nie</span><span class="sxs-lookup"><span data-stu-id="f82f6-181">No</span></span> |<span data-ttu-id="f82f6-182">Witaj maksymalną długość ciągu, secureString i parametrów typu tablicy, ta wartość jest włącznie.</span><span class="sxs-lookup"><span data-stu-id="f82f6-182">hello maximum length for string, secureString, and array type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="f82f6-183">description</span><span class="sxs-lookup"><span data-stu-id="f82f6-183">description</span></span> |<span data-ttu-id="f82f6-184">Nie</span><span class="sxs-lookup"><span data-stu-id="f82f6-184">No</span></span> |<span data-ttu-id="f82f6-185">Opis parametru hello, który jest wyświetlany toousers za pośrednictwem portalu hello.</span><span class="sxs-lookup"><span data-stu-id="f82f6-185">Description of hello parameter that is displayed toousers through hello portal.</span></span> |

<span data-ttu-id="f82f6-186">Witaj dozwolonymi typami i wartości to:</span><span class="sxs-lookup"><span data-stu-id="f82f6-186">hello allowed types and values are:</span></span>

* <span data-ttu-id="f82f6-187">**ciąg**</span><span class="sxs-lookup"><span data-stu-id="f82f6-187">**string**</span></span>
* <span data-ttu-id="f82f6-188">**secureString**</span><span class="sxs-lookup"><span data-stu-id="f82f6-188">**secureString**</span></span>
* <span data-ttu-id="f82f6-189">**int**</span><span class="sxs-lookup"><span data-stu-id="f82f6-189">**int**</span></span>
* <span data-ttu-id="f82f6-190">**wartość logiczna**</span><span class="sxs-lookup"><span data-stu-id="f82f6-190">**bool**</span></span>
* <span data-ttu-id="f82f6-191">**obiekt**</span><span class="sxs-lookup"><span data-stu-id="f82f6-191">**object**</span></span> 
* <span data-ttu-id="f82f6-192">**secureObject**</span><span class="sxs-lookup"><span data-stu-id="f82f6-192">**secureObject**</span></span>
* <span data-ttu-id="f82f6-193">**Tablica**</span><span class="sxs-lookup"><span data-stu-id="f82f6-193">**array**</span></span>

<span data-ttu-id="f82f6-194">toospecify parametr jako opcjonalną, podaj wartości (może być ciągiem pustym).</span><span class="sxs-lookup"><span data-stu-id="f82f6-194">toospecify a parameter as optional, provide a defaultValue (can be an empty string).</span></span> 

<span data-ttu-id="f82f6-195">Jeśli określono nazwę parametru w szablonie parametru hello polecenia toodeploy hello szablonu jest zgodny, jest potencjalnych niejednoznaczności wartości hello.</span><span class="sxs-lookup"><span data-stu-id="f82f6-195">If you specify a parameter name in your template that matches a parameter in hello command toodeploy hello template, there is potential ambiguity about hello values you provide.</span></span> <span data-ttu-id="f82f6-196">Menedżer zasobów usuwa to pomyłka, dodając przyrostek hello **FromTemplate** toohello parametru szablonu.</span><span class="sxs-lookup"><span data-stu-id="f82f6-196">Resource Manager resolves this confusion by adding hello postfix **FromTemplate** toohello template parameter.</span></span> <span data-ttu-id="f82f6-197">Na przykład, jeśli zawiera parametr o nazwie **ResourceGroupName** w szablonie, powoduje konflikt z hello **ResourceGroupName** parametru w hello [ Nowy AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f82f6-197">For example, if you include a parameter named **ResourceGroupName** in your template, it conflicts with hello **ResourceGroupName** parameter in hello [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet.</span></span> <span data-ttu-id="f82f6-198">Podczas wdrażania, są tooprovide zostanie wyświetlony monit o wartości **ResourceGroupNameFromTemplate**.</span><span class="sxs-lookup"><span data-stu-id="f82f6-198">During deployment, you are prompted tooprovide a value for **ResourceGroupNameFromTemplate**.</span></span> <span data-ttu-id="f82f6-199">Ogólnie rzecz biorąc należy unikać to pomyłka nie nadawanie nazw parametrów z hello takie same nazwy jako parametry używane dla operacji wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="f82f6-199">In general, you should avoid this confusion by not naming parameters with hello same name as parameters used for deployment operations.</span></span>

> [!NOTE]
> <span data-ttu-id="f82f6-200">Wszystkie hasła, klucze i innych informacji poufnych, należy użyć hello **secureString** typu.</span><span class="sxs-lookup"><span data-stu-id="f82f6-200">All passwords, keys, and other secrets should use hello **secureString** type.</span></span> <span data-ttu-id="f82f6-201">W przypadku przekazania danych poufnych w obiekcie JSON, użyj hello **secureObject** typu.</span><span class="sxs-lookup"><span data-stu-id="f82f6-201">If you pass sensitive data in a JSON object, use hello **secureObject** type.</span></span> <span data-ttu-id="f82f6-202">Nie można odczytać parametrów szablonu z typami secureString lub secureObject po wdrożeniu zasobów.</span><span class="sxs-lookup"><span data-stu-id="f82f6-202">Template parameters with secureString or secureObject types cannot be read after resource deployment.</span></span> 
> 
> <span data-ttu-id="f82f6-203">Na przykład hello następujący wpis w historii wdrożenia hello pokazuje hello wartość dla ciągu lub obiektu, ale nie dla secureString i secureObject.</span><span class="sxs-lookup"><span data-stu-id="f82f6-203">For example, hello following entry in hello deployment history shows hello value for a string and object but not for secureString and secureObject.</span></span>
>
> ![Pokaż wartości wdrożenia](./media/resource-group-authoring-templates/show-parameters.png)  
>

<span data-ttu-id="f82f6-205">powitania po przykładzie pokazano, jak toodefine parametry:</span><span class="sxs-lookup"><span data-stu-id="f82f6-205">hello following example shows how toodefine parameters:</span></span>

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

<span data-ttu-id="f82f6-206">Dla jak wartości parametrów hello tooinput, podczas wdrażania, zobacz [wdrażania aplikacji przy użyciu szablonu usługi Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="f82f6-206">For how tooinput hello parameter values during deployment, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span> 

## <a name="variables"></a><span data-ttu-id="f82f6-207">Zmienne</span><span class="sxs-lookup"><span data-stu-id="f82f6-207">Variables</span></span>
<span data-ttu-id="f82f6-208">W sekcji zmiennych hello utworzymy wartości, które mogą być używane w szablonie.</span><span class="sxs-lookup"><span data-stu-id="f82f6-208">In hello variables section, you construct values that can be used throughout your template.</span></span> <span data-ttu-id="f82f6-209">Nie trzeba toodefine zmiennych, ale one często uprościć szablonu zmniejszając złożonych wyrażeń.</span><span class="sxs-lookup"><span data-stu-id="f82f6-209">You do not need toodefine variables, but they often simplify your template by reducing complex expressions.</span></span>

<span data-ttu-id="f82f6-210">Można zdefiniować zmienne z następującej struktury hello:</span><span class="sxs-lookup"><span data-stu-id="f82f6-210">You define variables with hello following structure:</span></span>

```json
"variables": {
    "<variable-name>": "<variable-value>",
    "<variable-name>": { 
        <variable-complex-type-value> 
    }
}
```

<span data-ttu-id="f82f6-211">powitania po przykładzie pokazano, jak toodefine zmiennej, która jest tworzony z dwóch wartości parametrów:</span><span class="sxs-lookup"><span data-stu-id="f82f6-211">hello following example shows how toodefine a variable that is constructed from two parameter values:</span></span>

```json
"variables": {
    "connectionString": "[concat('Name=', parameters('username'), ';Password=', parameters('password'))]"
}
```

<span data-ttu-id="f82f6-212">Witaj kolejnym przykładzie pokazano zmiennej, która jest typem złożonym JSON i zmienne, które są tworzone na podstawie innych zmiennych:</span><span class="sxs-lookup"><span data-stu-id="f82f6-212">hello next example shows a variable that is a complex JSON type, and variables that are constructed from other variables:</span></span>

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

## <a name="resources"></a><span data-ttu-id="f82f6-213">Zasoby</span><span class="sxs-lookup"><span data-stu-id="f82f6-213">Resources</span></span>
<span data-ttu-id="f82f6-214">W sekcji zasobów hello można zdefiniować hello zasobów, które są wdrożone lub aktualizowane.</span><span class="sxs-lookup"><span data-stu-id="f82f6-214">In hello resources section, you define hello resources that are deployed or updated.</span></span> <span data-ttu-id="f82f6-215">W tej sekcji można uzyskać skomplikowane, ponieważ należy poznać hello typów wdrażania tooprovide hello właściwych wartości.</span><span class="sxs-lookup"><span data-stu-id="f82f6-215">This section can get complicated because you must understand hello types you are deploying tooprovide hello right values.</span></span> <span data-ttu-id="f82f6-216">Witaj określonych zasobów wartości (apiVersion, typ i właściwości) należy tooset, zobacz [zdefiniować zasoby w szablonach usługi Azure Resource Manager](/azure/templates/).</span><span class="sxs-lookup"><span data-stu-id="f82f6-216">For hello resource-specific values (apiVersion, type, and properties) that you need tooset, see [Define resources in Azure Resource Manager templates](/azure/templates/).</span></span> 

<span data-ttu-id="f82f6-217">Definiuje się zasoby z następującej struktury hello:</span><span class="sxs-lookup"><span data-stu-id="f82f6-217">You define resources with hello following structure:</span></span>

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

| <span data-ttu-id="f82f6-218">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="f82f6-218">Element name</span></span> | <span data-ttu-id="f82f6-219">Wymagane</span><span class="sxs-lookup"><span data-stu-id="f82f6-219">Required</span></span> | <span data-ttu-id="f82f6-220">Opis</span><span class="sxs-lookup"><span data-stu-id="f82f6-220">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="f82f6-221">Warunek</span><span class="sxs-lookup"><span data-stu-id="f82f6-221">condition</span></span> | <span data-ttu-id="f82f6-222">Nie</span><span class="sxs-lookup"><span data-stu-id="f82f6-222">No</span></span> | <span data-ttu-id="f82f6-223">Wartość logiczna wskazująca, czy zasób hello jest wdrażany.</span><span class="sxs-lookup"><span data-stu-id="f82f6-223">Boolean value that indicates whether hello resource is deployed.</span></span> |
| <span data-ttu-id="f82f6-224">apiVersion</span><span class="sxs-lookup"><span data-stu-id="f82f6-224">apiVersion</span></span> |<span data-ttu-id="f82f6-225">Tak</span><span class="sxs-lookup"><span data-stu-id="f82f6-225">Yes</span></span> |<span data-ttu-id="f82f6-226">Wersja hello toouse interfejsu API REST do tworzenia hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="f82f6-226">Version of hello REST API toouse for creating hello resource.</span></span> |
| <span data-ttu-id="f82f6-227">type</span><span class="sxs-lookup"><span data-stu-id="f82f6-227">type</span></span> |<span data-ttu-id="f82f6-228">Tak</span><span class="sxs-lookup"><span data-stu-id="f82f6-228">Yes</span></span> |<span data-ttu-id="f82f6-229">Typ zasobu hello.</span><span class="sxs-lookup"><span data-stu-id="f82f6-229">Type of hello resource.</span></span> <span data-ttu-id="f82f6-230">Ta wartość jest kombinacją hello przestrzeń nazw dostawcy zasobów hello i typu zasobu hello (takich jak **magazyn.Microsoft/kontamagazynu**).</span><span class="sxs-lookup"><span data-stu-id="f82f6-230">This value is a combination of hello namespace of hello resource provider and hello resource type (such as **Microsoft.Storage/storageAccounts**).</span></span> |
| <span data-ttu-id="f82f6-231">name</span><span class="sxs-lookup"><span data-stu-id="f82f6-231">name</span></span> |<span data-ttu-id="f82f6-232">Tak</span><span class="sxs-lookup"><span data-stu-id="f82f6-232">Yes</span></span> |<span data-ttu-id="f82f6-233">Nazwa zasobu hello.</span><span class="sxs-lookup"><span data-stu-id="f82f6-233">Name of hello resource.</span></span> <span data-ttu-id="f82f6-234">Witaj musi spełniać zdefiniowane w RFC3986 ograniczenia składnika identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="f82f6-234">hello name must follow URI component restrictions defined in RFC3986.</span></span> <span data-ttu-id="f82f6-235">Ponadto usług platformy Azure, które udostępniają hello zasobu Nazwa toooutside strony sprawdzania poprawności, nie jest toospoof próba toomake nazwa hello tożsamość.</span><span class="sxs-lookup"><span data-stu-id="f82f6-235">In addition, Azure services that expose hello resource name toooutside parties validate hello name toomake sure it is not an attempt toospoof another identity.</span></span> |
| <span data-ttu-id="f82f6-236">location</span><span class="sxs-lookup"><span data-stu-id="f82f6-236">location</span></span> |<span data-ttu-id="f82f6-237">Zmienia się</span><span class="sxs-lookup"><span data-stu-id="f82f6-237">Varies</span></span> |<span data-ttu-id="f82f6-238">Obsługiwane lokalizacje geograficzne z hello podać zasobów.</span><span class="sxs-lookup"><span data-stu-id="f82f6-238">Supported geo-locations of hello provided resource.</span></span> <span data-ttu-id="f82f6-239">Można wybrać dowolny z dostępnych lokalizacji hello, ale zazwyczaj ułatwia wykrywanie toopick jest Zamknij tooyour użytkowników.</span><span class="sxs-lookup"><span data-stu-id="f82f6-239">You can select any of hello available locations, but typically it makes sense toopick one that is close tooyour users.</span></span> <span data-ttu-id="f82f6-240">Zazwyczaj również dobrym rozwiązaniem jest tooplace zasobów, współpracujące ze sobą w hello sam region.</span><span class="sxs-lookup"><span data-stu-id="f82f6-240">Usually, it also makes sense tooplace resources that interact with each other in hello same region.</span></span> <span data-ttu-id="f82f6-241">Większość typów zasobów wymaga lokalizacji, ale nie wymagają lokalizację niektórych typów (takich jak przypisanie roli).</span><span class="sxs-lookup"><span data-stu-id="f82f6-241">Most resource types require a location, but some types (such as a role assignment) do not require a location.</span></span> <span data-ttu-id="f82f6-242">Zobacz [Ustaw lokalizację zasobów w szablonach usługi Azure Resource Manager](resource-manager-template-location.md).</span><span class="sxs-lookup"><span data-stu-id="f82f6-242">See [Set resource location in Azure Resource Manager templates](resource-manager-template-location.md).</span></span> |
| <span data-ttu-id="f82f6-243">tags</span><span class="sxs-lookup"><span data-stu-id="f82f6-243">tags</span></span> |<span data-ttu-id="f82f6-244">Nie</span><span class="sxs-lookup"><span data-stu-id="f82f6-244">No</span></span> |<span data-ttu-id="f82f6-245">Tagi, które są skojarzone z hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="f82f6-245">Tags that are associated with hello resource.</span></span> <span data-ttu-id="f82f6-246">Zobacz [tagów zasobów w szablonach usługi Azure Resource Manager](resource-manager-template-tags.md).</span><span class="sxs-lookup"><span data-stu-id="f82f6-246">See [Tag resources in Azure Resource Manager templates](resource-manager-template-tags.md).</span></span> |
| <span data-ttu-id="f82f6-247">Komentarze</span><span class="sxs-lookup"><span data-stu-id="f82f6-247">comments</span></span> |<span data-ttu-id="f82f6-248">Nie</span><span class="sxs-lookup"><span data-stu-id="f82f6-248">No</span></span> |<span data-ttu-id="f82f6-249">Notatki za dokumentację hello zasobów w szablonie</span><span class="sxs-lookup"><span data-stu-id="f82f6-249">Your notes for documenting hello resources in your template</span></span> |
| <span data-ttu-id="f82f6-250">Kopiuj</span><span class="sxs-lookup"><span data-stu-id="f82f6-250">copy</span></span> |<span data-ttu-id="f82f6-251">Nie</span><span class="sxs-lookup"><span data-stu-id="f82f6-251">No</span></span> |<span data-ttu-id="f82f6-252">W razie potrzeby więcej niż jedno wystąpienie hello liczba toocreate zasobów.</span><span class="sxs-lookup"><span data-stu-id="f82f6-252">If more than one instance is needed, hello number of resources toocreate.</span></span> <span data-ttu-id="f82f6-253">tryb domyślny Hello jest równoległe.</span><span class="sxs-lookup"><span data-stu-id="f82f6-253">hello default mode is parallel.</span></span> <span data-ttu-id="f82f6-254">Określ tryb serial, gdy nie ma wszystkich lub hello toodeploy zasobów na powitania tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="f82f6-254">Specify serial mode when you do not want all or hello resources toodeploy at hello same time.</span></span> <span data-ttu-id="f82f6-255">Aby uzyskać więcej informacji, zobacz [utworzyć wiele wystąpień zasobów usługi Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="f82f6-255">For more information, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span> |
| <span data-ttu-id="f82f6-256">dependsOn</span><span class="sxs-lookup"><span data-stu-id="f82f6-256">dependsOn</span></span> |<span data-ttu-id="f82f6-257">Nie</span><span class="sxs-lookup"><span data-stu-id="f82f6-257">No</span></span> |<span data-ttu-id="f82f6-258">Zasoby, które należy wdrożyć przed wdrożeniem tego zasobu.</span><span class="sxs-lookup"><span data-stu-id="f82f6-258">Resources that must be deployed before this resource is deployed.</span></span> <span data-ttu-id="f82f6-259">Menedżer zasobów ocenia hello zależności między zasobami i wdraża je w odpowiedniej kolejności hello.</span><span class="sxs-lookup"><span data-stu-id="f82f6-259">Resource Manager evaluates hello dependencies between resources and deploys them in hello correct order.</span></span> <span data-ttu-id="f82f6-260">Zasoby nie są zależne od siebie, są wdrożone równolegle.</span><span class="sxs-lookup"><span data-stu-id="f82f6-260">When resources are not dependent on each other, they are deployed in parallel.</span></span> <span data-ttu-id="f82f6-261">Hello wartość może być rozdzielaną przecinkami listą zasobu nazwy lub unikatowych identyfikatorów zasobów.</span><span class="sxs-lookup"><span data-stu-id="f82f6-261">hello value can be a comma-separated list of a resource names or resource unique identifiers.</span></span> <span data-ttu-id="f82f6-262">Tylko listy zasobów, które są wdrażane w tym szablonie.</span><span class="sxs-lookup"><span data-stu-id="f82f6-262">Only list resources that are deployed in this template.</span></span> <span data-ttu-id="f82f6-263">Zasoby, które nie są zdefiniowane w tym szablonie musi już istnieć.</span><span class="sxs-lookup"><span data-stu-id="f82f6-263">Resources that are not defined in this template must already exist.</span></span> <span data-ttu-id="f82f6-264">Unikaj Dodawanie zależności niepotrzebne, jak mogą spowalniać wdrożenia i utworzyć zależności cykliczne.</span><span class="sxs-lookup"><span data-stu-id="f82f6-264">Avoid adding unnecessary dependencies as they can slow your deployment and create circular dependencies.</span></span> <span data-ttu-id="f82f6-265">Aby uzyskać wskazówki dotyczące zależności ustawienia, zobacz [Definiowanie zależności w szablonach usługi Azure Resource Manager](resource-group-define-dependencies.md).</span><span class="sxs-lookup"><span data-stu-id="f82f6-265">For guidance on setting dependencies, see [Defining dependencies in Azure Resource Manager templates](resource-group-define-dependencies.md).</span></span> |
| <span data-ttu-id="f82f6-266">properties</span><span class="sxs-lookup"><span data-stu-id="f82f6-266">properties</span></span> |<span data-ttu-id="f82f6-267">Nie</span><span class="sxs-lookup"><span data-stu-id="f82f6-267">No</span></span> |<span data-ttu-id="f82f6-268">Ustawienia konfiguracji określonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="f82f6-268">Resource-specific configuration settings.</span></span> <span data-ttu-id="f82f6-269">Hello wartości właściwości hello są takie same hello jako wartości hello, podane w treści żądania hello hello interfejsu API REST operacji (metody PUT) toocreate hello zasobu.</span><span class="sxs-lookup"><span data-stu-id="f82f6-269">hello values for hello properties are hello same as hello values you provide in hello request body for hello REST API operation (PUT method) toocreate hello resource.</span></span> <span data-ttu-id="f82f6-270">Można również określić toocreate tablicy kopiowania wielu wystąpień właściwości.</span><span class="sxs-lookup"><span data-stu-id="f82f6-270">You can also specify a copy array toocreate multiple instances of a property.</span></span> <span data-ttu-id="f82f6-271">Aby uzyskać więcej informacji, zobacz [utworzyć wiele wystąpień zasobów usługi Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="f82f6-271">For more information, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span> |
| <span data-ttu-id="f82f6-272">Zasoby</span><span class="sxs-lookup"><span data-stu-id="f82f6-272">resources</span></span> |<span data-ttu-id="f82f6-273">Nie</span><span class="sxs-lookup"><span data-stu-id="f82f6-273">No</span></span> |<span data-ttu-id="f82f6-274">Zasoby podrzędne, które są zależne od zasobów hello definiowanego.</span><span class="sxs-lookup"><span data-stu-id="f82f6-274">Child resources that depend on hello resource being defined.</span></span> <span data-ttu-id="f82f6-275">Podaj tylko typy zasobów, które są dozwolone w ramach schematu hello hello zasobu nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="f82f6-275">Only provide resource types that are permitted by hello schema of hello parent resource.</span></span> <span data-ttu-id="f82f6-276">Witaj pełny typ zasobu podrzędnego hello zawiera typ zasobu nadrzędnego hello, takich jak **Microsoft.Web/sites/extensions**.</span><span class="sxs-lookup"><span data-stu-id="f82f6-276">hello fully qualified type of hello child resource includes hello parent resource type, such as **Microsoft.Web/sites/extensions**.</span></span> <span data-ttu-id="f82f6-277">Zależność od zasobu nadrzędnego hello jest niejawnego.</span><span class="sxs-lookup"><span data-stu-id="f82f6-277">Dependency on hello parent resource is not implied.</span></span> <span data-ttu-id="f82f6-278">Jawnie zdefiniuj tej zależności.</span><span class="sxs-lookup"><span data-stu-id="f82f6-278">You must explicitly define that dependency.</span></span> |

<span data-ttu-id="f82f6-279">Witaj sekcja zasobów zawiera tablicę hello toodeploy zasobów.</span><span class="sxs-lookup"><span data-stu-id="f82f6-279">hello resources section contains an array of hello resources toodeploy.</span></span> <span data-ttu-id="f82f6-280">W ramach każdego zasobu można również zdefiniować tablicę zasoby podrzędne.</span><span class="sxs-lookup"><span data-stu-id="f82f6-280">Within each resource, you can also define an array of child resources.</span></span> <span data-ttu-id="f82f6-281">W związku z tym sekcji zasobów można mieć struktury, takiej jak:</span><span class="sxs-lookup"><span data-stu-id="f82f6-281">Therefore, your resources section could have a structure like:</span></span>

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

<span data-ttu-id="f82f6-282">Aby uzyskać więcej informacji na temat definiowania zasoby podrzędne, zobacz [Ustaw nazwę i typ zasobu podrzędnego w szablonie usługi Resource Manager](resource-manager-template-child-resource.md).</span><span class="sxs-lookup"><span data-stu-id="f82f6-282">For more information about defining child resources, see [Set name and type for child resource in Resource Manager template](resource-manager-template-child-resource.md).</span></span>

<span data-ttu-id="f82f6-283">Witaj **warunku** element określa, czy zasób hello jest wdrażany.</span><span class="sxs-lookup"><span data-stu-id="f82f6-283">hello **condition** element specifies whether hello resource is deployed.</span></span> <span data-ttu-id="f82f6-284">Witaj wartość dla tego elementu rozpoznaje tootrue, lub FAŁSZ.</span><span class="sxs-lookup"><span data-stu-id="f82f6-284">hello value for this element resolves tootrue or false.</span></span> <span data-ttu-id="f82f6-285">Na przykład toospecify czy nowe konto magazynu jest wdrażana, użyj:</span><span class="sxs-lookup"><span data-stu-id="f82f6-285">For example, toospecify whether a new storage account is deployed, use:</span></span>

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

<span data-ttu-id="f82f6-286">Na przykład za pomocą nowego lub istniejącego zasobu, zobacz [nowy lub istniejący szablon warunku](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span><span class="sxs-lookup"><span data-stu-id="f82f6-286">For an example of using a new or existing resource, see [New or existing condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span></span>

<span data-ttu-id="f82f6-287">toospecify czy wdrożono maszynę wirtualną za pomocą hasła lub klucza SSH, zdefiniuj dwie wersje hello maszyny wirtualnej w szablonie i użyj **warunku** toodifferentiate użycia.</span><span class="sxs-lookup"><span data-stu-id="f82f6-287">toospecify whether a virtual machine is deployed with a password or SSH key, define two versions of hello virtual machine in your template and use **condition** toodifferentiate usage.</span></span> <span data-ttu-id="f82f6-288">Podaj parametr, który określa, które toodeploy scenariusza.</span><span class="sxs-lookup"><span data-stu-id="f82f6-288">Pass a parameter that specifies which scenario toodeploy.</span></span>

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

<span data-ttu-id="f82f6-289">Na przykład przy użyciu hasła lub maszyny wirtualnej toodeploy klucza SSH, zobacz [nazwa użytkownika lub SSH szablonu warunku](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span><span class="sxs-lookup"><span data-stu-id="f82f6-289">For an example of using a password or SSH key toodeploy virtual machine, see [Username or SSH condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span></span>

## <a name="outputs"></a><span data-ttu-id="f82f6-290">dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="f82f6-290">Outputs</span></span>
<span data-ttu-id="f82f6-291">W sekcji danych wyjściowych hello należy określić wartości, które są zwracane z wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="f82f6-291">In hello Outputs section, you specify values that are returned from deployment.</span></span> <span data-ttu-id="f82f6-292">Na przykład można zwrócić hello URI tooaccess wdrożonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="f82f6-292">For example, you could return hello URI tooaccess a deployed resource.</span></span>

<span data-ttu-id="f82f6-293">Witaj poniższy przykład przedstawia hello struktura definicji danych wyjściowych:</span><span class="sxs-lookup"><span data-stu-id="f82f6-293">hello following example shows hello structure of an output definition:</span></span>

```json
"outputs": {
    "<outputName>" : {
        "type" : "<type-of-output-value>",
        "value": "<output-value-expression>"
    }
}
```

| <span data-ttu-id="f82f6-294">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="f82f6-294">Element name</span></span> | <span data-ttu-id="f82f6-295">Wymagane</span><span class="sxs-lookup"><span data-stu-id="f82f6-295">Required</span></span> | <span data-ttu-id="f82f6-296">Opis</span><span class="sxs-lookup"><span data-stu-id="f82f6-296">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="f82f6-297">outputName</span><span class="sxs-lookup"><span data-stu-id="f82f6-297">outputName</span></span> |<span data-ttu-id="f82f6-298">Tak</span><span class="sxs-lookup"><span data-stu-id="f82f6-298">Yes</span></span> |<span data-ttu-id="f82f6-299">Nazwa wartości wyjściowych hello.</span><span class="sxs-lookup"><span data-stu-id="f82f6-299">Name of hello output value.</span></span> <span data-ttu-id="f82f6-300">Musi być prawidłowym identyfikatorem języka JavaScript.</span><span class="sxs-lookup"><span data-stu-id="f82f6-300">Must be a valid JavaScript identifier.</span></span> |
| <span data-ttu-id="f82f6-301">type</span><span class="sxs-lookup"><span data-stu-id="f82f6-301">type</span></span> |<span data-ttu-id="f82f6-302">Tak</span><span class="sxs-lookup"><span data-stu-id="f82f6-302">Yes</span></span> |<span data-ttu-id="f82f6-303">Typ wartości wyjściowych hello.</span><span class="sxs-lookup"><span data-stu-id="f82f6-303">Type of hello output value.</span></span> <span data-ttu-id="f82f6-304">Dane wyjściowe wartości obsługuje hello takie same typy tablic jako parametrów wejściowych szablonu.</span><span class="sxs-lookup"><span data-stu-id="f82f6-304">Output values support hello same types as template input parameters.</span></span> |
| <span data-ttu-id="f82f6-305">wartość</span><span class="sxs-lookup"><span data-stu-id="f82f6-305">value</span></span> |<span data-ttu-id="f82f6-306">Tak</span><span class="sxs-lookup"><span data-stu-id="f82f6-306">Yes</span></span> |<span data-ttu-id="f82f6-307">Wyrażenia języka szablonu, który jest obliczany i zwracany, jako wartość wyjściowa.</span><span class="sxs-lookup"><span data-stu-id="f82f6-307">Template language expression that is evaluated and returned as output value.</span></span> |

<span data-ttu-id="f82f6-308">Witaj poniższy przykład przedstawia wartość, która jest zwracana w sekcji danych wyjściowych hello.</span><span class="sxs-lookup"><span data-stu-id="f82f6-308">hello following example shows a value that is returned in hello Outputs section.</span></span>

```json
"outputs": {
    "siteUri" : {
        "type" : "string",
        "value": "[concat('http://',reference(resourceId('Microsoft.Web/sites', parameters('siteName'))).hostNames[0])]"
    }
}
```

<span data-ttu-id="f82f6-309">Aby uzyskać więcej informacji na temat pracy z danych wyjściowych, zobacz [udostępniania stanu w szablonach usługi Azure Resource Manager](best-practices-resource-manager-state.md).</span><span class="sxs-lookup"><span data-stu-id="f82f6-309">For more information about working with output, see [Sharing state in Azure Resource Manager templates](best-practices-resource-manager-state.md).</span></span>

## <a name="template-limits"></a><span data-ttu-id="f82f6-310">Limity szablonu</span><span class="sxs-lookup"><span data-stu-id="f82f6-310">Template limits</span></span>

<span data-ttu-id="f82f6-311">Limit rozmiaru hello too1 Twojego szablonu MB, a każdy parametr plików too64 KB.</span><span class="sxs-lookup"><span data-stu-id="f82f6-311">Limit hello size of your template too1 MB, and each parameter file too64 KB.</span></span> <span data-ttu-id="f82f6-312">limit 1 MB Hello jest stosowana toohello stan końcowy hello szablonu zostanie rozwinięty definicje interakcyjnych zasobów i wartości zmiennych i parametrów.</span><span class="sxs-lookup"><span data-stu-id="f82f6-312">hello 1-MB limit applies toohello final state of hello template after it has been expanded with iterative resource definitions, and values for variables and parameters.</span></span> 

<span data-ttu-id="f82f6-313">Możesz również są ograniczone do:</span><span class="sxs-lookup"><span data-stu-id="f82f6-313">You are also limited to:</span></span>

* <span data-ttu-id="f82f6-314">Parametry 256</span><span class="sxs-lookup"><span data-stu-id="f82f6-314">256 parameters</span></span>
* <span data-ttu-id="f82f6-315">zmienne 256</span><span class="sxs-lookup"><span data-stu-id="f82f6-315">256 variables</span></span>
* <span data-ttu-id="f82f6-316">800 zasoby (w tym liczba kopii)</span><span class="sxs-lookup"><span data-stu-id="f82f6-316">800 resources (including copy count)</span></span>
* <span data-ttu-id="f82f6-317">64 wartości danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="f82f6-317">64 output values</span></span>
* <span data-ttu-id="f82f6-318">24 576 znaków w wyrażeniu szablonu</span><span class="sxs-lookup"><span data-stu-id="f82f6-318">24,576 characters in a template expression</span></span>

<span data-ttu-id="f82f6-319">Niektóre limity szablonu może przekroczyć przy użyciu szablonu zagnieżdżonego.</span><span class="sxs-lookup"><span data-stu-id="f82f6-319">You can exceed some template limits by using a nested template.</span></span> <span data-ttu-id="f82f6-320">Aby uzyskać więcej informacji, zobacz [przy użyciu szablonów połączonych w przypadku wdrażania zasobów Azure](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="f82f6-320">For more information, see [Using linked templates when deploying Azure resources](resource-group-linked-templates.md).</span></span> <span data-ttu-id="f82f6-321">numer hello tooreduce parametrów, zmiennych lub dane wyjściowe, można połączyć kilka wartości do obiektu.</span><span class="sxs-lookup"><span data-stu-id="f82f6-321">tooreduce hello number of parameters, variables, or outputs, you can combine several values into an object.</span></span> <span data-ttu-id="f82f6-322">Aby uzyskać więcej informacji, zobacz [obiektów jako parametry](resource-manager-objects-as-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="f82f6-322">For more information, see [Objects as parameters](resource-manager-objects-as-parameters.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f82f6-323">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f82f6-323">Next steps</span></span>
* <span data-ttu-id="f82f6-324">Szablony pełną tooview do różnych rozwiązań, zobacz hello [szablonów Szybki Start Azure](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="f82f6-324">tooview complete templates for many different types of solutions, see hello [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/).</span></span>
* <span data-ttu-id="f82f6-325">Szczegółowe informacje na temat korzystania z szablonu jako funkcje hello, zobacz [funkcje szablonów usługi Azure Resource Manager](resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="f82f6-325">For details about hello functions you can use from within a template, see [Azure Resource Manager Template Functions](resource-group-template-functions.md).</span></span>
* <span data-ttu-id="f82f6-326">toocombine wielu szablonów podczas wdrażania, zobacz [za pomocą szablonów połączonych z usługą Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="f82f6-326">toocombine multiple templates during deployment, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="f82f6-327">Może być konieczne toouse zasoby, które istnieją w innej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="f82f6-327">You may need toouse resources that exist within a different resource group.</span></span> <span data-ttu-id="f82f6-328">Ten scenariusz jest typowy podczas pracy z kontami magazynu lub sieci wirtualne, które są współdzielone przez wiele grup zasobów.</span><span class="sxs-lookup"><span data-stu-id="f82f6-328">This scenario is common when working with storage accounts or virtual networks that are shared across multiple resource groups.</span></span> <span data-ttu-id="f82f6-329">Aby uzyskać więcej informacji, zobacz hello [funkcja resourceId](resource-group-template-functions-resource.md#resourceid).</span><span class="sxs-lookup"><span data-stu-id="f82f6-329">For more information, see hello [resourceId function](resource-group-template-functions-resource.md#resourceid).</span></span>
