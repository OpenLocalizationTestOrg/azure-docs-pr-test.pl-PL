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
# <a name="create-workflow-definitions-for-logic-apps-using-json"></a><span data-ttu-id="a4ca9-103">Tworzenie definicji przepływu pracy dla usługi logic apps za pomocą formatu JSON</span><span class="sxs-lookup"><span data-stu-id="a4ca9-103">Create workflow definitions for logic apps using JSON</span></span>

<span data-ttu-id="a4ca9-104">Można utworzyć definicji przepływu pracy dla [Azure Logic Apps](logic-apps-what-are-logic-apps.md) prosty, deklaratywny języka JSON.</span><span class="sxs-lookup"><span data-stu-id="a4ca9-104">You can create workflow definitions for [Azure Logic Apps](logic-apps-what-are-logic-apps.md) with simple, declarative JSON language.</span></span> <span data-ttu-id="a4ca9-105">Jeśli nie jest jeszcze, najpierw należy przejrzeć [jak toocreate pierwszej aplikacji logiki z projektanta aplikacji logiki](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="a4ca9-105">If you haven't already, first review [how toocreate your first logic app with Logic App Designer](logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="a4ca9-106">Zobacz też hello [pełne informacje dotyczące hello język definicji przepływu pracy](http://aka.ms/logicappsdocs).</span><span class="sxs-lookup"><span data-stu-id="a4ca9-106">Also, see hello [full reference for hello Workflow Definition Language](http://aka.ms/logicappsdocs).</span></span>

## <a name="repeat-steps-over-a-list"></a><span data-ttu-id="a4ca9-107">Powtórz kroki od listy</span><span class="sxs-lookup"><span data-stu-id="a4ca9-107">Repeat steps over a list</span></span>

<span data-ttu-id="a4ca9-108">tooiterate przez tablicę, która ma too10, 000 elementów i wykonania czynności dla każdego elementu, użyj hello [typu foreach](logic-apps-loops-and-scopes.md).</span><span class="sxs-lookup"><span data-stu-id="a4ca9-108">tooiterate through an array that has up too10,000 items and perform an action for each item, use hello [foreach type](logic-apps-loops-and-scopes.md).</span></span>

## <a name="handle-failures-if-something-goes-wrong"></a><span data-ttu-id="a4ca9-109">Obsługa błędów, jeśli jakaś nieprawidłowość</span><span class="sxs-lookup"><span data-stu-id="a4ca9-109">Handle failures if something goes wrong</span></span>

<span data-ttu-id="a4ca9-110">Zwykle ma tooinclude *krok korygowania* — niektóre logikę, która wykonuje *tylko wtedy, gdy* co najmniej jednego wywołania zakończyć się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="a4ca9-110">Usually, you want tooinclude a *remediation step* — some logic that executes *if and only if* one or more of your calls fail.</span></span> <span data-ttu-id="a4ca9-111">W tym przykładzie pobiera dane z różnych miejsc, ale w przypadku niepowodzenia wywołania hello chcemy tooPOST wiadomość gdzieś, firma Microsoft może śledzić awarii później:</span><span class="sxs-lookup"><span data-stu-id="a4ca9-111">This example gets data from various places, but if hello call fails, we want tooPOST a message somewhere so we can track down that failure later:</span></span>  

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

<span data-ttu-id="a4ca9-112">toospecify który `postToErrorMessageQueue` działa tylko `readData` ma `Failed`, użyj hello `runAfter` właściwości, na przykład toospecify listę możliwych wartości, tak aby `runAfter` może być `["Succeeded", "Failed"]`.</span><span class="sxs-lookup"><span data-stu-id="a4ca9-112">toospecify that `postToErrorMessageQueue` only runs after `readData` has `Failed`, use hello `runAfter` property, for example, toospecify a list of possible values, so that `runAfter` could be `["Succeeded", "Failed"]`.</span></span>

<span data-ttu-id="a4ca9-113">Na koniec, ponieważ w tym przykładzie obsługuje teraz błąd hello, firma Microsoft nie jest już oznaczyć hello Uruchom jako `Failed`.</span><span class="sxs-lookup"><span data-stu-id="a4ca9-113">Finally, because this example now handles hello error, we no longer mark hello run as `Failed`.</span></span> <span data-ttu-id="a4ca9-114">Ponieważ dodaliśmy hello kroku obsługi tego błędu w tym przykładzie ma hello Uruchom `Succeeded` chociaż jeden krok `Failed`.</span><span class="sxs-lookup"><span data-stu-id="a4ca9-114">Because we added hello step for handling this failure in this example, hello run has `Succeeded` although one step `Failed`.</span></span>

## <a name="execute-two-or-more-steps-in-parallel"></a><span data-ttu-id="a4ca9-115">Wykonaj kroki co najmniej dwa równolegle</span><span class="sxs-lookup"><span data-stu-id="a4ca9-115">Execute two or more steps in parallel</span></span>

<span data-ttu-id="a4ca9-116">toorun hello wielu akcji równolegle, `runAfter` właściwości musi być taka sama w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="a4ca9-116">toorun multiple actions in parallel, hello `runAfter` property must be equivalent at runtime.</span></span> 

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

<span data-ttu-id="a4ca9-117">W tym przykładzie zarówno `branch1` i `branch2` są ustawione toorun po `readData`.</span><span class="sxs-lookup"><span data-stu-id="a4ca9-117">In this example, both `branch1` and `branch2` are set toorun after `readData`.</span></span> <span data-ttu-id="a4ca9-118">W związku z tym obu gałęziach są uruchamiane równolegle.</span><span class="sxs-lookup"><span data-stu-id="a4ca9-118">As a result, both branches run in parallel.</span></span> <span data-ttu-id="a4ca9-119">Sygnatura czasowa powitania dla obu gałęziach są identyczne.</span><span class="sxs-lookup"><span data-stu-id="a4ca9-119">hello timestamp for both branches is identical.</span></span>

![Równoległe](media/logic-apps-author-definitions/parallel.png)

## <a name="join-two-parallel-branches"></a><span data-ttu-id="a4ca9-121">Dołącz do dwóch równoległych gałęziach</span><span class="sxs-lookup"><span data-stu-id="a4ca9-121">Join two parallel branches</span></span>

<span data-ttu-id="a4ca9-122">Możesz także dołączyć do dwóch akcje, które są ustawione toorun równolegle przez dodanie elementów toohello `runAfter` właściwości, jak w poprzednim przykładzie hello.</span><span class="sxs-lookup"><span data-stu-id="a4ca9-122">You can join two actions that are set toorun in parallel by adding items toohello `runAfter` property as in hello previous example.</span></span>

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

## <a name="map-list-items-tooa-different-configuration"></a><span data-ttu-id="a4ca9-124">Mapa listy elementów tooa innej konfiguracji</span><span class="sxs-lookup"><span data-stu-id="a4ca9-124">Map list items tooa different configuration</span></span>

<span data-ttu-id="a4ca9-125">Następnie Załóżmy, że chcemy tooget innej zawartości na podstawie hello wartości właściwości.</span><span class="sxs-lookup"><span data-stu-id="a4ca9-125">Next, let's say that we want tooget different content based on hello value of a property.</span></span> <span data-ttu-id="a4ca9-126">Można utworzyć mapy toodestinations wartości jako parametr:</span><span class="sxs-lookup"><span data-stu-id="a4ca9-126">We can create a map of values toodestinations as a parameter:</span></span>  

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

<span data-ttu-id="a4ca9-127">W takim przypadku najpierw pobrać listę artykułów.</span><span class="sxs-lookup"><span data-stu-id="a4ca9-127">In this case, we first get a list of articles.</span></span> <span data-ttu-id="a4ca9-128">W oparciu o kategorię hello, która została zdefiniowana jako parametru, drugi etap hello używa toolook mapy, zapasowej hello adresu URL pobierania zawartości hello.</span><span class="sxs-lookup"><span data-stu-id="a4ca9-128">Based on hello category that was defined as a parameter, hello second step uses a map toolook up hello URL for getting hello content.</span></span>

<span data-ttu-id="a4ca9-129">W tym miejscu toonote sytuacje:</span><span class="sxs-lookup"><span data-stu-id="a4ca9-129">Some times toonote here:</span></span> 

*   <span data-ttu-id="a4ca9-130">Witaj [ `intersection()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#intersection) funkcja sprawdza, czy kategoria hello zgodny jedną hello znane zdefiniowanych kategoriach.</span><span class="sxs-lookup"><span data-stu-id="a4ca9-130">hello [`intersection()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#intersection) function checks whether hello category matches one of hello known defined categories.</span></span>

*   <span data-ttu-id="a4ca9-131">Po uzyskujemy kategorii hello możemy ściągnięcia hello elementu z użyciem nawiasów kwadratowych mapy hello:`parameters[...]`</span><span class="sxs-lookup"><span data-stu-id="a4ca9-131">After we get hello category, we can pull hello item from hello map using square brackets: `parameters[...]`</span></span>

## <a name="process-strings"></a><span data-ttu-id="a4ca9-132">Ciągi procesu</span><span class="sxs-lookup"><span data-stu-id="a4ca9-132">Process strings</span></span>

<span data-ttu-id="a4ca9-133">Można użyć różnych funkcji toomanipulate ciągów.</span><span class="sxs-lookup"><span data-stu-id="a4ca9-133">You can use various functions toomanipulate strings.</span></span> <span data-ttu-id="a4ca9-134">Na przykład załóżmy, że mamy ciąg chcemy toopass tooa system, że nie wątpliwości właściwe obsługę kodowania znaków.</span><span class="sxs-lookup"><span data-stu-id="a4ca9-134">For example, suppose we have a string that we want toopass tooa system, but we aren't confident about proper handling for character encoding.</span></span> <span data-ttu-id="a4ca9-135">Jedną z opcji jest toobase64 ten ciąg do zakodowania.</span><span class="sxs-lookup"><span data-stu-id="a4ca9-135">One option is toobase64 encode this string.</span></span> <span data-ttu-id="a4ca9-136">Jednak tooavoid anulowanie w adresie URL zamierzamy tooreplace kilku znaków.</span><span class="sxs-lookup"><span data-stu-id="a4ca9-136">However, tooavoid escaping in a URL, we are going tooreplace a few characters.</span></span> 

<span data-ttu-id="a4ca9-137">Również chcemy podciąg nazwy hello kolejności, ponieważ hello pięć pierwszych znaków nie są używane.</span><span class="sxs-lookup"><span data-stu-id="a4ca9-137">We also want a substring of hello order's name because hello first five characters are not used.</span></span>

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

<span data-ttu-id="a4ca9-138">Pracy z wewnątrz toooutside:</span><span class="sxs-lookup"><span data-stu-id="a4ca9-138">Working from inside toooutside:</span></span>

1. <span data-ttu-id="a4ca9-139">Pobierz hello [ `length()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#length) o nazwę osoby hello zamawiającej, dlatego firma Microsoft wrócić hello całkowita liczba znaków.</span><span class="sxs-lookup"><span data-stu-id="a4ca9-139">Get hello [`length()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#length) for hello orderer's name, so we get back hello total number of characters.</span></span>

2. <span data-ttu-id="a4ca9-140">Odejmowanie 5, ponieważ chcemy krótszego ciągu.</span><span class="sxs-lookup"><span data-stu-id="a4ca9-140">Subtract 5 because we want a shorter string.</span></span>

3. <span data-ttu-id="a4ca9-141">W rzeczywistości zająć hello [ `substring()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#substring).</span><span class="sxs-lookup"><span data-stu-id="a4ca9-141">Actually, take hello [`substring()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#substring).</span></span> <span data-ttu-id="a4ca9-142">Rozpoczniemy pod indeksem `5` i przejdź hello pozostałej części ciąg hello.</span><span class="sxs-lookup"><span data-stu-id="a4ca9-142">We start at index `5` and go hello remainder of hello string.</span></span>

4. <span data-ttu-id="a4ca9-143">Konwertuj to tooa podciąg [ `base64()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#base64) ciąg.</span><span class="sxs-lookup"><span data-stu-id="a4ca9-143">Convert this substring tooa [`base64()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#base64) string.</span></span>

5. <span data-ttu-id="a4ca9-144">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace)wszystkie hello `+` znaków i zawierają `-` znaków.</span><span class="sxs-lookup"><span data-stu-id="a4ca9-144">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace) all hello `+` characters with `-` characters.</span></span>

6. <span data-ttu-id="a4ca9-145">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace)wszystkie hello `/` znaków i zawierają `_` znaków.</span><span class="sxs-lookup"><span data-stu-id="a4ca9-145">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace) all hello `/` characters with `_` characters.</span></span>

## <a name="work-with-date-times"></a><span data-ttu-id="a4ca9-146">Praca z daty i godziny</span><span class="sxs-lookup"><span data-stu-id="a4ca9-146">Work with Date Times</span></span>

<span data-ttu-id="a4ca9-147">Daty i godziny mogą być przydatne, szczególnie w przypadku, gdy chcesz toopull danych ze źródła danych, który nie obsługuje naturalnie *wyzwalaczy*.</span><span class="sxs-lookup"><span data-stu-id="a4ca9-147">Date Times can be useful, particularly when you are trying toopull data from a data source that doesn't naturally support *triggers*.</span></span> <span data-ttu-id="a4ca9-148">Umożliwia także daty i godziny do znajdowania, jak długo różne kroki są tworzone.</span><span class="sxs-lookup"><span data-stu-id="a4ca9-148">You can also use Date Times for finding how long various steps are taking.</span></span>

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

<span data-ttu-id="a4ca9-149">W tym przykładzie mamy wyodrębnić hello `startTime` hello w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="a4ca9-149">In this example, we extract hello `startTime` from hello previous step.</span></span> <span data-ttu-id="a4ca9-150">Następnie możemy pobrać hello bieżącego czasu i odjąć 1 sekundy:</span><span class="sxs-lookup"><span data-stu-id="a4ca9-150">Then we get hello current time, and subtract one second:</span></span>

[`addseconds(..., -1)`](https://msdn.microsoft.com/library/azure/mt643789.aspx#addseconds) 

<span data-ttu-id="a4ca9-151">Inne jednostki czasu, można używać tak samo, jak `minutes` lub `hours`.</span><span class="sxs-lookup"><span data-stu-id="a4ca9-151">You can use other units of time, like `minutes` or `hours`.</span></span> <span data-ttu-id="a4ca9-152">Na koniec mamy Porównaj te dwie wartości.</span><span class="sxs-lookup"><span data-stu-id="a4ca9-152">Finally, we can compare these two values.</span></span> <span data-ttu-id="a4ca9-153">Jeśli hello pierwsza wartość jest mniejsza niż wartość drugiego hello, a następnie więcej niż jednej sekundy są spełnione, ponieważ najpierw umieszczono hello kolejności.</span><span class="sxs-lookup"><span data-stu-id="a4ca9-153">If hello first value is less than hello second value, then more than one second has passed since hello order was first placed.</span></span>

<span data-ttu-id="a4ca9-154">tooformat dat, możemy użyć ciągu elementy formatujące.</span><span class="sxs-lookup"><span data-stu-id="a4ca9-154">tooformat dates, we can use string formatters.</span></span> <span data-ttu-id="a4ca9-155">Na przykład hello tooget RFC1123, używamy [ `utcnow('r')` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span><span class="sxs-lookup"><span data-stu-id="a4ca9-155">For example, tooget hello RFC1123, we use [`utcnow('r')`](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span></span> <span data-ttu-id="a4ca9-156">toolearn o formatowania daty, zobacz [język definicji przepływu pracy](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span><span class="sxs-lookup"><span data-stu-id="a4ca9-156">toolearn about date formatting, see [Workflow Definition Language](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span></span>

## <a name="deployment-parameters-for-different-environments"></a><span data-ttu-id="a4ca9-157">Parametry wdrożenia dla różnych środowisk</span><span class="sxs-lookup"><span data-stu-id="a4ca9-157">Deployment parameters for different environments</span></span>

<span data-ttu-id="a4ca9-158">Zazwyczaj cyklami życia wdrożenia ma środowiska programowania, środowisku przemieszczania i środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="a4ca9-158">Commonly, deployment lifecycles have a development environment, a staging environment, and a production environment.</span></span> <span data-ttu-id="a4ca9-159">Na przykład możesz użyć tej samej definicji w tych środowiskach hello, ale Użyj różnych baz danych.</span><span class="sxs-lookup"><span data-stu-id="a4ca9-159">For example, you might use hello same definition in all these environments but use different databases.</span></span> <span data-ttu-id="a4ca9-160">Podobnie, może być toouse hello tej samej definicji w różnych regionach, wysokiej dostępności, ale mają każdego logiki aplikacji wystąpienia tootalk toothat regionu bazy danych.</span><span class="sxs-lookup"><span data-stu-id="a4ca9-160">Likewise, you might want toouse hello same definition across different regions for high availability but want each logic app instance tootalk toothat region's database.</span></span>
<span data-ttu-id="a4ca9-161">W tym scenariuszu różni się od podejmowania parametrów w *środowiska uruchomieniowego* gdzie zamiast tego należy używać hello `trigger()` działać jak w poprzednim przykładzie hello.</span><span class="sxs-lookup"><span data-stu-id="a4ca9-161">This scenario differs from taking parameters at *runtime* where instead, you should use hello `trigger()` function as in hello previous example.</span></span>

<span data-ttu-id="a4ca9-162">Można uruchomić z podstawową definicję, tak jak ten przykład:</span><span class="sxs-lookup"><span data-stu-id="a4ca9-162">You can start with a basic definition like this example:</span></span>

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

<span data-ttu-id="a4ca9-163">W rzeczywistych hello `PUT` żądania dla aplikacji logiki hello, możesz podać parametr hello `uri`.</span><span class="sxs-lookup"><span data-stu-id="a4ca9-163">In hello actual `PUT` request for hello logic apps, you can provide hello parameter `uri`.</span></span> <span data-ttu-id="a4ca9-164">Ponieważ istnieje już wartość domyślną, ładunku aplikacji logiki hello wymaga tego parametru:</span><span class="sxs-lookup"><span data-stu-id="a4ca9-164">Because a default value no longer exists, hello logic app payload requires this parameter:</span></span>

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

<span data-ttu-id="a4ca9-165">W każdym środowisku można podać inną wartość dla hello `connection` parametru.</span><span class="sxs-lookup"><span data-stu-id="a4ca9-165">In each environment, you can provide a different value for hello `connection` parameter.</span></span> 

<span data-ttu-id="a4ca9-166">Dla wszystkich hello opcje dotyczące tworzenia i zarządzania aplikacji logiki, zobacz hello [dokumentacja interfejsu API REST](https://msdn.microsoft.com/library/azure/mt643787.aspx).</span><span class="sxs-lookup"><span data-stu-id="a4ca9-166">For all hello options that you have for creating and managing logic apps, see hello [REST API documentation](https://msdn.microsoft.com/library/azure/mt643787.aspx).</span></span> 
