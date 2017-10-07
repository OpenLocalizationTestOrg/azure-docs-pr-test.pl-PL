---
title: "Menedżer zasobów aaaAzure struktury szablonu i składni | Dokumentacja firmy Microsoft"
description: "Opis hello struktury i właściwości szablonów usługi Azure Resource Manager za pomocą składni deklaratywnej JSON."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 19694cb4-d9ed-499a-a2cc-bcfc4922d7f5
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/14/2017
ms.author: tomfitz
ms.openlocfilehash: b0709852f8777c91cc1704d6bca16257a017d515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="understand-hello-structure-and-syntax-of-azure-resource-manager-templates"></a>Struktura hello i składni szablonów usługi Azure Resource Manager
W tym temacie opisano strukturę hello szablonu usługi Azure Resource Manager. Stanowi hello różnych części szablonu i hello właściwości, które są dostępne w tych sekcjach. Szablon Hello składa się z kodu JSON i wyrażeń, że możesz użyć wartości tooconstruct dla danego wdrożenia. Samouczek krok po kroku dotyczące tworzenia szablonu, zobacz [Tworzenie pierwszego szablonu usługi Azure Resource Manager](resource-manager-create-first-template.md).

## <a name="template-format"></a>Format szablonu
W swojej najprostszej struktury szablonu zawiera hello następujące elementy:

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "",
    "parameters": {  },
    "variables": {  },
    "resources": [  ],
    "outputs": {  }
}
```

| Nazwa elementu | Wymagane | Opis |
|:--- |:--- |:--- |
| $schema |Tak |Lokalizacja pliku hello schematu JSON, który zawiera opis wersji hello hello języka szablonu. Użyj adresu URL hello pokazano hello poprzedzających przykład. |
| contentVersion |Tak |Wersja szablonu hello (na przykład 1.0.0.0). Musisz podać wartości dla tego elementu. W przypadku wdrażania zasobów przy użyciu szablonu hello, ta wartość może być używane toomake się, że ten szablon prawo hello jest używany. |
| parameters |Nie |Wartości, które są dostarczane, gdy wdrożenie jest wykonywane toocustomize zasobu wdrożenia. |
| zmienne |Nie |Wartości, które są używane jako fragmenty JSON w wyrażeń języka szablonu hello szablonu toosimplify. |
| Zasoby |Tak |Typy zasobów, które są wdrożone lub zaktualizowane w grupie zasobów. |
| dane wyjściowe |Nie |Wartości, które są zwracane po wdrożeniu. |

Każdy element zawiera właściwości, które można ustawić. Poniższy przykład Hello zawiera hello pełnej składni szablonu:

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "",
    "parameters": {  
        "<parameter-name>" : {
            "type" : "<type-of-parameter-value>",
            "defaultValue": "<default-value-of-parameter>",
            "allowedValues": [ "<array-of-allowed-values>" ],
            "minValue": <minimum-value-for-int>,
            "maxValue": <maximum-value-for-int>,
            "minLength": <minimum-length-for-string-or-array>,
            "maxLength": <maximum-length-for-string-or-array-parameters>,
            "metadata": {
                "description": "<description-of-hello parameter>" 
            }
        }
    },
    "variables": {  
        "<variable-name>": "<variable-value>",
        "<variable-name>": { 
            <variable-complex-type-value> 
        }
    },
    "resources": [
      {
          "condition": "<boolean-value-whether-to-deploy>",
          "apiVersion": "<api-version-of-resource>",
          "type": "<resource-provider-namespace/resource-type-name>",
          "name": "<name-of-the-resource>",
          "location": "<location-of-resource>",
          "tags": {
              "<tag-name1>": "<tag-value1>",
              "<tag-name2>": "<tag-value2>"
          },
          "comments": "<your-reference-notes>",
          "copy": {
              "name": "<name-of-copy-loop>",
              "count": "<number-of-iterations>",
              "mode": "<serial-or-parallel>",
              "batchSize": "<number-to-deploy-serially>"
          },
          "dependsOn": [
              "<array-of-related-resource-names>"
          ],
          "properties": {
              "<settings-for-the-resource>",
              "copy": [
                  {
                      "name": ,
                      "count": ,
                      "input": {}
                  }
              ]
          },
          "resources": [
              "<array-of-child-resources>"
          ]
      }
    ],
    "outputs": {
        "<outputName>" : {
            "type" : "<type-of-output-value>",
            "value": "<output-value-expression>"
        }
    }
}
```

Omówione hello części szablonu hello bardziej szczegółowo w dalszej części tego tematu.

## <a name="expressions-and-functions"></a>Wyrażeń i funkcji
Podstawowa składnia Hello szablonu hello jest JSON. Jednak wartości JSON hello dostępnych w szablonie hello rozszerzyć wyrażeń i funkcji.  Wyrażenia są zapisywane w literałach ciągu JSON, których pierwszy i ostatnie znaki to nawiasy hello: `[` i `]`odpowiednio. Hello wartość wyrażenia hello jest oceniane podczas wdrażania szablonu hello. Gdy zapisywane jako literału ciągu, hello wynikiem obliczenia wyrażenia hello może mieć innego typu JSON, takich jak tablicy lub liczba całkowita, w zależności od hello rzeczywistego wyrażenia.  toohave literałem rozpoczynać nawiasu `[`, ale nie została ona interpretowana jako wyrażenie, Dodaj ciąg hello nawiasu dodatkowe toostart z `[[`.

Zwykle Użyj wyrażenia z operacjami tooperform funkcje związane z konfigurowaniem wdrażania hello. Po prostu, tak jak w języku JavaScript, wywołania funkcji są sformatowane jako `functionName(arg1,arg2,arg3)`. Możesz odwoływać się do właściwości przy użyciu operatorów hello kropka i [Indeks].

Witaj poniższy przykład pokazuje, jak toouse kilka funkcji podczas tworzenia wartości:

```json
"variables": {
    "location": "[resourceGroup().location]",
    "usernameAndPassword": "[concat(parameters('username'), ':', parameters('password'))]",
    "authorizationHeader": "[concat('Basic ', base64(variables('usernameAndPassword')))]"
}
```

Witaj pełną listę funkcji szablonu, zobacz [funkcje szablonu usługi Azure Resource Manager](resource-group-template-functions.md). 

## <a name="parameters"></a>Parametry
W sekcji parametrów hello hello szablonu należy określić wartości, które można wprowadzić w przypadku wdrażania hello zasobów. Wartości tych parametrów Włącz toocustomize hello wdrożenia, podając wartości, które są dostosowane określonym środowisku (na przykład deweloperów, testowego i produkcyjnego). Nie masz tooprovide parametry w szablonie, ale bez parametrów szablonu będzie zawsze wdrażać hello hello tyle samo zasobów o tej samej nazwy, lokalizacji i właściwości.

Definiuje parametry z następującej struktury hello:

```json
"parameters": {
    "<parameter-name>" : {
        "type" : "<type-of-parameter-value>",
        "defaultValue": "<default-value-of-parameter>",
        "allowedValues": [ "<array-of-allowed-values>" ],
        "minValue": <minimum-value-for-int>,
        "maxValue": <maximum-value-for-int>,
        "minLength": <minimum-length-for-string-or-array>,
        "maxLength": <maximum-length-for-string-or-array-parameters>,
        "metadata": {
            "description": "<description-of-hello parameter>" 
        }
    }
}
```

| Nazwa elementu | Wymagane | Opis |
|:--- |:--- |:--- |
| Nazwa parametru |Tak |Nazwa parametru hello. Musi być prawidłowym identyfikatorem języka JavaScript. |
| type |Tak |Typ wartości parametru hello. Lista hello dozwolonymi typami pod tą tabelą. |
| Wartość domyślna |Nie |Wartość domyślna parametru hello, jeśli wartość nie zostanie podana dla parametru hello. |
| allowedValues |Nie |Tablica toomake parametru hello się upewnić, że wartość prawej strony hello jest dozwolonych wartości. |
| Wartość MinValue |Nie |Witaj minimalną wartość parametrów typu int, ta wartość jest włącznie. |
| MaxValue |Nie |Witaj maksymalną wartość parametrów typu int, ta wartość jest włącznie. |
| Element minLength |Nie |Witaj minimalną długość ciągu, secureString i parametrów typu tablicy, ta wartość jest włącznie. |
| Element maxLength |Nie |Witaj maksymalną długość ciągu, secureString i parametrów typu tablicy, ta wartość jest włącznie. |
| description |Nie |Opis parametru hello, który jest wyświetlany toousers za pośrednictwem portalu hello. |

Witaj dozwolonymi typami i wartości to:

* **ciąg**
* **secureString**
* **int**
* **wartość logiczna**
* **obiekt** 
* **secureObject**
* **Tablica**

toospecify parametr jako opcjonalną, podaj wartości (może być ciągiem pustym). 

Jeśli określono nazwę parametru w szablonie parametru hello polecenia toodeploy hello szablonu jest zgodny, jest potencjalnych niejednoznaczności wartości hello. Menedżer zasobów usuwa to pomyłka, dodając przyrostek hello **FromTemplate** toohello parametru szablonu. Na przykład, jeśli zawiera parametr o nazwie **ResourceGroupName** w szablonie, powoduje konflikt z hello **ResourceGroupName** parametru w hello [ Nowy AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) polecenia cmdlet. Podczas wdrażania, są tooprovide zostanie wyświetlony monit o wartości **ResourceGroupNameFromTemplate**. Ogólnie rzecz biorąc należy unikać to pomyłka nie nadawanie nazw parametrów z hello takie same nazwy jako parametry używane dla operacji wdrożenia.

> [!NOTE]
> Wszystkie hasła, klucze i innych informacji poufnych, należy użyć hello **secureString** typu. W przypadku przekazania danych poufnych w obiekcie JSON, użyj hello **secureObject** typu. Nie można odczytać parametrów szablonu z typami secureString lub secureObject po wdrożeniu zasobów. 
> 
> Na przykład hello następujący wpis w historii wdrożenia hello pokazuje hello wartość dla ciągu lub obiektu, ale nie dla secureString i secureObject.
>
> ![Pokaż wartości wdrożenia](./media/resource-group-authoring-templates/show-parameters.png)  
>

powitania po przykładzie pokazano, jak toodefine parametry:

```json
"parameters": {
    "siteName": {
        "type": "string",
        "defaultValue": "[concat('site', uniqueString(resourceGroup().id))]"
    },
    "hostingPlanName": {
        "type": "string",
        "defaultValue": "[concat(parameters('siteName'),'-plan')]"
    },
    "skuName": {
        "type": "string",
        "defaultValue": "F1",
        "allowedValues": [
          "F1",
          "D1",
          "B1",
          "B2",
          "B3",
          "S1",
          "S2",
          "S3",
          "P1",
          "P2",
          "P3",
          "P4"
        ]
    },
    "skuCapacity": {
        "type": "int",
        "defaultValue": 1,
        "minValue": 1
    }
}
```

Dla jak wartości parametrów hello tooinput, podczas wdrażania, zobacz [wdrażania aplikacji przy użyciu szablonu usługi Azure Resource Manager](resource-group-template-deploy.md). 

## <a name="variables"></a>Zmienne
W sekcji zmiennych hello utworzymy wartości, które mogą być używane w szablonie. Nie trzeba toodefine zmiennych, ale one często uprościć szablonu zmniejszając złożonych wyrażeń.

Można zdefiniować zmienne z następującej struktury hello:

```json
"variables": {
    "<variable-name>": "<variable-value>",
    "<variable-name>": { 
        <variable-complex-type-value> 
    }
}
```

powitania po przykładzie pokazano, jak toodefine zmiennej, która jest tworzony z dwóch wartości parametrów:

```json
"variables": {
    "connectionString": "[concat('Name=', parameters('username'), ';Password=', parameters('password'))]"
}
```

Witaj kolejnym przykładzie pokazano zmiennej, która jest typem złożonym JSON i zmienne, które są tworzone na podstawie innych zmiennych:

```json
"parameters": {
    "environmentName": {
        "type": "string",
        "allowedValues": [
          "test",
          "prod"
        ]
    }
},
"variables": {
    "environmentSettings": {
        "test": {
            "instancesSize": "Small",
            "instancesCount": 1
        },
        "prod": {
            "instancesSize": "Large",
            "instancesCount": 4
        }
    },
    "currentEnvironmentSettings": "[variables('environmentSettings')[parameters('environmentName')]]",
    "instancesSize": "[variables('currentEnvironmentSettings').instancesSize]",
    "instancesCount": "[variables('currentEnvironmentSettings').instancesCount]"
}
```

## <a name="resources"></a>Zasoby
W sekcji zasobów hello można zdefiniować hello zasobów, które są wdrożone lub aktualizowane. W tej sekcji można uzyskać skomplikowane, ponieważ należy poznać hello typów wdrażania tooprovide hello właściwych wartości. Witaj określonych zasobów wartości (apiVersion, typ i właściwości) należy tooset, zobacz [zdefiniować zasoby w szablonach usługi Azure Resource Manager](/azure/templates/). 

Definiuje się zasoby z następującej struktury hello:

```json
"resources": [
  {
      "condition": "<boolean-value-whether-to-deploy>",
      "apiVersion": "<api-version-of-resource>",
      "type": "<resource-provider-namespace/resource-type-name>",
      "name": "<name-of-the-resource>",
      "location": "<location-of-resource>",
      "tags": {
          "<tag-name1>": "<tag-value1>",
          "<tag-name2>": "<tag-value2>"
      },
      "comments": "<your-reference-notes>",
      "copy": {
          "name": "<name-of-copy-loop>",
          "count": "<number-of-iterations>",
          "mode": "<serial-or-parallel>",
          "batchSize": "<number-to-deploy-serially>"
      },
      "dependsOn": [
          "<array-of-related-resource-names>"
      ],
      "properties": {
          "<settings-for-the-resource>",
          "copy": [
              {
                  "name": ,
                  "count": ,
                  "input": {}
              }
          ]
      },
      "resources": [
          "<array-of-child-resources>"
      ]
  }
]
```

| Nazwa elementu | Wymagane | Opis |
|:--- |:--- |:--- |
| Warunek | Nie | Wartość logiczna wskazująca, czy zasób hello jest wdrażany. |
| apiVersion |Tak |Wersja hello toouse interfejsu API REST do tworzenia hello zasobów. |
| type |Tak |Typ zasobu hello. Ta wartość jest kombinacją hello przestrzeń nazw dostawcy zasobów hello i typu zasobu hello (takich jak **magazyn.Microsoft/kontamagazynu**). |
| name |Tak |Nazwa zasobu hello. Witaj musi spełniać zdefiniowane w RFC3986 ograniczenia składnika identyfikatora URI. Ponadto usług platformy Azure, które udostępniają hello zasobu Nazwa toooutside strony sprawdzania poprawności, nie jest toospoof próba toomake nazwa hello tożsamość. |
| location |Zmienia się |Obsługiwane lokalizacje geograficzne z hello podać zasobów. Można wybrać dowolny z dostępnych lokalizacji hello, ale zazwyczaj ułatwia wykrywanie toopick jest Zamknij tooyour użytkowników. Zazwyczaj również dobrym rozwiązaniem jest tooplace zasobów, współpracujące ze sobą w hello sam region. Większość typów zasobów wymaga lokalizacji, ale nie wymagają lokalizację niektórych typów (takich jak przypisanie roli). Zobacz [Ustaw lokalizację zasobów w szablonach usługi Azure Resource Manager](resource-manager-template-location.md). |
| tags |Nie |Tagi, które są skojarzone z hello zasobów. Zobacz [tagów zasobów w szablonach usługi Azure Resource Manager](resource-manager-template-tags.md). |
| Komentarze |Nie |Notatki za dokumentację hello zasobów w szablonie |
| Kopiuj |Nie |W razie potrzeby więcej niż jedno wystąpienie hello liczba toocreate zasobów. tryb domyślny Hello jest równoległe. Określ tryb serial, gdy nie ma wszystkich lub hello toodeploy zasobów na powitania tym samym czasie. Aby uzyskać więcej informacji, zobacz [utworzyć wiele wystąpień zasobów usługi Azure Resource Manager](resource-group-create-multiple.md). |
| dependsOn |Nie |Zasoby, które należy wdrożyć przed wdrożeniem tego zasobu. Menedżer zasobów ocenia hello zależności między zasobami i wdraża je w odpowiedniej kolejności hello. Zasoby nie są zależne od siebie, są wdrożone równolegle. Hello wartość może być rozdzielaną przecinkami listą zasobu nazwy lub unikatowych identyfikatorów zasobów. Tylko listy zasobów, które są wdrażane w tym szablonie. Zasoby, które nie są zdefiniowane w tym szablonie musi już istnieć. Unikaj Dodawanie zależności niepotrzebne, jak mogą spowalniać wdrożenia i utworzyć zależności cykliczne. Aby uzyskać wskazówki dotyczące zależności ustawienia, zobacz [Definiowanie zależności w szablonach usługi Azure Resource Manager](resource-group-define-dependencies.md). |
| properties |Nie |Ustawienia konfiguracji określonych zasobów. Hello wartości właściwości hello są takie same hello jako wartości hello, podane w treści żądania hello hello interfejsu API REST operacji (metody PUT) toocreate hello zasobu. Można również określić toocreate tablicy kopiowania wielu wystąpień właściwości. Aby uzyskać więcej informacji, zobacz [utworzyć wiele wystąpień zasobów usługi Azure Resource Manager](resource-group-create-multiple.md). |
| Zasoby |Nie |Zasoby podrzędne, które są zależne od zasobów hello definiowanego. Podaj tylko typy zasobów, które są dozwolone w ramach schematu hello hello zasobu nadrzędnego. Witaj pełny typ zasobu podrzędnego hello zawiera typ zasobu nadrzędnego hello, takich jak **Microsoft.Web/sites/extensions**. Zależność od zasobu nadrzędnego hello jest niejawnego. Jawnie zdefiniuj tej zależności. |

Witaj sekcja zasobów zawiera tablicę hello toodeploy zasobów. W ramach każdego zasobu można również zdefiniować tablicę zasoby podrzędne. W związku z tym sekcji zasobów można mieć struktury, takiej jak:

```json
"resources": [
  {
      "name": "resourceA",
  },
  {
      "name": "resourceB",
      "resources": [
        {
            "name": "firstChildResourceB",
        },
        {   
            "name": "secondChildResourceB",
        }
      ]
  },
  {
      "name": "resourceC",
  }
]
```      

Aby uzyskać więcej informacji na temat definiowania zasoby podrzędne, zobacz [Ustaw nazwę i typ zasobu podrzędnego w szablonie usługi Resource Manager](resource-manager-template-child-resource.md).

Witaj **warunku** element określa, czy zasób hello jest wdrażany. Witaj wartość dla tego elementu rozpoznaje tootrue, lub FAŁSZ. Na przykład toospecify czy nowe konto magazynu jest wdrażana, użyj:

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

toospecify czy wdrożono maszynę wirtualną za pomocą hasła lub klucza SSH, zdefiniuj dwie wersje hello maszyny wirtualnej w szablonie i użyj **warunku** toodifferentiate użycia. Podaj parametr, który określa, które toodeploy scenariusza.

```json
{
    "condition": "[equals(parameters('passwordOrSshKey'),'password')]",
    "apiVersion": "2016-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[concat(variables('vmName'),'password')]",
    "properties": {
        "osProfile": {
            "computerName": "[variables('vmName')]",
            "adminUsername": "[parameters('adminUsername')]",
            "adminPassword": "[parameters('adminPassword')]"
        },
        ...
    },
    ...
},
{
    "condition": "[equals(parameters('passwordOrSshKey'),'sshKey')]",
    "apiVersion": "2016-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[concat(variables('vmName'),'ssh')]",
    "properties": {
        "osProfile": {
            "linuxConfiguration": {
                "disablePasswordAuthentication": "true",
                "ssh": {
                    "publicKeys": [
                        {
                            "path": "[variables('sshKeyPath')]",
                            "keyData": "[parameters('adminSshKey')]"
                        }
                    ]
                }
            }
        },
        ...
    },
    ...
}
``` 

Na przykład przy użyciu hasła lub maszyny wirtualnej toodeploy klucza SSH, zobacz [nazwa użytkownika lub SSH szablonu warunku](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).

## <a name="outputs"></a>dane wyjściowe
W sekcji danych wyjściowych hello należy określić wartości, które są zwracane z wdrożenia. Na przykład można zwrócić hello URI tooaccess wdrożonych zasobów.

Witaj poniższy przykład przedstawia hello struktura definicji danych wyjściowych:

```json
"outputs": {
    "<outputName>" : {
        "type" : "<type-of-output-value>",
        "value": "<output-value-expression>"
    }
}
```

| Nazwa elementu | Wymagane | Opis |
|:--- |:--- |:--- |
| outputName |Tak |Nazwa wartości wyjściowych hello. Musi być prawidłowym identyfikatorem języka JavaScript. |
| type |Tak |Typ wartości wyjściowych hello. Dane wyjściowe wartości obsługuje hello takie same typy tablic jako parametrów wejściowych szablonu. |
| wartość |Tak |Wyrażenia języka szablonu, który jest obliczany i zwracany, jako wartość wyjściowa. |

Witaj poniższy przykład przedstawia wartość, która jest zwracana w sekcji danych wyjściowych hello.

```json
"outputs": {
    "siteUri" : {
        "type" : "string",
        "value": "[concat('http://',reference(resourceId('Microsoft.Web/sites', parameters('siteName'))).hostNames[0])]"
    }
}
```

Aby uzyskać więcej informacji na temat pracy z danych wyjściowych, zobacz [udostępniania stanu w szablonach usługi Azure Resource Manager](best-practices-resource-manager-state.md).

## <a name="template-limits"></a>Limity szablonu

Limit rozmiaru hello too1 Twojego szablonu MB, a każdy parametr plików too64 KB. limit 1 MB Hello jest stosowana toohello stan końcowy hello szablonu zostanie rozwinięty definicje interakcyjnych zasobów i wartości zmiennych i parametrów. 

Możesz również są ograniczone do:

* Parametry 256
* zmienne 256
* 800 zasoby (w tym liczba kopii)
* 64 wartości danych wyjściowych
* 24 576 znaków w wyrażeniu szablonu

Niektóre limity szablonu może przekroczyć przy użyciu szablonu zagnieżdżonego. Aby uzyskać więcej informacji, zobacz [przy użyciu szablonów połączonych w przypadku wdrażania zasobów Azure](resource-group-linked-templates.md). numer hello tooreduce parametrów, zmiennych lub dane wyjściowe, można połączyć kilka wartości do obiektu. Aby uzyskać więcej informacji, zobacz [obiektów jako parametry](resource-manager-objects-as-parameters.md).

## <a name="next-steps"></a>Następne kroki
* Szablony pełną tooview do różnych rozwiązań, zobacz hello [szablonów Szybki Start Azure](https://azure.microsoft.com/documentation/templates/).
* Szczegółowe informacje na temat korzystania z szablonu jako funkcje hello, zobacz [funkcje szablonów usługi Azure Resource Manager](resource-group-template-functions.md).
* toocombine wielu szablonów podczas wdrażania, zobacz [za pomocą szablonów połączonych z usługą Azure Resource Manager](resource-group-linked-templates.md).
* Może być konieczne toouse zasoby, które istnieją w innej grupie zasobów. Ten scenariusz jest typowy podczas pracy z kontami magazynu lub sieci wirtualne, które są współdzielone przez wiele grup zasobów. Aby uzyskać więcej informacji, zobacz hello [funkcja resourceId](resource-group-template-functions-resource.md#resourceid).
