Aby oznaczyć zasób podczas wdrażania, do wdrażanego zasobu dodaj element `tags`. Podaj nazwę i wartość tagu.

### <a name="apply-a-literal-value-to-the-tag-name"></a>Stosowanie wartości literału do nazwy tagu
W poniższym przykładzie przedstawiono konto magazynu z dwoma tagami (`Dept` i `Environment`), dla których ustawiono wartości literału:

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

### <a name="apply-an-object-to-the-tag-element"></a>Stosowanie obiektu do elementu tagu
Możesz zdefiniować parametr obiektu przechowującego kilka tagów i zastosować ten obiekt do elementu tagu. Każda właściwość obiektu będzie osobnym tagiem dla zasobu. Poniższy przykład zawiera parametr o nazwie `tagValues`, który został zastosowany do elementu tagu.

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

### <a name="apply-a-json-string-to-the-tag-name"></a>Stosowanie ciągu JSON do nazwy tagu

Aby przechowywać wiele wartości w jednym tagu, zastosuj ciąg JSON reprezentujący te wartości. Cały ciąg JSON jest przechowywany jako jeden tag, który nie może przekraczać 256 znaków. Poniższy przykład zawiera pojedynczy tag o nazwie `CostCenter`, który zawiera kilka wartości z ciągu JSON:  

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