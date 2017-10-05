---
title: Azure wyzwalacza czasomierza funkcje | Dokumentacja firmy Microsoft
description: "Zrozumienie, jak używać czasomierza Wyzwalacze w funkcji Azure."
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
ms.openlocfilehash: 6a97ab8508f889b77d064a5da70e3c726d62900c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-timer-trigger"></a><span data-ttu-id="97863-104">Azure wyzwalacza czasomierza funkcji</span><span class="sxs-lookup"><span data-stu-id="97863-104">Azure Functions timer trigger</span></span>

[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="97863-105">W tym artykule opisano sposób konfigurowania i wyzwalaczy czasomierza kodu w usługi Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="97863-105">This article explains how to configure and code timer triggers in Azure Functions.</span></span> <span data-ttu-id="97863-106">Środowisko Azure Functions ma powiązanie wyzwalacza czasomierza umożliwia uruchamianie funkcji kodu na podstawie zdefiniowanego harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="97863-106">Azure Functions has a timer trigger binding that lets you run your function code based on a defined schedule.</span></span> 

<span data-ttu-id="97863-107">Wyzwalacz czasomierza obsługuje wiele wystąpień skalowalnego w poziomie. Pojedyncze wystąpienie funkcji określonego czasomierza jest uruchamiane we wszystkich wystąpieniach.</span><span class="sxs-lookup"><span data-stu-id="97863-107">The timer trigger supports multi-instance scale-out. A single instance of a particular timer function is run across all instances.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a id="trigger"></a>

## <a name="timer-trigger"></a><span data-ttu-id="97863-108">Wyzwalacz czasomierza</span><span class="sxs-lookup"><span data-stu-id="97863-108">Timer trigger</span></span>
<span data-ttu-id="97863-109">Wyzwalacz czasomierza funkcji używa następujący obiekt JSON w `bindings` tablicy function.json:</span><span class="sxs-lookup"><span data-stu-id="97863-109">The timer trigger to a function uses the following JSON object in the `bindings` array of function.json:</span></span>

```json
{
    "schedule": "<CRON expression - see below>",
    "name": "<Name of trigger parameter in function signature>",
    "type": "timerTrigger",
    "direction": "in"
}
```

<span data-ttu-id="97863-110">Wartość `schedule` jest [wyrażenie CRON](http://en.wikipedia.org/wiki/Cron#CRON_expression) zawierających te sześć pola:</span><span class="sxs-lookup"><span data-stu-id="97863-110">The value of `schedule` is a [CRON expression](http://en.wikipedia.org/wiki/Cron#CRON_expression) that includes these six fields:</span></span> 

    {second} {minute} {hour} {day} {month} {day-of-week}
&nbsp;
>[!NOTE]   
><span data-ttu-id="97863-111">Wiele wyrażeń cron możesz znaleźć online Pomiń `{second}` pola.</span><span class="sxs-lookup"><span data-stu-id="97863-111">Many of the cron expressions you find online omit the `{second}` field.</span></span> <span data-ttu-id="97863-112">Po skopiowaniu jednego z nich, należy dostosować nadmiarowe `{second}` pola.</span><span class="sxs-lookup"><span data-stu-id="97863-112">If you copy from one of them, you need to adjust for the extra `{second}` field.</span></span> <span data-ttu-id="97863-113">Aby uzyskać szczegółowe przykłady, zobacz [zaplanować przykłady](#examples) poniżej.</span><span class="sxs-lookup"><span data-stu-id="97863-113">For specific examples, see [Schedule examples](#examples) below.</span></span>

<span data-ttu-id="97863-114">Domyślna strefa czasowa używane w wyrażeniach CRON jest uniwersalny czas koordynowany (UTC).</span><span class="sxs-lookup"><span data-stu-id="97863-114">The default time zone used with the CRON expressions is Coordinated Universal Time (UTC).</span></span> <span data-ttu-id="97863-115">Aby wymusić wyrażenie CRON oparte na innej strefie czasowej, Utwórz nowe ustawienie aplikacji dla aplikacji funkcja o nazwie `WEBSITE_TIME_ZONE`.</span><span class="sxs-lookup"><span data-stu-id="97863-115">To have your CRON expression based on another time zone, create a new app setting for your function app named `WEBSITE_TIME_ZONE`.</span></span> <span data-ttu-id="97863-116">Ustaw wartość na nazwę odpowiednie strefy czasowej, jak pokazano w [indeksu strefy czasowej Microsoft](https://msdn.microsoft.com/library/ms912391.aspx).</span><span class="sxs-lookup"><span data-stu-id="97863-116">Set the value to the name of the desired time zone as shown in the [Microsoft Time Zone Index](https://msdn.microsoft.com/library/ms912391.aspx).</span></span> 

<span data-ttu-id="97863-117">Na przykład *wschodni czas standardowy* jest UTC-05:00.</span><span class="sxs-lookup"><span data-stu-id="97863-117">For example, *Eastern Standard Time* is UTC-05:00.</span></span> <span data-ttu-id="97863-118">Aby Twoje czasomierza wyzwolenia fire na 10:00 CET codziennie, użyj następujących kont dla strefy czasowej UTC wyrażenie CRON:</span><span class="sxs-lookup"><span data-stu-id="97863-118">To have your timer trigger fire at 10:00 AM EST every day, use the following CRON expression that accounts for UTC time zone:</span></span>

```json
"schedule": "0 0 15 * * *",
``` 

<span data-ttu-id="97863-119">Alternatywnie możesz dodać nowe ustawienie aplikacji dla aplikacji funkcja o nazwie `WEBSITE_TIME_ZONE` i ustaw wartość **wschodni czas standardowy**.</span><span class="sxs-lookup"><span data-stu-id="97863-119">Alternatively, you could add a new app setting for your function app named `WEBSITE_TIME_ZONE` and set the value to **Eastern Standard Time**.</span></span>  <span data-ttu-id="97863-120">Poniższe wyrażenie CRON można następnie używać do 10:00 AM EST:</span><span class="sxs-lookup"><span data-stu-id="97863-120">Then the following CRON expression could be used for 10:00 AM EST:</span></span> 

```json
"schedule": "0 0 10 * * *",
``` 


<a name="examples"></a>

## <a name="schedule-examples"></a><span data-ttu-id="97863-121">Przykłady harmonogramu</span><span class="sxs-lookup"><span data-stu-id="97863-121">Schedule examples</span></span>
<span data-ttu-id="97863-122">Poniżej przedstawiono niektóre przykłady można użyć dla wyrażeń CRON `schedule` właściwości.</span><span class="sxs-lookup"><span data-stu-id="97863-122">Here are some samples of CRON expressions you can use for the `schedule` property.</span></span> 

<span data-ttu-id="97863-123">Aby wyzwolić co pięć minut:</span><span class="sxs-lookup"><span data-stu-id="97863-123">To trigger once every five minutes:</span></span>

```json
"schedule": "0 */5 * * * *"
```

<span data-ttu-id="97863-124">Aby wyzwolić raz, w górnej części co godzinę:</span><span class="sxs-lookup"><span data-stu-id="97863-124">To trigger once at the top of every hour:</span></span>

```json
"schedule": "0 0 * * * *",
```

<span data-ttu-id="97863-125">Aby wyzwolić co dwie godziny:</span><span class="sxs-lookup"><span data-stu-id="97863-125">To trigger once every two hours:</span></span>

```json
"schedule": "0 0 */2 * * *",
```

<span data-ttu-id="97863-126">Aby wyzwolić co godzinę z 9 AM do 17: 00:</span><span class="sxs-lookup"><span data-stu-id="97863-126">To trigger once every hour from 9 AM to 5 PM:</span></span>

```json
"schedule": "0 0 9-17 * * *",
```

<span data-ttu-id="97863-127">Aby wyzwolić na 9:30 AM codziennie:</span><span class="sxs-lookup"><span data-stu-id="97863-127">To trigger At 9:30 AM every day:</span></span>

```json
"schedule": "0 30 9 * * *",
```

<span data-ttu-id="97863-128">Aby wyzwolić na 9:30 AM każdy dzień tygodnia:</span><span class="sxs-lookup"><span data-stu-id="97863-128">To trigger At 9:30 AM every weekday:</span></span>

```json
"schedule": "0 30 9 * * 1-5",
```

<a name="usage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="97863-129">Użycie wyzwalacza</span><span class="sxs-lookup"><span data-stu-id="97863-129">Trigger usage</span></span>
<span data-ttu-id="97863-130">Po wywołaniu funkcji wyzwalacza czasomierza [obiekt czasomierza](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerInfo.cs) została przekazana do funkcji.</span><span class="sxs-lookup"><span data-stu-id="97863-130">When a timer trigger function is invoked, the [timer object](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerInfo.cs) is passed into the function.</span></span> <span data-ttu-id="97863-131">Następujący kod JSON jest przykład reprezentację obiekt czasomierza.</span><span class="sxs-lookup"><span data-stu-id="97863-131">The following JSON is an example representation of the timer object.</span></span> 

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

## <a name="trigger-sample"></a><span data-ttu-id="97863-132">Przykładowe wyzwalacza</span><span class="sxs-lookup"><span data-stu-id="97863-132">Trigger sample</span></span>
<span data-ttu-id="97863-133">Załóżmy, że masz następujące wyzwalacza czasomierza `bindings` tablicy function.json:</span><span class="sxs-lookup"><span data-stu-id="97863-133">Suppose you have the following timer trigger in the `bindings` array of function.json:</span></span>

```json
{
    "schedule": "0 */5 * * * *",
    "name": "myTimer",
    "type": "timerTrigger",
    "direction": "in"
}
```

<span data-ttu-id="97863-134">Zobacz próbka specyficzny dla języka, która odczytuje obiekt czasomierza, aby zobaczyć, czy działa późne.</span><span class="sxs-lookup"><span data-stu-id="97863-134">See the language-specific sample that reads the timer object to see whether it's running late.</span></span>

* [<span data-ttu-id="97863-135">C#</span><span class="sxs-lookup"><span data-stu-id="97863-135">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="97863-136">F#</span><span class="sxs-lookup"><span data-stu-id="97863-136">F#</span></span>](#triggerfsharp)
* [<span data-ttu-id="97863-137">Node.js</span><span class="sxs-lookup"><span data-stu-id="97863-137">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="97863-138">Przykładowe wyzwalacza w języku C#</span><span class="sxs-lookup"><span data-stu-id="97863-138">Trigger sample in C#</span></span> #
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

### <a name="trigger-sample-in-f"></a><span data-ttu-id="97863-139">Przykładowe wyzwalacza w języku F #</span><span class="sxs-lookup"><span data-stu-id="97863-139">Trigger sample in F#</span></span> #
```fsharp
let Run(myTimer: TimerInfo, log: TraceWriter ) =
    if (myTimer.IsPastDue) then
        log.Info("F# function is running late.")
    let now = DateTime.Now.ToLongTimeString()
    log.Info(sprintf "F# function executed at %s!" now)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="97863-140">Przykładowe wyzwalacza w środowisku Node.js</span><span class="sxs-lookup"><span data-stu-id="97863-140">Trigger sample in Node.js</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="97863-141">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="97863-141">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

