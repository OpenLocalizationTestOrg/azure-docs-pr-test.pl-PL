---
title: wyzwalacz czasomierza funkcje aaaAzure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toouse czasomierza wyzwala w funkcji platformy Azure."
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: "funkcje usługi Azure, funkcje, przetwarzania zdarzeń, dynamiczne obliczeń niekorzystającą architektury"
ms.assetid: d2f013d1-f458-42ae-baf8-1810138118ac
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 02/27/2017
ms.author: glenga
ms.custom: 
ms.openlocfilehash: 17fca22372dbc55d4684c8c099cc97923a7d3cf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-timer-trigger"></a>Azure wyzwalacza czasomierza funkcji

[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

W tym artykule opisano, jak tooconfigure i kod czasomierza wyzwala w funkcji platformy Azure. Środowisko Azure Functions ma powiązanie wyzwalacza czasomierza umożliwia uruchamianie funkcji kodu na podstawie zdefiniowanego harmonogramu. 

wyzwalacz czasomierza Hello obsługuje wiele wystąpień skalowalnego w poziomie. Pojedyncze wystąpienie funkcji określonego czasomierza jest uruchamiane we wszystkich wystąpieniach.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a id="trigger"></a>

## <a name="timer-trigger"></a>Wyzwalacz czasomierza
Witaj czasomierza wyzwalacza tooa funkcja używa powitania po obiekt JSON w hello `bindings` tablicy function.json:

```json
{
    "schedule": "<CRON expression - see below>",
    "name": "<Name of trigger parameter in function signature>",
    "type": "timerTrigger",
    "direction": "in"
}
```

Witaj wartość `schedule` jest [wyrażenie CRON](http://en.wikipedia.org/wiki/Cron#CRON_expression) zawierających te sześć pola: 

    {second} {minute} {hour} {day} {month} {day-of-week}
&nbsp;
>[!NOTE]   
>Pomiń wiele wyrażeń cron hello możesz znaleźć online hello `{second}` pola. Po skopiowaniu jednego z nich, potrzebne tooadjust dla hello dodatkowe `{second}` pola. Aby uzyskać szczegółowe przykłady, zobacz [zaplanować przykłady](#examples) poniżej.

Witaj domyślną strefę czasową używane w wyrażeniach CRON hello jest uniwersalny czas koordynowany (UTC). toohave wyrażenie CRON oparte na innej strefie czasowej, Utwórz nowe ustawienie aplikacji dla aplikacji funkcja o nazwie `WEBSITE_TIME_ZONE`. Zestaw hello wartość toohello nazwę hello potrzeby strefy czasowej, pokazane na powitania [indeksu strefy czasowej Microsoft](https://msdn.microsoft.com/library/ms912391.aspx). 

Na przykład *wschodni czas standardowy* jest UTC-05:00. toohave Twojego czasomierza wyzwolić fire na 10:00 AM EST każdego dnia hello Użyj następującego konta dla strefy czasowej UTC wyrażenie CRON:

```json
"schedule": "0 0 15 * * *",
``` 

Alternatywnie możesz dodać nowe ustawienie aplikacji dla aplikacji funkcja o nazwie `WEBSITE_TIME_ZONE` i ustaw wartość hello zbyt**wschodni czas standardowy**.  Następnie po wyrażeniu CRON hello może służyć do 10:00 AM EST: 

```json
"schedule": "0 0 10 * * *",
``` 


<a name="examples"></a>

## <a name="schedule-examples"></a>Przykłady harmonogramu
Poniżej przedstawiono niektóre przykłady można użyć dla hello wyrażeń CRON `schedule` właściwości. 

tootrigger co pięć minut:

```json
"schedule": "0 */5 * * * *"
```

tootrigger raz u góry hello co godzinę:

```json
"schedule": "0 0 * * * *",
```

tootrigger co dwie godziny:

```json
"schedule": "0 0 */2 * * *",
```

tootrigger co godzinę z 9 AM too5 PM:

```json
"schedule": "0 0 9-17 * * *",
```

tootrigger na 9:30 AM codziennie:

```json
"schedule": "0 30 9 * * *",
```

tootrigger na 9:30 AM każdy dzień tygodnia:

```json
"schedule": "0 30 9 * * 1-5",
```

<a name="usage"></a>

## <a name="trigger-usage"></a>Użycie wyzwalacza
Po wywołaniu funkcji wyzwalacza czasomierza hello [obiekt czasomierza](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerInfo.cs) została przekazana do funkcji hello. Witaj następujące JSON to przykład reprezentację hello obiekt czasomierza. 

```json
{
    "Schedule":{
    },
    "ScheduleStatus": {
        "Last":"2016-10-04T10:15:00.012699+00:00",
        "Next":"2016-10-04T10:20:00+00:00"
    },
    "IsPastDue":false
}
```

<a name="sample"></a>

## <a name="trigger-sample"></a>Przykładowe wyzwalacza
Załóżmy, że masz powitania po czasomierza wyzwalacza w hello `bindings` tablicy function.json:

```json
{
    "schedule": "0 */5 * * * *",
    "name": "myTimer",
    "type": "timerTrigger",
    "direction": "in"
}
```

Zobacz próbka specyficzny dla języka hello, która odczytuje czasomierza hello toosee obiektu, czy jest uruchomiona opóźnienia.

* [C#](#triggercsharp)
* [F#](#triggerfsharp)
* [Node.js](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a>Przykładowe wyzwalacza w języku C# #
```csharp
public static void Run(TimerInfo myTimer, TraceWriter log)
{
    if(myTimer.IsPastDue)
    {
        log.Info("Timer is running late!");
    }
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}" );  
}
```

<a name="triggerfsharp"></a>

### <a name="trigger-sample-in-f"></a>Przykładowe wyzwalacza w języku F # #
```fsharp
let Run(myTimer: TimerInfo, log: TraceWriter ) =
    if (myTimer.IsPastDue) then
        log.Info("F# function is running late.")
    let now = DateTime.Now.ToLongTimeString()
    log.Info(sprintf "F# function executed at %s!" now)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a>Przykładowe wyzwalacza w środowisku Node.js
```JavaScript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();

    if(myTimer.isPastDue)
    {
        context.log('Node.js is running late!');
    }
    context.log('Node.js timer trigger function ran!', timeStamp);   

    context.done();
};
```

## <a name="next-steps"></a>Następne kroki
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

