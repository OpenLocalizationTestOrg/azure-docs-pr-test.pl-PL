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
# <a name="deployment-functions-for-azure-resource-manager-templates"></a>Funkcje wdrażania dla szablonów usługi Azure Resource Manager 

Usługa Resource Manager zapewnia hello następujące funkcje do pobierania wartości z części szablonu hello i wartości wdrożenia toohello pokrewne:

* [wdrożenia](#deployment)
* [Parametry](#parameters)
* [zmienne](#variables)

wartości tooget z zasobów, grupy zasobów lub subskrypcji, zobacz [funkcji zasobów](resource-group-template-functions-resource.md).

<a id="deployment" />

## <a name="deployment"></a>wdrożenie
`deployment()`

Zwraca informacje o hello bieżącej operacji wdrożenia.

### <a name="return-value"></a>Wartość zwracana

Ta funkcja zwraca obiekt hello, który jest przekazywany podczas wdrażania. właściwości Hello w hello zwrócił obiekt się różnić w zależności od tego, czy hello obiektu wdrożenia jest przekazywany jako łącze lub obiekt w wierszu. Gdy obiektu wdrożenia hello jest przekazywany w zewnętrznych, takich jak przy użyciu hello **- TemplateFile** parametru w toopoint programu Azure PowerShell tooa pliku lokalnego, hello zwrócony obiekt ma hello następującego formatu:

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

Gdy obiekt hello jest przekazywany jako łącze, takie jak kiedy hello przy użyciu **- TemplateUri** obiektu zdalnego tooa toopoint parametru hello obiekt jest zwracany w hello następującego formatu: 

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

### <a name="remarks"></a>Uwagi

Można użyć szablonu tooanother toolink deployment() opartego na powitania URI szablonu nadrzędnego hello.

```json
"variables": {  
    "sharedTemplateUrl": "[uri(deployment().properties.templateLink.uri, 'shared-resources.json')]"  
}
```  

### <a name="example"></a>Przykład

Witaj poniższy przykład zwraca obiekt wdrożenia hello:

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

Witaj poprzednim przykładzie zwraca hello następującego obiektu:

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

## <a name="parameters"></a>parameters
`parameters(parameterName)`

Zwraca wartość parametru. Witaj określona nazwa parametru musi być zdefiniowany w sekcji parametrów hello hello szablonu.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| Nazwa parametru |Tak |Ciąg |Nazwa Hello hello tooreturn parametru. |

### <a name="return-value"></a>Wartość zwracana

wartość Hello hello określony parametr.

### <a name="remarks"></a>Uwagi

Należy zwykle użyć wartości zasobów tooset parametrów. Witaj poniższy przykład przedstawia hello nazwa witryny sieci web toohello wartość parametru w podczas wdrażania.

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

### <a name="example"></a>Przykład

Witaj poniższym przykładzie pokazano uproszczony Użyj hello parametrów funkcji.

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

przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| stringOutput | Ciąg | Opcja 1 |
| intOutput | int | 1 |
| objectOutput | Obiekt | {"jeden": "", "2": "b"} |
| arrayOutput | Tablica | [1, 2, 3] |
| crossOutput | Ciąg | Opcja 1 |

<a id="variables" />

## <a name="variables"></a>zmienne
`variables(variableName)`

Zwraca hello wartość zmiennej. Określona nazwa zmiennej Hello muszą być zdefiniowane w sekcji zmiennych hello hello szablonu.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| nazwa_zmiennej |Tak |Ciąg |Nazwa Hello hello tooreturn zmiennej. |

### <a name="return-value"></a>Wartość zwracana

wartość Hello hello określonej zmiennej.

### <a name="remarks"></a>Uwagi

Należy zwykle użyć, toosimplify zmiennych szablonu tworząc wartości złożonych tylko raz. Witaj poniższy przykład tworzy unikatową nazwę konta magazynu.

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

### <a name="example"></a>Przykład

Szablon przykład Hello zwraca różne wartości zmiennej.

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

przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| exampleOutput1 | Ciąg | myVariable |
| exampleOutput2 | Tablica | [1, 2, 3, 4] |
| exampleOutput3 | Ciąg | myVariable |
| exampleOutput4 |  Obiekt | {"właściwości property1": "wartość1", "property2": "wartość2"} |

## <a name="next-steps"></a>Następne kroki
* Aby uzyskać opis hello części szablonu usługi Azure Resource Manager, zobacz [szablonów Authoring Azure Resource Manager](resource-group-authoring-templates.md).
* Zobacz wielu szablonów toomerge [za pomocą szablonów połączonych z usługą Azure Resource Manager](resource-group-linked-templates.md).
* tooiterate określoną liczbę razy podczas tworzenia typu zasobu, zobacz [utworzyć wiele wystąpień zasobów usługi Azure Resource Manager](resource-group-create-multiple.md).
* toosee toodeploy hello szablonu po utworzeniu, zobacz [wdrażania aplikacji przy użyciu szablonu usługi Azure Resource Manager](resource-group-template-deploy.md).

