---
title: "przepływy pracy aaaDefine z JSON - Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Jak toowrite definicji przepływu pracy w formacie JSON dla usługi logic apps"
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: d565873c-6b1b-4057-9250-cf81a96180ae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 03/29/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 0d69d334ecee9c3e7f8684cfde68ef0e85280358
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-workflow-definitions-for-logic-apps-using-json"></a>Tworzenie definicji przepływu pracy dla usługi logic apps za pomocą formatu JSON

Można utworzyć definicji przepływu pracy dla [Azure Logic Apps](logic-apps-what-are-logic-apps.md) prosty, deklaratywny języka JSON. Jeśli nie jest jeszcze, najpierw należy przejrzeć [jak toocreate pierwszej aplikacji logiki z projektanta aplikacji logiki](logic-apps-create-a-logic-app.md). Zobacz też hello [pełne informacje dotyczące hello język definicji przepływu pracy](http://aka.ms/logicappsdocs).

## <a name="repeat-steps-over-a-list"></a>Powtórz kroki od listy

tooiterate przez tablicę, która ma too10, 000 elementów i wykonania czynności dla każdego elementu, użyj hello [typu foreach](logic-apps-loops-and-scopes.md).

## <a name="handle-failures-if-something-goes-wrong"></a>Obsługa błędów, jeśli jakaś nieprawidłowość

Zwykle ma tooinclude *krok korygowania* — niektóre logikę, która wykonuje *tylko wtedy, gdy* co najmniej jednego wywołania zakończyć się niepowodzeniem. W tym przykładzie pobiera dane z różnych miejsc, ale w przypadku niepowodzenia wywołania hello chcemy tooPOST wiadomość gdzieś, firma Microsoft może śledzić awarii później:  

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {},
  "triggers": {
    "Request": {
      "type": "request",
      "kind": "http"
    }
  },
  "actions": {
    "readData": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      }
    },
    "postToErrorMessageQueue": {
      "type": "ApiConnection",
      "inputs": "...",
      "runAfter": {
        "readData": [
          "Failed"
        ]
      }
    }
  },
  "outputs": {}
}
```

toospecify który `postToErrorMessageQueue` działa tylko `readData` ma `Failed`, użyj hello `runAfter` właściwości, na przykład toospecify listę możliwych wartości, tak aby `runAfter` może być `["Succeeded", "Failed"]`.

Na koniec, ponieważ w tym przykładzie obsługuje teraz błąd hello, firma Microsoft nie jest już oznaczyć hello Uruchom jako `Failed`. Ponieważ dodaliśmy hello kroku obsługi tego błędu w tym przykładzie ma hello Uruchom `Succeeded` chociaż jeden krok `Failed`.

## <a name="execute-two-or-more-steps-in-parallel"></a>Wykonaj kroki co najmniej dwa równolegle

toorun hello wielu akcji równolegle, `runAfter` właściwości musi być taka sama w czasie wykonywania. 

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {},
  "triggers": {
    "Request": {
      "kind": "http",
      "type": "Request"
    }
  },
  "actions": {
    "readData": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      }
    },
    "branch1": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "readData": [
          "Succeeded"
        ]
      }
    },
    "branch2": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "readData": [
          "Succeeded"
        ]
      }
    }
  },
  "outputs": {}
}
```

W tym przykładzie zarówno `branch1` i `branch2` są ustawione toorun po `readData`. W związku z tym obu gałęziach są uruchamiane równolegle. Sygnatura czasowa powitania dla obu gałęziach są identyczne.

![Równoległe](media/logic-apps-author-definitions/parallel.png)

## <a name="join-two-parallel-branches"></a>Dołącz do dwóch równoległych gałęziach

Możesz także dołączyć do dwóch akcje, które są ustawione toorun równolegle przez dodanie elementów toohello `runAfter` właściwości, jak w poprzednim przykładzie hello.

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-04-01-preview/workflowdefinition.json#",
  "actions": {
    "readData": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {}
    },
    "branch1": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "readData": [
          "Succeeded"
        ]
      }
    },
    "branch2": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "readData": [
          "Succeeded"
        ]
      }
    },
    "join": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "branch1": [
          "Succeeded"
        ],
        "branch2": [
          "Succeeded"
        ]
      }
    }
  },
  "parameters": {},
  "triggers": {
    "Request": {
      "type": "Request",
      "kind": "Http",
      "inputs": {
        "schema": {}
      }
    }
  },
  "contentVersion": "1.0.0.0",
  "outputs": {}
}
```

![Równoległe](media/logic-apps-author-definitions/join.png)

## <a name="map-list-items-tooa-different-configuration"></a>Mapa listy elementów tooa innej konfiguracji

Następnie Załóżmy, że chcemy tooget innej zawartości na podstawie hello wartości właściwości. Można utworzyć mapy toodestinations wartości jako parametr:  

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "specialCategories": {
      "defaultValue": [
        "science",
        "google",
        "microsoft",
        "robots",
        "NSA"
      ],
      "type": "Array"
    },
    "destinationMap": {
      "defaultValue": {
        "science": "http://www.nasa.gov",
        "microsoft": "https://www.microsoft.com/en-us/default.aspx",
        "google": "https://www.google.com",
        "robots": "https://en.wikipedia.org/wiki/Robot",
        "NSA": "https://www.nsa.gov/"
      },
      "type": "Object"
    }
  },
  "triggers": {
    "Request": {
      "type": "Request",
      "kind": "http"
    }
  },
  "actions": {
    "getArticles": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "https://ajax.googleapis.com/ajax/services/feed/load?v=1.0&q=http://feeds.wired.com/wired/index"
      }
    },
    "forEachArticle": {
      "type": "foreach",
      "foreach": "@body('getArticles').responseData.feed.entries",
      "actions": {
        "ifGreater": {
          "type": "if",
          "expression": "@greater(length(intersection(item().categories, parameters('specialCategories'))), 0)",
          "actions": {
            "getSpecialPage": {
              "type": "Http",
              "inputs": {
                "method": "GET",
                "uri": "@parameters('destinationMap')[first(intersection(item().categories, parameters('specialCategories')))]"
              }
            }
          }
        }
      },
      "runAfter": {
        "getArticles": [
          "Succeeded"
        ]
      }
    }
  }
}
```

W takim przypadku najpierw pobrać listę artykułów. W oparciu o kategorię hello, która została zdefiniowana jako parametru, drugi etap hello używa toolook mapy, zapasowej hello adresu URL pobierania zawartości hello.

W tym miejscu toonote sytuacje: 

*   Witaj [ `intersection()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#intersection) funkcja sprawdza, czy kategoria hello zgodny jedną hello znane zdefiniowanych kategoriach.

*   Po uzyskujemy kategorii hello możemy ściągnięcia hello elementu z użyciem nawiasów kwadratowych mapy hello:`parameters[...]`

## <a name="process-strings"></a>Ciągi procesu

Można użyć różnych funkcji toomanipulate ciągów. Na przykład załóżmy, że mamy ciąg chcemy toopass tooa system, że nie wątpliwości właściwe obsługę kodowania znaków. Jedną z opcji jest toobase64 ten ciąg do zakodowania. Jednak tooavoid anulowanie w adresie URL zamierzamy tooreplace kilku znaków. 

Również chcemy podciąg nazwy hello kolejności, ponieważ hello pięć pierwszych znaków nie są używane.

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "order": {
      "defaultValue": {
        "quantity": 10,
        "id": "myorder1",
        "orderer": "NAME=Contoso"
      },
      "type": "Object"
    }
  },
  "triggers": {
    "request": {
      "type": "request",
      "kind": "http"
    }
  },
  "actions": {
    "order": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://www.example.com/?id=@{replace(replace(base64(substring(parameters('order').orderer,5,sub(length(parameters('order').orderer), 5) )),'+','-') ,'/' ,'_' )}"
      }
    }
  },
  "outputs": {}
}
```

Pracy z wewnątrz toooutside:

1. Pobierz hello [ `length()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#length) o nazwę osoby hello zamawiającej, dlatego firma Microsoft wrócić hello całkowita liczba znaków.

2. Odejmowanie 5, ponieważ chcemy krótszego ciągu.

3. W rzeczywistości zająć hello [ `substring()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#substring). Rozpoczniemy pod indeksem `5` i przejdź hello pozostałej części ciąg hello.

4. Konwertuj to tooa podciąg [ `base64()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#base64) ciąg.

5. [`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace)wszystkie hello `+` znaków i zawierają `-` znaków.

6. [`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace)wszystkie hello `/` znaków i zawierają `_` znaków.

## <a name="work-with-date-times"></a>Praca z daty i godziny

Daty i godziny mogą być przydatne, szczególnie w przypadku, gdy chcesz toopull danych ze źródła danych, który nie obsługuje naturalnie *wyzwalaczy*. Umożliwia także daty i godziny do znajdowania, jak długo różne kroki są tworzone.

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "order": {
      "defaultValue": {
        "quantity": 10,
        "id": "myorder1"
      },
      "type": "Object"
    }
  },
  "triggers": {
    "Request": {
      "type": "request",
      "kind": "http"
    }
  },
  "actions": {
    "order": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://www.example.com/?id=@{parameters('order').id}"
      }
    },
    "ifTimingWarning": {
      "type": "If",
      "expression": "@less(actions('order').startTime,addseconds(utcNow(),-1))",
      "actions": {
        "timingWarning": {
          "type": "Http",
          "inputs": {
            "method": "GET",
            "uri": "http://www.example.com/?recordLongOrderTime=@{parameters('order').id}&currentTime=@{utcNow('r')}"
          }
        }
      },
      "runAfter": {
        "order": [
          "Succeeded"
        ]
      }
    }
  },
  "outputs": {}
}
```

W tym przykładzie mamy wyodrębnić hello `startTime` hello w poprzednim kroku. Następnie możemy pobrać hello bieżącego czasu i odjąć 1 sekundy:

[`addseconds(..., -1)`](https://msdn.microsoft.com/library/azure/mt643789.aspx#addseconds) 

Inne jednostki czasu, można używać tak samo, jak `minutes` lub `hours`. Na koniec mamy Porównaj te dwie wartości. Jeśli hello pierwsza wartość jest mniejsza niż wartość drugiego hello, a następnie więcej niż jednej sekundy są spełnione, ponieważ najpierw umieszczono hello kolejności.

tooformat dat, możemy użyć ciągu elementy formatujące. Na przykład hello tooget RFC1123, używamy [ `utcnow('r')` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow). toolearn o formatowania daty, zobacz [język definicji przepływu pracy](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).

## <a name="deployment-parameters-for-different-environments"></a>Parametry wdrożenia dla różnych środowisk

Zazwyczaj cyklami życia wdrożenia ma środowiska programowania, środowisku przemieszczania i środowiska produkcyjnego. Na przykład możesz użyć tej samej definicji w tych środowiskach hello, ale Użyj różnych baz danych. Podobnie, może być toouse hello tej samej definicji w różnych regionach, wysokiej dostępności, ale mają każdego logiki aplikacji wystąpienia tootalk toothat regionu bazy danych.
W tym scenariuszu różni się od podejmowania parametrów w *środowiska uruchomieniowego* gdzie zamiast tego należy używać hello `trigger()` działać jak w poprzednim przykładzie hello.

Można uruchomić z podstawową definicję, tak jak ten przykład:

```
{
    "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "uri": {
            "type": "string"
        }
    },
    "triggers": {
        "request": {
          "type": "request",
          "kind": "http"
        }
    },
    "actions": {
        "readData": {
            "type": "Http",
            "inputs": {
                "method": "GET",
                "uri": "@parameters('uri')"
            }
        }
    },
    "outputs": {}
}
```

W rzeczywistych hello `PUT` żądania dla aplikacji logiki hello, możesz podać parametr hello `uri`. Ponieważ istnieje już wartość domyślną, ładunku aplikacji logiki hello wymaga tego parametru:

```
{
    "properties": {},
        "definition": {
          // Use hello definition from above here
        },
        "parameters": {
            "connection": {
                "value": "https://my.connection.that.is.per.enviornment"
            }
        }
    },
    "location": "westus"
}
``` 

W każdym środowisku można podać inną wartość dla hello `connection` parametru. 

Dla wszystkich hello opcje dotyczące tworzenia i zarządzania aplikacji logiki, zobacz hello [dokumentacja interfejsu API REST](https://msdn.microsoft.com/library/azure/mt643787.aspx). 
