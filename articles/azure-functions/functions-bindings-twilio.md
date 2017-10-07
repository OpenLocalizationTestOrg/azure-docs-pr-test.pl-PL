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
# <a name="send-sms-messages-from-azure-functions-using-hello-twilio-output-binding"></a><span data-ttu-id="fe72f-104">Wysyłanie wiadomości SMS z usługi Azure Functions przy użyciu hello usługi Twilio powiązania wyjściowego</span><span class="sxs-lookup"><span data-stu-id="fe72f-104">Send SMS messages from Azure Functions using hello Twilio output binding</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="fe72f-105">W tym artykule opisano sposób powiązania usługi Twilio tooconfigure i korzystania z usługi Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="fe72f-105">This article explains how tooconfigure and use Twilio bindings with Azure Functions.</span></span> 

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="fe72f-106">Środowisko Azure Functions obsługuje tooenable powiązania danych wyjściowych usługi Twilio tekst wiadomości SMS toosend funkcji wiadomości przy użyciu kilku wierszy kodu i [usługi Twilio](https://www.twilio.com/) konta.</span><span class="sxs-lookup"><span data-stu-id="fe72f-106">Azure Functions supports Twilio output bindings tooenable your functions toosend SMS text messages with a few lines of code and a [Twilio](https://www.twilio.com/) account.</span></span> 

## <a name="functionjson-for-hello-twilio-output-binding"></a><span data-ttu-id="fe72f-107">Powiązanie output usługi Twilio Function.JSON dla hello</span><span class="sxs-lookup"><span data-stu-id="fe72f-107">function.json for hello Twilio output binding</span></span>
<span data-ttu-id="fe72f-108">Plik function.json Hello zawiera hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="fe72f-108">hello function.json file provides hello following properties:</span></span>

* <span data-ttu-id="fe72f-109">`name`: Nazwa zmiennej używane w kodzie funkcja hello wiadomości SMS usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="fe72f-109">`name` : Variable name used in function code for hello Twilio SMS text message.</span></span>
* <span data-ttu-id="fe72f-110">`type`: musi być ustawiona zbyt*"twilioSms"*.</span><span class="sxs-lookup"><span data-stu-id="fe72f-110">`type` : must be set too*"twilioSms"*.</span></span>
* <span data-ttu-id="fe72f-111">`accountSid`: Ta wartość musi być ustawiona nazwa toohello ustawienia aplikacji, które przechowuje Twojego identyfikatora Sid konta usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="fe72f-111">`accountSid` : This value must be set toohello name of an App Setting that holds your Twilio Account Sid.</span></span>
* <span data-ttu-id="fe72f-112">`authToken`: Ta wartość musi być ustawiona nazwa toohello ustawienia aplikacji, który zawiera token uwierzytelniania usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="fe72f-112">`authToken` : This value must be set toohello name of an App Setting that holds your Twilio authentication token.</span></span>
* <span data-ttu-id="fe72f-113">`to`: Ta wartość jest ustawiana toohello numer telefonu, który hello tekst wiadomości SMS są wysyłane do.</span><span class="sxs-lookup"><span data-stu-id="fe72f-113">`to` : This value is set toohello phone number that hello SMS text is sent to.</span></span>
* <span data-ttu-id="fe72f-114">`from`: Ta wartość jest ustawiana toohello numer telefonu, który hello tekst wiadomości SMS są wysyłane z.</span><span class="sxs-lookup"><span data-stu-id="fe72f-114">`from` : This value is set toohello phone number that hello SMS text is sent from.</span></span>
* <span data-ttu-id="fe72f-115">`direction`: musi być ustawiona zbyt*"out"*.</span><span class="sxs-lookup"><span data-stu-id="fe72f-115">`direction` : must be set too*"out"*.</span></span>
* <span data-ttu-id="fe72f-116">`body`: Ta wartość może być wiadomość SMS hello kodu toohard używane, jeśli nie ma potrzeby tooset dynamicznie w hello kodu dla funkcji.</span><span class="sxs-lookup"><span data-stu-id="fe72f-116">`body` : This value can be used toohard code hello SMS text message if you don't need tooset it dynamically in hello code for your function.</span></span> 

<span data-ttu-id="fe72f-117">Przykład function.json:</span><span class="sxs-lookup"><span data-stu-id="fe72f-117">Example function.json:</span></span>

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


## <a name="example-c-queue-trigger-with-twilio-output-binding"></a><span data-ttu-id="fe72f-118">Przykład C# kolejki wyzwalacza z usługi Twilio powiązania wyjściowego</span><span class="sxs-lookup"><span data-stu-id="fe72f-118">Example C# queue trigger with Twilio output binding</span></span>
#### <a name="synchronous"></a><span data-ttu-id="fe72f-119">Synchroniczne</span><span class="sxs-lookup"><span data-stu-id="fe72f-119">Synchronous</span></span>
<span data-ttu-id="fe72f-120">Ten synchroniczne przykładowy kod służący do wyzwalania kolejki usługi Azure Storage korzysta poza toosend parametr zamówienia klient tooa tekst wiadomości.</span><span class="sxs-lookup"><span data-stu-id="fe72f-120">This synchronous example code for an Azure Storage queue trigger uses an out parameter toosend a text message tooa customer who placed an order.</span></span>

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

#### <a name="asynchronous"></a><span data-ttu-id="fe72f-121">Asynchroniczne</span><span class="sxs-lookup"><span data-stu-id="fe72f-121">Asynchronous</span></span>
<span data-ttu-id="fe72f-122">Ten asynchroniczne przykładowy kod służący do wyzwalania kolejki usługi Azure Storage wysyła zamówienia klient tooa tekst wiadomości.</span><span class="sxs-lookup"><span data-stu-id="fe72f-122">This asynchronous example code for an Azure Storage queue trigger sends a text message tooa customer who placed an order.</span></span>

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

## <a name="example-nodejs-queue-trigger-with-twilio-output-binding"></a><span data-ttu-id="fe72f-123">Przykład Node.js kolejki wyzwalacza z usługi Twilio powiązania wyjściowego</span><span class="sxs-lookup"><span data-stu-id="fe72f-123">Example Node.js queue trigger with Twilio output binding</span></span>
<span data-ttu-id="fe72f-124">W tym przykładzie Node.js wysyła zamówienia klient tooa tekst wiadomości.</span><span class="sxs-lookup"><span data-stu-id="fe72f-124">This Node.js example sends a text message tooa customer who placed an order.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="fe72f-125">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fe72f-125">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

