tootag zasobów podczas wdrażania, Dodaj hello `tags` elementu toohello zasobów są wdrażane. Podaj nazwę tagu hello i wartość.

### <a name="apply-a-literal-value-toohello-tag-name"></a>Zastosuj nazwę znacznika toohello wartość literału
Witaj poniższy przykład przedstawia konto magazynu z dwoma tagami (`Dept` i `Environment`) ustawionych tooliteral wartości:

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

### <a name="apply-an-object-toohello-tag-element"></a>Zastosuj element tag toohello obiektu
Można określić parametr obiektu, który przechowuje kilka tagów i zastosować tego elementu tag toohello obiektu. Każdej właściwości w obiekcie hello staje się oddzielne tag hello zasobu. Witaj poniższym przykładzie ma parametr o nazwie `tagValues` czyli element tagów toohello zastosowane.

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

### <a name="apply-a-json-string-toohello-tag-name"></a>Zastosuj nazwy tagu toohello ciągu JSON

toostore ciąg JSON, który reprezentuje wartości hello zastosowanie wielu wartości w jeden tag. cały ciąg JSON Hello jest przechowywana jako jeden tag, który nie może być dłuższa niż 256 znaków. Witaj poniższym przykładzie przedstawiono jeden tag o nazwie `CostCenter` zawiera kilka wartości z ciągu JSON:  

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