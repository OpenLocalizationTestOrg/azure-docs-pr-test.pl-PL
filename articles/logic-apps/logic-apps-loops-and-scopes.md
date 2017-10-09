---
title: "aaaCreate pętli i zakresów lub debatch danych w przepływach pracy - Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Tworzenie pętli tooiterate za pośrednictwem danych, akcje grupy do zakresów, lub debatch toostart danych jeden przepływ pracy w aplikacjach logiki platformy Azure."
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 75b52eeb-23a7-47dd-a42f-1351c6dfebdc
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/29/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: e612ec2e83541f028916a07bf12c44e7b1f57ad1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="logic-apps-loops-scopes-and-debatching"></a><span data-ttu-id="fca96-103">Pętle, zakresy i usuwanie partii aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="fca96-103">Logic Apps Loops, Scopes, and Debatching</span></span>
  
<span data-ttu-id="fca96-104">Logic Apps oferuje następujące sposoby toowork z tablic, kolekcje partii i pętle w przepływie pracy.</span><span class="sxs-lookup"><span data-stu-id="fca96-104">Logic Apps provides a number of ways toowork with arrays, collections, batches, and loops within a workflow.</span></span>
  
## <a name="foreach-loop-and-arrays"></a><span data-ttu-id="fca96-105">ForEach — pętla i tablic</span><span class="sxs-lookup"><span data-stu-id="fca96-105">ForEach loop and arrays</span></span>
  
<span data-ttu-id="fca96-106">Logic Apps umożliwia tooloop dla zestawu danych i wykonywania akcji dla każdego elementu.</span><span class="sxs-lookup"><span data-stu-id="fca96-106">Logic Apps allows you tooloop over a set of data and perform an action for each item.</span></span>  <span data-ttu-id="fca96-107">Jest to możliwe za pośrednictwem hello `foreach` akcji.</span><span class="sxs-lookup"><span data-stu-id="fca96-107">This is possible via hello `foreach` action.</span></span>  <span data-ttu-id="fca96-108">W Projektancie hello tooadd można określić dla każdej pętli.</span><span class="sxs-lookup"><span data-stu-id="fca96-108">In hello designer, you can specify tooadd a for each loop.</span></span>  <span data-ttu-id="fca96-109">Po wybraniu tablicy hello, które mają zostać tooiterate za pośrednictwem, możesz rozpocząć dodawanie akcji.</span><span class="sxs-lookup"><span data-stu-id="fca96-109">After selecting hello array you wish tooiterate over, you can begin adding actions.</span></span>  <span data-ttu-id="fca96-110">Obecnie są ograniczone tooonly jedną akcję dla pętli foreach, ale to ograniczenie będzie podnoszone w hello przesyłanych tygodni.</span><span class="sxs-lookup"><span data-stu-id="fca96-110">Currently you are limited tooonly one action per foreach loop, but this restriction will be lifted in hello coming weeks.</span></span>  <span data-ttu-id="fca96-111">Raz w pętli hello można rozpocząć toospecify, co ma mieć miejsce w każdej wartości hello tablicy.</span><span class="sxs-lookup"><span data-stu-id="fca96-111">Once within hello loop you can begin toospecify what should occur at each value of hello array.</span></span>

<span data-ttu-id="fca96-112">Jeśli używasz widoku kodu, można określić dla każdej pętli, takie jak poniżej.</span><span class="sxs-lookup"><span data-stu-id="fca96-112">If using code-view, you can specify a for each loop like below.</span></span>  <span data-ttu-id="fca96-113">To jest przykład dla każdej pętli, który wysyła wiadomości e-mail dla każdego adresu e-mail, który zawiera "microsoft.com":</span><span class="sxs-lookup"><span data-stu-id="fca96-113">This is an example of a for each loop that sends an email for each email address that contains 'microsoft.com':</span></span>

``` json
{
    "email_filter": {
        "type": "query",
        "inputs": {
            "from": "@triggerBody()['emails']",
            "where": "@contains(item()['email'], 'microsoft.com')"
        }
    },
    "forEach_email": {
        "type": "foreach",
        "foreach": "@body('email_filter')",
        "actions": {
            "send_email": {
                "type": "ApiConnection",
                "inputs": {
                "body": {
                    "to": "@item()",
                    "from": "me@contoso.com",
                    "message": "Hello, thank you for ordering"
                },
                "host": {
                    "connection": {
                        "id": "@parameters('$connections')['office365']['connection']['id']"
                    }
                },
                }
            }
        },
        "runAfter":{
            "email_filter": [ "Succeeded" ]
        }
    }
}
```
  
  <span data-ttu-id="fca96-114">A `foreach` akcji można Iterowanie przez tablice się too5, 000 wierszy.</span><span class="sxs-lookup"><span data-stu-id="fca96-114">A `foreach` action can iterate over arrays up too5,000 rows.</span></span>  <span data-ttu-id="fca96-115">Domyślnie każdej iteracji będą wykonywane równolegle.</span><span class="sxs-lookup"><span data-stu-id="fca96-115">Each iteration will execute in parallel by default.</span></span>  

### <a name="sequential-foreach-loops"></a><span data-ttu-id="fca96-116">Sekwencyjne pętli ForEach</span><span class="sxs-lookup"><span data-stu-id="fca96-116">Sequential ForEach loops</span></span>

<span data-ttu-id="fca96-117">tooenable tooexecute pętli foreach sekwencyjnie, hello `Sequential` opcji operacji powinny zostać dodane.</span><span class="sxs-lookup"><span data-stu-id="fca96-117">tooenable a foreach loop tooexecute sequentially, hello `Sequential` operation option should be added.</span></span>

``` json
"forEach_email": {
        "type": "foreach",
        "foreach": "@body('email_filter')",
        "operationOptions": "Sequential",
        "..."
}
```
  
## <a name="until-loop"></a><span data-ttu-id="fca96-118">Do pętli</span><span class="sxs-lookup"><span data-stu-id="fca96-118">Until loop</span></span>
  
  <span data-ttu-id="fca96-119">Do momentu spełnienia warunku można wykonać akcji lub serii akcji.</span><span class="sxs-lookup"><span data-stu-id="fca96-119">You can perform an action or series of actions until a condition is met.</span></span>  <span data-ttu-id="fca96-120">Witaj najbardziej typowy scenariusz, w tym wywołuje punkt końcowy do momentu uzyskania odpowiedzi hello, którego szukasz.</span><span class="sxs-lookup"><span data-stu-id="fca96-120">hello most common scenario for this is calling an endpoint until you get hello response you are looking for.</span></span>  <span data-ttu-id="fca96-121">W Projektancie hello, można określić tooadd do pętli.</span><span class="sxs-lookup"><span data-stu-id="fca96-121">In hello designer, you can specify tooadd an until loop.</span></span>  <span data-ttu-id="fca96-122">Po dodaniu Akcje wewnątrz pętli hello, możesz można ustawić warunku exit hello, a także hello limity pętli.</span><span class="sxs-lookup"><span data-stu-id="fca96-122">After adding actions inside hello loop, you can set hello exit condition, as well as hello loop limits.</span></span>  <span data-ttu-id="fca96-123">Istnieje opóźnienie 1 minutę, między cykle pętli.</span><span class="sxs-lookup"><span data-stu-id="fca96-123">There is a 1 minute delay between loop cycles.</span></span>
  
  <span data-ttu-id="fca96-124">Jeśli używasz widoku kodu, można określić aż pętli, takich jak poniżej.</span><span class="sxs-lookup"><span data-stu-id="fca96-124">If using code-view, you can specify an until loop like below.</span></span>  <span data-ttu-id="fca96-125">To jest przykład wywołania punktu końcowego HTTP, dopóki treść odpowiedzi hello ma wartość hello "Ukończona".</span><span class="sxs-lookup"><span data-stu-id="fca96-125">This is an example of calling an HTTP endpoint until hello response body has hello value 'Completed'.</span></span>  <span data-ttu-id="fca96-126">Proces zostanie zakończony, kiedy użytkownik</span><span class="sxs-lookup"><span data-stu-id="fca96-126">It will complete when either</span></span> 
  
  * <span data-ttu-id="fca96-127">Odpowiedź HTTP ma stan "Ukończona"</span><span class="sxs-lookup"><span data-stu-id="fca96-127">HTTP Response has status of 'Completed'</span></span>
  * <span data-ttu-id="fca96-128">Maksymalnie 1 godziny</span><span class="sxs-lookup"><span data-stu-id="fca96-128">It has tried for 1 hour</span></span>
  * <span data-ttu-id="fca96-129">Wystąpiło sprzężenie 100 razy</span><span class="sxs-lookup"><span data-stu-id="fca96-129">It has looped 100 times</span></span>
  
  ``` json
  {
      "until_successful":{
        "type": "until",
        "expression": "@equals(actions('http')['status'], 'Completed')",
        "limit": {
            "count": 100,
            "timeout": "PT1H"
        },
        "actions": {
            "create_resource": {
                "type": "http",
                "inputs": {
                    "url": "http://provisionRseource.com",
                    "body": {
                        "resourceId": "@triggerBody()"
                    }
                }
            }
        }
      }
  }
  ```
  
## <a name="spliton-and-debatching"></a><span data-ttu-id="fca96-130">SplitOn i debatching</span><span class="sxs-lookup"><span data-stu-id="fca96-130">SplitOn and debatching</span></span>

<span data-ttu-id="fca96-131">Czasami może zostać wyświetlony wyzwalacz tablicę elementów chcesz toodebatch, a następnie uruchomić przepływ pracy dla każdego elementu.</span><span class="sxs-lookup"><span data-stu-id="fca96-131">Sometimes a trigger may receive an array of items that you want toodebatch and start a workflow per item.</span></span>  <span data-ttu-id="fca96-132">Można to zrobić za pomocą hello `spliton` polecenia.</span><span class="sxs-lookup"><span data-stu-id="fca96-132">This can be accomplished via hello `spliton` command.</span></span>  <span data-ttu-id="fca96-133">Domyślnie, jeśli programu swagger wyzwalacza określa ładunku, który jest tablicą `spliton` zostanie dodany i uruchomić Uruchom dla każdego elementu.</span><span class="sxs-lookup"><span data-stu-id="fca96-133">By default, if your trigger swagger specifies a payload that is an array, a `spliton` will be added and start a run per item.</span></span>  <span data-ttu-id="fca96-134">SplitOn mogą być dodawane tylko tooa wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="fca96-134">SplitOn can only be added tooa trigger.</span></span>  <span data-ttu-id="fca96-135">Może to ręcznie skonfigurowane lub zastąpiony w definicji widoku kodu.</span><span class="sxs-lookup"><span data-stu-id="fca96-135">This can be manually configured or overridden in definition code-view.</span></span>  <span data-ttu-id="fca96-136">Obecnie SplitOn można debatch tablice się too5, 000 elementów.</span><span class="sxs-lookup"><span data-stu-id="fca96-136">Currently SplitOn can debatch arrays up too5,000 items.</span></span>  <span data-ttu-id="fca96-137">Nie może mieć `spliton` i również implementują wzorzec synchronicznej odpowiedzi hello.</span><span class="sxs-lookup"><span data-stu-id="fca96-137">You cannot have a `spliton` and also implement hello synchronous response pattern.</span></span>  <span data-ttu-id="fca96-138">Każdy przepływ pracy, który wywołuje ma `response` akcji oprócz zbyt`spliton` będą uruchamiane asynchronicznie i wysyłać natychmiastowego `202 Accepted` odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="fca96-138">Any workflow called that has a `response` action in addition too`spliton` will run asynchronously and send an immediate `202 Accepted` response.</span></span>  

<span data-ttu-id="fca96-139">W widoku kodu można określić SplitOn jako hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="fca96-139">SplitOn can be specified in code-view as hello following example.</span></span>  <span data-ttu-id="fca96-140">Odbiera tablicę elementów i debatches w każdym wierszu.</span><span class="sxs-lookup"><span data-stu-id="fca96-140">This receives an array of items and debatches on each row.</span></span>

```
{
    "myDebatchTrigger": {
        "type": "Http",
        "inputs": {
            "url": "http://getNewCustomers",
        },
        "recurrence": {
            "frequencey": "Second",
            "interval": 15
        },
        "spliton": "@triggerBody()['rows']"
    }
}
```

## <a name="scopes"></a><span data-ttu-id="fca96-141">Zakresy</span><span class="sxs-lookup"><span data-stu-id="fca96-141">Scopes</span></span>

<span data-ttu-id="fca96-142">Jest możliwe toogroup serią działań ze sobą przy użyciu zakresu.</span><span class="sxs-lookup"><span data-stu-id="fca96-142">It is possible toogroup a series of actions together using a scope.</span></span>  <span data-ttu-id="fca96-143">Jest to szczególnie przydatne dla Implementowanie obsługi wyjątków.</span><span class="sxs-lookup"><span data-stu-id="fca96-143">This is particularly useful for implementing exception handling.</span></span>  <span data-ttu-id="fca96-144">W Projektancie hello można dodać nowego zakresu i rozpocząć dodawanie wszystkie akcje wewnątrz niej.</span><span class="sxs-lookup"><span data-stu-id="fca96-144">In hello designer you can add a new scope, and begin adding any actions inside of it.</span></span>  <span data-ttu-id="fca96-145">Zakresy można zdefiniować w widoku kodu, takie jak następujące hello:</span><span class="sxs-lookup"><span data-stu-id="fca96-145">You can define scopes in code-view like hello following:</span></span>


```
{
    "myScope": {
        "type": "scope",
        "actions": {
            "call_bing": {
                "type": "http",
                "inputs": {
                    "url": "http://www.bing.com"
                }
            }
        }
    }
}
```