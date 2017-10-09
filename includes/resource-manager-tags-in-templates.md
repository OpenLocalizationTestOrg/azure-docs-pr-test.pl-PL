<span data-ttu-id="ea79e-101">tootag zasobów podczas wdrażania, Dodaj hello `tags` elementu toohello zasobów są wdrażane.</span><span class="sxs-lookup"><span data-stu-id="ea79e-101">tootag a resource during deployment, add hello `tags` element toohello resource you are deploying.</span></span> <span data-ttu-id="ea79e-102">Podaj nazwę tagu hello i wartość.</span><span class="sxs-lookup"><span data-stu-id="ea79e-102">Provide hello tag name and value.</span></span>

### <a name="apply-a-literal-value-toohello-tag-name"></a><span data-ttu-id="ea79e-103">Zastosuj nazwę znacznika toohello wartość literału</span><span class="sxs-lookup"><span data-stu-id="ea79e-103">Apply a literal value toohello tag name</span></span>
<span data-ttu-id="ea79e-104">Witaj poniższy przykład przedstawia konto magazynu z dwoma tagami (`Dept` i `Environment`) ustawionych tooliteral wartości:</span><span class="sxs-lookup"><span data-stu-id="ea79e-104">hello following example shows a storage account with two tags (`Dept` and `Environment`) that are set tooliteral values:</span></span>

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

### <a name="apply-an-object-toohello-tag-element"></a><span data-ttu-id="ea79e-105">Zastosuj element tag toohello obiektu</span><span class="sxs-lookup"><span data-stu-id="ea79e-105">Apply an object toohello tag element</span></span>
<span data-ttu-id="ea79e-106">Można określić parametr obiektu, który przechowuje kilka tagów i zastosować tego elementu tag toohello obiektu.</span><span class="sxs-lookup"><span data-stu-id="ea79e-106">You can define an object parameter that stores several tags, and apply that object toohello tag element.</span></span> <span data-ttu-id="ea79e-107">Każdej właściwości w obiekcie hello staje się oddzielne tag hello zasobu.</span><span class="sxs-lookup"><span data-stu-id="ea79e-107">Each property in hello object becomes a separate tag for hello resource.</span></span> <span data-ttu-id="ea79e-108">Witaj poniższym przykładzie ma parametr o nazwie `tagValues` czyli element tagów toohello zastosowane.</span><span class="sxs-lookup"><span data-stu-id="ea79e-108">hello following example has a parameter named `tagValues` that is applied toohello tag element.</span></span>

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

### <a name="apply-a-json-string-toohello-tag-name"></a><span data-ttu-id="ea79e-109">Zastosuj nazwy tagu toohello ciągu JSON</span><span class="sxs-lookup"><span data-stu-id="ea79e-109">Apply a JSON string toohello tag name</span></span>

<span data-ttu-id="ea79e-110">toostore ciąg JSON, który reprezentuje wartości hello zastosowanie wielu wartości w jeden tag.</span><span class="sxs-lookup"><span data-stu-id="ea79e-110">toostore many values in a single tag, apply a JSON string that represents hello values.</span></span> <span data-ttu-id="ea79e-111">cały ciąg JSON Hello jest przechowywana jako jeden tag, który nie może być dłuższa niż 256 znaków.</span><span class="sxs-lookup"><span data-stu-id="ea79e-111">hello entire JSON string is stored as one tag that cannot exceed 256 characters.</span></span> <span data-ttu-id="ea79e-112">Witaj poniższym przykładzie przedstawiono jeden tag o nazwie `CostCenter` zawiera kilka wartości z ciągu JSON:</span><span class="sxs-lookup"><span data-stu-id="ea79e-112">hello following example has a single tag named `CostCenter` that contains several values from a JSON string:</span></span>  

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