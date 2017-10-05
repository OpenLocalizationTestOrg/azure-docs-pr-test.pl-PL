---
title: "Funkcje szablonów Menedżera zasobów Azure - zasobów | Dokumentacja firmy Microsoft"
description: "Zawiera opis funkcji można użyć w szablonie usługi Azure Resource Manager można pobrać wartości o zasobach."
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
ms.date: 08/09/2017
ms.author: tomfitz
ms.openlocfilehash: 494ade55f21c19d9c68d5cc52756528401d9bb77
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="resource-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="7adec-103">Funkcje zasobów dla szablonów usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7adec-103">Resource functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="7adec-104">Usługa Resource Manager zapewnia następujące funkcje do pobierania wartości zasobu:</span><span class="sxs-lookup"><span data-stu-id="7adec-104">Resource Manager provides the following functions for getting resource values:</span></span>

* [<span data-ttu-id="7adec-105">listKeys i listy {Value}</span><span class="sxs-lookup"><span data-stu-id="7adec-105">listKeys and list{Value}</span></span>](#listkeys)
* [<span data-ttu-id="7adec-106">dostawców</span><span class="sxs-lookup"><span data-stu-id="7adec-106">providers</span></span>](#providers)
* [<span data-ttu-id="7adec-107">Odwołanie</span><span class="sxs-lookup"><span data-stu-id="7adec-107">reference</span></span>](#reference)
* [<span data-ttu-id="7adec-108">Grupa zasobów</span><span class="sxs-lookup"><span data-stu-id="7adec-108">resourceGroup</span></span>](#resourcegroup)
* [<span data-ttu-id="7adec-109">Identyfikator zasobu</span><span class="sxs-lookup"><span data-stu-id="7adec-109">resourceId</span></span>](#resourceid)
* [<span data-ttu-id="7adec-110">Subskrypcja</span><span class="sxs-lookup"><span data-stu-id="7adec-110">subscription</span></span>](#subscription)

<span data-ttu-id="7adec-111">Aby uzyskać wartości z parametrów, zmiennych lub bieżącego wdrożenia, zobacz [wdrożenia wartość funkcji](resource-group-template-functions-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="7adec-111">To get values from parameters, variables, or the current deployment, see [Deployment value functions](resource-group-template-functions-deployment.md).</span></span>

<a id="listkeys" />
<a id="list" />

## <a name="listkeys-and-listvalue"></a><span data-ttu-id="7adec-112">listKeys i listy {Value}</span><span class="sxs-lookup"><span data-stu-id="7adec-112">listKeys and list{Value}</span></span>
`listKeys(resourceName or resourceIdentifier, apiVersion)`

`list{Value}(resourceName or resourceIdentifier, apiVersion)`

<span data-ttu-id="7adec-113">Zwraca wartości dla dowolnego typu zasobu, który obsługuje operacja listy.</span><span class="sxs-lookup"><span data-stu-id="7adec-113">Returns the values for any resource type that supports the list operation.</span></span> <span data-ttu-id="7adec-114">Najbardziej typowe obciążenie jest `listKeys`.</span><span class="sxs-lookup"><span data-stu-id="7adec-114">The most common usage is `listKeys`.</span></span> 

### <a name="parameters"></a><span data-ttu-id="7adec-115">Parametry</span><span class="sxs-lookup"><span data-stu-id="7adec-115">Parameters</span></span>

| <span data-ttu-id="7adec-116">Parametr</span><span class="sxs-lookup"><span data-stu-id="7adec-116">Parameter</span></span> | <span data-ttu-id="7adec-117">Wymagane</span><span class="sxs-lookup"><span data-stu-id="7adec-117">Required</span></span> | <span data-ttu-id="7adec-118">Typ</span><span class="sxs-lookup"><span data-stu-id="7adec-118">Type</span></span> | <span data-ttu-id="7adec-119">Opis</span><span class="sxs-lookup"><span data-stu-id="7adec-119">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="7adec-120">resourceName lub resourceIdentifier</span><span class="sxs-lookup"><span data-stu-id="7adec-120">resourceName or resourceIdentifier</span></span> |<span data-ttu-id="7adec-121">Tak</span><span class="sxs-lookup"><span data-stu-id="7adec-121">Yes</span></span> |<span data-ttu-id="7adec-122">Ciąg</span><span class="sxs-lookup"><span data-stu-id="7adec-122">string</span></span> |<span data-ttu-id="7adec-123">Unikatowy identyfikator zasobu.</span><span class="sxs-lookup"><span data-stu-id="7adec-123">Unique identifier for the resource.</span></span> |
| <span data-ttu-id="7adec-124">apiVersion</span><span class="sxs-lookup"><span data-stu-id="7adec-124">apiVersion</span></span> |<span data-ttu-id="7adec-125">Tak</span><span class="sxs-lookup"><span data-stu-id="7adec-125">Yes</span></span> |<span data-ttu-id="7adec-126">Ciąg</span><span class="sxs-lookup"><span data-stu-id="7adec-126">string</span></span> |<span data-ttu-id="7adec-127">Wersja interfejsu API stanu środowiska uruchomieniowego zasobu.</span><span class="sxs-lookup"><span data-stu-id="7adec-127">API version of resource runtime state.</span></span> <span data-ttu-id="7adec-128">Zazwyczaj w formacie **rrrr mm-dd**.</span><span class="sxs-lookup"><span data-stu-id="7adec-128">Typically, in the format, **yyyy-mm-dd**.</span></span> |

### <a name="return-value"></a><span data-ttu-id="7adec-129">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="7adec-129">Return value</span></span>

<span data-ttu-id="7adec-130">Obiekt zwrócony z listKeys ma następujący format:</span><span class="sxs-lookup"><span data-stu-id="7adec-130">The returned object from listKeys has the following format:</span></span>

```json
{
  "keys": [
    {
      "keyName": "key1",
      "permissions": "Full",
      "value": "{value}"
    },
    {
      "keyName": "key2",
      "permissions": "Full",
      "value": "{value}"
    }
  ]
}
```

<span data-ttu-id="7adec-131">Inne funkcje listy mają różne formaty zwracany.</span><span class="sxs-lookup"><span data-stu-id="7adec-131">Other list functions have different return formats.</span></span> <span data-ttu-id="7adec-132">Aby wyświetlić format funkcji, Uwzględnij go w sekcji danych wyjściowych jak pokazano w przykładzie szablonu.</span><span class="sxs-lookup"><span data-stu-id="7adec-132">To see the format of a function, include it in the outputs section as shown in the example template.</span></span> 

### <a name="remarks"></a><span data-ttu-id="7adec-133">Uwagi</span><span class="sxs-lookup"><span data-stu-id="7adec-133">Remarks</span></span>

<span data-ttu-id="7adec-134">Żadnej operacji, która rozpoczyna się od **listy** mogą być używane jako funkcję w szablonie.</span><span class="sxs-lookup"><span data-stu-id="7adec-134">Any operation that starts with **list** can be used as a function in your template.</span></span> <span data-ttu-id="7adec-135">Dostępne operacje zawiera nie tylko listKeys, ale również operacji, takich jak `list`, `listAdminKeys`, i `listStatus`.</span><span class="sxs-lookup"><span data-stu-id="7adec-135">The available operations include not only listKeys, but also operations like `list`, `listAdminKeys`, and `listStatus`.</span></span> <span data-ttu-id="7adec-136">Nie można jednak użyć **listy** operacje, które wymagają wartości w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="7adec-136">However, you cannot use **list** operations that require values in the request body.</span></span> <span data-ttu-id="7adec-137">Na przykład [SAS konta listy](/rest/api/storagerp/storageaccounts#StorageAccounts_ListAccountSAS) operacja wymaga parametrów treści żądania, takich jak *signedExpiry*, więc nie można go użyć w ramach szablonu.</span><span class="sxs-lookup"><span data-stu-id="7adec-137">For example, the [List Account SAS](/rest/api/storagerp/storageaccounts#StorageAccounts_ListAccountSAS) operation requires request body parameters like *signedExpiry*, so you cannot use it within a template.</span></span>

<span data-ttu-id="7adec-138">Aby określić, jakie typy zasobów operacja listy, masz następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="7adec-138">To determine which resource types have a list operation, you have the following options:</span></span>

* <span data-ttu-id="7adec-139">Widok [operacje interfejsu API REST](/rest/api/) dla dostawcy zasobów, a następnie wyszukaj listę operacji.</span><span class="sxs-lookup"><span data-stu-id="7adec-139">View the [REST API operations](/rest/api/) for a resource provider, and look for list operations.</span></span> <span data-ttu-id="7adec-140">Na przykład mieć kont magazynu [operacji listKeys](/rest/api/storagerp/storageaccounts#StorageAccounts_ListKeys).</span><span class="sxs-lookup"><span data-stu-id="7adec-140">For example, storage accounts have the [listKeys operation](/rest/api/storagerp/storageaccounts#StorageAccounts_ListKeys).</span></span>
* <span data-ttu-id="7adec-141">Użyj [Get-AzureRmProviderOperation](/powershell/module/azurerm.resources/get-azurermprovideroperation) polecenia cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7adec-141">Use the [Get-AzureRmProviderOperation](/powershell/module/azurerm.resources/get-azurermprovideroperation) PowerShell cmdlet.</span></span> <span data-ttu-id="7adec-142">Poniższy przykład pobiera wszystkie operacje listy kont magazynu:</span><span class="sxs-lookup"><span data-stu-id="7adec-142">The following example gets all list operations for storage accounts:</span></span>

  ```powershell
  Get-AzureRmProviderOperation -OperationSearchString "Microsoft.Storage/*" | where {$_.Operation -like "*list*"} | FT Operation
  ```
* <span data-ttu-id="7adec-143">Użyj następującego polecenia wiersza polecenia platformy Azure, aby filtrować tylko operacje listy:</span><span class="sxs-lookup"><span data-stu-id="7adec-143">Use the following Azure CLI command to filter only the list operations:</span></span>

  ```azurecli
  az provider operation show --namespace Microsoft.Storage --query "resourceTypes[?name=='storageAccounts'].operations[].name | [?contains(@, 'list')]"
  ```

<span data-ttu-id="7adec-144">Określ zasób, używając [funkcja resourceId](#resourceid), lub format `{providerNamespace}/{resourceType}/{resourceName}`.</span><span class="sxs-lookup"><span data-stu-id="7adec-144">Specify the resource by using either the [resourceId function](#resourceid), or the format `{providerNamespace}/{resourceType}/{resourceName}`.</span></span>


### <a name="example"></a><span data-ttu-id="7adec-145">Przykład</span><span class="sxs-lookup"><span data-stu-id="7adec-145">Example</span></span>

<span data-ttu-id="7adec-146">Poniższy przykład przedstawia sposób zwrócenia klucze podstawowe i pomocnicze z konta magazynu w sekcji danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="7adec-146">The following example shows how to return the primary and secondary keys from a storage account in the outputs section.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountId": {
            "type": "string"
        }
    },
    "resources": [],
    "outputs": {
        "storageKeysOutput": {
            "value": "[listKeys(parameters('storageAccountId'), '2016-01-01')]",
            "type" : "object"
        }
    }
}
``` 

<a id="providers" />

## <a name="providers"></a><span data-ttu-id="7adec-147">dostawców</span><span class="sxs-lookup"><span data-stu-id="7adec-147">providers</span></span>
`providers(providerNamespace, [resourceType])`

<span data-ttu-id="7adec-148">Zwraca informacje o dostawcy zasobów i jego obsługiwane typy zasobów.</span><span class="sxs-lookup"><span data-stu-id="7adec-148">Returns information about a resource provider and its supported resource types.</span></span> <span data-ttu-id="7adec-149">Jeśli typ zasobu nie zostanie określona, funkcja zwraca obsługiwane typy dla dostawcy zasobów.</span><span class="sxs-lookup"><span data-stu-id="7adec-149">If you do not provide a resource type, the function returns all the supported types for the resource provider.</span></span>

### <a name="parameters"></a><span data-ttu-id="7adec-150">Parametry</span><span class="sxs-lookup"><span data-stu-id="7adec-150">Parameters</span></span>

| <span data-ttu-id="7adec-151">Parametr</span><span class="sxs-lookup"><span data-stu-id="7adec-151">Parameter</span></span> | <span data-ttu-id="7adec-152">Wymagane</span><span class="sxs-lookup"><span data-stu-id="7adec-152">Required</span></span> | <span data-ttu-id="7adec-153">Typ</span><span class="sxs-lookup"><span data-stu-id="7adec-153">Type</span></span> | <span data-ttu-id="7adec-154">Opis</span><span class="sxs-lookup"><span data-stu-id="7adec-154">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="7adec-155">providerNamespace</span><span class="sxs-lookup"><span data-stu-id="7adec-155">providerNamespace</span></span> |<span data-ttu-id="7adec-156">Tak</span><span class="sxs-lookup"><span data-stu-id="7adec-156">Yes</span></span> |<span data-ttu-id="7adec-157">Ciąg</span><span class="sxs-lookup"><span data-stu-id="7adec-157">string</span></span> |<span data-ttu-id="7adec-158">Namespace dostawcy</span><span class="sxs-lookup"><span data-stu-id="7adec-158">Namespace of the provider</span></span> |
| <span data-ttu-id="7adec-159">Typ zasobu</span><span class="sxs-lookup"><span data-stu-id="7adec-159">resourceType</span></span> |<span data-ttu-id="7adec-160">Nie</span><span class="sxs-lookup"><span data-stu-id="7adec-160">No</span></span> |<span data-ttu-id="7adec-161">Ciąg</span><span class="sxs-lookup"><span data-stu-id="7adec-161">string</span></span> |<span data-ttu-id="7adec-162">Typ zasobu w określonej przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="7adec-162">The type of resource within the specified namespace.</span></span> |

### <a name="return-value"></a><span data-ttu-id="7adec-163">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="7adec-163">Return value</span></span>

<span data-ttu-id="7adec-164">Zwrócono każdego obsługiwanego typu w następującym formacie:</span><span class="sxs-lookup"><span data-stu-id="7adec-164">Each supported type is returned in the following format:</span></span> 

```json
{
    "resourceType": "{name of resource type}",
    "locations": [ all supported locations ],
    "apiVersions": [ all supported API versions ]
}
```

<span data-ttu-id="7adec-165">Kolejność zwracanych wartości tablicy nie jest gwarantowana.</span><span class="sxs-lookup"><span data-stu-id="7adec-165">Array ordering of the returned values is not guaranteed.</span></span>

### <a name="example"></a><span data-ttu-id="7adec-166">Przykład</span><span class="sxs-lookup"><span data-stu-id="7adec-166">Example</span></span>

<span data-ttu-id="7adec-167">Poniższy przykład przedstawia sposób użycia funkcji dostawcy:</span><span class="sxs-lookup"><span data-stu-id="7adec-167">The following example shows how to use the provider function:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "providerOutput": {
            "value": "[providers('Microsoft.Web', 'sites')]",
            "type" : "object"
        }
    }
}
```

<span data-ttu-id="7adec-168">Poprzedni przykład zwraca obiekt w następującym formacie:</span><span class="sxs-lookup"><span data-stu-id="7adec-168">The preceding example returns an object in the following format:</span></span>

```json
{
  "resourceType": "sites",
  "locations": [
    "South Central US",
    "North Europe",
    "West Europe",
    "Southeast Asia",
    ...
  ],
  "apiVersions": [
    "2016-08-01",
    "2016-03-01",
    "2015-08-01-preview",
    "2015-08-01",
    ...
  ]
}
```

<a id="reference" />

## <a name="reference"></a><span data-ttu-id="7adec-169">Odwołanie</span><span class="sxs-lookup"><span data-stu-id="7adec-169">reference</span></span>
`reference(resourceName or resourceIdentifier, [apiVersion])`

<span data-ttu-id="7adec-170">Zwraca obiekt reprezentujący stan czasu wykonywania zasobu.</span><span class="sxs-lookup"><span data-stu-id="7adec-170">Returns an object representing a resource's runtime state.</span></span>

### <a name="parameters"></a><span data-ttu-id="7adec-171">Parametry</span><span class="sxs-lookup"><span data-stu-id="7adec-171">Parameters</span></span>

| <span data-ttu-id="7adec-172">Parametr</span><span class="sxs-lookup"><span data-stu-id="7adec-172">Parameter</span></span> | <span data-ttu-id="7adec-173">Wymagane</span><span class="sxs-lookup"><span data-stu-id="7adec-173">Required</span></span> | <span data-ttu-id="7adec-174">Typ</span><span class="sxs-lookup"><span data-stu-id="7adec-174">Type</span></span> | <span data-ttu-id="7adec-175">Opis</span><span class="sxs-lookup"><span data-stu-id="7adec-175">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="7adec-176">resourceName lub resourceIdentifier</span><span class="sxs-lookup"><span data-stu-id="7adec-176">resourceName or resourceIdentifier</span></span> |<span data-ttu-id="7adec-177">Tak</span><span class="sxs-lookup"><span data-stu-id="7adec-177">Yes</span></span> |<span data-ttu-id="7adec-178">Ciąg</span><span class="sxs-lookup"><span data-stu-id="7adec-178">string</span></span> |<span data-ttu-id="7adec-179">Nazwa lub identyfikator zasobu.</span><span class="sxs-lookup"><span data-stu-id="7adec-179">Name or unique identifier of a resource.</span></span> |
| <span data-ttu-id="7adec-180">apiVersion</span><span class="sxs-lookup"><span data-stu-id="7adec-180">apiVersion</span></span> |<span data-ttu-id="7adec-181">Nie</span><span class="sxs-lookup"><span data-stu-id="7adec-181">No</span></span> |<span data-ttu-id="7adec-182">Ciąg</span><span class="sxs-lookup"><span data-stu-id="7adec-182">string</span></span> |<span data-ttu-id="7adec-183">Wersja interfejsu API określonego zasobu.</span><span class="sxs-lookup"><span data-stu-id="7adec-183">API version of the specified resource.</span></span> <span data-ttu-id="7adec-184">Obejmują tego parametru, gdy zasób nie zostanie zainicjowana w ramach tego samego szablonu.</span><span class="sxs-lookup"><span data-stu-id="7adec-184">Include this parameter when the resource is not provisioned within same template.</span></span> <span data-ttu-id="7adec-185">Zazwyczaj w formacie **rrrr mm-dd**.</span><span class="sxs-lookup"><span data-stu-id="7adec-185">Typically, in the format, **yyyy-mm-dd**.</span></span> |

### <a name="return-value"></a><span data-ttu-id="7adec-186">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="7adec-186">Return value</span></span>

<span data-ttu-id="7adec-187">Każdy typ zasobu zwraca inne właściwości dla funkcji odwołania.</span><span class="sxs-lookup"><span data-stu-id="7adec-187">Every resource type returns different properties for the reference function.</span></span> <span data-ttu-id="7adec-188">Funkcja nie zwraca jednego, wstępnie zdefiniowanego formatu.</span><span class="sxs-lookup"><span data-stu-id="7adec-188">The function does not return a single, predefined format.</span></span> <span data-ttu-id="7adec-189">Aby wyświetlić właściwości dla typu zasobu, zwracać obiekt w sekcji danych wyjściowych, jak pokazano w przykładzie.</span><span class="sxs-lookup"><span data-stu-id="7adec-189">To see the properties for a resource type, return the object in the outputs section as shown in the example.</span></span>

### <a name="remarks"></a><span data-ttu-id="7adec-190">Uwagi</span><span class="sxs-lookup"><span data-stu-id="7adec-190">Remarks</span></span>

<span data-ttu-id="7adec-191">Funkcja odwołanie pochodzi wartość ze stanu środowiska uruchomieniowego i nie można użyć w sekcji zmiennych.</span><span class="sxs-lookup"><span data-stu-id="7adec-191">The reference function derives its value from a runtime state, and therefore cannot be used in the variables section.</span></span> <span data-ttu-id="7adec-192">Można go w sekcji danych wyjściowych szablonu.</span><span class="sxs-lookup"><span data-stu-id="7adec-192">It can be used in outputs section of a template.</span></span> 

<span data-ttu-id="7adec-193">Za pomocą funkcji odwołania, niejawnie deklarowaniu czy jeden zasób jest zależny od innego zasobu, jeśli przywoływany zasób jest udostępniony w ramach tego samego szablonu.</span><span class="sxs-lookup"><span data-stu-id="7adec-193">By using the reference function, you implicitly declare that one resource depends on another resource if the referenced resource is provisioned within same template.</span></span> <span data-ttu-id="7adec-194">Nie trzeba również użyć dependsOn właściwości.</span><span class="sxs-lookup"><span data-stu-id="7adec-194">You do not need to also use the dependsOn property.</span></span> <span data-ttu-id="7adec-195">Funkcja nie jest oceniany, aż do zakończenia wdrażania żądanego zasobu.</span><span class="sxs-lookup"><span data-stu-id="7adec-195">The function is not evaluated until the referenced resource has completed deployment.</span></span>

<span data-ttu-id="7adec-196">Aby wyświetlić nazwy właściwości i wartości dla typu zasobu, należy utworzyć szablon, który zwraca obiekt, w sekcji danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="7adec-196">To see the property names and values for a resource type, create a template that returns the object in the outputs section.</span></span> <span data-ttu-id="7adec-197">Jeśli masz istniejący zasób tego typu do szablonu zwraca obiekt bez wdrażania żadnych nowych zasobów.</span><span class="sxs-lookup"><span data-stu-id="7adec-197">If you have an existing resource of that type, your template returns the object without deploying any new resources.</span></span> 

<span data-ttu-id="7adec-198">Zazwyczaj **odwołania** funkcja zwraca wartość określonego obiektu, na przykład obiektu blob identyfikatora URI punktu końcowego lub w pełni kwalifikowaną nazwę domeny.</span><span class="sxs-lookup"><span data-stu-id="7adec-198">Typically, you use the **reference** function to return a particular value from an object, such as the blob endpoint URI or fully qualified domain name.</span></span>

```json
"outputs": {
    "BlobUri": {
        "value": "[reference(concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName')), '2016-01-01').primaryEndpoints.blob]",
        "type" : "string"
    },
    "FQDN": {
        "value": "[reference(concat('Microsoft.Network/publicIPAddresses/', parameters('ipAddressName')), '2016-03-30').dnsSettings.fqdn]",
        "type" : "string"
    }
}
```

### <a name="example"></a><span data-ttu-id="7adec-199">Przykład</span><span class="sxs-lookup"><span data-stu-id="7adec-199">Example</span></span>

<span data-ttu-id="7adec-200">Aby wdrożyć i odwoływać się do zasobu w tym samym szablonie, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="7adec-200">To deploy and reference the resource in the same template, use:</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
      "storageAccountName": { 
          "type": "string"
      }
  },
  "resources": [
    {
      "name": "[parameters('storageAccountName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-12-01",
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {
      }
    }
  ],
  "outputs": {
      "referenceOutput": {
          "type": "object",
          "value": "[reference(parameters('storageAccountName'))]"
      }
    }
}
``` 

<span data-ttu-id="7adec-201">Poprzedni przykład zwraca obiekt w następującym formacie:</span><span class="sxs-lookup"><span data-stu-id="7adec-201">The preceding example returns an object in the following format:</span></span>

```json
{
   "creationTime": "2017-06-13T21:24:46.618364Z",
   "primaryEndpoints": {
     "blob": "https://examplestorage.blob.core.windows.net/",
     "file": "https://examplestorage.file.core.windows.net/",
     "queue": "https://examplestorage.queue.core.windows.net/",
     "table": "https://examplestorage.table.core.windows.net/"
   },
   "primaryLocation": "southcentralus",
   "provisioningState": "Succeeded",
   "statusOfPrimary": "available",
   "supportsHttpsTrafficOnly": false
}
```

<span data-ttu-id="7adec-202">Poniższy przykład odwołuje się do konta magazynu, który nie jest wdrożony w tym szablonie.</span><span class="sxs-lookup"><span data-stu-id="7adec-202">The following example references a storage account that is not deployed in this template.</span></span> <span data-ttu-id="7adec-203">Konto magazynu już istnieje w tej samej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="7adec-203">The storage account already exists within the same resource group.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountName": {
            "type": "string"
        }
    },
    "resources": [],
    "outputs": {
        "ExistingStorage": {
            "value": "[reference(concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName')), '2016-01-01')]",
            "type" : "object"
        }
    }
}
```

<a id="resourcegroup" />

## <a name="resourcegroup"></a><span data-ttu-id="7adec-204">Grupa zasobów</span><span class="sxs-lookup"><span data-stu-id="7adec-204">resourceGroup</span></span>
`resourceGroup()`

<span data-ttu-id="7adec-205">Zwraca obiekt reprezentujący bieżącej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="7adec-205">Returns an object that represents the current resource group.</span></span> 

### <a name="return-value"></a><span data-ttu-id="7adec-206">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="7adec-206">Return value</span></span>

<span data-ttu-id="7adec-207">Zwrócony obiekt jest w następującym formacie:</span><span class="sxs-lookup"><span data-stu-id="7adec-207">The returned object is in the following format:</span></span>

```json
{
  "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}",
  "name": "{resourceGroupName}",
  "location": "{resourceGroupLocation}",
  "tags": {
  },
  "properties": {
    "provisioningState": "{status}"
  }
}
```

### <a name="remarks"></a><span data-ttu-id="7adec-208">Uwagi</span><span class="sxs-lookup"><span data-stu-id="7adec-208">Remarks</span></span>

<span data-ttu-id="7adec-209">Użycia funkcji grupa zasobów ma tworzyć zasoby w tej samej lokalizacji co grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="7adec-209">A common use of the resourceGroup function is to create resources in the same location as the resource group.</span></span> <span data-ttu-id="7adec-210">W poniższym przykładzie użyto lokalizacja grupy zasobów, aby przypisać lokalizacji dla witryny sieci web.</span><span class="sxs-lookup"><span data-stu-id="7adec-210">The following example uses the resource group location to assign the location for a web site.</span></span>

```json
"resources": [
   {
      "apiVersion": "2016-08-01",
      "type": "Microsoft.Web/sites",
      "name": "[parameters('siteName')]",
      "location": "[resourceGroup().location]",
      ...
   }
]
```

### <a name="example"></a><span data-ttu-id="7adec-211">Przykład</span><span class="sxs-lookup"><span data-stu-id="7adec-211">Example</span></span>

<span data-ttu-id="7adec-212">Następujący szablon zwraca właściwości grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="7adec-212">The following template returns the properties of the resource group.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[resourceGroup()]",
            "type" : "object"
        }
    }
}
```

<span data-ttu-id="7adec-213">Poprzedni przykład zwraca obiekt w następującym formacie:</span><span class="sxs-lookup"><span data-stu-id="7adec-213">The preceding example returns an object in the following format:</span></span>

```json
{
  "id": "/subscriptions/{subscription-id}/resourceGroups/examplegroup",
  "name": "examplegroup",
  "location": "southcentralus",
  "properties": {
    "provisioningState": "Succeeded"
  }
}
```

<a id="resourceid" />

## <a name="resourceid"></a><span data-ttu-id="7adec-214">resourceId</span><span class="sxs-lookup"><span data-stu-id="7adec-214">resourceId</span></span>
`resourceId([subscriptionId], [resourceGroupName], resourceType, resourceName1, [resourceName2]...)`

<span data-ttu-id="7adec-215">Zwraca unikatowy identyfikator zasobu.</span><span class="sxs-lookup"><span data-stu-id="7adec-215">Returns the unique identifier of a resource.</span></span> <span data-ttu-id="7adec-216">Aby użyć tej funkcji, jeśli nazwa zasobu jest niejednoznaczny lub nie udostępnione w ramach tego samego szablonu.</span><span class="sxs-lookup"><span data-stu-id="7adec-216">You use this function when the resource name is ambiguous or not provisioned within the same template.</span></span> 

### <a name="parameters"></a><span data-ttu-id="7adec-217">Parametry</span><span class="sxs-lookup"><span data-stu-id="7adec-217">Parameters</span></span>

| <span data-ttu-id="7adec-218">Parametr</span><span class="sxs-lookup"><span data-stu-id="7adec-218">Parameter</span></span> | <span data-ttu-id="7adec-219">Wymagane</span><span class="sxs-lookup"><span data-stu-id="7adec-219">Required</span></span> | <span data-ttu-id="7adec-220">Typ</span><span class="sxs-lookup"><span data-stu-id="7adec-220">Type</span></span> | <span data-ttu-id="7adec-221">Opis</span><span class="sxs-lookup"><span data-stu-id="7adec-221">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="7adec-222">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="7adec-222">subscriptionId</span></span> |<span data-ttu-id="7adec-223">Nie</span><span class="sxs-lookup"><span data-stu-id="7adec-223">No</span></span> |<span data-ttu-id="7adec-224">ciąg (format identyfikatora GUID w)</span><span class="sxs-lookup"><span data-stu-id="7adec-224">string (In GUID format)</span></span> |<span data-ttu-id="7adec-225">Wartość domyślna to bieżącej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="7adec-225">Default value is the current subscription.</span></span> <span data-ttu-id="7adec-226">Należy podać tę wartość, gdy trzeba pobrać zasobu w innej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="7adec-226">Specify this value when you need to retrieve a resource in another subscription.</span></span> |
| <span data-ttu-id="7adec-227">Grupy zasobów o nazwie</span><span class="sxs-lookup"><span data-stu-id="7adec-227">resourceGroupName</span></span> |<span data-ttu-id="7adec-228">Nie</span><span class="sxs-lookup"><span data-stu-id="7adec-228">No</span></span> |<span data-ttu-id="7adec-229">Ciąg</span><span class="sxs-lookup"><span data-stu-id="7adec-229">string</span></span> |<span data-ttu-id="7adec-230">Wartość domyślna to bieżącej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="7adec-230">Default value is current resource group.</span></span> <span data-ttu-id="7adec-231">Należy podać tę wartość, gdy trzeba pobrać zasobu w innej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="7adec-231">Specify this value when you need to retrieve a resource in another resource group.</span></span> |
| <span data-ttu-id="7adec-232">Typ zasobu</span><span class="sxs-lookup"><span data-stu-id="7adec-232">resourceType</span></span> |<span data-ttu-id="7adec-233">Tak</span><span class="sxs-lookup"><span data-stu-id="7adec-233">Yes</span></span> |<span data-ttu-id="7adec-234">Ciąg</span><span class="sxs-lookup"><span data-stu-id="7adec-234">string</span></span> |<span data-ttu-id="7adec-235">Typ zasobu, włącznie z przestrzenią nazw dostawcy zasobów.</span><span class="sxs-lookup"><span data-stu-id="7adec-235">Type of resource including resource provider namespace.</span></span> |
| <span data-ttu-id="7adec-236">resourceName1</span><span class="sxs-lookup"><span data-stu-id="7adec-236">resourceName1</span></span> |<span data-ttu-id="7adec-237">Tak</span><span class="sxs-lookup"><span data-stu-id="7adec-237">Yes</span></span> |<span data-ttu-id="7adec-238">Ciąg</span><span class="sxs-lookup"><span data-stu-id="7adec-238">string</span></span> |<span data-ttu-id="7adec-239">Nazwa zasobu.</span><span class="sxs-lookup"><span data-stu-id="7adec-239">Name of resource.</span></span> |
| <span data-ttu-id="7adec-240">resourceName2</span><span class="sxs-lookup"><span data-stu-id="7adec-240">resourceName2</span></span> |<span data-ttu-id="7adec-241">Nie</span><span class="sxs-lookup"><span data-stu-id="7adec-241">No</span></span> |<span data-ttu-id="7adec-242">Ciąg</span><span class="sxs-lookup"><span data-stu-id="7adec-242">string</span></span> |<span data-ttu-id="7adec-243">Następny nazwy segmentu zasobu, jeśli zasób jest zagnieżdżony.</span><span class="sxs-lookup"><span data-stu-id="7adec-243">Next resource name segment if resource is nested.</span></span> |

### <a name="return-value"></a><span data-ttu-id="7adec-244">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="7adec-244">Return value</span></span>

<span data-ttu-id="7adec-245">Identyfikator jest zwracany w następującym formacie:</span><span class="sxs-lookup"><span data-stu-id="7adec-245">The identifier is returned in the following format:</span></span>

```json
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{resourceType}/{resourceName}
```

### <a name="remarks"></a><span data-ttu-id="7adec-246">Uwagi</span><span class="sxs-lookup"><span data-stu-id="7adec-246">Remarks</span></span>

<span data-ttu-id="7adec-247">Wartości parametrów, które określisz zależą od tego, czy zasób jest w tej samej grupie subskrypcji i zasobu jako bieżącego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="7adec-247">The parameter values you specify depend on whether the resource is in the same subscription and resource group as the current deployment.</span></span>

<span data-ttu-id="7adec-248">Aby uzyskać identyfikator zasobu dla konta magazynu w tej samej subskrypcji i grupy zasobów, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="7adec-248">To get the resource ID for a storage account in the same subscription and resource group, use:</span></span>

```json
"[resourceId('Microsoft.Storage/storageAccounts','examplestorage')]"
```

<span data-ttu-id="7adec-249">Aby uzyskać identyfikator zasobu dla konta magazynu w tej samej subskrypcji, ale innej grupie zasobów, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="7adec-249">To get the resource ID for a storage account in the same subscription but a different resource group, use:</span></span>

```json
"[resourceId('otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

<span data-ttu-id="7adec-250">Aby uzyskać identyfikator zasobu dla konta magazynu w innej subskrypcji i grupy zasobów, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="7adec-250">To get the resource ID for a storage account in a different subscription and resource group, use:</span></span>

```json
"[resourceId('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

<span data-ttu-id="7adec-251">Aby uzyskać identyfikator zasobu bazy danych w innej grupie zasobów, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="7adec-251">To get the resource ID for a database in a different resource group, use:</span></span>

```json
"[resourceId('otherResourceGroup', 'Microsoft.SQL/servers/databases', parameters('serverName'), parameters('databaseName'))]"
```

<span data-ttu-id="7adec-252">Często należy użyć tej funkcji, korzystając z konta magazynu lub sieci wirtualnej w grupie zasobów alternatywny.</span><span class="sxs-lookup"><span data-stu-id="7adec-252">Often, you need to use this function when using a storage account or virtual network in an alternate resource group.</span></span> <span data-ttu-id="7adec-253">W poniższym przykładzie pokazano, jak łatwo można zasobu z grupy zasobów zewnętrznych:</span><span class="sxs-lookup"><span data-stu-id="7adec-253">The following example shows how a resource from an external resource group can easily be used:</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
      "virtualNetworkName": {
          "type": "string"
      },
      "virtualNetworkResourceGroup": {
          "type": "string"
      },
      "subnet1Name": {
          "type": "string"
      },
      "nicName": {
          "type": "string"
      }
  },
  "variables": {
      "vnetID": "[resourceId(parameters('virtualNetworkResourceGroup'), 'Microsoft.Network/virtualNetworks', parameters('virtualNetworkName'))]",
      "subnet1Ref": "[concat(variables('vnetID'),'/subnets/', parameters('subnet1Name'))]"
  },
  "resources": [
  {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[parameters('nicName')]",
      "location": "[parameters('location')]",
      "properties": {
          "ipConfigurations": [{
              "name": "ipconfig1",
              "properties": {
                  "privateIPAllocationMethod": "Dynamic",
                  "subnet": {
                      "id": "[variables('subnet1Ref')]"
                  }
              }
          }]
       }
  }]
}
```

### <a name="example"></a><span data-ttu-id="7adec-254">Przykład</span><span class="sxs-lookup"><span data-stu-id="7adec-254">Example</span></span>

<span data-ttu-id="7adec-255">Poniższy przykład zwraca identyfikator zasobu dla konta magazynu w grupie zasobów:</span><span class="sxs-lookup"><span data-stu-id="7adec-255">The following example returns the resource ID for a storage account in the resource group:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "sameRGOutput": {
            "value": "[resourceId('Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "differentRGOutput": {
            "value": "[resourceId('otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "differentSubOutput": {
            "value": "[resourceId('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "nestedResourceOutput": {
            "value": "[resourceId('Microsoft.SQL/servers/databases', 'serverName', 'databaseName')]",
            "type" : "string"
        }
    }
}
```

<span data-ttu-id="7adec-256">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="7adec-256">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="7adec-257">Nazwa</span><span class="sxs-lookup"><span data-stu-id="7adec-257">Name</span></span> | <span data-ttu-id="7adec-258">Typ</span><span class="sxs-lookup"><span data-stu-id="7adec-258">Type</span></span> | <span data-ttu-id="7adec-259">Wartość</span><span class="sxs-lookup"><span data-stu-id="7adec-259">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="7adec-260">sameRGOutput</span><span class="sxs-lookup"><span data-stu-id="7adec-260">sameRGOutput</span></span> | <span data-ttu-id="7adec-261">Ciąg</span><span class="sxs-lookup"><span data-stu-id="7adec-261">String</span></span> | <span data-ttu-id="7adec-262">/Subscriptions/{Current-Sub-ID}/resourceGroups/examplegroup/Providers/Microsoft.Storage/storageAccounts/examplestorage</span><span class="sxs-lookup"><span data-stu-id="7adec-262">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span></span> |
| <span data-ttu-id="7adec-263">differentRGOutput</span><span class="sxs-lookup"><span data-stu-id="7adec-263">differentRGOutput</span></span> | <span data-ttu-id="7adec-264">Ciąg</span><span class="sxs-lookup"><span data-stu-id="7adec-264">String</span></span> | <span data-ttu-id="7adec-265">/Subscriptions/{Current-Sub-ID}/resourceGroups/otherResourceGroup/Providers/Microsoft.Storage/storageAccounts/examplestorage</span><span class="sxs-lookup"><span data-stu-id="7adec-265">/subscriptions/{current-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span></span> |
| <span data-ttu-id="7adec-266">differentSubOutput</span><span class="sxs-lookup"><span data-stu-id="7adec-266">differentSubOutput</span></span> | <span data-ttu-id="7adec-267">Ciąg</span><span class="sxs-lookup"><span data-stu-id="7adec-267">String</span></span> | <span data-ttu-id="7adec-268">/Subscriptions/{different-Sub-ID}/resourceGroups/otherResourceGroup/Providers/Microsoft.Storage/storageAccounts/examplestorage</span><span class="sxs-lookup"><span data-stu-id="7adec-268">/subscriptions/{different-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span></span> |
| <span data-ttu-id="7adec-269">nestedResourceOutput</span><span class="sxs-lookup"><span data-stu-id="7adec-269">nestedResourceOutput</span></span> | <span data-ttu-id="7adec-270">Ciąg</span><span class="sxs-lookup"><span data-stu-id="7adec-270">String</span></span> | <span data-ttu-id="7adec-271">/Subscriptions/{Current-Sub-ID}/resourceGroups/examplegroup/Providers/Microsoft.SQL/Servers/serverName/Databases/databaseName</span><span class="sxs-lookup"><span data-stu-id="7adec-271">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.SQL/servers/serverName/databases/databaseName</span></span> |

<a id="subscription" />

## <a name="subscription"></a><span data-ttu-id="7adec-272">subskrypcja</span><span class="sxs-lookup"><span data-stu-id="7adec-272">subscription</span></span>
`subscription()`

<span data-ttu-id="7adec-273">Zwraca szczegółowe informacje o subskrypcji dla bieżącego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="7adec-273">Returns details about the subscription for the current deployment.</span></span> 

### <a name="return-value"></a><span data-ttu-id="7adec-274">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="7adec-274">Return value</span></span>

<span data-ttu-id="7adec-275">Funkcja zwraca następujący format:</span><span class="sxs-lookup"><span data-stu-id="7adec-275">The function returns the following format:</span></span>

```json
{
    "id": "/subscriptions/{subscription-id}",
    "subscriptionId": "{subscription-id}",
    "tenantId": "{tenant-id}",
    "displayName": "{name-of-subscription}"
}
```

### <a name="example"></a><span data-ttu-id="7adec-276">Przykład</span><span class="sxs-lookup"><span data-stu-id="7adec-276">Example</span></span>

<span data-ttu-id="7adec-277">Poniższy przykład przedstawia funkcję subskrypcji o nazwie w sekcji danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="7adec-277">The following example shows the subscription function called in the outputs section.</span></span> 

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[subscription()]",
            "type" : "object"
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="7adec-278">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7adec-278">Next steps</span></span>
* <span data-ttu-id="7adec-279">Opis części szablonu usługi Azure Resource Manager, zobacz [szablonów Authoring Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="7adec-279">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="7adec-280">Aby scalić wiele szablonów, zobacz [za pomocą szablonów połączonych z usługą Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="7adec-280">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="7adec-281">Do wykonywania iteracji określoną liczbę razy podczas tworzenia typu zasobu, zobacz [utworzyć wiele wystąpień zasobów usługi Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="7adec-281">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="7adec-282">Aby zobaczyć, jak wdrożyć szablon został utworzony, zobacz [wdrażania aplikacji przy użyciu szablonu usługi Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="7adec-282">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

