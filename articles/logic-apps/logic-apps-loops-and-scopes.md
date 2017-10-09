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
# <a name="logic-apps-loops-scopes-and-debatching"></a>Pętle, zakresy i usuwanie partii aplikacji logiki
  
Logic Apps oferuje następujące sposoby toowork z tablic, kolekcje partii i pętle w przepływie pracy.
  
## <a name="foreach-loop-and-arrays"></a>ForEach — pętla i tablic
  
Logic Apps umożliwia tooloop dla zestawu danych i wykonywania akcji dla każdego elementu.  Jest to możliwe za pośrednictwem hello `foreach` akcji.  W Projektancie hello tooadd można określić dla każdej pętli.  Po wybraniu tablicy hello, które mają zostać tooiterate za pośrednictwem, możesz rozpocząć dodawanie akcji.  Obecnie są ograniczone tooonly jedną akcję dla pętli foreach, ale to ograniczenie będzie podnoszone w hello przesyłanych tygodni.  Raz w pętli hello można rozpocząć toospecify, co ma mieć miejsce w każdej wartości hello tablicy.

Jeśli używasz widoku kodu, można określić dla każdej pętli, takie jak poniżej.  To jest przykład dla każdej pętli, który wysyła wiadomości e-mail dla każdego adresu e-mail, który zawiera "microsoft.com":

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
  
  A `foreach` akcji można Iterowanie przez tablice się too5, 000 wierszy.  Domyślnie każdej iteracji będą wykonywane równolegle.  

### <a name="sequential-foreach-loops"></a>Sekwencyjne pętli ForEach

tooenable tooexecute pętli foreach sekwencyjnie, hello `Sequential` opcji operacji powinny zostać dodane.

``` json
"forEach_email": {
        "type": "foreach",
        "foreach": "@body('email_filter')",
        "operationOptions": "Sequential",
        "..."
}
```
  
## <a name="until-loop"></a>Do pętli
  
  Do momentu spełnienia warunku można wykonać akcji lub serii akcji.  Witaj najbardziej typowy scenariusz, w tym wywołuje punkt końcowy do momentu uzyskania odpowiedzi hello, którego szukasz.  W Projektancie hello, można określić tooadd do pętli.  Po dodaniu Akcje wewnątrz pętli hello, możesz można ustawić warunku exit hello, a także hello limity pętli.  Istnieje opóźnienie 1 minutę, między cykle pętli.
  
  Jeśli używasz widoku kodu, można określić aż pętli, takich jak poniżej.  To jest przykład wywołania punktu końcowego HTTP, dopóki treść odpowiedzi hello ma wartość hello "Ukończona".  Proces zostanie zakończony, kiedy użytkownik 
  
  * Odpowiedź HTTP ma stan "Ukończona"
  * Maksymalnie 1 godziny
  * Wystąpiło sprzężenie 100 razy
  
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
  
## <a name="spliton-and-debatching"></a>SplitOn i debatching

Czasami może zostać wyświetlony wyzwalacz tablicę elementów chcesz toodebatch, a następnie uruchomić przepływ pracy dla każdego elementu.  Można to zrobić za pomocą hello `spliton` polecenia.  Domyślnie, jeśli programu swagger wyzwalacza określa ładunku, który jest tablicą `spliton` zostanie dodany i uruchomić Uruchom dla każdego elementu.  SplitOn mogą być dodawane tylko tooa wyzwalacza.  Może to ręcznie skonfigurowane lub zastąpiony w definicji widoku kodu.  Obecnie SplitOn można debatch tablice się too5, 000 elementów.  Nie może mieć `spliton` i również implementują wzorzec synchronicznej odpowiedzi hello.  Każdy przepływ pracy, który wywołuje ma `response` akcji oprócz zbyt`spliton` będą uruchamiane asynchronicznie i wysyłać natychmiastowego `202 Accepted` odpowiedzi.  

W widoku kodu można określić SplitOn jako hello poniższy przykład.  Odbiera tablicę elementów i debatches w każdym wierszu.

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

## <a name="scopes"></a>Zakresy

Jest możliwe toogroup serią działań ze sobą przy użyciu zakresu.  Jest to szczególnie przydatne dla Implementowanie obsługi wyjątków.  W Projektancie hello można dodać nowego zakresu i rozpocząć dodawanie wszystkie akcje wewnątrz niej.  Zakresy można zdefiniować w widoku kodu, takie jak następujące hello:


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