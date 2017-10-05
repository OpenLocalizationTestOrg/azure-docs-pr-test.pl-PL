---
title: "Definiuje przepływy pracy z JSON - Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Jak napisać definicji przepływu pracy w formacie JSON dla usługi logic apps"
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
ms.openlocfilehash: 7f9e5a10066df8a464c285273e77a85c0d562ebb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-workflow-definitions-for-logic-apps-using-json"></a><span data-ttu-id="34da0-103">Tworzenie definicji przepływu pracy dla usługi logic apps za pomocą formatu JSON</span><span class="sxs-lookup"><span data-stu-id="34da0-103">Create workflow definitions for logic apps using JSON</span></span>

<span data-ttu-id="34da0-104">Można utworzyć definicji przepływu pracy dla [Azure Logic Apps](logic-apps-what-are-logic-apps.md) prosty, deklaratywny języka JSON.</span><span class="sxs-lookup"><span data-stu-id="34da0-104">You can create workflow definitions for [Azure Logic Apps](logic-apps-what-are-logic-apps.md) with simple, declarative JSON language.</span></span> <span data-ttu-id="34da0-105">Jeśli nie jest jeszcze, najpierw należy przejrzeć [tworzenie pierwszej aplikacji logiki z projektanta aplikacji logiki](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="34da0-105">If you haven't already, first review [how to create your first logic app with Logic App Designer](logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="34da0-106">Zobacz też [pełne odwołania dla języka definicji przepływu pracy](http://aka.ms/logicappsdocs).</span><span class="sxs-lookup"><span data-stu-id="34da0-106">Also, see the [full reference for the Workflow Definition Language](http://aka.ms/logicappsdocs).</span></span>

## <a name="repeat-steps-over-a-list"></a><span data-ttu-id="34da0-107">Powtórz kroki od listy</span><span class="sxs-lookup"><span data-stu-id="34da0-107">Repeat steps over a list</span></span>

<span data-ttu-id="34da0-108">Aby wykonać iterację tablicę, która zawiera elementy do 10 000 i wykonania czynności dla każdego elementu, użyj [typu foreach](logic-apps-loops-and-scopes.md).</span><span class="sxs-lookup"><span data-stu-id="34da0-108">To iterate through an array that has up to 10,000 items and perform an action for each item, use the [foreach type](logic-apps-loops-and-scopes.md).</span></span>

## <a name="handle-failures-if-something-goes-wrong"></a><span data-ttu-id="34da0-109">Obsługa błędów, jeśli jakaś nieprawidłowość</span><span class="sxs-lookup"><span data-stu-id="34da0-109">Handle failures if something goes wrong</span></span>

<span data-ttu-id="34da0-110">Zwykle, które chcesz dołączyć *krok korygowania* — niektóre logikę, która wykonuje *tylko wtedy, gdy* co najmniej jednego wywołania zakończyć się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="34da0-110">Usually, you want to include a *remediation step* — some logic that executes *if and only if* one or more of your calls fail.</span></span> <span data-ttu-id="34da0-111">W tym przykładzie pobiera dane z różnych miejsc, ale w przypadku niepowodzenia wywołania chcemy, aby wysłać wiadomość gdzieś, dlatego firma Microsoft może śledzić awarii później:</span><span class="sxs-lookup"><span data-stu-id="34da0-111">This example gets data from various places, but if the call fails, we want to POST a message somewhere so we can track down that failure later:</span></span>  

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

<span data-ttu-id="34da0-112">Aby określić, że `postToErrorMessageQueue` działa tylko `readData` ma `Failed`, użyj `runAfter` właściwości, na przykład, aby określić listę możliwych wartości, tak aby `runAfter` może być `["Succeeded", "Failed"]`.</span><span class="sxs-lookup"><span data-stu-id="34da0-112">To specify that `postToErrorMessageQueue` only runs after `readData` has `Failed`, use the `runAfter` property, for example, to specify a list of possible values, so that `runAfter` could be `["Succeeded", "Failed"]`.</span></span>

<span data-ttu-id="34da0-113">Na koniec, ponieważ w tym przykładzie obsługuje teraz błąd, firma Microsoft nie jest już oznaczyć Uruchom jako `Failed`.</span><span class="sxs-lookup"><span data-stu-id="34da0-113">Finally, because this example now handles the error, we no longer mark the run as `Failed`.</span></span> <span data-ttu-id="34da0-114">Ponieważ dodaliśmy kroku obsługi tego błędu w tym przykładzie ma `Succeeded` chociaż jeden krok `Failed`.</span><span class="sxs-lookup"><span data-stu-id="34da0-114">Because we added the step for handling this failure in this example, the run has `Succeeded` although one step `Failed`.</span></span>

## <a name="execute-two-or-more-steps-in-parallel"></a><span data-ttu-id="34da0-115">Wykonaj kroki co najmniej dwa równolegle</span><span class="sxs-lookup"><span data-stu-id="34da0-115">Execute two or more steps in parallel</span></span>

<span data-ttu-id="34da0-116">Do uruchomienia wielu akcji równolegle, `runAfter` właściwości musi być taka sama w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="34da0-116">To run multiple actions in parallel, the `runAfter` property must be equivalent at runtime.</span></span> 

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

<span data-ttu-id="34da0-117">W tym przykładzie zarówno `branch1` i `branch2` są ustawione na uruchamianie `readData`.</span><span class="sxs-lookup"><span data-stu-id="34da0-117">In this example, both `branch1` and `branch2` are set to run after `readData`.</span></span> <span data-ttu-id="34da0-118">W związku z tym obu gałęziach są uruchamiane równolegle.</span><span class="sxs-lookup"><span data-stu-id="34da0-118">As a result, both branches run in parallel.</span></span> <span data-ttu-id="34da0-119">Znacznik czasu dla obu gałęziach są identyczne.</span><span class="sxs-lookup"><span data-stu-id="34da0-119">The timestamp for both branches is identical.</span></span>

![Równoległe](media/logic-apps-author-definitions/parallel.png)

## <a name="join-two-parallel-branches"></a><span data-ttu-id="34da0-121">Dołącz do dwóch równoległych gałęziach</span><span class="sxs-lookup"><span data-stu-id="34da0-121">Join two parallel branches</span></span>

<span data-ttu-id="34da0-122">Możesz także dołączyć do dwóch akcje, które są ustawione na uruchamianie równoległe przez dodanie elementów do `runAfter` właściwości co w poprzednim przykładzie.</span><span class="sxs-lookup"><span data-stu-id="34da0-122">You can join two actions that are set to run in parallel by adding items to the `runAfter` property as in the previous example.</span></span>

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

## <a name="map-list-items-to-a-different-configuration"></a><span data-ttu-id="34da0-124">Mapa elementów listy do innej konfiguracji</span><span class="sxs-lookup"><span data-stu-id="34da0-124">Map list items to a different configuration</span></span>

<span data-ttu-id="34da0-125">Następnie Załóżmy, że chcemy uzyskać różne zawartości na podstawie wartości właściwości.</span><span class="sxs-lookup"><span data-stu-id="34da0-125">Next, let's say that we want to get different content based on the value of a property.</span></span> <span data-ttu-id="34da0-126">Można utworzyć mapy wartości do miejsc docelowych jako parametr:</span><span class="sxs-lookup"><span data-stu-id="34da0-126">We can create a map of values to destinations as a parameter:</span></span>  

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

<span data-ttu-id="34da0-127">W takim przypadku najpierw pobrać listę artykułów.</span><span class="sxs-lookup"><span data-stu-id="34da0-127">In this case, we first get a list of articles.</span></span> <span data-ttu-id="34da0-128">W oparciu o kategorię, która została zdefiniowana jako parametru, drugi etap używa mapy do wyszukania adres URL pobierania zawartości.</span><span class="sxs-lookup"><span data-stu-id="34da0-128">Based on the category that was defined as a parameter, the second step uses a map to look up the URL for getting the content.</span></span>

<span data-ttu-id="34da0-129">Sytuacje, w tym miejscu należy pamiętać:</span><span class="sxs-lookup"><span data-stu-id="34da0-129">Some times to note here:</span></span> 

*   <span data-ttu-id="34da0-130">[ `intersection()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#intersection) Funkcja sprawdza, czy kategoria zgodny jedną znane zdefiniowanych kategoriach.</span><span class="sxs-lookup"><span data-stu-id="34da0-130">The [`intersection()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#intersection) function checks whether the category matches one of the known defined categories.</span></span>

*   <span data-ttu-id="34da0-131">Po uzyskujemy kategorii, możemy pobierać elementu z tablicy przy użyciu nawiasy kwadratowe:`parameters[...]`</span><span class="sxs-lookup"><span data-stu-id="34da0-131">After we get the category, we can pull the item from the map using square brackets: `parameters[...]`</span></span>

## <a name="process-strings"></a><span data-ttu-id="34da0-132">Ciągi procesu</span><span class="sxs-lookup"><span data-stu-id="34da0-132">Process strings</span></span>

<span data-ttu-id="34da0-133">Można użyć różnych funkcji do manipulowania ciągami.</span><span class="sxs-lookup"><span data-stu-id="34da0-133">You can use various functions to manipulate strings.</span></span> <span data-ttu-id="34da0-134">Na przykład załóżmy, że mamy ciąg, który chcemy przekazać do systemu, ale nie wątpliwości właściwe obsługę kodowania znaków.</span><span class="sxs-lookup"><span data-stu-id="34da0-134">For example, suppose we have a string that we want to pass to a system, but we aren't confident about proper handling for character encoding.</span></span> <span data-ttu-id="34da0-135">Jedną z opcji jest w formacie base64 ten ciąg do zakodowania.</span><span class="sxs-lookup"><span data-stu-id="34da0-135">One option is to base64 encode this string.</span></span> <span data-ttu-id="34da0-136">Jednak aby uniknąć anulowanie w adresie URL, zamierzamy Zastąp kilku znaków.</span><span class="sxs-lookup"><span data-stu-id="34da0-136">However, to avoid escaping in a URL, we are going to replace a few characters.</span></span> 

<span data-ttu-id="34da0-137">Również chcemy podciąg nazwy zamówienia, ponieważ nie są używane przez pięć pierwszych znaków.</span><span class="sxs-lookup"><span data-stu-id="34da0-137">We also want a substring of the order's name because the first five characters are not used.</span></span>

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

<span data-ttu-id="34da0-138">Praca z wewnątrz do poza:</span><span class="sxs-lookup"><span data-stu-id="34da0-138">Working from inside to outside:</span></span>

1. <span data-ttu-id="34da0-139">Pobierz [ `length()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#length) o nazwę osoby zamawiającej, dlatego firma Microsoft wrócić całkowita liczba znaków.</span><span class="sxs-lookup"><span data-stu-id="34da0-139">Get the [`length()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#length) for the orderer's name, so we get back the total number of characters.</span></span>

2. <span data-ttu-id="34da0-140">Odejmowanie 5, ponieważ chcemy krótszego ciągu.</span><span class="sxs-lookup"><span data-stu-id="34da0-140">Subtract 5 because we want a shorter string.</span></span>

3. <span data-ttu-id="34da0-141">W rzeczywistości zająć [ `substring()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#substring).</span><span class="sxs-lookup"><span data-stu-id="34da0-141">Actually, take the [`substring()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#substring).</span></span> <span data-ttu-id="34da0-142">Rozpoczniemy pod indeksem `5` i przejdź do końca ciągu.</span><span class="sxs-lookup"><span data-stu-id="34da0-142">We start at index `5` and go the remainder of the string.</span></span>

4. <span data-ttu-id="34da0-143">Konwertuj to podciąg do [ `base64()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#base64) ciąg.</span><span class="sxs-lookup"><span data-stu-id="34da0-143">Convert this substring to a [`base64()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#base64) string.</span></span>

5. <span data-ttu-id="34da0-144">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace)wszystkie `+` znaków i zawierają `-` znaków.</span><span class="sxs-lookup"><span data-stu-id="34da0-144">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace) all the `+` characters with `-` characters.</span></span>

6. <span data-ttu-id="34da0-145">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace)wszystkie `/` znaków i zawierają `_` znaków.</span><span class="sxs-lookup"><span data-stu-id="34da0-145">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace) all the `/` characters with `_` characters.</span></span>

## <a name="work-with-date-times"></a><span data-ttu-id="34da0-146">Praca z daty i godziny</span><span class="sxs-lookup"><span data-stu-id="34da0-146">Work with Date Times</span></span>

<span data-ttu-id="34da0-147">Daty i godziny mogą być użyteczne, zwłaszcza w przypadku próby pobierania danych ze źródła danych, który nie obsługuje naturalnie *wyzwalaczy*.</span><span class="sxs-lookup"><span data-stu-id="34da0-147">Date Times can be useful, particularly when you are trying to pull data from a data source that doesn't naturally support *triggers*.</span></span> <span data-ttu-id="34da0-148">Umożliwia także daty i godziny do znajdowania, jak długo różne kroki są tworzone.</span><span class="sxs-lookup"><span data-stu-id="34da0-148">You can also use Date Times for finding how long various steps are taking.</span></span>

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

<span data-ttu-id="34da0-149">W tym przykładzie mamy wyodrębnić `startTime` z poprzedniego kroku.</span><span class="sxs-lookup"><span data-stu-id="34da0-149">In this example, we extract the `startTime` from the previous step.</span></span> <span data-ttu-id="34da0-150">Następnie możemy pobrać bieżącego czasu i odjąć 1 sekundy:</span><span class="sxs-lookup"><span data-stu-id="34da0-150">Then we get the current time, and subtract one second:</span></span>

[`addseconds(..., -1)`](https://msdn.microsoft.com/library/azure/mt643789.aspx#addseconds) 

<span data-ttu-id="34da0-151">Inne jednostki czasu, można używać tak samo, jak `minutes` lub `hours`.</span><span class="sxs-lookup"><span data-stu-id="34da0-151">You can use other units of time, like `minutes` or `hours`.</span></span> <span data-ttu-id="34da0-152">Na koniec mamy Porównaj te dwie wartości.</span><span class="sxs-lookup"><span data-stu-id="34da0-152">Finally, we can compare these two values.</span></span> <span data-ttu-id="34da0-153">Jeśli pierwsza wartość jest mniejsza niż wartość drugiej, a następnie więcej niż jednej sekundy są spełnione, ponieważ najpierw umieszczono kolejności.</span><span class="sxs-lookup"><span data-stu-id="34da0-153">If the first value is less than the second value, then more than one second has passed since the order was first placed.</span></span>

<span data-ttu-id="34da0-154">Do formatowania daty, możemy użyć ciągu elementy formatujące.</span><span class="sxs-lookup"><span data-stu-id="34da0-154">To format dates, we can use string formatters.</span></span> <span data-ttu-id="34da0-155">Na przykład, aby uzyskać RFC1123, używamy [ `utcnow('r')` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span><span class="sxs-lookup"><span data-stu-id="34da0-155">For example, to get the RFC1123, we use [`utcnow('r')`](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span></span> <span data-ttu-id="34da0-156">Aby uzyskać informacje dotyczące formatowania daty, zobacz [język definicji przepływu pracy](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span><span class="sxs-lookup"><span data-stu-id="34da0-156">To learn about date formatting, see [Workflow Definition Language](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span></span>

## <a name="deployment-parameters-for-different-environments"></a><span data-ttu-id="34da0-157">Parametry wdrożenia dla różnych środowisk</span><span class="sxs-lookup"><span data-stu-id="34da0-157">Deployment parameters for different environments</span></span>

<span data-ttu-id="34da0-158">Zazwyczaj cyklami życia wdrożenia ma środowiska programowania, środowisku przemieszczania i środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="34da0-158">Commonly, deployment lifecycles have a development environment, a staging environment, and a production environment.</span></span> <span data-ttu-id="34da0-159">Na przykład może użyć tej samej definicji w tych środowiskach, ale Użyj różnych baz danych.</span><span class="sxs-lookup"><span data-stu-id="34da0-159">For example, you might use the same definition in all these environments but use different databases.</span></span> <span data-ttu-id="34da0-160">Podobnie możesz użyć tej samej definicji w różnych regionach, wysokiej dostępności, ale mają każde wystąpienie aplikacji logiki, aby komunikował się z bazą danych tego regionu.</span><span class="sxs-lookup"><span data-stu-id="34da0-160">Likewise, you might want to use the same definition across different regions for high availability but want each logic app instance to talk to that region's database.</span></span>
<span data-ttu-id="34da0-161">W tym scenariuszu różni się od podejmowania parametrów w *środowiska uruchomieniowego* gdzie zamiast tego należy używać `trigger()` działać tak jak w poprzednim przykładzie.</span><span class="sxs-lookup"><span data-stu-id="34da0-161">This scenario differs from taking parameters at *runtime* where instead, you should use the `trigger()` function as in the previous example.</span></span>

<span data-ttu-id="34da0-162">Można uruchomić z podstawową definicję, tak jak ten przykład:</span><span class="sxs-lookup"><span data-stu-id="34da0-162">You can start with a basic definition like this example:</span></span>

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

<span data-ttu-id="34da0-163">W rzeczywistym `PUT` żądania dla aplikacji logiki możesz podać parametr `uri`.</span><span class="sxs-lookup"><span data-stu-id="34da0-163">In the actual `PUT` request for the logic apps, you can provide the parameter `uri`.</span></span> <span data-ttu-id="34da0-164">Ponieważ istnieje już wartość domyślną, ładunku aplikacji logiki wymaga tego parametru:</span><span class="sxs-lookup"><span data-stu-id="34da0-164">Because a default value no longer exists, the logic app payload requires this parameter:</span></span>

```
{
    "properties": {},
        "definition": {
          // Use the definition from above here
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

<span data-ttu-id="34da0-165">W każdym środowisku można podać inną wartość dla `connection` parametru.</span><span class="sxs-lookup"><span data-stu-id="34da0-165">In each environment, you can provide a different value for the `connection` parameter.</span></span> 

<span data-ttu-id="34da0-166">Aby uzyskać wszystkie opcje, które mają do tworzenia i zarządzania aplikacji logiki, zobacz [dokumentacja interfejsu API REST](https://msdn.microsoft.com/library/azure/mt643787.aspx).</span><span class="sxs-lookup"><span data-stu-id="34da0-166">For all the options that you have for creating and managing logic apps, see the [REST API documentation](https://msdn.microsoft.com/library/azure/mt643787.aspx).</span></span> 
