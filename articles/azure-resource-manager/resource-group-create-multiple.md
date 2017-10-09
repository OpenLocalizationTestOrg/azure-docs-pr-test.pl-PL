---
title: "aaaDeploy wiele wystąpień zasobów platformy Azure | Dokumentacja firmy Microsoft"
description: "Użyj operacji kopiowania i tablic w tooiterate szablonu usługi Azure Resource Manager wielokrotnie podczas wdrażania zasobów."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: 
ms.assetid: 94d95810-a87b-460f-8e82-c69d462ac3ca
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/26/2017
ms.author: tomfitz
ms.openlocfilehash: a3bd42f694053317c30b639c33dc4efae41a9a9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-multiple-instances-of-a-resource-or-property-in-azure-resource-manager-templates"></a>Wdrażanie wielu wystąpień zasobów lub właściwości w szablonach usługi Azure Resource Manager
W tym temacie opisano sposób tooiterate w Twojej toocreate szablonu usługi Azure Resource Manager wiele wystąpień zasobu lub wiele wystąpień właściwości w zasobie.

Jeśli potrzebujesz tooadd logiki tooyour szablon, który pozwala toospecify Określa, czy zasób jest wdrażana, zobacz [warunkowo wdrażanie zasobów](#conditionally-deploy-resource).

## <a name="resource-iteration"></a>Iteracja zasobów
Dodawanie wielu wystąpień typu zasobu toocreate `copy` typ zasobu toohello elementu. W elemencie kopiowania hello można określić numer hello iteracji i nazwę tej pętli. wartość licznika Hello musi być dodatnią liczbą całkowitą i nie może przekraczać 800. Menedżer zasobów tworzy zasobów hello równolegle. W związku z tym nie jest gwarantowana hello kolejności, w której zostały utworzone. zasoby toocreate iterowane w sekwencji, zobacz [Serial kopiowania](#serial-copy). 

toocreate zasobów Hello wielokrotnie przyjmuje hello następującego formatu:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
        {
            "apiVersion": "2016-01-01",
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[concat(copyIndex(),'storage', uniqueString(resourceGroup().id))]",
            "location": "[resourceGroup().location]",
            "sku": {
                "name": "Standard_LRS"
            },
            "kind": "Storage",
            "properties": {},
            "copy": {
                "name": "storagecopy",
                "count": 3
            }
        }
    ],
    "outputs": {}
}
```

Zwróć uwagę, że hello nazwa każdego zasobu zawiera hello `copyIndex()` funkcji, która zwraca bieżącą iterację hello w pętli hello. `copyIndex()`jest liczony od zera. Poniższy przykład tak, hello:

```json
"name": "[concat('storage', copyIndex())]",
```

Tworzy następujące nazwy:

* storage0
* storage1
* storage2.

wartość indeksu hello toooffset, można przekazać wartość w funkcji copyIndex() hello. Hello liczby iteracji tooperform jest nadal określona w elemencie kopiowania hello, ale jest zwracana wartość hello copyIndex w hello określona wartość. Poniższy przykład tak, hello:

```json
"name": "[concat('storage', copyIndex(1))]",
```

Tworzy następujące nazwy:

* storage1
* storage2
* storage3

Operacja kopiowania Hello jest przydatne podczas pracy z tablicami, ponieważ można wykonać iterację każdego elementu w tablicy hello. Użyj hello `length` funkcja na powitania tablicy toospecify hello liczba iteracji, i `copyIndex` tooretrieve hello bieżący indeks w tablicy hello. Poniższy przykład tak, hello:

```json
"parameters": { 
  "org": { 
     "type": "array", 
     "defaultValue": [ 
         "contoso", 
         "fabrikam", 
         "coho" 
      ] 
  }
}, 
"resources": [ 
  { 
      "name": "[concat('storage', parameters('org')[copyIndex()])]", 
      "copy": { 
         "name": "storagecopy", 
         "count": "[length(parameters('org'))]" 
      }, 
      ...
  } 
]
```

Tworzy następujące nazwy:

* storagecontoso
* storagefabrikam
* storagecoho

## <a name="serial-copy"></a>Kopiuj szeregowe

Gdy używasz hello kopiowania elementu toocreate wiele wystąpień typu zasobu, Menedżer zasobów domyślnie wdroży je równolegle. Jednak możesz toospecify hello, że zasoby są wdrażane w sekwencji. Na przykład podczas aktualizacji do środowiska produkcyjnego, może zaistnieć toostagger hello aktualizacji, tylko pewne są aktualizowane w dowolnym momencie.

Usługa Resource Manager zapewnia, że właściwości w elemencie kopiowania hello umożliwiających tooserially można wdrożyć wiele wystąpień. W zestawie elementów kopiowania hello, `mode` za**serial** i `batchSize` toohello liczbę wystąpień toodeploy naraz. Serial w trybie Menedżera zasobów tworzy zależność w wystąpieniach wcześniej w pętli hello, więc nie zostanie uruchomiony serii do chwili zakończenia poprzedniej wsadowym hello.

```json
"copy": {
    "name": "iterator",
    "count": "[parameters('numberToDeploy')]",
    "mode": "serial",
    "batchSize": 2
},
```

Witaj właściwości tryb również akceptuje **równoległych**, która jest wartością domyślną hello.

tootest serial kopiowania bez tworzenia rzeczywistych zasobów hello Użyj następującego szablonu, który wdraża pusty zagnieżdżone szablony:

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "numberToDeploy": {
      "type": "int",
      "minValue": 2,
      "defaultValue": 5
    }
  },
  "resources": [
    {
      "apiVersion": "2015-01-01",
      "type": "Microsoft.Resources/deployments",
      "name": "[concat('loop-', copyIndex())]",
      "copy": {
        "name": "iterator",
        "count": "[parameters('numberToDeploy')]",
        "mode": "serial",
        "batchSize": 1
      },
      "properties": {
        "mode": "Incremental",
        "template": {
          "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
          "contentVersion": "1.0.0.0",
          "parameters": {},
          "variables": {},
          "resources": [],
          "outputs": {
          }
        }
      }
    }
  ],
  "outputs": {
  }
}
```

W historii wdrożenia hello Zwróć uwagę, że hello zagnieżdżonych wdrożenia są przetwarzane w sekwencji.

![Serial wdrożenia](./media/resource-group-create-multiple/serial-copy.png)

Dla scenariusza bardziej realistyczne hello poniższy przykład wdraża dwóch wystąpień w czasie z zagnieżdżonych szablonu maszyny wirtualnej systemu Linux:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "adminUsername": {
            "type": "string",
            "metadata": {
                "description": "User name for hello Virtual Machine."
            }
        },
        "adminPassword": {
            "type": "securestring",
            "metadata": {
                "description": "Password for hello Virtual Machine."
            }
        },
        "dnsLabelPrefix": {
            "type": "string",
            "metadata": {
                "description": "Unique DNS Name for hello Public IP used tooaccess hello Virtual Machine."
            }
        },
        "ubuntuOSVersion": {
            "type": "string",
            "defaultValue": "16.04.0-LTS",
            "allowedValues": [
                "12.04.5-LTS",
                "14.04.5-LTS",
                "15.10",
                "16.04.0-LTS"
            ],
            "metadata": {
                "description": "hello Ubuntu version for hello VM. This will pick a fully patched image of this given Ubuntu version."
            }
        }
    },
    "variables": {
        "templatelink": "https://raw.githubusercontent.com/rjmax/Build2017/master/Act1.TemplateEnhancements/Chapter03.LinuxVM.json"
    },
    "resources": [
        {
            "apiVersion": "2015-01-01",
            "name": "[concat('nestedDeployment',copyIndex())]",
            "type": "Microsoft.Resources/deployments",
            "copy": {
                "name": "myCopySet",
                "count": 4,
                "mode": "serial",
                "batchSize": 2
            },
            "properties": {
                "mode": "Incremental",
                "templateLink": {
                    "uri": "[variables('templatelink')]",
                    "contentVersion": "1.0.0.0"
                },
                "parameters": {
                    "adminUsername": {
                        "value": "[parameters('adminUsername')]"
                    },
                    "adminPassword": {
                        "value": "[parameters('adminPassword')]"
                    },
                    "dnsLabelPrefix": {
                        "value": "[parameters('dnsLabelPrefix')]"
                    },
                    "ubuntuOSVersion": {
                        "value": "[parameters('ubuntuOSVersion')]"
                    },
                    "index":{
                        "value": "[copyIndex()]"
                    }
                }
            }
        }
    ]
}
```

## <a name="property-iteration"></a>Właściwość iteracji

Dodaj wiele wartości dla właściwości w zasobie toocreate `copy` tablicy w elemencie właściwości hello. Ta tablica zawiera obiekty, a każdy obiekt ma hello następujące właściwości:

* Nazwa hello z toocreate właściwości hello wielu wartości
* Liczba — liczba hello toocreate wartości
* dane wejściowe - obiekt, który zawiera właściwości toohello tooassign wartości hello  

powitania po przykładzie pokazano, jak tooapply `copy` toohello dataDisks właściwości na maszynie wirtualnej:

```json
{
  "name": "examplevm",
  "type": "Microsoft.Compute/virtualMachines",
  "apiVersion": "2017-03-30",
  "properties": {
    "storageProfile": {
      "copy": [{
          "name": "dataDisks",
          "count": 3,
          "input": {
              "lun": "[copyIndex('dataDisks')]",
              "createOption": "Empty",
              "diskSizeGB": "1023"
          }
      }],
      ...
```

Zwróć uwagę, że przy użyciu `copyIndex` wewnątrz iteracji właściwości, należy podać nazwę hello hello iteracji. Nie masz nazwy hello tooprovide, gdy jest używany z zasobów iteracji.

Menedżer zasobów rozszerza hello `copy` tablicy podczas wdrażania. Nazwa Hello tablicy hello staje się nazwa hello hello właściwości. wartości wejściowe Hello stają się hello właściwości obiektu. Witaj wdrożyć szablon staje się:

```json
{
  "name": "examplevm",
  "type": "Microsoft.Compute/virtualMachines",
  "apiVersion": "2017-03-30",
  "properties": {
    "storageProfile": {
      "dataDisks": [
          {
              "lun": 0,
              "createOption": "Empty",
              "diskSizeGB": "1023"
          },
          {
              "lun": 1,
              "createOption": "Empty",
              "diskSizeGB": "1023"
          },
          {
              "lun": 2,
              "createOption": "Empty",
              "diskSizeGB": "1023"
          }
      }],
      ...
```

Iteracja zasobów i właściwości można użyć razem. Odwołanie hello iteracji właściwości według nazwy.

```json
{
    "type": "Microsoft.Network/virtualNetworks",
    "name": "[concat(parameters('vnetname'), copyIndex())]",
    "apiVersion": "2016-06-01",
    "copy":{
        "count": 2,
        "name": "vnetloop"
    },
    "location": "[resourceGroup().location]",
    "properties": {
        "addressSpace": {
            "addressPrefixes": [
                "[parameters('addressPrefix')]"
            ]
        },
        "copy": [
            {
                "name": "subnets",
                "count": 2,
                "input": {
                    "name": "[concat('subnet-', copyIndex('subnets'))]",
                    "properties": {
                        "addressPrefix": "[variables('subnetAddressPrefix')[copyIndex('subnets')]]"
                    }
                }
            }
        ]
    }
}
```

Może zawierać tylko jeden element kopiowania hello właściwości dla każdego zasobu. toospecify iteracji pętli dla więcej niż jedną właściwość, należy zdefiniować wiele obiektów w hello kopiowania tablicy. Każdy obiekt jest iterowane oddzielnie. Na przykład toocreate wiele wystąpień zarówno hello `frontendIPConfigurations` właściwości i hello `loadBalancingRules` właściwości modułu równoważenia obciążenia, zdefiniuj zarówno do obiektów w elemencie pojedynczej kopii: 

```json
{
    "name": "[variables('loadBalancerName')]",
    "type": "Microsoft.Network/loadBalancers",
    "properties": {
        "copy": [
          {
              "name": "frontendIPConfigurations",
              "count": 2,
              "input": {
                  "name": "[concat('loadBalancerFrontEnd', copyIndex('frontendIPConfigurations', 1))]",
                  "properties": {
                      "publicIPAddress": {
                          "id": "[variables(concat('publicIPAddressID', copyIndex('frontendIPConfigurations', 1)))]"
                      }
                  }
              }
          },
          {
              "name": "loadBalancingRules",
              "count": 2,
              "input": {
                  "name": "[concat('LBRuleForVIP', copyIndex('loadBalancingRules', 1))]",
                  "properties": {
                      "frontendIPConfiguration": {
                          "id": "[variables(concat('frontEndIPConfigID', copyIndex('loadBalancingRules', 1)))]"
                      },
                      "backendAddressPool": {
                          "id": "[variables('lbBackendPoolID')]"
                      },
                      "protocol": "tcp",
                      "frontendPort": "[variables(concat('frontEndPort' copyIndex('loadBalancingRules', 1))]",
                      "backendPort": "[variables(concat('backEndPort' copyIndex('loadBalancingRules', 1))]",
                      "probe": {
                          "id": "[variables('lbProbeID')]"
                      }
                  }
              }
          }
        ],
        ...
    }
}
```

## <a name="depend-on-resources-in-a-loop"></a>Są zależne od zasobów w pętli
Określ, czy zasób jest wdrażane po innego zasobu za pomocą hello `dependsOn` elementu. toodeploy z zasobem, który jest zależny od hello kolekcji zasobów w pętli, podaj nazwę hello pętlę kopiowania hello w elemencie dependsOn hello. Witaj poniższy przykład pokazuje, jak toodeploy trzy konta magazynu przed wdrożeniem hello maszyny wirtualnej. Witaj pełnej definicji maszyny wirtualnej nie jest widoczne. Powiadomienia elementu kopiowania hello ma nazwę ustawić także`storagecopy` i elementu dependsOn hello hello maszyn wirtualnych jest również ustawiona zbyt`storagecopy`.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {},
    "resources": [
        {
            "apiVersion": "2016-01-01",
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[concat(copyIndex(),'storage', uniqueString(resourceGroup().id))]",
            "location": "[resourceGroup().location]",
            "sku": {
                "name": "Standard_LRS"
            },
            "kind": "Storage",
            "properties": {},
            "copy": {
                "name": "storagecopy",
                "count": 3
            }
        },
        {
            "apiVersion": "2015-06-15", 
            "type": "Microsoft.Compute/virtualMachines", 
            "name": "[concat('VM', uniqueString(resourceGroup().id))]",  
            "dependsOn": ["storagecopy"],
            ...
        }
    ],
    "outputs": {}
}
```

## <a name="create-multiple-instances-of-a-child-resource"></a>Tworzenie wielu wystąpień zasobu podrzędnego
Nie można używać pętli kopii zasobu podrzędnego. toocreate wiele wystąpień z zasobem, który zazwyczaj zdefiniowane jako zagnieżdżony w innym zasobem, należy zamiast tego utworzyć tego zasobu jako zasób najwyższego poziomu. Można zdefiniować relacji hello z zasobu nadrzędnego hello za pośrednictwem hello typem i nazwą właściwości.

Na przykład załóżmy, że zazwyczaj Definiowanie zestawu danych jako zasób podrzędnych w fabryce danych.

```json
"resources": [
{
    "type": "Microsoft.DataFactory/datafactories",
    "name": "exampleDataFactory",
    ...
    "resources": [
    {
        "type": "datasets",
        "name": "exampleDataSet",
        "dependsOn": [
            "exampleDataFactory"
        ],
        ...
    }
}]
```

toocreate instancje zestawów danych, przenieś go poza hello fabryki danych. Hello zestawu danych musi znajdować się na powitania sam poziom jako hello fabryki danych, ale nadal jest zasobem podrzędnych hello fabryki danych. Możesz zachować hello relacja między zestawu danych i fabryki danych za pośrednictwem hello typem i nazwą właściwości. Ponieważ nie można wywnioskować typu z pozycji w szablonie hello, musisz podać typ hello w pełni kwalifikowana w formacie hello: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`.

tooestablish relacji nadrzędny/podrzędny z wystąpienia fabryki danych hello, podaj nazwę dla zestawu danych hello, która zawiera nazwę zasobu nadrzędnego hello. Użyj formatu hello: `{parent-resource-name}/{child-resource-name}`.  

Witaj poniższy przykład przedstawia implementację hello:

```json
"resources": [
{
    "type": "Microsoft.DataFactory/datafactories",
    "name": "exampleDataFactory",
    ...
},
{
    "type": "Microsoft.DataFactory/datafactories/datasets",
    "name": "[concat('exampleDataFactory', '/', 'exampleDataSet', copyIndex())]",
    "dependsOn": [
        "exampleDataFactory"
    ],
    "copy": { 
        "name": "datasetcopy", 
        "count": "3" 
    } 
    ...
}]
```

## <a name="conditionally-deploy-resource"></a>Warunkowo wdrażanie zasobów

toospecify, czy zasób jest wdrażana, użyj hello `condition` elementu. Witaj wartość dla tego elementu rozpoznaje tootrue, lub FAŁSZ. Jeśli wartość hello ma wartość true, zasobów hello jest wdrażana. Gdy wartość hello ma wartość false, hello zasobów nie są wdrażane. Na przykład toospecify czy nowe konto magazynu jest wdrożony lub istniejącego konta magazynu jest używany, użyj:

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

Na przykład za pomocą nowego lub istniejącego zasobu, zobacz [nowy lub istniejący szablon warunku](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).

Na przykład przy użyciu hasła lub maszyny wirtualnej toodeploy klucza SSH, zobacz [nazwa użytkownika lub SSH szablonu warunku](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).

## <a name="next-steps"></a>Następne kroki
* Jeśli toolearn sekcje hello szablonu informacje, zobacz [Authoring Azure Resource Manager szablony](resource-group-authoring-templates.md).
* toolearn jak toodeploy szablonu, zobacz [wdrażanie aplikacji przy użyciu szablonu usługi Resource Manager Azure](resource-group-template-deploy.md).

