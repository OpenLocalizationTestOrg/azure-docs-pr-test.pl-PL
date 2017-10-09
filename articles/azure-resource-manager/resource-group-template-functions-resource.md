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
# <a name="resource-functions-for-azure-resource-manager-templates"></a>Funkcje zasobów dla szablonów usługi Azure Resource Manager

Usługa Resource Manager zapewnia następujące funkcje do pobierania wartości zasobów hello:

* [listKeys i listy {Value}](#listkeys)
* [dostawców](#providers)
* [Odwołanie](#reference)
* [Grupa zasobów](#resourcegroup)
* [Identyfikator zasobu](#resourceid)
* [Subskrypcja](#subscription)

tooget wartości z parametrów, zmiennych lub hello bieżącego wdrożenia, zobacz [wdrożenia wartość funkcji](resource-group-template-functions-deployment.md).

<a id="listkeys" />
<a id="list" />

## <a name="listkeys-and-listvalue"></a>listKeys i listy {Value}
`listKeys(resourceName or resourceIdentifier, apiVersion)`

`list{Value}(resourceName or resourceIdentifier, apiVersion)`

Zwraca hello wartości dla dowolnego typu zasobu, który obsługuje hello listy operacji. najbardziej typowe użycie Hello jest `listKeys`. 

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| resourceName lub resourceIdentifier |Tak |Ciąg |Unikatowy identyfikator zasobu hello. |
| apiVersion |Tak |Ciąg |Wersja interfejsu API stanu środowiska uruchomieniowego zasobu. Zazwyczaj w formacie hello **rrrr mm-dd**. |

### <a name="return-value"></a>Wartość zwracana

Witaj zwracany obiekt listKeys ma hello następującego formatu:

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

Inne funkcje listy mają różne formaty zwracany. format hello toosee funkcji, uwzględnić go w sekcji danych wyjściowych hello, jak pokazano w szablonie przykład hello. 

### <a name="remarks"></a>Uwagi

Żadnej operacji, która rozpoczyna się od **listy** mogą być używane jako funkcję w szablonie. Witaj dostępne operacji zalicza się nie tylko listKeys, ale również operacji, takich jak `list`, `listAdminKeys`, i `listStatus`. Nie można jednak użyć **listy** operacje, które wymagają wartości hello treść żądania. Na przykład Witaj [SAS konta listy](/rest/api/storagerp/storageaccounts#StorageAccounts_ListAccountSAS) operacja wymaga parametrów treści żądania, takich jak *signedExpiry*, więc nie można go użyć w ramach szablonu.

typy zasobów, które mają operacja listy toodetermine, masz hello następujące opcje:

* Widok hello [operacje interfejsu API REST](/rest/api/) dla dostawcy zasobów, a następnie wyszukaj listę operacji. Na przykład konta magazynu ma hello [operacji listKeys](/rest/api/storagerp/storageaccounts#StorageAccounts_ListKeys).
* Użyj hello [Get-AzureRmProviderOperation](/powershell/module/azurerm.resources/get-azurermprovideroperation) polecenia cmdlet programu PowerShell. Witaj poniższy przykład pobiera wszystkie operacje listy kont magazynu:

  ```powershell
  Get-AzureRmProviderOperation -OperationSearchString "Microsoft.Storage/*" | where {$_.Operation -like "*list*"} | FT Operation
  ```
* Użyj następującego polecenia wiersza polecenia platformy Azure toofilter hello tylko operacje listy hello:

  ```azurecli
  az provider operation show --namespace Microsoft.Storage --query "resourceTypes[?name=='storageAccounts'].operations[].name | [?contains(@, 'list')]"
  ```

Określ zasób hello przy użyciu albo hello [funkcja resourceId](#resourceid), lub hello format `{providerNamespace}/{resourceType}/{resourceName}`.


### <a name="example"></a>Przykład

Witaj poniższy przykład przedstawia sposób tooreturn klucze podstawowe i pomocnicze hello z konta magazynu w hello generuje sekcji.

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

Zwraca informacje o dostawcy zasobów i jego obsługiwane typy zasobów. Jeśli typ zasobu nie zostanie określona, funkcja hello zwraca wszystkie typy hello obsługiwane dla dostawcy zasobów hello.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| providerNamespace |Tak |Ciąg |Namespace hello dostawcy |
| Typ zasobu |Nie |Ciąg |określony Hello typ zasobu w hello przestrzeni nazw. |

### <a name="return-value"></a>Wartość zwracana

Każdego obsługiwanego typu, jest zwracany w hello następującego formatu: 

```json
{
    "resourceType": "{name of resource type}",
    "locations": [ all supported locations ],
    "apiVersions": [ all supported API versions ]
}
```

Tablica kolejność hello zwracane wartości nie jest gwarantowana.

### <a name="example"></a>Przykład

Witaj poniższy przykład pokazuje, jak toouse hello funkcja dostawcy:

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

Witaj poprzednim przykładzie zwraca obiekt hello następującego formatu:

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
| apiVersion |Nie |Ciąg |Wersja interfejsu API hello określony zasób. Ten parametr jest uwzględniony, gdy nie zainicjowano hello zasobów w ramach tego samego szablonu. Zazwyczaj w formacie hello **rrrr mm-dd**. |

### <a name="return-value"></a>Wartość zwracana

Każdy typ zasobu zwraca inne właściwości hello odwołanie do funkcji. Funkcja Hello nie zwraca jednego, wstępnie zdefiniowanego formatu. Obiekt hello w hello generuje sekcji, jak pokazano w przykładzie hello zwrotu toosee hello właściwości dla typu zasobu.

### <a name="remarks"></a>Uwagi

Hello odwołanie funkcji pochodzi wartość ze stanu środowiska uruchomieniowego i nie można użyć w sekcji zmiennych hello. Można go w sekcji danych wyjściowych szablonu. 

Funkcja odwołanie hello niejawnie deklarowaniu czy jeden zasób jest zależny od innego zasobu, jeśli hello odwołuje się do zasobu jest udostępniony w ramach tego samego szablonu. Nie trzeba tooalso Użyj hello dependsOn właściwości. Witaj funkcja nie jest oceniany, dopóki nie zakończy się hello zasobu wdrożenia.

toosee hello nazwy i wartości właściwości dla typu zasobu, utworzyć szablon, który zwraca obiekt hello w sekcji danych wyjściowych hello. Jeśli masz istniejący zasób tego typu do szablonu zwraca obiekt hello bez wdrażania żadnych nowych zasobów. 

Należy zwykle użyć hello **odwołania** funkcji tooreturn określonej wartości z obiektu, na przykład hello identyfikator URI punktu końcowego obiektu blob lub w pełni kwalifikowaną nazwę domeny.

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

Dokumentacja i toodeploy zasobu hello w hello tego samego szablonu, użyj:

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

Witaj poprzednim przykładzie zwraca obiekt hello następującego formatu:

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

Witaj poniższy przykład odwołuje się do konta magazynu, który nie jest wdrożony w tym szablonie. Witaj konto magazynu już istnieje w ramach hello same grupy zasobów.

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

Zwraca obiekt reprezentujący hello bieżącej grupie zasobów. 

### <a name="return-value"></a>Wartość zwracana

Witaj zwrócony obiekt jest zgodny z formatem hello:

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

Zazwyczaj hello funkcji grupa zasobów jest używane zasoby toocreate w hello tej samej lokalizacji co hello grupy zasobów. Witaj poniższym przykładzie użyto lokalizacja hello tooassign lokalizacji hello grupy zasobów dla witryny sieci web.

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

Witaj następujący szablon zwraca hello właściwości hello grupy zasobów.

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

Witaj poprzednim przykładzie zwraca obiekt hello następującego formatu:

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

Zwraca hello Unikatowy identyfikator zasobu. Aby użyć tej funkcji, gdy nazwa zasobu hello jest niejednoznaczny lub nie jest inicjowana w hello tego samego szablonu. 

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| subscriptionId |Nie |ciąg (format identyfikatora GUID w) |Wartość domyślna to hello bieżącej subskrypcji. Należy podać tę wartość, gdy będziesz potrzebować tooretrieve zasobów w innej subskrypcji. |
| Grupy zasobów o nazwie |Nie |Ciąg |Wartość domyślna to bieżącej grupie zasobów. Należy podać tę wartość, gdy będziesz potrzebować tooretrieve zasobów w innej grupie zasobów. |
| Typ zasobu |Tak |Ciąg |Typ zasobu, włącznie z przestrzenią nazw dostawcy zasobów. |
| resourceName1 |Tak |Ciąg |Nazwa zasobu. |
| resourceName2 |Nie |Ciąg |Następny nazwy segmentu zasobu, jeśli zasób jest zagnieżdżony. |

### <a name="return-value"></a>Wartość zwracana

Identyfikator Hello jest zwracany w hello następującego formatu:

```json
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{resourceType}/{resourceName}
```

### <a name="remarks"></a>Uwagi

Hello można określić wartości parametrów są zależne od tego, czy zasób hello jest hello tej samej subskrypcji i zasobu grupy jako hello bieżącego wdrożenia.

tooget hello zasobów identyfikator dla konta magazynu w hello sam subskrypcji i grupy zasobów, należy użyć:

```json
"[resourceId('Microsoft.Storage/storageAccounts','examplestorage')]"
```

Identyfikator zasobu hello tooget dla konta magazynu w hello tej samej subskrypcji, ale innej grupie zasobów, użyj:

```json
"[resourceId('otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

Identyfikator zasobu hello tooget dla konta magazynu w innej subskrypcji i grupy zasobów, należy użyć:

```json
"[resourceId('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

Identyfikator zasobu hello tooget bazy danych w innej grupie zasobów, należy użyć:

```json
"[resourceId('otherResourceGroup', 'Microsoft.SQL/servers/databases', parameters('serverName'), parameters('databaseName'))]"
```

Często potrzebne toouse tej funkcji za pomocą konta magazynu lub sieci wirtualnej w grupie zasobów alternatywny. Witaj poniższy przykład przedstawia zasobu z grupy zasobów zewnętrznych można łatwo użycia:

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

Witaj poniższy przykład zwraca identyfikator zasobu powitania dla konta magazynu w grupie zasobów hello:

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

przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| sameRGOutput | Ciąg | /Subscriptions/{Current-Sub-ID}/resourceGroups/examplegroup/Providers/Microsoft.Storage/storageAccounts/examplestorage |
| differentRGOutput | Ciąg | /Subscriptions/{Current-Sub-ID}/resourceGroups/otherResourceGroup/Providers/Microsoft.Storage/storageAccounts/examplestorage |
| differentSubOutput | Ciąg | /Subscriptions/{different-Sub-ID}/resourceGroups/otherResourceGroup/Providers/Microsoft.Storage/storageAccounts/examplestorage |
| nestedResourceOutput | Ciąg | /Subscriptions/{Current-Sub-ID}/resourceGroups/examplegroup/Providers/Microsoft.SQL/Servers/serverName/Databases/databaseName |

<a id="subscription" />

## <a name="subscription"></a>subskrypcja
`subscription()`

Zwraca szczegółowe informacje o subskrypcji hello hello bieżące wdrożenia. 

### <a name="return-value"></a>Wartość zwracana

Witaj, funkcja zwraca hello następującego formatu:

```json
{
    "id": "/subscriptions/{subscription-id}",
    "subscriptionId": "{subscription-id}",
    "tenantId": "{tenant-id}",
    "displayName": "{name-of-subscription}"
}
```

### <a name="example"></a>Przykład

Witaj poniższy przykład przedstawia hello subskrypcji funkcji o nazwie w sekcji danych wyjściowych hello. 

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
* Aby uzyskać opis hello części szablonu usługi Azure Resource Manager, zobacz [szablonów Authoring Azure Resource Manager](resource-group-authoring-templates.md).
* Zobacz wielu szablonów toomerge [za pomocą szablonów połączonych z usługą Azure Resource Manager](resource-group-linked-templates.md).
* tooiterate określoną liczbę razy podczas tworzenia typu zasobu, zobacz [utworzyć wiele wystąpień zasobów usługi Azure Resource Manager](resource-group-create-multiple.md).
* toosee toodeploy hello szablonu po utworzeniu, zobacz [wdrażania aplikacji przy użyciu szablonu usługi Azure Resource Manager](resource-group-template-deploy.md).

