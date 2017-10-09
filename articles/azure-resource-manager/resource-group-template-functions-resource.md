---
title: "funkcje szablonu usługi Resource Manager aaaAzure — zasoby | Dokumentacja firmy Microsoft"
description: "Opisuje hello funkcje toouse wartości tooretrieve szablonu usługi Azure Resource Manager dotyczących zasobów."
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
ms.openlocfilehash: c9d524b338b8b7ea6d8c9e0135d48e4fb8f167c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="resource-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="c6e95-103">Funkcje zasobów dla szablonów usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c6e95-103">Resource functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="c6e95-104">Usługa Resource Manager zapewnia następujące funkcje do pobierania wartości zasobów hello:</span><span class="sxs-lookup"><span data-stu-id="c6e95-104">Resource Manager provides hello following functions for getting resource values:</span></span>

* [<span data-ttu-id="c6e95-105">listKeys i listy {Value}</span><span class="sxs-lookup"><span data-stu-id="c6e95-105">listKeys and list{Value}</span></span>](#listkeys)
* [<span data-ttu-id="c6e95-106">dostawców</span><span class="sxs-lookup"><span data-stu-id="c6e95-106">providers</span></span>](#providers)
* [<span data-ttu-id="c6e95-107">Odwołanie</span><span class="sxs-lookup"><span data-stu-id="c6e95-107">reference</span></span>](#reference)
* [<span data-ttu-id="c6e95-108">Grupa zasobów</span><span class="sxs-lookup"><span data-stu-id="c6e95-108">resourceGroup</span></span>](#resourcegroup)
* [<span data-ttu-id="c6e95-109">Identyfikator zasobu</span><span class="sxs-lookup"><span data-stu-id="c6e95-109">resourceId</span></span>](#resourceid)
* [<span data-ttu-id="c6e95-110">Subskrypcja</span><span class="sxs-lookup"><span data-stu-id="c6e95-110">subscription</span></span>](#subscription)

<span data-ttu-id="c6e95-111">tooget wartości z parametrów, zmiennych lub hello bieżącego wdrożenia, zobacz [wdrożenia wartość funkcji](resource-group-template-functions-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="c6e95-111">tooget values from parameters, variables, or hello current deployment, see [Deployment value functions](resource-group-template-functions-deployment.md).</span></span>

<a id="listkeys" />
<a id="list" />

## <a name="listkeys-and-listvalue"></a><span data-ttu-id="c6e95-112">listKeys i listy {Value}</span><span class="sxs-lookup"><span data-stu-id="c6e95-112">listKeys and list{Value}</span></span>
`listKeys(resourceName or resourceIdentifier, apiVersion)`

`list{Value}(resourceName or resourceIdentifier, apiVersion)`

<span data-ttu-id="c6e95-113">Zwraca hello wartości dla dowolnego typu zasobu, który obsługuje hello listy operacji.</span><span class="sxs-lookup"><span data-stu-id="c6e95-113">Returns hello values for any resource type that supports hello list operation.</span></span> <span data-ttu-id="c6e95-114">najbardziej typowe użycie Hello jest `listKeys`.</span><span class="sxs-lookup"><span data-stu-id="c6e95-114">hello most common usage is `listKeys`.</span></span> 

### <a name="parameters"></a><span data-ttu-id="c6e95-115">Parametry</span><span class="sxs-lookup"><span data-stu-id="c6e95-115">Parameters</span></span>

| <span data-ttu-id="c6e95-116">Parametr</span><span class="sxs-lookup"><span data-stu-id="c6e95-116">Parameter</span></span> | <span data-ttu-id="c6e95-117">Wymagane</span><span class="sxs-lookup"><span data-stu-id="c6e95-117">Required</span></span> | <span data-ttu-id="c6e95-118">Typ</span><span class="sxs-lookup"><span data-stu-id="c6e95-118">Type</span></span> | <span data-ttu-id="c6e95-119">Opis</span><span class="sxs-lookup"><span data-stu-id="c6e95-119">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c6e95-120">resourceName lub resourceIdentifier</span><span class="sxs-lookup"><span data-stu-id="c6e95-120">resourceName or resourceIdentifier</span></span> |<span data-ttu-id="c6e95-121">Tak</span><span class="sxs-lookup"><span data-stu-id="c6e95-121">Yes</span></span> |<span data-ttu-id="c6e95-122">Ciąg</span><span class="sxs-lookup"><span data-stu-id="c6e95-122">string</span></span> |<span data-ttu-id="c6e95-123">Unikatowy identyfikator zasobu hello.</span><span class="sxs-lookup"><span data-stu-id="c6e95-123">Unique identifier for hello resource.</span></span> |
| <span data-ttu-id="c6e95-124">apiVersion</span><span class="sxs-lookup"><span data-stu-id="c6e95-124">apiVersion</span></span> |<span data-ttu-id="c6e95-125">Tak</span><span class="sxs-lookup"><span data-stu-id="c6e95-125">Yes</span></span> |<span data-ttu-id="c6e95-126">Ciąg</span><span class="sxs-lookup"><span data-stu-id="c6e95-126">string</span></span> |<span data-ttu-id="c6e95-127">Wersja interfejsu API stanu środowiska uruchomieniowego zasobu.</span><span class="sxs-lookup"><span data-stu-id="c6e95-127">API version of resource runtime state.</span></span> <span data-ttu-id="c6e95-128">Zazwyczaj w formacie hello **rrrr mm-dd**.</span><span class="sxs-lookup"><span data-stu-id="c6e95-128">Typically, in hello format, **yyyy-mm-dd**.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c6e95-129">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="c6e95-129">Return value</span></span>

<span data-ttu-id="c6e95-130">Witaj zwracany obiekt listKeys ma hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="c6e95-130">hello returned object from listKeys has hello following format:</span></span>

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

<span data-ttu-id="c6e95-131">Inne funkcje listy mają różne formaty zwracany.</span><span class="sxs-lookup"><span data-stu-id="c6e95-131">Other list functions have different return formats.</span></span> <span data-ttu-id="c6e95-132">format hello toosee funkcji, uwzględnić go w sekcji danych wyjściowych hello, jak pokazano w szablonie przykład hello.</span><span class="sxs-lookup"><span data-stu-id="c6e95-132">toosee hello format of a function, include it in hello outputs section as shown in hello example template.</span></span> 

### <a name="remarks"></a><span data-ttu-id="c6e95-133">Uwagi</span><span class="sxs-lookup"><span data-stu-id="c6e95-133">Remarks</span></span>

<span data-ttu-id="c6e95-134">Żadnej operacji, która rozpoczyna się od **listy** mogą być używane jako funkcję w szablonie.</span><span class="sxs-lookup"><span data-stu-id="c6e95-134">Any operation that starts with **list** can be used as a function in your template.</span></span> <span data-ttu-id="c6e95-135">Witaj dostępne operacji zalicza się nie tylko listKeys, ale również operacji, takich jak `list`, `listAdminKeys`, i `listStatus`.</span><span class="sxs-lookup"><span data-stu-id="c6e95-135">hello available operations include not only listKeys, but also operations like `list`, `listAdminKeys`, and `listStatus`.</span></span> <span data-ttu-id="c6e95-136">Nie można jednak użyć **listy** operacje, które wymagają wartości hello treść żądania.</span><span class="sxs-lookup"><span data-stu-id="c6e95-136">However, you cannot use **list** operations that require values in hello request body.</span></span> <span data-ttu-id="c6e95-137">Na przykład Witaj [SAS konta listy](/rest/api/storagerp/storageaccounts#StorageAccounts_ListAccountSAS) operacja wymaga parametrów treści żądania, takich jak *signedExpiry*, więc nie można go użyć w ramach szablonu.</span><span class="sxs-lookup"><span data-stu-id="c6e95-137">For example, hello [List Account SAS](/rest/api/storagerp/storageaccounts#StorageAccounts_ListAccountSAS) operation requires request body parameters like *signedExpiry*, so you cannot use it within a template.</span></span>

<span data-ttu-id="c6e95-138">typy zasobów, które mają operacja listy toodetermine, masz hello następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="c6e95-138">toodetermine which resource types have a list operation, you have hello following options:</span></span>

* <span data-ttu-id="c6e95-139">Widok hello [operacje interfejsu API REST](/rest/api/) dla dostawcy zasobów, a następnie wyszukaj listę operacji.</span><span class="sxs-lookup"><span data-stu-id="c6e95-139">View hello [REST API operations](/rest/api/) for a resource provider, and look for list operations.</span></span> <span data-ttu-id="c6e95-140">Na przykład konta magazynu ma hello [operacji listKeys](/rest/api/storagerp/storageaccounts#StorageAccounts_ListKeys).</span><span class="sxs-lookup"><span data-stu-id="c6e95-140">For example, storage accounts have hello [listKeys operation](/rest/api/storagerp/storageaccounts#StorageAccounts_ListKeys).</span></span>
* <span data-ttu-id="c6e95-141">Użyj hello [Get-AzureRmProviderOperation](/powershell/module/azurerm.resources/get-azurermprovideroperation) polecenia cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c6e95-141">Use hello [Get-AzureRmProviderOperation](/powershell/module/azurerm.resources/get-azurermprovideroperation) PowerShell cmdlet.</span></span> <span data-ttu-id="c6e95-142">Witaj poniższy przykład pobiera wszystkie operacje listy kont magazynu:</span><span class="sxs-lookup"><span data-stu-id="c6e95-142">hello following example gets all list operations for storage accounts:</span></span>

  ```powershell
  Get-AzureRmProviderOperation -OperationSearchString "Microsoft.Storage/*" | where {$_.Operation -like "*list*"} | FT Operation
  ```
* <span data-ttu-id="c6e95-143">Użyj następującego polecenia wiersza polecenia platformy Azure toofilter hello tylko operacje listy hello:</span><span class="sxs-lookup"><span data-stu-id="c6e95-143">Use hello following Azure CLI command toofilter only hello list operations:</span></span>

  ```azurecli
  az provider operation show --namespace Microsoft.Storage --query "resourceTypes[?name=='storageAccounts'].operations[].name | [?contains(@, 'list')]"
  ```

<span data-ttu-id="c6e95-144">Określ zasób hello przy użyciu albo hello [funkcja resourceId](#resourceid), lub hello format `{providerNamespace}/{resourceType}/{resourceName}`.</span><span class="sxs-lookup"><span data-stu-id="c6e95-144">Specify hello resource by using either hello [resourceId function](#resourceid), or hello format `{providerNamespace}/{resourceType}/{resourceName}`.</span></span>


### <a name="example"></a><span data-ttu-id="c6e95-145">Przykład</span><span class="sxs-lookup"><span data-stu-id="c6e95-145">Example</span></span>

<span data-ttu-id="c6e95-146">Witaj poniższy przykład przedstawia sposób tooreturn klucze podstawowe i pomocnicze hello z konta magazynu w hello generuje sekcji.</span><span class="sxs-lookup"><span data-stu-id="c6e95-146">hello following example shows how tooreturn hello primary and secondary keys from a storage account in hello outputs section.</span></span>

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

## <a name="providers"></a><span data-ttu-id="c6e95-147">dostawców</span><span class="sxs-lookup"><span data-stu-id="c6e95-147">providers</span></span>
`providers(providerNamespace, [resourceType])`

<span data-ttu-id="c6e95-148">Zwraca informacje o dostawcy zasobów i jego obsługiwane typy zasobów.</span><span class="sxs-lookup"><span data-stu-id="c6e95-148">Returns information about a resource provider and its supported resource types.</span></span> <span data-ttu-id="c6e95-149">Jeśli typ zasobu nie zostanie określona, funkcja hello zwraca wszystkie typy hello obsługiwane dla dostawcy zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="c6e95-149">If you do not provide a resource type, hello function returns all hello supported types for hello resource provider.</span></span>

### <a name="parameters"></a><span data-ttu-id="c6e95-150">Parametry</span><span class="sxs-lookup"><span data-stu-id="c6e95-150">Parameters</span></span>

| <span data-ttu-id="c6e95-151">Parametr</span><span class="sxs-lookup"><span data-stu-id="c6e95-151">Parameter</span></span> | <span data-ttu-id="c6e95-152">Wymagane</span><span class="sxs-lookup"><span data-stu-id="c6e95-152">Required</span></span> | <span data-ttu-id="c6e95-153">Typ</span><span class="sxs-lookup"><span data-stu-id="c6e95-153">Type</span></span> | <span data-ttu-id="c6e95-154">Opis</span><span class="sxs-lookup"><span data-stu-id="c6e95-154">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c6e95-155">providerNamespace</span><span class="sxs-lookup"><span data-stu-id="c6e95-155">providerNamespace</span></span> |<span data-ttu-id="c6e95-156">Tak</span><span class="sxs-lookup"><span data-stu-id="c6e95-156">Yes</span></span> |<span data-ttu-id="c6e95-157">Ciąg</span><span class="sxs-lookup"><span data-stu-id="c6e95-157">string</span></span> |<span data-ttu-id="c6e95-158">Namespace hello dostawcy</span><span class="sxs-lookup"><span data-stu-id="c6e95-158">Namespace of hello provider</span></span> |
| <span data-ttu-id="c6e95-159">Typ zasobu</span><span class="sxs-lookup"><span data-stu-id="c6e95-159">resourceType</span></span> |<span data-ttu-id="c6e95-160">Nie</span><span class="sxs-lookup"><span data-stu-id="c6e95-160">No</span></span> |<span data-ttu-id="c6e95-161">Ciąg</span><span class="sxs-lookup"><span data-stu-id="c6e95-161">string</span></span> |<span data-ttu-id="c6e95-162">określony Hello typ zasobu w hello przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="c6e95-162">hello type of resource within hello specified namespace.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c6e95-163">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="c6e95-163">Return value</span></span>

<span data-ttu-id="c6e95-164">Każdego obsługiwanego typu, jest zwracany w hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="c6e95-164">Each supported type is returned in hello following format:</span></span> 

```json
{
    "resourceType": "{name of resource type}",
    "locations": [ all supported locations ],
    "apiVersions": [ all supported API versions ]
}
```

<span data-ttu-id="c6e95-165">Tablica kolejność hello zwracane wartości nie jest gwarantowana.</span><span class="sxs-lookup"><span data-stu-id="c6e95-165">Array ordering of hello returned values is not guaranteed.</span></span>

### <a name="example"></a><span data-ttu-id="c6e95-166">Przykład</span><span class="sxs-lookup"><span data-stu-id="c6e95-166">Example</span></span>

<span data-ttu-id="c6e95-167">Witaj poniższy przykład pokazuje, jak toouse hello funkcja dostawcy:</span><span class="sxs-lookup"><span data-stu-id="c6e95-167">hello following example shows how toouse hello provider function:</span></span>

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

<span data-ttu-id="c6e95-168">Witaj poprzednim przykładzie zwraca obiekt hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="c6e95-168">hello preceding example returns an object in hello following format:</span></span>

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

## <a name="reference"></a><span data-ttu-id="c6e95-169">Odwołanie</span><span class="sxs-lookup"><span data-stu-id="c6e95-169">reference</span></span>
`reference(resourceName or resourceIdentifier, [apiVersion])`

<span data-ttu-id="c6e95-170">Zwraca obiekt reprezentujący stan czasu wykonywania zasobu.</span><span class="sxs-lookup"><span data-stu-id="c6e95-170">Returns an object representing a resource's runtime state.</span></span>

### <a name="parameters"></a><span data-ttu-id="c6e95-171">Parametry</span><span class="sxs-lookup"><span data-stu-id="c6e95-171">Parameters</span></span>

| <span data-ttu-id="c6e95-172">Parametr</span><span class="sxs-lookup"><span data-stu-id="c6e95-172">Parameter</span></span> | <span data-ttu-id="c6e95-173">Wymagane</span><span class="sxs-lookup"><span data-stu-id="c6e95-173">Required</span></span> | <span data-ttu-id="c6e95-174">Typ</span><span class="sxs-lookup"><span data-stu-id="c6e95-174">Type</span></span> | <span data-ttu-id="c6e95-175">Opis</span><span class="sxs-lookup"><span data-stu-id="c6e95-175">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c6e95-176">resourceName lub resourceIdentifier</span><span class="sxs-lookup"><span data-stu-id="c6e95-176">resourceName or resourceIdentifier</span></span> |<span data-ttu-id="c6e95-177">Tak</span><span class="sxs-lookup"><span data-stu-id="c6e95-177">Yes</span></span> |<span data-ttu-id="c6e95-178">Ciąg</span><span class="sxs-lookup"><span data-stu-id="c6e95-178">string</span></span> |<span data-ttu-id="c6e95-179">Nazwa lub identyfikator zasobu.</span><span class="sxs-lookup"><span data-stu-id="c6e95-179">Name or unique identifier of a resource.</span></span> |
| <span data-ttu-id="c6e95-180">apiVersion</span><span class="sxs-lookup"><span data-stu-id="c6e95-180">apiVersion</span></span> |<span data-ttu-id="c6e95-181">Nie</span><span class="sxs-lookup"><span data-stu-id="c6e95-181">No</span></span> |<span data-ttu-id="c6e95-182">Ciąg</span><span class="sxs-lookup"><span data-stu-id="c6e95-182">string</span></span> |<span data-ttu-id="c6e95-183">Wersja interfejsu API hello określony zasób.</span><span class="sxs-lookup"><span data-stu-id="c6e95-183">API version of hello specified resource.</span></span> <span data-ttu-id="c6e95-184">Ten parametr jest uwzględniony, gdy nie zainicjowano hello zasobów w ramach tego samego szablonu.</span><span class="sxs-lookup"><span data-stu-id="c6e95-184">Include this parameter when hello resource is not provisioned within same template.</span></span> <span data-ttu-id="c6e95-185">Zazwyczaj w formacie hello **rrrr mm-dd**.</span><span class="sxs-lookup"><span data-stu-id="c6e95-185">Typically, in hello format, **yyyy-mm-dd**.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c6e95-186">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="c6e95-186">Return value</span></span>

<span data-ttu-id="c6e95-187">Każdy typ zasobu zwraca inne właściwości hello odwołanie do funkcji.</span><span class="sxs-lookup"><span data-stu-id="c6e95-187">Every resource type returns different properties for hello reference function.</span></span> <span data-ttu-id="c6e95-188">Funkcja Hello nie zwraca jednego, wstępnie zdefiniowanego formatu.</span><span class="sxs-lookup"><span data-stu-id="c6e95-188">hello function does not return a single, predefined format.</span></span> <span data-ttu-id="c6e95-189">Obiekt hello w hello generuje sekcji, jak pokazano w przykładzie hello zwrotu toosee hello właściwości dla typu zasobu.</span><span class="sxs-lookup"><span data-stu-id="c6e95-189">toosee hello properties for a resource type, return hello object in hello outputs section as shown in hello example.</span></span>

### <a name="remarks"></a><span data-ttu-id="c6e95-190">Uwagi</span><span class="sxs-lookup"><span data-stu-id="c6e95-190">Remarks</span></span>

<span data-ttu-id="c6e95-191">Hello odwołanie funkcji pochodzi wartość ze stanu środowiska uruchomieniowego i nie można użyć w sekcji zmiennych hello.</span><span class="sxs-lookup"><span data-stu-id="c6e95-191">hello reference function derives its value from a runtime state, and therefore cannot be used in hello variables section.</span></span> <span data-ttu-id="c6e95-192">Można go w sekcji danych wyjściowych szablonu.</span><span class="sxs-lookup"><span data-stu-id="c6e95-192">It can be used in outputs section of a template.</span></span> 

<span data-ttu-id="c6e95-193">Funkcja odwołanie hello niejawnie deklarowaniu czy jeden zasób jest zależny od innego zasobu, jeśli hello odwołuje się do zasobu jest udostępniony w ramach tego samego szablonu.</span><span class="sxs-lookup"><span data-stu-id="c6e95-193">By using hello reference function, you implicitly declare that one resource depends on another resource if hello referenced resource is provisioned within same template.</span></span> <span data-ttu-id="c6e95-194">Nie trzeba tooalso Użyj hello dependsOn właściwości.</span><span class="sxs-lookup"><span data-stu-id="c6e95-194">You do not need tooalso use hello dependsOn property.</span></span> <span data-ttu-id="c6e95-195">Witaj funkcja nie jest oceniany, dopóki nie zakończy się hello zasobu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="c6e95-195">hello function is not evaluated until hello referenced resource has completed deployment.</span></span>

<span data-ttu-id="c6e95-196">toosee hello nazwy i wartości właściwości dla typu zasobu, utworzyć szablon, który zwraca obiekt hello w sekcji danych wyjściowych hello.</span><span class="sxs-lookup"><span data-stu-id="c6e95-196">toosee hello property names and values for a resource type, create a template that returns hello object in hello outputs section.</span></span> <span data-ttu-id="c6e95-197">Jeśli masz istniejący zasób tego typu do szablonu zwraca obiekt hello bez wdrażania żadnych nowych zasobów.</span><span class="sxs-lookup"><span data-stu-id="c6e95-197">If you have an existing resource of that type, your template returns hello object without deploying any new resources.</span></span> 

<span data-ttu-id="c6e95-198">Należy zwykle użyć hello **odwołania** funkcji tooreturn określonej wartości z obiektu, na przykład hello identyfikator URI punktu końcowego obiektu blob lub w pełni kwalifikowaną nazwę domeny.</span><span class="sxs-lookup"><span data-stu-id="c6e95-198">Typically, you use hello **reference** function tooreturn a particular value from an object, such as hello blob endpoint URI or fully qualified domain name.</span></span>

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

### <a name="example"></a><span data-ttu-id="c6e95-199">Przykład</span><span class="sxs-lookup"><span data-stu-id="c6e95-199">Example</span></span>

<span data-ttu-id="c6e95-200">Dokumentacja i toodeploy zasobu hello w hello tego samego szablonu, użyj:</span><span class="sxs-lookup"><span data-stu-id="c6e95-200">toodeploy and reference hello resource in hello same template, use:</span></span>

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

<span data-ttu-id="c6e95-201">Witaj poprzednim przykładzie zwraca obiekt hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="c6e95-201">hello preceding example returns an object in hello following format:</span></span>

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

<span data-ttu-id="c6e95-202">Witaj poniższy przykład odwołuje się do konta magazynu, który nie jest wdrożony w tym szablonie.</span><span class="sxs-lookup"><span data-stu-id="c6e95-202">hello following example references a storage account that is not deployed in this template.</span></span> <span data-ttu-id="c6e95-203">Witaj konto magazynu już istnieje w ramach hello same grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="c6e95-203">hello storage account already exists within hello same resource group.</span></span>

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

## <a name="resourcegroup"></a><span data-ttu-id="c6e95-204">Grupa zasobów</span><span class="sxs-lookup"><span data-stu-id="c6e95-204">resourceGroup</span></span>
`resourceGroup()`

<span data-ttu-id="c6e95-205">Zwraca obiekt reprezentujący hello bieżącej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="c6e95-205">Returns an object that represents hello current resource group.</span></span> 

### <a name="return-value"></a><span data-ttu-id="c6e95-206">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="c6e95-206">Return value</span></span>

<span data-ttu-id="c6e95-207">Witaj zwrócony obiekt jest zgodny z formatem hello:</span><span class="sxs-lookup"><span data-stu-id="c6e95-207">hello returned object is in hello following format:</span></span>

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

### <a name="remarks"></a><span data-ttu-id="c6e95-208">Uwagi</span><span class="sxs-lookup"><span data-stu-id="c6e95-208">Remarks</span></span>

<span data-ttu-id="c6e95-209">Zazwyczaj hello funkcji grupa zasobów jest używane zasoby toocreate w hello tej samej lokalizacji co hello grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="c6e95-209">A common use of hello resourceGroup function is toocreate resources in hello same location as hello resource group.</span></span> <span data-ttu-id="c6e95-210">Witaj poniższym przykładzie użyto lokalizacja hello tooassign lokalizacji hello grupy zasobów dla witryny sieci web.</span><span class="sxs-lookup"><span data-stu-id="c6e95-210">hello following example uses hello resource group location tooassign hello location for a web site.</span></span>

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

### <a name="example"></a><span data-ttu-id="c6e95-211">Przykład</span><span class="sxs-lookup"><span data-stu-id="c6e95-211">Example</span></span>

<span data-ttu-id="c6e95-212">Witaj następujący szablon zwraca hello właściwości hello grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="c6e95-212">hello following template returns hello properties of hello resource group.</span></span>

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

<span data-ttu-id="c6e95-213">Witaj poprzednim przykładzie zwraca obiekt hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="c6e95-213">hello preceding example returns an object in hello following format:</span></span>

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

## <a name="resourceid"></a><span data-ttu-id="c6e95-214">resourceId</span><span class="sxs-lookup"><span data-stu-id="c6e95-214">resourceId</span></span>
`resourceId([subscriptionId], [resourceGroupName], resourceType, resourceName1, [resourceName2]...)`

<span data-ttu-id="c6e95-215">Zwraca hello Unikatowy identyfikator zasobu.</span><span class="sxs-lookup"><span data-stu-id="c6e95-215">Returns hello unique identifier of a resource.</span></span> <span data-ttu-id="c6e95-216">Aby użyć tej funkcji, gdy nazwa zasobu hello jest niejednoznaczny lub nie jest inicjowana w hello tego samego szablonu.</span><span class="sxs-lookup"><span data-stu-id="c6e95-216">You use this function when hello resource name is ambiguous or not provisioned within hello same template.</span></span> 

### <a name="parameters"></a><span data-ttu-id="c6e95-217">Parametry</span><span class="sxs-lookup"><span data-stu-id="c6e95-217">Parameters</span></span>

| <span data-ttu-id="c6e95-218">Parametr</span><span class="sxs-lookup"><span data-stu-id="c6e95-218">Parameter</span></span> | <span data-ttu-id="c6e95-219">Wymagane</span><span class="sxs-lookup"><span data-stu-id="c6e95-219">Required</span></span> | <span data-ttu-id="c6e95-220">Typ</span><span class="sxs-lookup"><span data-stu-id="c6e95-220">Type</span></span> | <span data-ttu-id="c6e95-221">Opis</span><span class="sxs-lookup"><span data-stu-id="c6e95-221">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c6e95-222">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="c6e95-222">subscriptionId</span></span> |<span data-ttu-id="c6e95-223">Nie</span><span class="sxs-lookup"><span data-stu-id="c6e95-223">No</span></span> |<span data-ttu-id="c6e95-224">ciąg (format identyfikatora GUID w)</span><span class="sxs-lookup"><span data-stu-id="c6e95-224">string (In GUID format)</span></span> |<span data-ttu-id="c6e95-225">Wartość domyślna to hello bieżącej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="c6e95-225">Default value is hello current subscription.</span></span> <span data-ttu-id="c6e95-226">Należy podać tę wartość, gdy będziesz potrzebować tooretrieve zasobów w innej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="c6e95-226">Specify this value when you need tooretrieve a resource in another subscription.</span></span> |
| <span data-ttu-id="c6e95-227">Grupy zasobów o nazwie</span><span class="sxs-lookup"><span data-stu-id="c6e95-227">resourceGroupName</span></span> |<span data-ttu-id="c6e95-228">Nie</span><span class="sxs-lookup"><span data-stu-id="c6e95-228">No</span></span> |<span data-ttu-id="c6e95-229">Ciąg</span><span class="sxs-lookup"><span data-stu-id="c6e95-229">string</span></span> |<span data-ttu-id="c6e95-230">Wartość domyślna to bieżącej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="c6e95-230">Default value is current resource group.</span></span> <span data-ttu-id="c6e95-231">Należy podać tę wartość, gdy będziesz potrzebować tooretrieve zasobów w innej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="c6e95-231">Specify this value when you need tooretrieve a resource in another resource group.</span></span> |
| <span data-ttu-id="c6e95-232">Typ zasobu</span><span class="sxs-lookup"><span data-stu-id="c6e95-232">resourceType</span></span> |<span data-ttu-id="c6e95-233">Tak</span><span class="sxs-lookup"><span data-stu-id="c6e95-233">Yes</span></span> |<span data-ttu-id="c6e95-234">Ciąg</span><span class="sxs-lookup"><span data-stu-id="c6e95-234">string</span></span> |<span data-ttu-id="c6e95-235">Typ zasobu, włącznie z przestrzenią nazw dostawcy zasobów.</span><span class="sxs-lookup"><span data-stu-id="c6e95-235">Type of resource including resource provider namespace.</span></span> |
| <span data-ttu-id="c6e95-236">resourceName1</span><span class="sxs-lookup"><span data-stu-id="c6e95-236">resourceName1</span></span> |<span data-ttu-id="c6e95-237">Tak</span><span class="sxs-lookup"><span data-stu-id="c6e95-237">Yes</span></span> |<span data-ttu-id="c6e95-238">Ciąg</span><span class="sxs-lookup"><span data-stu-id="c6e95-238">string</span></span> |<span data-ttu-id="c6e95-239">Nazwa zasobu.</span><span class="sxs-lookup"><span data-stu-id="c6e95-239">Name of resource.</span></span> |
| <span data-ttu-id="c6e95-240">resourceName2</span><span class="sxs-lookup"><span data-stu-id="c6e95-240">resourceName2</span></span> |<span data-ttu-id="c6e95-241">Nie</span><span class="sxs-lookup"><span data-stu-id="c6e95-241">No</span></span> |<span data-ttu-id="c6e95-242">Ciąg</span><span class="sxs-lookup"><span data-stu-id="c6e95-242">string</span></span> |<span data-ttu-id="c6e95-243">Następny nazwy segmentu zasobu, jeśli zasób jest zagnieżdżony.</span><span class="sxs-lookup"><span data-stu-id="c6e95-243">Next resource name segment if resource is nested.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c6e95-244">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="c6e95-244">Return value</span></span>

<span data-ttu-id="c6e95-245">Identyfikator Hello jest zwracany w hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="c6e95-245">hello identifier is returned in hello following format:</span></span>

```json
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{resourceType}/{resourceName}
```

### <a name="remarks"></a><span data-ttu-id="c6e95-246">Uwagi</span><span class="sxs-lookup"><span data-stu-id="c6e95-246">Remarks</span></span>

<span data-ttu-id="c6e95-247">Hello można określić wartości parametrów są zależne od tego, czy zasób hello jest hello tej samej subskrypcji i zasobu grupy jako hello bieżącego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="c6e95-247">hello parameter values you specify depend on whether hello resource is in hello same subscription and resource group as hello current deployment.</span></span>

<span data-ttu-id="c6e95-248">tooget hello zasobów identyfikator dla konta magazynu w hello sam subskrypcji i grupy zasobów, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="c6e95-248">tooget hello resource ID for a storage account in hello same subscription and resource group, use:</span></span>

```json
"[resourceId('Microsoft.Storage/storageAccounts','examplestorage')]"
```

<span data-ttu-id="c6e95-249">Identyfikator zasobu hello tooget dla konta magazynu w hello tej samej subskrypcji, ale innej grupie zasobów, użyj:</span><span class="sxs-lookup"><span data-stu-id="c6e95-249">tooget hello resource ID for a storage account in hello same subscription but a different resource group, use:</span></span>

```json
"[resourceId('otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

<span data-ttu-id="c6e95-250">Identyfikator zasobu hello tooget dla konta magazynu w innej subskrypcji i grupy zasobów, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="c6e95-250">tooget hello resource ID for a storage account in a different subscription and resource group, use:</span></span>

```json
"[resourceId('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

<span data-ttu-id="c6e95-251">Identyfikator zasobu hello tooget bazy danych w innej grupie zasobów, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="c6e95-251">tooget hello resource ID for a database in a different resource group, use:</span></span>

```json
"[resourceId('otherResourceGroup', 'Microsoft.SQL/servers/databases', parameters('serverName'), parameters('databaseName'))]"
```

<span data-ttu-id="c6e95-252">Często potrzebne toouse tej funkcji za pomocą konta magazynu lub sieci wirtualnej w grupie zasobów alternatywny.</span><span class="sxs-lookup"><span data-stu-id="c6e95-252">Often, you need toouse this function when using a storage account or virtual network in an alternate resource group.</span></span> <span data-ttu-id="c6e95-253">Witaj poniższy przykład przedstawia zasobu z grupy zasobów zewnętrznych można łatwo użycia:</span><span class="sxs-lookup"><span data-stu-id="c6e95-253">hello following example shows how a resource from an external resource group can easily be used:</span></span>

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

### <a name="example"></a><span data-ttu-id="c6e95-254">Przykład</span><span class="sxs-lookup"><span data-stu-id="c6e95-254">Example</span></span>

<span data-ttu-id="c6e95-255">Witaj poniższy przykład zwraca identyfikator zasobu powitania dla konta magazynu w grupie zasobów hello:</span><span class="sxs-lookup"><span data-stu-id="c6e95-255">hello following example returns hello resource ID for a storage account in hello resource group:</span></span>

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

<span data-ttu-id="c6e95-256">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="c6e95-256">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="c6e95-257">Nazwa</span><span class="sxs-lookup"><span data-stu-id="c6e95-257">Name</span></span> | <span data-ttu-id="c6e95-258">Typ</span><span class="sxs-lookup"><span data-stu-id="c6e95-258">Type</span></span> | <span data-ttu-id="c6e95-259">Wartość</span><span class="sxs-lookup"><span data-stu-id="c6e95-259">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c6e95-260">sameRGOutput</span><span class="sxs-lookup"><span data-stu-id="c6e95-260">sameRGOutput</span></span> | <span data-ttu-id="c6e95-261">Ciąg</span><span class="sxs-lookup"><span data-stu-id="c6e95-261">String</span></span> | <span data-ttu-id="c6e95-262">/Subscriptions/{Current-Sub-ID}/resourceGroups/examplegroup/Providers/Microsoft.Storage/storageAccounts/examplestorage</span><span class="sxs-lookup"><span data-stu-id="c6e95-262">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span></span> |
| <span data-ttu-id="c6e95-263">differentRGOutput</span><span class="sxs-lookup"><span data-stu-id="c6e95-263">differentRGOutput</span></span> | <span data-ttu-id="c6e95-264">Ciąg</span><span class="sxs-lookup"><span data-stu-id="c6e95-264">String</span></span> | <span data-ttu-id="c6e95-265">/Subscriptions/{Current-Sub-ID}/resourceGroups/otherResourceGroup/Providers/Microsoft.Storage/storageAccounts/examplestorage</span><span class="sxs-lookup"><span data-stu-id="c6e95-265">/subscriptions/{current-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span></span> |
| <span data-ttu-id="c6e95-266">differentSubOutput</span><span class="sxs-lookup"><span data-stu-id="c6e95-266">differentSubOutput</span></span> | <span data-ttu-id="c6e95-267">Ciąg</span><span class="sxs-lookup"><span data-stu-id="c6e95-267">String</span></span> | <span data-ttu-id="c6e95-268">/Subscriptions/{different-Sub-ID}/resourceGroups/otherResourceGroup/Providers/Microsoft.Storage/storageAccounts/examplestorage</span><span class="sxs-lookup"><span data-stu-id="c6e95-268">/subscriptions/{different-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span></span> |
| <span data-ttu-id="c6e95-269">nestedResourceOutput</span><span class="sxs-lookup"><span data-stu-id="c6e95-269">nestedResourceOutput</span></span> | <span data-ttu-id="c6e95-270">Ciąg</span><span class="sxs-lookup"><span data-stu-id="c6e95-270">String</span></span> | <span data-ttu-id="c6e95-271">/Subscriptions/{Current-Sub-ID}/resourceGroups/examplegroup/Providers/Microsoft.SQL/Servers/serverName/Databases/databaseName</span><span class="sxs-lookup"><span data-stu-id="c6e95-271">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.SQL/servers/serverName/databases/databaseName</span></span> |

<a id="subscription" />

## <a name="subscription"></a><span data-ttu-id="c6e95-272">subskrypcja</span><span class="sxs-lookup"><span data-stu-id="c6e95-272">subscription</span></span>
`subscription()`

<span data-ttu-id="c6e95-273">Zwraca szczegółowe informacje o subskrypcji hello hello bieżące wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="c6e95-273">Returns details about hello subscription for hello current deployment.</span></span> 

### <a name="return-value"></a><span data-ttu-id="c6e95-274">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="c6e95-274">Return value</span></span>

<span data-ttu-id="c6e95-275">Witaj, funkcja zwraca hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="c6e95-275">hello function returns hello following format:</span></span>

```json
{
    "id": "/subscriptions/{subscription-id}",
    "subscriptionId": "{subscription-id}",
    "tenantId": "{tenant-id}",
    "displayName": "{name-of-subscription}"
}
```

### <a name="example"></a><span data-ttu-id="c6e95-276">Przykład</span><span class="sxs-lookup"><span data-stu-id="c6e95-276">Example</span></span>

<span data-ttu-id="c6e95-277">Witaj poniższy przykład przedstawia hello subskrypcji funkcji o nazwie w sekcji danych wyjściowych hello.</span><span class="sxs-lookup"><span data-stu-id="c6e95-277">hello following example shows hello subscription function called in hello outputs section.</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="c6e95-278">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c6e95-278">Next steps</span></span>
* <span data-ttu-id="c6e95-279">Aby uzyskać opis hello części szablonu usługi Azure Resource Manager, zobacz [szablonów Authoring Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="c6e95-279">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="c6e95-280">Zobacz wielu szablonów toomerge [za pomocą szablonów połączonych z usługą Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="c6e95-280">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="c6e95-281">tooiterate określoną liczbę razy podczas tworzenia typu zasobu, zobacz [utworzyć wiele wystąpień zasobów usługi Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="c6e95-281">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="c6e95-282">toosee toodeploy hello szablonu po utworzeniu, zobacz [wdrażania aplikacji przy użyciu szablonu usługi Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="c6e95-282">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

