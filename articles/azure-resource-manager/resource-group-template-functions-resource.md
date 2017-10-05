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
# <a name="resource-functions-for-azure-resource-manager-templates"></a>Funkcje zasobów dla szablonów usługi Azure Resource Manager

Usługa Resource Manager zapewnia następujące funkcje do pobierania wartości zasobu:

* [listKeys i listy {Value}](#listkeys)
* [dostawców](#providers)
* [Odwołanie](#reference)
* [Grupa zasobów](#resourcegroup)
* [Identyfikator zasobu](#resourceid)
* [Subskrypcja](#subscription)

Aby uzyskać wartości z parametrów, zmiennych lub bieżącego wdrożenia, zobacz [wdrożenia wartość funkcji](resource-group-template-functions-deployment.md).

<a id="listkeys" />
<a id="list" />

## <a name="listkeys-and-listvalue"></a>listKeys i listy {Value}
`listKeys(resourceName or resourceIdentifier, apiVersion)`

`list{Value}(resourceName or resourceIdentifier, apiVersion)`

Zwraca wartości dla dowolnego typu zasobu, który obsługuje operacja listy. Najbardziej typowe obciążenie jest `listKeys`. 

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| resourceName lub resourceIdentifier |Tak |Ciąg |Unikatowy identyfikator zasobu. |
| apiVersion |Tak |Ciąg |Wersja interfejsu API stanu środowiska uruchomieniowego zasobu. Zazwyczaj w formacie **rrrr mm-dd**. |

### <a name="return-value"></a>Wartość zwracana

Obiekt zwrócony z listKeys ma następujący format:

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

Inne funkcje listy mają różne formaty zwracany. Aby wyświetlić format funkcji, Uwzględnij go w sekcji danych wyjściowych jak pokazano w przykładzie szablonu. 

### <a name="remarks"></a>Uwagi

Żadnej operacji, która rozpoczyna się od **listy** mogą być używane jako funkcję w szablonie. Dostępne operacje zawiera nie tylko listKeys, ale również operacji, takich jak `list`, `listAdminKeys`, i `listStatus`. Nie można jednak użyć **listy** operacje, które wymagają wartości w treści żądania. Na przykład [SAS konta listy](/rest/api/storagerp/storageaccounts#StorageAccounts_ListAccountSAS) operacja wymaga parametrów treści żądania, takich jak *signedExpiry*, więc nie można go użyć w ramach szablonu.

Aby określić, jakie typy zasobów operacja listy, masz następujące opcje:

* Widok [operacje interfejsu API REST](/rest/api/) dla dostawcy zasobów, a następnie wyszukaj listę operacji. Na przykład mieć kont magazynu [operacji listKeys](/rest/api/storagerp/storageaccounts#StorageAccounts_ListKeys).
* Użyj [Get-AzureRmProviderOperation](/powershell/module/azurerm.resources/get-azurermprovideroperation) polecenia cmdlet programu PowerShell. Poniższy przykład pobiera wszystkie operacje listy kont magazynu:

  ```powershell
  Get-AzureRmProviderOperation -OperationSearchString "Microsoft.Storage/*" | where {$_.Operation -like "*list*"} | FT Operation
  ```
* Użyj następującego polecenia wiersza polecenia platformy Azure, aby filtrować tylko operacje listy:

  ```azurecli
  az provider operation show --namespace Microsoft.Storage --query "resourceTypes[?name=='storageAccounts'].operations[].name | [?contains(@, 'list')]"
  ```

Określ zasób, używając [funkcja resourceId](#resourceid), lub format `{providerNamespace}/{resourceType}/{resourceName}`.


### <a name="example"></a>Przykład

Poniższy przykład przedstawia sposób zwrócenia klucze podstawowe i pomocnicze z konta magazynu w sekcji danych wyjściowych.

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

## <a name="providers"></a>dostawców
`providers(providerNamespace, [resourceType])`

Zwraca informacje o dostawcy zasobów i jego obsługiwane typy zasobów. Jeśli typ zasobu nie zostanie określona, funkcja zwraca obsługiwane typy dla dostawcy zasobów.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| providerNamespace |Tak |Ciąg |Namespace dostawcy |
| Typ zasobu |Nie |Ciąg |Typ zasobu w określonej przestrzeni nazw. |

### <a name="return-value"></a>Wartość zwracana

Zwrócono każdego obsługiwanego typu w następującym formacie: 

```json
{
    "resourceType": "{name of resource type}",
    "locations": [ all supported locations ],
    "apiVersions": [ all supported API versions ]
}
```

Kolejność zwracanych wartości tablicy nie jest gwarantowana.

### <a name="example"></a>Przykład

Poniższy przykład przedstawia sposób użycia funkcji dostawcy:

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

Poprzedni przykład zwraca obiekt w następującym formacie:

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

## <a name="reference"></a>Odwołanie
`reference(resourceName or resourceIdentifier, [apiVersion])`

Zwraca obiekt reprezentujący stan czasu wykonywania zasobu.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| resourceName lub resourceIdentifier |Tak |Ciąg |Nazwa lub identyfikator zasobu. |
| apiVersion |Nie |Ciąg |Wersja interfejsu API określonego zasobu. Obejmują tego parametru, gdy zasób nie zostanie zainicjowana w ramach tego samego szablonu. Zazwyczaj w formacie **rrrr mm-dd**. |

### <a name="return-value"></a>Wartość zwracana

Każdy typ zasobu zwraca inne właściwości dla funkcji odwołania. Funkcja nie zwraca jednego, wstępnie zdefiniowanego formatu. Aby wyświetlić właściwości dla typu zasobu, zwracać obiekt w sekcji danych wyjściowych, jak pokazano w przykładzie.

### <a name="remarks"></a>Uwagi

Funkcja odwołanie pochodzi wartość ze stanu środowiska uruchomieniowego i nie można użyć w sekcji zmiennych. Można go w sekcji danych wyjściowych szablonu. 

Za pomocą funkcji odwołania, niejawnie deklarowaniu czy jeden zasób jest zależny od innego zasobu, jeśli przywoływany zasób jest udostępniony w ramach tego samego szablonu. Nie trzeba również użyć dependsOn właściwości. Funkcja nie jest oceniany, aż do zakończenia wdrażania żądanego zasobu.

Aby wyświetlić nazwy właściwości i wartości dla typu zasobu, należy utworzyć szablon, który zwraca obiekt, w sekcji danych wyjściowych. Jeśli masz istniejący zasób tego typu do szablonu zwraca obiekt bez wdrażania żadnych nowych zasobów. 

Zazwyczaj **odwołania** funkcja zwraca wartość określonego obiektu, na przykład obiektu blob identyfikatora URI punktu końcowego lub w pełni kwalifikowaną nazwę domeny.

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

### <a name="example"></a>Przykład

Aby wdrożyć i odwoływać się do zasobu w tym samym szablonie, należy użyć:

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

Poprzedni przykład zwraca obiekt w następującym formacie:

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

Poniższy przykład odwołuje się do konta magazynu, który nie jest wdrożony w tym szablonie. Konto magazynu już istnieje w tej samej grupie zasobów.

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

## <a name="resourcegroup"></a>Grupa zasobów
`resourceGroup()`

Zwraca obiekt reprezentujący bieżącej grupie zasobów. 

### <a name="return-value"></a>Wartość zwracana

Zwrócony obiekt jest w następującym formacie:

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

### <a name="remarks"></a>Uwagi

Użycia funkcji grupa zasobów ma tworzyć zasoby w tej samej lokalizacji co grupy zasobów. W poniższym przykładzie użyto lokalizacja grupy zasobów, aby przypisać lokalizacji dla witryny sieci web.

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

### <a name="example"></a>Przykład

Następujący szablon zwraca właściwości grupy zasobów.

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

Poprzedni przykład zwraca obiekt w następującym formacie:

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

## <a name="resourceid"></a>resourceId
`resourceId([subscriptionId], [resourceGroupName], resourceType, resourceName1, [resourceName2]...)`

Zwraca unikatowy identyfikator zasobu. Aby użyć tej funkcji, jeśli nazwa zasobu jest niejednoznaczny lub nie udostępnione w ramach tego samego szablonu. 

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| subscriptionId |Nie |ciąg (format identyfikatora GUID w) |Wartość domyślna to bieżącej subskrypcji. Należy podać tę wartość, gdy trzeba pobrać zasobu w innej subskrypcji. |
| Grupy zasobów o nazwie |Nie |Ciąg |Wartość domyślna to bieżącej grupie zasobów. Należy podać tę wartość, gdy trzeba pobrać zasobu w innej grupie zasobów. |
| Typ zasobu |Tak |Ciąg |Typ zasobu, włącznie z przestrzenią nazw dostawcy zasobów. |
| resourceName1 |Tak |Ciąg |Nazwa zasobu. |
| resourceName2 |Nie |Ciąg |Następny nazwy segmentu zasobu, jeśli zasób jest zagnieżdżony. |

### <a name="return-value"></a>Wartość zwracana

Identyfikator jest zwracany w następującym formacie:

```json
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{resourceType}/{resourceName}
```

### <a name="remarks"></a>Uwagi

Wartości parametrów, które określisz zależą od tego, czy zasób jest w tej samej grupie subskrypcji i zasobu jako bieżącego wdrożenia.

Aby uzyskać identyfikator zasobu dla konta magazynu w tej samej subskrypcji i grupy zasobów, należy użyć:

```json
"[resourceId('Microsoft.Storage/storageAccounts','examplestorage')]"
```

Aby uzyskać identyfikator zasobu dla konta magazynu w tej samej subskrypcji, ale innej grupie zasobów, należy użyć:

```json
"[resourceId('otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

Aby uzyskać identyfikator zasobu dla konta magazynu w innej subskrypcji i grupy zasobów, należy użyć:

```json
"[resourceId('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

Aby uzyskać identyfikator zasobu bazy danych w innej grupie zasobów, należy użyć:

```json
"[resourceId('otherResourceGroup', 'Microsoft.SQL/servers/databases', parameters('serverName'), parameters('databaseName'))]"
```

Często należy użyć tej funkcji, korzystając z konta magazynu lub sieci wirtualnej w grupie zasobów alternatywny. W poniższym przykładzie pokazano, jak łatwo można zasobu z grupy zasobów zewnętrznych:

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

### <a name="example"></a>Przykład

Poniższy przykład zwraca identyfikator zasobu dla konta magazynu w grupie zasobów:

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

Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| sameRGOutput | Ciąg | /Subscriptions/{Current-Sub-ID}/resourceGroups/examplegroup/Providers/Microsoft.Storage/storageAccounts/examplestorage |
| differentRGOutput | Ciąg | /Subscriptions/{Current-Sub-ID}/resourceGroups/otherResourceGroup/Providers/Microsoft.Storage/storageAccounts/examplestorage |
| differentSubOutput | Ciąg | /Subscriptions/{different-Sub-ID}/resourceGroups/otherResourceGroup/Providers/Microsoft.Storage/storageAccounts/examplestorage |
| nestedResourceOutput | Ciąg | /Subscriptions/{Current-Sub-ID}/resourceGroups/examplegroup/Providers/Microsoft.SQL/Servers/serverName/Databases/databaseName |

<a id="subscription" />

## <a name="subscription"></a>subskrypcja
`subscription()`

Zwraca szczegółowe informacje o subskrypcji dla bieżącego wdrożenia. 

### <a name="return-value"></a>Wartość zwracana

Funkcja zwraca następujący format:

```json
{
    "id": "/subscriptions/{subscription-id}",
    "subscriptionId": "{subscription-id}",
    "tenantId": "{tenant-id}",
    "displayName": "{name-of-subscription}"
}
```

### <a name="example"></a>Przykład

Poniższy przykład przedstawia funkcję subskrypcji o nazwie w sekcji danych wyjściowych. 

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

## <a name="next-steps"></a>Następne kroki
* Opis części szablonu usługi Azure Resource Manager, zobacz [szablonów Authoring Azure Resource Manager](resource-group-authoring-templates.md).
* Aby scalić wiele szablonów, zobacz [za pomocą szablonów połączonych z usługą Azure Resource Manager](resource-group-linked-templates.md).
* Do wykonywania iteracji określoną liczbę razy podczas tworzenia typu zasobu, zobacz [utworzyć wiele wystąpień zasobów usługi Azure Resource Manager](resource-group-create-multiple.md).
* Aby zobaczyć, jak wdrożyć szablon został utworzony, zobacz [wdrażania aplikacji przy użyciu szablonu usługi Azure Resource Manager](resource-group-template-deploy.md).

