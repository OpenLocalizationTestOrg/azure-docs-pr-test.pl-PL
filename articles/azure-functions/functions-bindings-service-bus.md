---
title: "Azure powiązania usługi Service Bus dla usługi Azure Functions"
description: "Zrozumienie, jak używać usługi Azure Service Bus wyzwalaczy i powiązań w funkcji platformy Azure."
services: functions
documentationcenter: na
author: tdykstra
manager: cfowler
editor: 
tags: 
keywords: "funkcje usługi Azure, funkcje, przetwarzania zdarzeń, dynamiczne obliczeń niekorzystającą architektury"
ms.assetid: daedacf0-6546-4355-a65c-50873e74f66b
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 04/01/2017
ms.author: tdykstra
ms.openlocfilehash: 2df003d47291570b31e1091f34994e4023000981
ms.sourcegitcommit: 85012dbead7879f1f6c2965daa61302eb78bd366
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/02/2018
---
# <a name="azure-service-bus-bindings-for-azure-functions"></a>Azure powiązania usługi Service Bus dla usługi Azure Functions

W tym artykule opisano sposób pracy z usługi Azure Service Bus powiązania usługi Azure Functions. Usługi Azure Functions obsługuje uruchomić i dane wyjściowe powiązania dla tematów i kolejek usługi Service Bus.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="trigger"></a>Wyzwalacz

Wyzwalacz usługi Service Bus umożliwia odpowiada na komunikaty z kolejki usługi Service Bus lub temat. 

## <a name="trigger---example"></a>Wyzwalacz — przykład

Zapoznaj się z przykładem specyficzny dla języka:

* [C#](#trigger---c-example)
* [Skryptu C# (csx)](#trigger---c-script-example)
* [F#](#trigger---f-example)
* [JavaScript](#trigger---javascript-example)

### <a name="trigger---c-example"></a>Wyzwalacz — przykład C#

W poniższym przykładzie przedstawiono [C# funkcja](functions-dotnet-class-library.md) loguje się komunikat z kolejki usługi Service Bus.

```cs
[FunctionName("ServiceBusQueueTriggerCSharp")]                    
public static void Run(
    [ServiceBusTrigger("myqueue", AccessRights.Manage, Connection = "ServiceBusConnection")] 
    string myQueueItem, 
    TraceWriter log)
{
    log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
}
```

### <a name="trigger---c-script-example"></a>Wyzwalacz — przykładowy skrypt w języku C#

W poniższym przykładzie przedstawiono wyzwalacz usługi Service Bus powiązanie w *function.json* pliku i [funkcji skryptu C#](functions-reference-csharp.md) używającą powiązania. Funkcja rejestruje komunikat z kolejki usługi Service Bus.

W tym miejscu jest powiązanie danych *function.json* pliku:

```json
{
"bindings": [
    {
    "queueName": "testqueue",
    "connection": "MyServiceBusConnection",
    "name": "myQueueItem",
    "type": "serviceBusTrigger",
    "direction": "in"
    }
],
"disabled": false
}
```

Oto kod skryptu C#:

```cs
public static void Run(string myQueueItem, TraceWriter log)
{
    log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
}
```

### <a name="trigger---f-example"></a>Wyzwalacz — przykład F #

W poniższym przykładzie przedstawiono wyzwalacz usługi Service Bus powiązanie w *function.json* pliku i [F # funkcja](functions-reference-fsharp.md) używającą powiązania. Funkcja rejestruje komunikat z kolejki usługi Service Bus. 

W tym miejscu jest powiązanie danych *function.json* pliku:

```json
{
"bindings": [
    {
    "queueName": "testqueue",
    "connection": "MyServiceBusConnection",
    "name": "myQueueItem",
    "type": "serviceBusTrigger",
    "direction": "in"
    }
],
"disabled": false
}
```

Oto kod skryptu języka F #:

```fsharp
let Run(myQueueItem: string, log: TraceWriter) =
    log.Info(sprintf "F# ServiceBus queue trigger function processed message: %s" myQueueItem)
```

### <a name="trigger---javascript-example"></a>Wyzwalacz — przykład JavaScript

W poniższym przykładzie przedstawiono wyzwalacz usługi Service Bus powiązanie w *function.json* pliku i [funkcji JavaScript](functions-reference-node.md) używającą powiązania. Funkcja rejestruje komunikat z kolejki usługi Service Bus. 

W tym miejscu jest powiązanie danych *function.json* pliku:

```json
{
"bindings": [
    {
    "queueName": "testqueue",
    "connection": "MyServiceBusConnection",
    "name": "myQueueItem",
    "type": "serviceBusTrigger",
    "direction": "in"
    }
],
"disabled": false
}
```

Oto kod skryptu JavaScript:

```javascript
module.exports = function(context, myQueueItem) {
    context.log('Node.js ServiceBus queue trigger function processed message', myQueueItem);
    context.done();
};
```

## <a name="trigger---attributes"></a>Wyzwalacz — atrybuty

W [bibliotek klas C#](functions-dotnet-class-library.md), umożliwia skonfigurowanie wyzwalacz usługi Service Bus następujące atrybuty:

* [ServiceBusTriggerAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusTriggerAttribute.cs), zdefiniowany w pakiecie NuGet [Microsoft.Azure.WebJobs.ServiceBus](http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus)

  Konstruktor atrybutu ma nazwę kolejki lub tematu i subskrypcji. Można również określić prawa dostępu do tego połączenia. Jeśli nie określisz praw dostępu, wartością domyślną jest `Manage`. Jak wybrać ustawienie prawa dostępu zostało wyjaśnione w dokumencie [wyzwalacza — Konfiguracja](#trigger---configuration) sekcji. Oto przykład pokazujący atrybut z parametru ciągu:

  ```csharp
  [FunctionName("ServiceBusQueueTriggerCSharp")]                    
  public static void Run(
      [ServiceBusTrigger("myqueue")] string myQueueItem, TraceWriter log)
  {
      ...
  }
  ```

  Można ustawić `Connection` właściwości w celu określenia konta usługi Service Bus do użycia, jak pokazano w poniższym przykładzie:

  ```csharp
  [FunctionName("ServiceBusQueueTriggerCSharp")]                    
  public static void Run(
      [ServiceBusTrigger("myqueue", Connection = "ServiceBusConnection")] 
      string myQueueItem, TraceWriter log)
  {
      ...
  }
  ```

  Pełny przykład, zobacz [wyzwalacza — przykład C#](#trigger---c-example).

* [ServiceBusAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs), zdefiniowany w pakiecie NuGet [Microsoft.Azure.WebJobs.ServiceBus](http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus)

  Umożliwia określenie konta usługi Service Bus w inny sposób. Konstruktor przyjmuje nazwę ustawienia aplikacji, która zawiera parametry połączenia magistrali usług. Ten atrybut można stosować na poziomie klasy parametrów, metody lub. W poniższym przykładzie przedstawiono poziom klasy i metody:

  ```csharp
  [ServiceBusAccount("ClassLevelServiceBusAppSetting")]
  public static class AzureFunctions
  {
      [ServiceBusAccount("MethodLevelServiceBusAppSetting")]
      [FunctionName("ServiceBusQueueTriggerCSharp")]
      public static void Run(
          [ServiceBusTrigger("myqueue", AccessRights.Manage)] 
          string myQueueItem, TraceWriter log)
  {
      ...
  }
  ```

Konto usługi Service Bus umożliwia jest określany w następującej kolejności:

* `ServiceBusTrigger` Atrybutu `Connection` właściwości.
* `ServiceBusAccount` Atrybut zastosowany do tego samego parametru jako `ServiceBusTrigger` atrybutu.
* `ServiceBusAccount` Atrybut zastosowany do funkcji.
* `ServiceBusAccount` Atrybut zastosowany do klasy.
* Ustawienie aplikacji "AzureWebJobsServiceBus".

## <a name="trigger---configuration"></a>Wyzwalacz — Konfiguracja

W poniższej tabeli opisano powiązania właściwości konfiguracyjne, które można ustawić w *function.json* pliku i `ServiceBusTrigger` atrybutu.

|Właściwość Function.JSON | Właściwość atrybutu |Opis|
|---------|---------|----------------------|
|**Typ** | Nie dotyczy | Musi być równa "serviceBusTrigger". Ta właściwość ma wartość automatycznie, podczas tworzenia wyzwalacza w portalu Azure.|
|**Kierunek** | Nie dotyczy | Należy wybrać opcję "w". Ta właściwość ma wartość automatycznie, podczas tworzenia wyzwalacza w portalu Azure. |
|**Nazwa** | Nie dotyczy | Nazwa zmiennej, która reprezentuje kolejka lub temat komunikat w kodzie funkcji. Wartość "$return" odwołują się do wartości zwracane funkcji. | 
|**queueName**|**QueueName**|Nazwa kolejki do monitorowania.  Ustawiona tylko wtedy, gdy monitorowania kolejki, a nie dla tematu.
|**topicName**|**TopicName**|Nazwa tematu do monitorowania. Ustawiona tylko wtedy, gdy monitorowania tematu, nie dla kolejki.|
|**Nazwa subskrypcji**|**Nazwa subskrypcji**|Nazwa subskrypcji do monitorowania. Ustawiona tylko wtedy, gdy monitorowania tematu, nie dla kolejki.|
|**połączenia**|**Połączenia**|Nazwa ustawienia aplikacji, która zawiera parametry połączenia magistrali usługi do użycia dla tego powiązania. Jeśli nazwa ustawienia aplikacji rozpoczyna się od "AzureWebJobs", można określić tylko w pozostałej części nazwy. Na przykład jeśli ustawisz `connection` do "MyServiceBus" środowisko uruchomieniowe Functions szuka ustawienie aplikacji o nazwie "AzureWebJobsMyServiceBus." Jeśli opuścisz `connection` pusta, domyślny ciąg połączenia usługi Service Bus używa funkcji środowiska uruchomieniowego w ustawieniu aplikacji o nazwie "AzureWebJobsServiceBus".<br><br>Aby uzyskać ciąg połączenia, wykonaj kroki opisane w [uzyskać poświadczenia zarządzania](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials). Parametry połączenia muszą mieć dla przestrzeni nazw usługi Service Bus, nie są ograniczone do określonych kolejka lub temat. |
|**accessRights**|**Dostęp**|Prawa dostępu do ciągu połączenia. Dostępne wartości to `manage` i `listen`. Wartość domyślna to `manage`, co oznacza, że `connection` ma **Zarządzaj** uprawnienia. Jeśli używasz parametry połączenia, które nie ma **Zarządzaj** zestawu uprawnień, `accessRights` "nasłuchiwanie". W przeciwnym razie środowiska uruchomieniowego może się nie powieść próba wykonania tej operacji, które wymagają funkcji zarządzania prawami.|

[!INCLUDE [app settings to local.settings.json](../../includes/functions-app-settings-local.md)]

## <a name="trigger---usage"></a>Wyzwalacz — użycie

W języku C# i skryptu C#, dostęp do kolejki lub tematu wiadomości przy użyciu parametru metody takie jak `string paramName`. W języku C# skryptu `paramName` jest wartością określoną w `name` właściwość *function.json*. Można użyć dowolnego z następujących typów zamiast `string`:

* `byte[]`-Przydatne dla danych binarnych.
* Niestandardowy typ — Jeśli komunikat zawiera dane JSON, usługi Azure Functions próbuje deserializowanie danych JSON.
* `BrokeredMessage`— Umożliwia zdeserializowany wiadomości z [BrokeredMessage.GetBody<T>()](https://msdn.microsoft.com/library/hh144211.aspx) metody.

W języku JavaScript, dostęp do kolejki lub tematu wiadomości przy użyciu `context.bindings.<name>`. `<name>`wartość jest określona w `name` właściwość *function.json*. Komunikatów usługi Service Bus jest przekazywany do funkcji jako ciąg lub obiekt JSON.

## <a name="trigger---poison-messages"></a>Wyzwalacz - skażone wiadomości

Obsługi uszkodzonych komunikatów nie może być kontrolowane ani skonfigurowane w funkcji platformy Azure. Usługa Service Bus obsługuje skażone wiadomości samej siebie.

## <a name="trigger---peeklock-behavior"></a>Wyzwalacz - PeekLock zachowanie

Środowisko uruchomieniowe Functions odbiera wiadomości w [tryb PeekLock](../service-bus-messaging/service-bus-performance-improvements.md#receive-mode). Wywołuje `Complete` na komunikat, jeśli funkcja zakończy działanie pomyślnie, lub wywołania `Abandon` Jeśli funkcja nie powiedzie się. Jeśli funkcja uruchomione dłużej niż `PeekLock` limit czasu blokady automatycznie zostanie odnowiona.

## <a name="trigger---hostjson-properties"></a>Wyzwalacz - host.json właściwości

[Host.json](functions-host-json.md#servicebus) plik zawiera ustawienia, które kontrolują zachowanie wyzwalacza usługi Service Bus.

[!INCLUDE [functions-host-json-event-hubs](../../includes/functions-host-json-service-bus.md)]

## <a name="output"></a>Dane wyjściowe

Powiązanie danych wyjściowych usługi Azure Service Bus wysyłać pomocą kolejka lub temat.

## <a name="output---example"></a>OUTPUT — przykład

Zapoznaj się z przykładem specyficzny dla języka:

* [C#](#output---c-example)
* [Skryptu C# (csx)](#output---c-script-example)
* [F#](#output---f-example)
* [JavaScript](#output---javascript-example)

### <a name="output---c-example"></a>Dane wyjściowe — przykład C#

W poniższym przykładzie przedstawiono [C# funkcja](functions-dotnet-class-library.md) który wysyła komunikat z kolejki usługi Service Bus:

```cs
[FunctionName("ServiceBusOutput")]
[return: ServiceBus("myqueue", Connection = "ServiceBusConnection")]
public static string ServiceBusOutput([HttpTrigger] dynamic input, TraceWriter log)
{
    log.Info($"C# function processed: {input.Text}");
    return input.Text;
}
```

### <a name="output---c-script-example"></a>Dane wyjściowe — przykładowy skrypt w języku C#

W poniższym przykładzie przedstawiono dane wyjściowe z usługi Service Bus powiązanie w *function.json* pliku i [funkcji skryptu C#](functions-reference-csharp.md) używającą powiązania. Funkcja używa wyzwalacza bazującego na czasomierzu do wysyłania komunikatu w kolejce co 15 s.

W tym miejscu jest powiązanie danych *function.json* pliku:

```json
{
    "bindings": [
        {
            "schedule": "0/15 * * * * *",
            "name": "myTimer",
            "runsOnStartup": true,
            "type": "timerTrigger",
            "direction": "in"
        },
        {
            "name": "outputSbQueue",
            "type": "serviceBus",
            "queueName": "testqueue",
            "connection": "MyServiceBusConnection",
            "direction": "out"
        }
    ],
    "disabled": false
}
```

Oto C# kodu skryptu, który tworzy pojedynczy komunikat:

```cs
public static void Run(TimerInfo myTimer, TraceWriter log, out string outputSbQueue)
{
    string message = $"Service Bus queue message created at: {DateTime.Now}";
    log.Info(message); 
    outputSbQueue = message;
}
```

W tym C# kodu skryptu, który tworzy wiele komunikatów:

```cs
public static void Run(TimerInfo myTimer, TraceWriter log, ICollector<string> outputSbQueue)
{
    string message = $"Service Bus queue messages created at: {DateTime.Now}";
    log.Info(message); 
    outputSbQueue.Add("1 " + message);
    outputSbQueue.Add("2 " + message);
}
```

### <a name="output---f-example"></a>Dane wyjściowe — przykład F #

W poniższym przykładzie przedstawiono dane wyjściowe z usługi Service Bus powiązanie w *function.json* pliku i [funkcji skryptu języka F #](functions-reference-fsharp.md) używającą powiązania. Funkcja używa wyzwalacza bazującego na czasomierzu do wysyłania komunikatu w kolejce co 15 s.

W tym miejscu jest powiązanie danych *function.json* pliku:

```json
{
    "bindings": [
        {
            "schedule": "0/15 * * * * *",
            "name": "myTimer",
            "runsOnStartup": true,
            "type": "timerTrigger",
            "direction": "in"
        },
        {
            "name": "outputSbQueue",
            "type": "serviceBus",
            "queueName": "testqueue",
            "connection": "MyServiceBusConnection",
            "direction": "out"
        }
    ],
    "disabled": false
}
```

Oto F # kodu skryptu, który tworzy pojedynczy komunikat:

```fsharp
let Run(myTimer: TimerInfo, log: TraceWriter, outputSbQueue: byref<string>) =
    let message = sprintf "Service Bus queue message created at: %s" (DateTime.Now.ToString())
    log.Info(message)
    outputSbQueue = message
```

### <a name="output---javascript-example"></a>Dane wyjściowe — przykład JavaScript

W poniższym przykładzie przedstawiono dane wyjściowe z usługi Service Bus powiązanie w *function.json* pliku i [funkcji JavaScript](functions-reference-node.md) używającą powiązania. Funkcja używa wyzwalacza bazującego na czasomierzu do wysyłania komunikatu w kolejce co 15 s.

W tym miejscu jest powiązanie danych *function.json* pliku:

```json
{
    "bindings": [
        {
            "schedule": "0/15 * * * * *",
            "name": "myTimer",
            "runsOnStartup": true,
            "type": "timerTrigger",
            "direction": "in"
        },
        {
            "name": "outputSbQueue",
            "type": "serviceBus",
            "queueName": "testqueue",
            "connection": "MyServiceBusConnection",
            "direction": "out"
        }
    ],
    "disabled": false
}
```

Oto kod skryptu JavaScript, który tworzy pojedynczy komunikat:

```javascript
module.exports = function (context, myTimer) {
    var message = 'Service Bus queue message created at ' + timeStamp;
    context.log(message);   
    context.bindings.outputSbQueueMsg = message;
    context.done();
};
```

Oto kod skryptu JavaScript, który tworzy wiele komunikatów:

```javascript
module.exports = function (context, myTimer) {
    var message = 'Service Bus queue message created at ' + timeStamp;
    context.log(message);   
    context.bindings.outputSbQueueMsg = [];
    context.bindings.outputSbQueueMsg.push("1 " + message);
    context.bindings.outputSbQueueMsg.push("2 " + message);
    context.done();
};
```

## <a name="output---attributes"></a>Dane wyjściowe — atrybuty

W [bibliotek klas C#](functions-dotnet-class-library.md), użyj [ServiceBusAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs), która jest zdefiniowana w pakiecie NuGet [Microsoft.Azure.WebJobs.ServiceBus](http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus).

Konstruktor atrybutu ma nazwę kolejki lub tematu i subskrypcji. Można również określić prawa dostępu do tego połączenia. Jak wybrać ustawienie prawa dostępu zostało wyjaśnione w dokumencie [wyjście - konfiguracji](#output---configuration) sekcji. Oto przykład pokazujący, atrybut zastosowany do wartość zwracana funkcji:

```csharp
[FunctionName("ServiceBusOutput")]
[return: ServiceBus("myqueue")]
public static string Run([HttpTrigger] dynamic input, TraceWriter log)
{
    ...
}
```

Można ustawić `Connection` właściwości w celu określenia konta usługi Service Bus do użycia, jak pokazano w poniższym przykładzie:

```csharp
[FunctionName("ServiceBusOutput")]
[return: ServiceBus("myqueue", Connection = "ServiceBusConnection")]
public static string Run([HttpTrigger] dynamic input, TraceWriter log)
{
    ...
}
```

Pełny przykład, zobacz [dane wyjściowe — przykład C#](#output---c-example).

Można użyć `ServiceBusAccount` atrybutu, aby określić konto usługi Service Bus do użycia na poziomie klasy, metody lub parametru.  Aby uzyskać więcej informacji, zobacz [wyzwalacza — atrybuty](#trigger---attributes).

## <a name="output---configuration"></a>OUTPUT — Konfiguracja

W poniższej tabeli opisano powiązania właściwości konfiguracyjne, które można ustawić w *function.json* pliku i `ServiceBus` atrybutu.

|Właściwość Function.JSON | Właściwość atrybutu |Opis|
|---------|---------|----------------------|
|**Typ** | Nie dotyczy | Musi być równa "magistrali usług". Ta właściwość ma wartość automatycznie, podczas tworzenia wyzwalacza w portalu Azure.|
|**Kierunek** | Nie dotyczy | Należy wybrać opcję "out". Ta właściwość ma wartość automatycznie, podczas tworzenia wyzwalacza w portalu Azure. |
|**Nazwa** | Nie dotyczy | Nazwa zmiennej, która reprezentuje kolejka lub temat w kodzie funkcji. Wartość "$return" odwołują się do wartości zwracane funkcji. | 
|**queueName**|**QueueName**|Nazwa kolejki.  Ustawiona tylko wtedy, gdy wysyłanie wiadomości w kolejce, nie dla tematu.
|**topicName**|**TopicName**|Nazwa tematu do monitorowania. Ustawiona tylko wtedy, gdy wysyłanie wiadomości tematu, nie dla kolejki.|
|**Nazwa subskrypcji**|**Nazwa subskrypcji**|Nazwa subskrypcji do monitorowania. Ustawiona tylko wtedy, gdy wysyłanie wiadomości tematu, nie dla kolejki.|
|**połączenia**|**Połączenia**|Nazwa ustawienia aplikacji, która zawiera parametry połączenia magistrali usługi do użycia dla tego powiązania. Jeśli nazwa ustawienia aplikacji rozpoczyna się od "AzureWebJobs", można określić tylko w pozostałej części nazwy. Na przykład jeśli ustawisz `connection` do "MyServiceBus" środowisko uruchomieniowe Functions szuka ustawienie aplikacji o nazwie "AzureWebJobsMyServiceBus." Jeśli opuścisz `connection` pusta, domyślny ciąg połączenia usługi Service Bus używa funkcji środowiska uruchomieniowego w ustawieniu aplikacji o nazwie "AzureWebJobsServiceBus".<br><br>Aby uzyskać ciąg połączenia, wykonaj kroki opisane w [uzyskać poświadczenia zarządzania](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials). Parametry połączenia muszą mieć dla przestrzeni nazw usługi Service Bus, nie są ograniczone do określonych kolejka lub temat.|
|**accessRights**|**Dostęp** |Prawa dostępu do ciągu połączenia. Dostępne wartości to "manage" i "nasłuchiwania". Wartość domyślna to "manage", która wskazuje, czy połączenie ma **Zarządzaj** uprawnienia. Jeśli używasz parametry połączenia, które nie ma **Zarządzaj** Ustaw uprawnienia, `accessRights` "nasłuchiwanie". W przeciwnym razie środowiska uruchomieniowego może się nie powieść próba wykonania tej operacji, które wymagają funkcji zarządzania prawami.|

[!INCLUDE [app settings to local.settings.json](../../includes/functions-app-settings-local.md)]

## <a name="output---usage"></a>Dane wyjściowe — użycie

W języku C# i skryptu C#, dostęp za pomocą parametru metody, takie jak kolejka lub temat `out string paramName`. W języku C# skryptu `paramName` jest wartością określoną w `name` właściwość *function.json*. Można użyć dowolnej z następujących parametrów:

* `out T paramName` - `T`mogą być dowolnego typu serializacji JSON. Jeśli wartość parametru jest równa null, gdy funkcja kończy, funkcje tworzy komunikat z obiektem null.
* `out string`— Jeśli wartość parametru ma wartość null, gdy funkcja kończy, funkcje nie tworzy komunikat.
* `out byte[]`— Jeśli wartość parametru ma wartość null, gdy funkcja kończy, funkcje nie tworzy komunikat.
* `out BrokeredMessage`— Jeśli wartość parametru ma wartość null, gdy funkcja kończy, funkcje nie tworzy komunikat.

W przypadku tworzenia wielu wiadomości w języku C# lub funkcji skryptu C#, można użyć `ICollector<T>` lub `IAsyncCollector<T>`. Komunikat jest tworzony podczas wywoływania `Add` metody.

W języku JavaScript, dostęp do kolejki lub temat przy użyciu `context.bindings.<name>`. `<name>`wartość jest określona w `name` właściwość *function.json*. Ciąg, tablica bajtów lub obiektu Javascript (deserializacji do postaci JSON) można przypisać do `context.binding.<name>`.

## <a name="next-steps"></a>Kolejne kroki

> [!div class="nextstepaction"]
> [Dowiedz się więcej o usługę Azure functions wyzwalaczy i powiązań](functions-triggers-bindings.md)
