---
title: "powiązanie funkcji usługi Twilio aaaAzure | Dokumentacja firmy Microsoft"
description: "Zrozumienie sposobu powiązania usługi Twilio toouse z usługi Azure Functions."
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: "funkcje usługi Azure, funkcje, przetwarzania zdarzeń, dynamiczne obliczeń niekorzystającą architektury"
ms.assetid: a60263aa-3de9-4e1b-a2bb-0b52e70d559b
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/20/2016
ms.author: wesmc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 882853947850e7d6795ca5b2f3fb6b9a83ede182
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="send-sms-messages-from-azure-functions-using-hello-twilio-output-binding"></a>Wysyłanie wiadomości SMS z usługi Azure Functions przy użyciu hello usługi Twilio powiązania wyjściowego
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

W tym artykule opisano sposób powiązania usługi Twilio tooconfigure i korzystania z usługi Azure Functions. 

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

Środowisko Azure Functions obsługuje tooenable powiązania danych wyjściowych usługi Twilio tekst wiadomości SMS toosend funkcji wiadomości przy użyciu kilku wierszy kodu i [usługi Twilio](https://www.twilio.com/) konta. 

## <a name="functionjson-for-hello-twilio-output-binding"></a>Powiązanie output usługi Twilio Function.JSON dla hello
Plik function.json Hello zawiera hello następujące właściwości:

* `name`: Nazwa zmiennej używane w kodzie funkcja hello wiadomości SMS usługi Twilio.
* `type`: musi być ustawiona zbyt*"twilioSms"*.
* `accountSid`: Ta wartość musi być ustawiona nazwa toohello ustawienia aplikacji, które przechowuje Twojego identyfikatora Sid konta usługi Twilio.
* `authToken`: Ta wartość musi być ustawiona nazwa toohello ustawienia aplikacji, który zawiera token uwierzytelniania usługi Twilio.
* `to`: Ta wartość jest ustawiana toohello numer telefonu, który hello tekst wiadomości SMS są wysyłane do.
* `from`: Ta wartość jest ustawiana toohello numer telefonu, który hello tekst wiadomości SMS są wysyłane z.
* `direction`: musi być ustawiona zbyt*"out"*.
* `body`: Ta wartość może być wiadomość SMS hello kodu toohard używane, jeśli nie ma potrzeby tooset dynamicznie w hello kodu dla funkcji. 

Przykład function.json:

```json
{
  "type": "twilioSms",
  "name": "message",
  "accountSid": "TwilioAccountSid",
  "authToken": "TwilioAuthToken",
  "to": "+1704XXXXXXX",
  "from": "+1425XXXXXXX",
  "direction": "out",
  "body": "Azure Functions Testing"
}
```


## <a name="example-c-queue-trigger-with-twilio-output-binding"></a>Przykład C# kolejki wyzwalacza z usługi Twilio powiązania wyjściowego
#### <a name="synchronous"></a>Synchroniczne
Ten synchroniczne przykładowy kod służący do wyzwalania kolejki usługi Azure Storage korzysta poza toosend parametr zamówienia klient tooa tekst wiadomości.

```cs
#r "Newtonsoft.Json"
#r "Twilio.Api"

using System;
using Newtonsoft.Json;
using Twilio;

public static void Run(string myQueueItem, out SMSMessage message,  TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example hello queue item is a JSON string representing an order that contains hello name of a 
    // customer and a mobile number toosend text updates to.
    dynamic order = JsonConvert.DeserializeObject(myQueueItem);
    string msg = "Hello " + order.name + ", thank you for your order.";

    // Even if you want toouse a hard coded message and number in hello binding, you must at least 
    // initialize hello SMSMessage variable.
    message = new SMSMessage();

    // A dynamic message can be set instead of hello body in hello output binding. In this example, we use 
    // hello order information toopersonalize a text message toohello mobile number provided for
    // order status updates.
    message.Body = msg;
    message.too= order.mobileNumber;
}
```

#### <a name="asynchronous"></a>Asynchroniczne
Ten asynchroniczne przykładowy kod służący do wyzwalania kolejki usługi Azure Storage wysyła zamówienia klient tooa tekst wiadomości.

```cs
#r "Newtonsoft.Json"
#r "Twilio.Api"

using System;
using Newtonsoft.Json;
using Twilio;

public static async Task Run(string myQueueItem, IAsyncCollector<SMSMessage> message,  TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example hello queue item is a JSON string representing an order that contains hello name of a 
    // customer and a mobile number toosend text updates to.
    dynamic order = JsonConvert.DeserializeObject(myQueueItem);
    string msg = "Hello " + order.name + ", thank you for your order.";

    // Even if you want toouse a hard coded message and number in hello binding, you must at least 
    // initialize hello SMSMessage variable.
    SMSMessage smsText = new SMSMessage();

    // A dynamic message can be set instead of hello body in hello output binding. In this example, we use 
    // hello order information toopersonalize a text message toohello mobile number provided for
    // order status updates.
    smsText.Body = msg;
    smsText.too= order.mobileNumber;

    await message.AddAsync(smsText);
}
```

## <a name="example-nodejs-queue-trigger-with-twilio-output-binding"></a>Przykład Node.js kolejki wyzwalacza z usługi Twilio powiązania wyjściowego
W tym przykładzie Node.js wysyła zamówienia klient tooa tekst wiadomości.

```javascript
module.exports = function (context, myQueueItem) {
    context.log('Node.js queue trigger function processed work item', myQueueItem);

    // In this example hello queue item is a JSON string representing an order that contains hello name of a 
    // customer and a mobile number toosend text updates to.
    var msg = "Hello " + myQueueItem.name + ", thank you for your order.";

    // Even if you want toouse a hard coded message and number in hello binding, you must at least 
    // initialize hello message binding.
    context.bindings.message = {};

    // A dynamic message can be set instead of hello body in hello output binding. In this example, we use 
    // hello order information toopersonalize a text message toohello mobile number provided for
    // order status updates.
    context.bindings.message = {
        body : msg,
        too: myQueueItem.mobileNumber
    };

    context.done();
};
```

## <a name="next-steps"></a>Następne kroki
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

