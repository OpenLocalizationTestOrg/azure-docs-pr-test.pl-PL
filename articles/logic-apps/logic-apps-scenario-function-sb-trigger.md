---
title: "aaaScenario — aplikacje logiki wyzwalacza z funkcjami platformy Azure i usługi Azure Service Bus | Dokumentacja firmy Microsoft"
description: "Tworzenie aplikacji logiki tootrigger funkcji przy użyciu usługi Azure Functions i usługi Azure Service Bus"
services: logic-apps,functions
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 19cbd921-7071-4221-ab86-b44d0fc0ecef
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 05/23/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: a7b78ebcfe492eee2e08ceeae6b9c5f8ed4717bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="scenario-trigger-a-logic-app-with-azure-functions-and-azure-service-bus"></a>Scenariusz: Wyzwolenia aplikacji logiki z funkcjami platformy Azure i usługi Azure Service Bus

Azure Functions toocreate wyzwalacz służącego do aplikacji logiki gdy będziesz potrzebować toodeploy długotrwałe odbiornika, lub zadania. Można na przykład tworzy funkcję, która nasłuchuje kolejki i natychmiast uruchomić aplikację logiki, jako wyzwalacz wypychania.

## <a name="build-hello-logic-app"></a>Tworzenie aplikacji logiki hello
W tym przykładzie należy funkcji uruchomione dla każdej aplikacji logiki, wymagającym toobe wyzwolone. Najpierw należy utworzyć aplikację logiki, która zawiera wyzwalacz żądania HTTP. Funkcja Hello wywołań tego punktu końcowego przy każdym odebraniu komunikatu w kolejce.  

1. Tworzenie aplikacji logiki.
2. Wybierz hello **ręczny — po odebraniu żądania HTTP** wyzwalacza.
   Opcjonalnie można określić toouse schematu JSON z hello komunikat z kolejki przy użyciu narzędzia, takiego jak [jsonschema.net](http://jsonschema.net). Wklej schematu hello hello wyzwalacza. Schematy pomóc zrozumieć kształtu hello hello właściwości do danych i przepływu łatwiej za pomocą przepływu pracy hello projektanta hello.
2. Dodaj wszelkie dodatkowe kroki, które mają toooccur po odebraniu komunikatu w kolejce. Na przykład wysłać wiadomość e-mail za pośrednictwem usługi Office 365.  
3. Zapisz hello logiki toogenerate hello wywołania zwrotnego adresu URL aplikacji hello wyzwalacza toothis logiki aplikacji. adres URL Hello pojawia się na karcie wyzwalacza hello.

![Hello wywołania zwrotnego adresu URL pojawia się na karcie wyzwalacza hello][1]

## <a name="build-hello-function"></a>Tworzenie hello — funkcja
Następnie należy utworzyć funkcję, która działa jako wyzwalacz hello i nasłuchuje toohello kolejki.

1. W hello [portalu Azure Functions](https://functions.azure.com/signin), wybierz pozycję **nową funkcję**, a następnie wybierz hello **ServiceBusQueueTrigger - C#** szablonu.
   
    ![Portalu Azure Functions][2]
2. Konfigurowanie kolejki usługi Service Bus pakietu hello połączenia toohello, który wykorzystuje hello Azure Service Bus SDK `OnMessageReceive()` odbiornika.
3. Zapisać podstawowych funkcji toocall hello logiki aplikacji punktu końcowego (wcześniej utworzone) przy użyciu wiadomości powitania kolejki jako wyzwalacz. W tym miejscu jest pełny przykład funkcji. przykład Witaj używa `application/json` typ zawartości komunikatu, ale można zmienić tego typu, w razie potrzeby.
   
   ```
   using System;
   using System.Threading.Tasks;
   using System.Net.Http;
   using System.Text;
   
   private static string logicAppUri = @"https://prod-05.westus.logic.azure.com:443/.........";
   
   public static void Run(string myQueueItem, TraceWriter log)
   {
   
       log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
       using (var client = new HttpClient())
       {
           var response = client.PostAsync(logicAppUri, new StringContent(myQueueItem, Encoding.UTF8, "application/json")).Result;
       }
   }
   ```

tootest, Dodaj komunikatu w kolejce za pomocą narzędzia, takiego jak [Service Bus Explorer](https://github.com/paolosalvatori/ServiceBusExplorer). Zobacz aplikacji logiki hello wyzwalać natychmiast, gdy funkcja hello otrzyma wiadomość hello.

<!-- Image References -->
[1]: ./media/logic-apps-scenario-function-sb-trigger/manualtrigger.png
[2]: ./media/logic-apps-scenario-function-sb-trigger/newqueuetriggerfunction.png
