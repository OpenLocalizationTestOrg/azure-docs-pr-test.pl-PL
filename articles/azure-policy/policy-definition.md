---
title: Struktura definicji zasad Azure | Dokumentacja firmy Microsoft
description: "W tym artykule opisano, jak definicji zasad zasobów jest używany przez zasady usługi Azure do ustanawiania konwencje dla zasobów w organizacji przez opisujące, gdy zasady są wymuszane i jaka akcja ma być."
services: azure-policy
keywords: 
author: bandersmsft
ms.author: banders
ms.date: 01/17/2018
ms.topic: article
ms.service: azure-policy
ms.custom: 
ms.openlocfilehash: af373e2770ad020b3a3eb669424c001670ec9204
ms.sourcegitcommit: f1c1789f2f2502d683afaf5a2f46cc548c0dea50
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/18/2018
---
# <a name="azure-policy-definition-structure"></a>Struktura definicji zasad platformy Azure

Definicja zasad zasobu używanego przez zasady usługi Azure umożliwia ustalenie Konwencji zasobów w organizacji przez opisujące, gdy zasady są wymuszane i jaka akcja ma być. Definiowanie Konwencji, można kontrolować koszty i zarządzania zasobami. Na przykład można określić, czy dozwolone są tylko niektóre typy maszyn wirtualnych. Alternatywnie można wymagać, że wszystkie zasoby mają określony tag. Zasady są dziedziczone przez wszystkie zasoby podrzędne. Tak Jeśli zasady są stosowane do grupy zasobów, ma zastosowanie do wszystkich zasobów w danej grupie zasobów.

JSON służy do tworzenia definicji zasad. Definicja zasad zawiera elementy dla:

* mode
* parameters
* Nazwa wyświetlana
* description
* Reguła zasad
  * Ocena logiczne
  * Efekt

Na przykład następujące JSON zawiera zasadę, która ogranicza wdrożonym zasobów:

```json
{
  "properties": {
    "mode": "all",
    "parameters": {
      "allowedLocations": {
        "type": "array",
        "metadata": {
          "description": "The list of locations that can be specified when deploying resources",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
      }
    },
    "displayName": "Allowed locations",
    "description": "This policy enables you to restrict the locations your organization can specify when deploying resources.",
    "policyRule": {
      "if": {
        "not": {
          "field": "location",
          "in": "[parameters('allowedLocations')]"
        }
      },
      "then": {
        "effect": "deny"
      }
    }
  }
}
```

Wszystkie próbki szablonu zasad Azure są [szablony zasad Azure](json-samples.md).

## <a name="mode"></a>Tryb

Firma Microsoft zaleca, aby ustawić `mode` do `all` zasad przydziału oceny wszystkich grup zasobów i typów. Można zobaczyć przykład wymusza tagów do grupy zasobów w definicji zasad [Zezwalaj niestandardowego obrazu maszyny Wirtualnej z grupy zasobów](scripts/allow-custom-vm-image.md).

Jeśli zostanie ustawiona **wszystkie**, grupy zasobów i wszystkie typy zasobów są oceniane pod kątem zasad. Portal używa **wszystkie** dla wszystkich zasad. Jeśli używasz programu PowerShell lub interfejsu wiersza polecenia Azure, należy określić `mode` parametru i wartości **wszystkich**.

Użyj wszystkich definicji zasad utworzonych przy użyciu portalu `all` tryb, jeśli chcesz użyć programu PowerShell lub interfejsu wiersza polecenia Azure, należy określić `mode` parametru i ustaw ją na `all`.

Jeśli ustawiono tryb `indexed`, przypisanie zasad, które zostanie obliczone tylko dla typów zasobów, które obsługują tagów i lokalizacji.


## <a name="parameters"></a>Parametry

Parametry ułatwić zarządzanie zasadami dzięki zmniejszeniu liczby definicje zasad. Pomyśl o parametry, takie jak pól na formularzu — `name`, `address`, `city`, `state`. Te parametry zawsze znajdują się takie same, jednak zmienić ich wartości opartych na poszczególnych wypełniania formularza. Parametry działają tak samo, podczas tworzenia zasad. Przy tym parametrów w definicji zasad, można ponownie użyć tej zasady dla różnych scenariuszy przy użyciu innej wartości.

Na przykład można zdefiniować zasady dla właściwości zasobów ograniczyć lokalizacje wdrożonym zasobów. W takim przypadku może zadeklarować następujące parametry podczas tworzenia zasad:


```json
"parameters": {
  "allowedLocations": {
    "type": "array",
    "metadata": {
      "description": "The list of allowed locations for resources.",
      "displayName": "Allowed locations",
      "strongType": "location"
    }
  }
}
```

Typ parametru może być ciągiem lub tablicą. Właściwość metadanych służy do narzędzi, takich jak portalu Azure do wyświetlania informacji przyjazną dla użytkownika.

W metadanych właściwości można użyć **strongType** zapewnienie wielokrotnego wyboru listy opcji w portalu Azure.  Dozwolone wartości **strongType** obecnie obejmują:

* `"location"`
* `"resourceTypes"`
* `"storageSkus"`
* `"vmSKUs"`

W regule zasad możesz odwołania do parametrów przy użyciu następującej składni:

```json
{
    "field": "location",
    "in": "[parameters('allowedLocations')]"
}
```

## <a name="display-name-and-description"></a>Nazwę wyświetlaną i opis

Można użyć **displayName** i **opis** do identyfikowania definicji zasad i podanie gdy jest używana w kontekście.

## <a name="policy-rule"></a>Reguła zasad

Reguły składa się z **Jeśli** i **następnie** bloków. W **Jeśli** bloku, należy zdefiniować co najmniej jeden warunek, które określają, gdy zasady są wymuszane. Operatory logiczne można zastosować do tych warunków, aby precyzyjnie zdefiniować scenariusz dla zasad.

W **następnie** bloku, zdefiniuj efekt, która jest wywoływana po **Jeśli** warunki są spełnione.

```json
{
  "if": {
    <condition> | <logical operator>
  },
  "then": {
    "effect": "deny | audit | append"
  }
}
```

### <a name="logical-operators"></a>Operatory logiczne

Operatory logiczne obsługiwane są:

* `"not": {condition  or operator}`
* `"allOf": [{condition or operator},{condition or operator}]`
* `"anyOf": [{condition or operator},{condition or operator}]`

**Nie** składni odwraca wynik w warunku. **Wszystkie** składni (podobny do logicznego **i** operacji) wymaga wszystkie warunki, które muszą być spełnione. **AnyOf** składni (podobny do logicznego **lub** operacji) wymaga co najmniej jeden warunków.

Operatory logiczne można zagnieżdżać. W poniższym przykładzie przedstawiono **nie** operacja, która jest zagnieżdżona w **wszystkie** operacji.

```json
"if": {
  "allOf": [
    {
      "not": {
        "field": "tags",
        "containsKey": "application"
      }
    },
    {
      "field": "type",
      "equals": "Microsoft.Storage/storageAccounts"
    }
  ]
},
```

### <a name="conditions"></a>Warunki

Wynikiem warunku jest czy **pola** spełnia określone kryteria. Są obsługiwane warunki:

* `"equals": "value"`
* `"like": "value"`
* `"match": "value"`
* `"contains": "value"`
* `"in": ["value1","value2"]`
* `"containsKey": "keyName"`
* `"exists": "bool"`

Korzystając z **jak** warunku, możesz podać symbol wieloznaczny (*) w wartości.

Korzystając z **odpowiada** warunku, podaj `#` do reprezentowania cyfrę, `?` literę i znak reprezentują rzeczywiste znaku. Aby uzyskać przykłady, zobacz [obrazy zatwierdzone wirtualna](scripts/allowed-custom-images.md).

### <a name="fields"></a>Pola
Warunki są utworzone za pomocą pola. Pole reprezentuje właściwości w ładunku żądania zasobu, który jest używany do opisu stanu typu zasobu.  

Obsługiwane są następujące pola:

* `name`
* `kind`
* `type`
* `location`
* `tags`
* `tags.*`
* Aliasy właściwości — Aby uzyskać listę, zobacz [aliasy](#aliases).

### <a name="effect"></a>Efekt
Zasady obsługuje następujące typy wpływu:

* **Odmów**: generuje zdarzenie w dzienniku inspekcji i niepowodzenia żądania
* **Inspekcja**: generuje to zdarzenie ostrzegawcze w dzienniku inspekcji, ale nie wystąpi niepowodzenie żądania
* **Dołącz**: dodaje zestaw określonych pól na żądanie
* **AuditIfNotExists**: włącza inspekcji, jeśli zasób nie istnieje.
* **DeployIfNotExists**: wdraża zasobu, jeśli jeszcze nie istnieje. Obecnie ten efekt jest obsługiwana tylko przy użyciu wbudowanych zasad.

Aby uzyskać **Dołącz**, należy podać następujące informacje:

```json
"effect": "append",
"details": [
  {
    "field": "field name",
    "value": "value of the field"
  }
]
```

Wartość może być ciągiem lub obiekt do formatu JSON.

Z **AuditIfNotExists** i **DeployIfNotExists** można ocenić istnienia zasobu podrzędnego i Zastosuj regułę i ich wpływ, gdy ten zasób nie istnieje. Można na przykład wymagać, że dla wszystkich sieci wirtualnych jest wdrażany obserwatora sieciowego.
Przykład inspekcję, gdy rozszerzenie maszyny wirtualnej nie została wdrożona, zobacz [inspekcji, jeśli rozszerzenie nie istnieje](scripts/audit-ext-not-exist.md).


## <a name="aliases"></a>Aliasy

Aliasy właściwości umożliwia dostęp do właściwości specyficzne dla typu zasobu. Aliasy pozwalają ograniczyć, jakie wartości lub warunki są dozwolone dla właściwości w zasobie. Każdy alias mapuje ścieżek w różnych wersjach interfejsu API dla typu zasobu. Podczas oceny zasad aparat zasad pobiera ścieżki właściwości dla tej wersji interfejsu API.

**Microsoft.Cache/Redis**

| Alias | Opis |
| ----- | ----------- |
| Microsoft.Cache/Redis/enableNonSslPort | Ustaw czy bez użycia protokołu ssl serwera Redis portu (6379) jest włączona. |
| Microsoft.Cache/Redis/shardCount | Ustaw liczbę fragmentów do utworzenia na pamięć podręczna klastra Premium.  |
| Microsoft.Cache/Redis/sku.capacity | Ustaw rozmiar pamięci podręcznej Redis do wdrożenia.  |
| Microsoft.Cache/Redis/sku.family | Ustaw rodziny SKU do użycia. |
| Microsoft.Cache/Redis/sku.name | Ustaw typ pamięci podręcznej Redis do wdrożenia. |

**Microsoft.Cdn/profiles**

| Alias | Opis |
| ----- | ----------- |
| Microsoft.CDN/profiles/sku.name | Ustaw nazwę warstwy cenowej. |

**Microsoft.Compute/disks**

| Alias | Opis |
| ----- | ----------- |
| Microsoft.Compute/imageOffer | Ustaw oferta obrazu platformy lub obrazu z witryny marketplace użyty do utworzenia maszyny wirtualnej. |
| Microsoft.Compute/imagePublisher | Ustaw wydawcy obrazu platformy lub obrazu z witryny marketplace użyty do utworzenia maszyny wirtualnej. |
| Microsoft.Compute/imageSku | Jednostka SKU obrazu platformy lub obrazu z witryny marketplace użyty do utworzenia maszyny wirtualnej zestawu. |
| Microsoft.Compute/imageVersion | Ustaw wersję obrazu platformy lub obrazu z witryny marketplace użyty do utworzenia maszyny wirtualnej. |


**Microsoft.Compute/virtualMachines**

| Alias | Opis |
| ----- | ----------- |
| Microsoft.Compute/imageId | Ustaw identyfikator obraz używany do utworzenia maszyny wirtualnej. |
| Microsoft.Compute/imageOffer | Ustaw oferta obrazu platformy lub obrazu z witryny marketplace użyty do utworzenia maszyny wirtualnej. |
| Microsoft.Compute/imagePublisher | Ustaw wydawcy obrazu platformy lub obrazu z witryny marketplace użyty do utworzenia maszyny wirtualnej. |
| Microsoft.Compute/imageSku | Jednostka SKU obrazu platformy lub obrazu z witryny marketplace użyty do utworzenia maszyny wirtualnej zestawu. |
| Microsoft.Compute/imageVersion | Ustaw wersję obrazu platformy lub obrazu z witryny marketplace użyty do utworzenia maszyny wirtualnej. |
| Microsoft.Compute/licenseType | Ustaw, że obraz lub dysk jest licencjonowane lokalnymi. Ta wartość jest używana tylko dla obrazów systemu operacyjnego Windows Server.  |
| Microsoft.Compute/virtualMachines/imageOffer | Ustaw oferta obrazu platformy lub obrazu z witryny marketplace użyty do utworzenia maszyny wirtualnej. |
| Microsoft.Compute/virtualMachines/imagePublisher | Ustaw wydawcy obrazu platformy lub obrazu z witryny marketplace użyty do utworzenia maszyny wirtualnej. |
| Microsoft.Compute/virtualMachines/imageSku | Jednostka SKU obrazu platformy lub obrazu z witryny marketplace użyty do utworzenia maszyny wirtualnej zestawu. |
| Microsoft.Compute/virtualMachines/imageVersion | Ustaw wersję obrazu platformy lub obrazu z witryny marketplace użyty do utworzenia maszyny wirtualnej. |
| Microsoft.Compute/virtualMachines/osDisk.Uri | Ustaw identyfikator URI dysku vhd. |
| Microsoft.Compute/virtualMachines/sku.name | Ustaw rozmiar maszyny wirtualnej. |

**Microsoft.Compute/virtualMachines/extensions**

| Alias | Opis |
| ----- | ----------- |
| Microsoft.Compute/virtualMachines/extensions/publisher | Ustaw nazwę wydawcy rozszerzenia. |
| Microsoft.Compute/virtualMachines/extensions/type | Ustaw typ rozszerzenia. |
| Microsoft.Compute/virtualMachines/extensions/typeHandlerVersion | Ustaw wersję rozszerzenia. |

**Microsoft.Compute/virtualMachineScaleSets**

| Alias | Opis |
| ----- | ----------- |
| Microsoft.Compute/imageId | Ustaw identyfikator obraz używany do utworzenia maszyny wirtualnej. |
| Microsoft.Compute/imageOffer | Ustaw oferta obrazu platformy lub obrazu z witryny marketplace użyty do utworzenia maszyny wirtualnej. |
| Microsoft.Compute/imagePublisher | Ustaw wydawcy obrazu platformy lub obrazu z witryny marketplace użyty do utworzenia maszyny wirtualnej. |
| Microsoft.Compute/imageSku | Jednostka SKU obrazu platformy lub obrazu z witryny marketplace użyty do utworzenia maszyny wirtualnej zestawu. |
| Microsoft.Compute/imageVersion | Ustaw wersję obrazu platformy lub obrazu z witryny marketplace użyty do utworzenia maszyny wirtualnej. |
| Microsoft.Compute/licenseType | Ustaw, że obraz lub dysk jest licencjonowane lokalnymi. Ta wartość jest używana tylko dla obrazów systemu operacyjnego Windows Server. |
| Microsoft.Compute/VirtualMachineScaleSets/computerNamePrefix | Ustaw prefiks nazwy komputera dla wszystkich maszyn wirtualnych w zestawie skalowania. |
| Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl | Ustaw identyfikator URI obiektu blob obrazu użytkownika. |
| Microsoft.Compute/VirtualMachineScaleSets/osdisk.vhdContainers | Ustawianie adresów URL kontenera, które są używane do przechowywania dysków systemu operacyjnego dla zestawu skalowania. |
| Microsoft.Compute/VirtualMachineScaleSets/sku.name | Ustaw rozmiar maszyn wirtualnych w zestawie skalowania. |
| Microsoft.Compute/VirtualMachineScaleSets/sku.tier | Ustawienie warstwy maszyn wirtualnych w zestawie skalowania. |

**Microsoft.Network/applicationGateways**

| Alias | Opis |
| ----- | ----------- |
| Microsoft.Network/applicationGateways/sku.name | Ustawianie rozmiaru bramy. |

**Microsoft.Network/virtualNetworkGateways**

| Alias | Opis |
| ----- | ----------- |
| Microsoft.Network/virtualNetworkGateways/gatewayType | Ustaw typ tej bramy sieci wirtualnej. |
| Microsoft.Network/virtualNetworkGateways/sku.name | Ustaw nazwę jednostki SKU bramy. |

**Microsoft.Sql/servers**

| Alias | Opis |
| ----- | ----------- |
| Microsoft.Sql/servers/version | Ustaw wersję serwera. |

**Microsoft.Sql/databases**

| Alias | Opis |
| ----- | ----------- |
| Microsoft.Sql/servers/databases/edition | Ustaw wersję bazy danych. |
| Microsoft.Sql/servers/databases/elasticPoolName | Zestaw nazwę puli elastycznej bazy danych jest. |
| Microsoft.Sql/servers/databases/requestedServiceObjectiveId | Ustawienia poziomu identyfikatorów celu skonfigurowanej usługi bazy danych. |
| Microsoft.Sql/servers/databases/requestedServiceObjectiveName | Ustaw nazwę celu poziomu usługi skonfigurowane bazy danych.  |

**Microsoft.Sql/elasticpools**

| Alias | Opis |
| ----- | ----------- |
| serwery/elasticpools | Microsoft.Sql/servers/elasticPools/dtu | Wartość całkowita udostępnionych jednostek DTU dla puli elastycznej bazy danych. |
| serwery/elasticpools | Microsoft.Sql/servers/elasticPools/edition | Ustaw edition puli elastycznej. |

**Microsoft.Storage/storageAccounts**

| Alias | Opis |
| ----- | ----------- |
| Microsoft.Storage/storageAccounts/accessTier | Ustawianie warstwy dostępu używany na potrzeby rozliczeń. |
| Microsoft.Storage/storageAccounts/accountType | Nazwa jednostki SKU zestawu. |
| Microsoft.Storage/storageAccounts/enableBlobEncryption | Określ, czy usługa szyfruje dane, jak są przechowywane w usłudze magazyn obiektów blob. |
| Microsoft.Storage/storageAccounts/enableFileEncryption | Określ, czy usługa szyfruje dane, jak są przechowywane w usłudze magazyn plików. |
| Microsoft.Storage/storageAccounts/sku.name | Nazwa jednostki SKU zestawu. |
| Microsoft.Storage/storageAccounts/supportsHttpsTrafficOnly | Ustaw, aby zezwolić tylko na ruch protokołu https do usługi Magazyn. |

## <a name="initiatives"></a>Inicjatywy

Włącz inicjatyw kilka grupy powiązane definicje zasad, aby uprościć zadania i zarządzania, ponieważ współdziała z grupą jako pojedynczy element. Na przykład można grupować wszystkie powiązane definicje zasad znakowania w jednym inicjatywy. Zamiast przypisywać każdej zasady pojedynczo, należy zastosować tej inicjatywy.

Poniższy przykład przedstawia sposób tworzenia inicjatywą obsługi dwa tagi: `costCenter` i `productName`. Używa dwóch wbudowane zasady do zastosowania domyślną wartość tagu.


```json
{
    "properties": {
        "displayName": "Billing Tags Policy",
        "policyType": "Custom",
        "description": "Specify cost Center tag and product name tag",
        "parameters": {
            "costCenterValue": {
                "type": "String",
                "metadata": {
                    "description": "required value for Cost Center tag"
                }
            },
            "productNameValue": {
                "type": "String",
                "metadata": {
                    "description": "required value for product Name tag"
                }
            }
        },
        "policyDefinitions": [
            {
                "policyDefinitionId": "/providers/Microsoft.Authorization/policyDefinitions/1e30110a-5ceb-460c-a204-c1c3969c6d62",
                "parameters": {
                    "tagName": {
                        "value": "costCenter"
                    },
                    "tagValue": {
                        "value": "[parameters('costCenterValue')]"
                    }
                }
            },
            {
                "policyDefinitionId": "/providers/Microsoft.Authorization/policyDefinitions/2a0e14a6-b0a6-4fab-991a-187a4f81c498",
                "parameters": {
                    "tagName": {
                        "value": "costCenter"
                    },
                    "tagValue": {
                        "value": "[parameters('costCenterValue')]"
                    }
                }
            },
            {
                "policyDefinitionId": "/providers/Microsoft.Authorization/policyDefinitions/1e30110a-5ceb-460c-a204-c1c3969c6d62",
                "parameters": {
                    "tagName": {
                        "value": "productName"
                    },
                    "tagValue": {
                        "value": "[parameters('productNameValue')]"
                    }
                }
            },
            {
                "policyDefinitionId": "/providers/Microsoft.Authorization/policyDefinitions/2a0e14a6-b0a6-4fab-991a-187a4f81c498",
                "parameters": {
                    "tagName": {
                        "value": "productName"
                    },
                    "tagValue": {
                        "value": "[parameters('productNameValue')]"
                    }
                }
            }
        ]
    },
    "id": "/subscriptions/<subscription-id>/providers/Microsoft.Authorization/policySetDefinitions/billingTagsPolicy",
    "type": "Microsoft.Authorization/policySetDefinitions",
    "name": "billingTagsPolicy"
}
```

## <a name="next-steps"></a>Kolejne kroki

- Przejrzyj przykłady szablonu zasad Azure w [szablony zasad Azure](json-samples.md).
