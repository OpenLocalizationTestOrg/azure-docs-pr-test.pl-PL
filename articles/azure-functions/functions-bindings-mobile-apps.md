---
title: "powiązania funkcji Mobile Apps aaaAzure | Dokumentacja firmy Microsoft"
description: "Zrozumienie sposobu toouse Azure Mobile Apps powiązania usługi Azure Functions."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
keywords: "funkcje usługi Azure, funkcje, przetwarzania zdarzeń, dynamiczne obliczeń niekorzystającą architektury"
ms.assetid: faad1263-0fa5-41a9-964f-aecbc0be706a
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/31/2016
ms.author: glenga
ms.openlocfilehash: d3679a5d5c66705b32e422ec17e3a1e6d6ac063c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-mobile-apps-bindings"></a>Azure powiązania funkcji Mobile Apps
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

W tym artykule opisano sposób tooconfigure i kod [Azure Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) powiązania usługi Azure Functions. Azure Functions obsługuje wejściowa i wyjściowa powiązania dla aplikacji mobilnych.

Witaj Mobile Apps argument wejściowy i powiązania danych wyjściowych pozwalają [odczytywać i zapisywać tabele toodata](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations) w aplikacji mobilnej.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="input"></a>

## <a name="mobile-apps-input-binding"></a>Powiązania wejściowego Mobile Apps
Witaj powiązania wejściowego Mobile Apps ładuje rekord z punktu końcowego przenośnych tabeli i przekazuje ją do funkcji. W C# i F # funkcjach rekord toohello wszelkie zmiany wprowadzone są automatycznie wysyłane tabeli wstecz toohello gdy funkcja hello kończy się pomyślnie.

Witaj Mobile Apps wejściowych funkcja tooa używa powitania po obiekt JSON w hello `bindings` tablicy function.json:

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "mobileTable",
    "tableName": "<Name of your mobile app's data table>",
    "id" : "<Id of hello record tooretrieve - see below>",
    "connection": "<Name of app setting that has your mobile app's URL - see below>",
    "apiKey": "<Name of app setting that has your mobile app's API key - see below>",
    "direction": "in"
}
```

Należy uwzględnić następujące hello:

* `id`może być statyczna, ani może bazować na powitania wyzwalacz, który wywołuje funkcję hello. Na przykład, jeśli używasz [wyzwalacza kolejki]() dla funkcji, następnie `"id": "{queueTrigger}"` używa hello ciąg hello kolejki wiadomości jako hello tooretrieve identyfikator rekordu.
* `connection`powinien zawierać nazwę hello ustawienie aplikacji w aplikacji funkcji, który z kolei zawiera adres URL hello aplikacji mobilnej. Funkcja Hello używa tego adresu URL tooconstruct hello wymagane REST operacji względem aplikacji mobilnej. Możesz [utworzyć ustawienie aplikacji w aplikacji funkcji]() zawierający adres URL aplikacji mobilnej (który wygląda podobnie `http://<appname>.azurewebsites.net`), następnie określ nazwę ustawienia aplikacji hello hello w hello `connection` właściwości w Twojej powiązania wejściowego. 
* Należy toospecify `apiKey` Jeśli możesz [implementować klucz interfejsu API zaplecza aplikacji mobilnej Node.js](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), lub [implementować klucz interfejsu API zaplecza aplikacji mobilnej .NET](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key). toodo, możesz [utworzyć ustawienie aplikacji w aplikacji funkcji]() zawierający klucz hello interfejsu API, następnie dodać hello `apiKey` właściwości w Twojej powiązania wejściowego o nazwie hello ustawienia aplikacji hello. 
  
  > [!IMPORTANT]
  > Ten klucz interfejsu API nie może być udostępniany z klientami aplikacji mobilnej. Powinno to być rozproszone bezpiecznie tooservice po stronie klientów, takie jak usługi Azure Functions. 
  > 
  > [!NOTE]
  > Azure Functions przechowuje informacje dotyczące połączenia, a klucze interfejsu API zgodnie z ustawieniami aplikacji, dzięki czemu nie są sprawdzane w Twoim repozytorium kontroli źródła. To chroni poufne informacje.
  > 
  > 

<a name="inputusage"></a>

## <a name="input-usage"></a>Użycie wejściowych
W tej sekcji przedstawiono, jak toouse aplikacji mobilnej wprowadź powiązania w kodzie funkcji. 

W przypadku hello rekord z hello jest odnaleźć Identyfikatora tabeli i rejestrowanie jest przekazywany do hello o nazwie [JObject](http://www.newtonsoft.com/json/help/html/t_newtonsoft_json_linq_jobject.htm) parametr (lub w środowisku Node.js, jest przekazywany do hello `context.bindings.<name>` obiektu). Gdy nie ma rekordu hello, parametr hello jest `null`. 

W funkcji języka C# i F # wszystkie zmiany wprowadzone rekordu toohello danych wejściowych (parametr wejściowy) są wysyłane automatycznie wstecz toohello tabeli Mobile Apps gdy funkcja hello kończy się pomyślnie. W przypadku funkcji Node.js użyj `context.bindings.<name>` tooaccess hello rekordu wejściowego. Nie można zmodyfikować rekord w środowisku Node.js.

<a name="inputsample"></a>

## <a name="input-sample"></a>Przykładowe wejściowych
Załóżmy, że masz następujące function.json hello, który pobiera rekord aplikacji mobilnej tabeli o identyfikatorze hello kolejki wyzwalacza wiadomość hello:

```json
{
"bindings": [
    {
    "name": "myQueueItem",
    "queueName": "myqueue-items",
    "connection":"",
    "type": "queueTrigger",
    "direction": "in"
    },
    {
        "name": "record",
        "type": "mobileTable",
        "tableName": "MyTable",
        "id" : "{queueTrigger}",
        "connection": "My_MobileApp_Url",
        "apiKey": "My_MobileApp_Key",
        "direction": "in"
    }
],
"disabled": false
}
```

Zobacz przykład specyficzny dla języka hello, który korzysta z rekordu wejściowego hello z hello powiązania. Przykłady Hello C# i F # również zmodyfikować rekord hello `text` właściwości.

* [C#](#inputcsharp)
* [Node.js](#inputnodejs)

<a name="inputcsharp"></a>

### <a name="input-sample-in-c"></a>Przykładowe wejściowego w języku C# #

```cs
#r "Newtonsoft.Json"    
using Newtonsoft.Json.Linq;

public static void Run(string myQueueItem, JObject record)
{
    if (record != null)
    {
        record["Text"] = "This has changed.";
    }    
}
```

<!--
<a name="inputfsharp"></a>
### Input sample in F# ## 

```fsharp
#r "Newtonsoft.Json"    
open Newtonsoft.Json.Linq
let Run(myQueueItem: string, record: JObject) =
  inputDocument?text <- "This has changed."
```
-->

<a name="inputnodejs"></a>

### <a name="input-sample-in-nodejs"></a>Przykładowe wejściowego w środowisku Node.js

```javascript
module.exports = function (context, myQueueItem) {    
    context.log(context.bindings.record);
    context.done();
};
```

<a name="output"></a>

## <a name="mobile-apps-output-binding"></a>Aplikacje mobilne powiązania wyjściowego
Użyj hello Mobile Apps dane wyjściowe powiązania toowrite nowy punkt końcowy tabeli Mobile Apps tooa rekordów.  

Witaj Mobile Apps danych wyjściowych dla następującego obiektu JSON w hello hello używa funkcji `bindings` tablicy function.json:

```json
{
    "name": "<Name of output parameter in function signature>",
    "type": "mobileTable",
    "tableName": "<Name of your mobile app's data table>",
    "connection": "<Name of app setting that has your mobile app's URL - see below>",
    "apiKey": "<Name of app setting that has your mobile app's API key - see below>",
    "direction": "out"
}
```

Należy uwzględnić następujące hello:

* `connection`powinien zawierać nazwę hello ustawienie aplikacji w aplikacji funkcji, który z kolei zawiera adres URL hello aplikacji mobilnej. Funkcja Hello używa tego adresu URL tooconstruct hello wymagane REST operacji względem aplikacji mobilnej. Możesz [utworzyć ustawienie aplikacji w aplikacji funkcji]() zawierający adres URL aplikacji mobilnej (który wygląda podobnie `http://<appname>.azurewebsites.net`), następnie określ nazwę ustawienia aplikacji hello hello w hello `connection` właściwości w Twojej powiązania wejściowego. 
* Należy toospecify `apiKey` Jeśli możesz [implementować klucz interfejsu API zaplecza aplikacji mobilnej Node.js](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), lub [implementować klucz interfejsu API zaplecza aplikacji mobilnej .NET](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key). toodo, możesz [utworzyć ustawienie aplikacji w aplikacji funkcji]() zawierający klucz hello interfejsu API, następnie dodać hello `apiKey` właściwości w Twojej powiązania wejściowego o nazwie hello ustawienia aplikacji hello. 
  
  > [!IMPORTANT]
  > Ten klucz interfejsu API nie może być udostępniany z klientami aplikacji mobilnej. Powinno to być rozproszone bezpiecznie tooservice po stronie klientów, takie jak usługi Azure Functions. 
  > 
  > [!NOTE]
  > Azure Functions przechowuje informacje dotyczące połączenia, a klucze interfejsu API zgodnie z ustawieniami aplikacji, dzięki czemu nie są sprawdzane w Twoim repozytorium kontroli źródła. To chroni poufne informacje.
  > 
  > 

<a name="outputusage"></a>

## <a name="output-usage"></a>Użycie danych wyjściowych
W tej sekcji przedstawiono, jak toouse aplikacji mobilnej output powiązania w kodzie funkcji. 

W języku C# funkcji, należy użyć parametru wyjściowego o nazwie typu `out object` tooaccess hello output rekordu. W przypadku funkcji Node.js użyj `context.bindings.<name>` tooaccess hello output rekordu.

<a name="outputsample"></a>

## <a name="output-sample"></a>Przykładowe dane wyjściowe
Załóżmy, że masz powitania po function.json, definiujący wyzwalacz kolejki i wyjścia Mobile Apps:

```json
{
"bindings": [
    {
    "name": "myQueueItem",
    "queueName": "myqueue-items",
    "connection":"",
    "type": "queueTrigger",
    "direction": "in"
    },
    {
    "name": "record",
    "type": "mobileTable",
    "tableName": "MyTable",
    "connection": "My_MobileApp_Url",
    "apiKey": "My_MobileApp_Key",
    "direction": "out"
    }
],
"disabled": false
}
```

Zobacz przykład specyficzny dla języka hello, który tworzy rekord w punkt końcowy tabel Mobile Apps hello z zawartością hello hello kolejki wiadomości.

* [C#](#outcsharp)
* [Node.js](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a>Przykładowe dane wyjściowe w języku C# #

```cs
public static void Run(string myQueueItem, out object record)
{
    record = new {
        Text = $"I'm running in a C# function! {myQueueItem}"
    };
}
```

<!--
<a name="outfsharp"></a>
### Output sample in F# ## 
```fsharp

```
-->
<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a>Przykładowe dane wyjściowe w środowisku Node.js

```javascript
module.exports = function (context, myQueueItem) {

    context.bindings.record = {
        text : "I'm running in a Node function! Data: '" + myQueueItem + "'"
    }   

    context.done();
};
```

## <a name="next-steps"></a>Następne kroki
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

