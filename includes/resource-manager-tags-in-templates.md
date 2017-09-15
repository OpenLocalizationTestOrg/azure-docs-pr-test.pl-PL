<span data-ttu-id="98537-101">Aby oznaczyć zasób podczas wdrażania, do wdrażanego zasobu dodaj element `tags`.</span><span class="sxs-lookup"><span data-stu-id="98537-101">To tag a resource during deployment, add the `tags` element to the resource you are deploying.</span></span> <span data-ttu-id="98537-102">Podaj nazwę i wartość tagu.</span><span class="sxs-lookup"><span data-stu-id="98537-102">Provide the tag name and value.</span></span>

### <a name="apply-a-literal-value-to-the-tag-name"></a><span data-ttu-id="98537-103">Stosowanie wartości literału do nazwy tagu</span><span class="sxs-lookup"><span data-stu-id="98537-103">Apply a literal value to the tag name</span></span>
<span data-ttu-id="98537-104">W poniższym przykładzie przedstawiono konto magazynu z dwoma tagami (`Dept` i `Environment`), dla których ustawiono wartości literału:</span><span class="sxs-lookup"><span data-stu-id="98537-104">The following example shows a storage account with two tags (`Dept` and `Environment`) that are set to literal values:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat('storage', uniqueString(resourceGroup().id))]",
      "location": "[resourceGroup().location]",
      "tags": {
        "Dept": "Finance",
        "Environment": "Production"
      },
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": { }
    }
    ]
}
```

### <a name="apply-an-object-to-the-tag-element"></a><span data-ttu-id="98537-105">Stosowanie obiektu do elementu tagu</span><span class="sxs-lookup"><span data-stu-id="98537-105">Apply an object to the tag element</span></span>
<span data-ttu-id="98537-106">Możesz zdefiniować parametr obiektu przechowującego kilka tagów i zastosować ten obiekt do elementu tagu.</span><span class="sxs-lookup"><span data-stu-id="98537-106">You can define an object parameter that stores several tags, and apply that object to the tag element.</span></span> <span data-ttu-id="98537-107">Każda właściwość obiektu będzie osobnym tagiem dla zasobu.</span><span class="sxs-lookup"><span data-stu-id="98537-107">Each property in the object becomes a separate tag for the resource.</span></span> <span data-ttu-id="98537-108">Poniższy przykład zawiera parametr o nazwie `tagValues`, który został zastosowany do elementu tagu.</span><span class="sxs-lookup"><span data-stu-id="98537-108">The following example has a parameter named `tagValues` that is applied to the tag element.</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "tagValues": {
      "type": "object",
      "defaultValue": {
        "Dept": "Finance",
        "Environment": "Production"
      }
    }
  },
  "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat('storage', uniqueString(resourceGroup().id))]",
      "location": "[resourceGroup().location]",
      "tags": "[parameters('tagValues')]",
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": {}
    }
  ]
}
```

### <a name="apply-a-json-string-to-the-tag-name"></a><span data-ttu-id="98537-109">Stosowanie ciągu JSON do nazwy tagu</span><span class="sxs-lookup"><span data-stu-id="98537-109">Apply a JSON string to the tag name</span></span>

<span data-ttu-id="98537-110">Aby przechowywać wiele wartości w jednym tagu, zastosuj ciąg JSON reprezentujący te wartości.</span><span class="sxs-lookup"><span data-stu-id="98537-110">To store many values in a single tag, apply a JSON string that represents the values.</span></span> <span data-ttu-id="98537-111">Cały ciąg JSON jest przechowywany jako jeden tag, który nie może przekraczać 256 znaków.</span><span class="sxs-lookup"><span data-stu-id="98537-111">The entire JSON string is stored as one tag that cannot exceed 256 characters.</span></span> <span data-ttu-id="98537-112">Poniższy przykład zawiera pojedynczy tag o nazwie `CostCenter`, który zawiera kilka wartości z ciągu JSON:</span><span class="sxs-lookup"><span data-stu-id="98537-112">The following example has a single tag named `CostCenter` that contains several values from a JSON string:</span></span>  

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat('storage', uniqueString(resourceGroup().id))]",
      "location": "[resourceGroup().location]",
      "tags": {
        "CostCenter": "{\"Dept\":\"Finance\",\"Environment\":\"Production\"}"
      },
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": { }
    }
    ]
}
```