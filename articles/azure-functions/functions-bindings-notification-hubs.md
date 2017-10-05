---
title: "Powiązanie funkcji Centrum powiadomień Azure | Dokumentacja firmy Microsoft"
description: "Zrozumienie, jak używać Centrum powiadomień Azure powiązania w usługi Azure Functions."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
keywords: "funkcje usługi Azure, funkcje, przetwarzania zdarzeń, dynamiczne obliczeń niekorzystającą architektury"
ms.assetid: 0ff0c949-20bf-430b-8dd5-d72b7b6ee6f7
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/27/2016
ms.author: glenga
ms.openlocfilehash: fa3d37b963c1bb6b58127b9180cd657d7b1dabcc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-notification-hub-output-binding"></a>Powiązanie danych wyjściowych Centrum powiadomień Azure funkcji
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

W tym artykule opisano sposób konfigurowania i Zakoduj powiązania Centrum powiadomień Azure w funkcji platformy Azure. 

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

Funkcji można wysyłać powiadomienia wypychane za pomocą skonfigurowanego centrum powiadomień Azure przy użyciu kilku wierszy kodu. Jednak Centrum powiadomień Azure musi być skonfigurowana dla platformy powiadomienia usługi (PNS) ma być używany. Aby uzyskać więcej informacji na temat konfigurowania Centrum powiadomień Azure tworzenie aplikacji klienckich, które Zarejestruj, aby otrzymywać powiadomienia, zobacz [wprowadzenie do korzystania z usługi Notification Hubs](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) i kliknij przycisk docelowej platformy klienta u góry .

Możesz wysłać powiadomienia mogą być natywnych powiadomień lub szablonu powiadomienia. Natywnych powiadomień Docelowa platforma powiadomień określonych zgodnie z konfiguracją `platform` właściwości powiązania danych wyjściowych. Powiadomienie o szablonu może służyć do wielu platform docelowych.   

## <a name="notification-hub-output-binding-properties"></a>Właściwości powiązania danych wyjściowych Centrum powiadomień
Plik function.json zawiera następujące właściwości:

* `name`: Nazwa zmiennej używane w kodzie funkcja komunikat Centrum powiadomień.
* `type`: musi być ustawiona na *"notificationHub"*.
* `tagExpression`: Wyrażeń tagów umożliwiają określenie, czy do zestawu urządzeń, które zostały zarejestrowane, aby otrzymywać powiadomienia, które odpowiada wyrażeniu tagu można dostarczyć powiadomień.  Aby uzyskać więcej informacji, zobacz [wyrażenia routingu i tagu](../notification-hubs/notification-hubs-tags-segment-push-message.md).
* `hubName`: Nazwa zasobu Centrum powiadomień, w portalu Azure.
* `connection`: Ten ciąg połączenia musi być **ustawienie aplikacji** ustawić parametry połączenia *DefaultFullSharedAccessSignature* wartość dla Centrum powiadomień.
* `direction`: musi być ustawiona na *"out"*. 
* `platform`: Właściwość platformy wskazuje powiadomień platformy celów powiadomień. Musi mieć jedną z następujących wartości:
  * Domyślnie w przypadku pominięcia właściwości platformy z wiązania danych wyjściowych szablonu powiadomienia można współpracować z dowolną platformą skonfigurowany w Centrum powiadomień Azure. Aby uzyskać więcej informacji na korzystanie z szablonów ogólnie do wysyłania wielu powiadomień platformy przy użyciu Centrum powiadomień Azure, zobacz [szablony](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).
  * `apns`: Apple Push Notification Service. Aby uzyskać więcej informacji na temat konfigurowania Centrum powiadomień dla APNS odbieranie powiadomień w aplikacji klienta, zobacz [wysyłanie powiadomień wypychanych do systemu iOS przy użyciu usługi Azure Notification Hubs](../notification-hubs/notification-hubs-ios-apple-push-notification-apns-get-started.md) 
  * `adm`: [Usługi Amazon Device Messaging](https://developer.amazon.com/device-messaging). Aby uzyskać więcej informacji na temat konfigurowania Centrum powiadomień dla ADM odbieranie powiadomień w aplikację dla urządzeń Kindle, zobacz [wprowadzenie do korzystania z usługi Notification Hubs dla aplikacji dla urządzeń Kindle](../notification-hubs/notification-hubs-kindle-amazon-adm-push-notification.md) 
  * `gcm`: [Usługi Google Cloud Messaging](https://developers.google.com/cloud-messaging/). Firebase Cloud Messaging, która jest nowa wersja usługi GCM, jest również obsługiwany. Aby uzyskać więcej informacji na temat konfigurowania Centrum powiadomień dla usługi GCM/FCM odbieranie powiadomień w aplikację kliencką dla systemu Android, zobacz [wysyłanie powiadomień wypychanych w systemie Android przy użyciu usługi Azure Notification Hubs](../notification-hubs/notification-hubs-android-push-notification-google-fcm-get-started.md)
  * `wns`: [Usług powiadomień Wns](https://msdn.microsoft.com/en-us/windows/uwp/controls-and-patterns/tiles-and-notifications-windows-push-notification-services--wns--overview) przeznaczonych dla platformy systemu Windows. Windows Phone 8.1 lub nowszy jest również obsługiwana przez usługi WNS. Aby uzyskać więcej informacji na temat konfigurowania Centrum powiadomień w przypadku usługi WNS odbieranie powiadomień w aplikacji Windows platformy Uniwersalnej, zobacz [wprowadzenie Notification Hubs dla uniwersalnych aplikacji systemu Windows platformy](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)
  * `mpns`: [Usługi powiadomień wypychanych firmy Microsoft](https://msdn.microsoft.com/en-us/library/windows/apps/ff402558.aspx). Ta platforma obsługuje starszych platform Windows Phone i Windows Phone 8. Aby uzyskać więcej informacji na temat konfigurowania Centrum powiadomień dla usługi MPNS odbieranie powiadomień w aplikacji Windows Phone, zobacz [wysyłanie powiadomień wypychanych przy użyciu usługi Azure Notification Hubs na Windows Phone](../notification-hubs/notification-hubs-windows-mobile-push-notifications-mpns.md)

Przykład function.json:

```json
{
  "bindings": [
    {
      "name": "notification",
      "type": "notificationHub",
      "tagExpression": "",
      "hubName": "my-notification-hub",
      "connection": "MyHubConnectionString",
      "platform": "gcm",
      "direction": "out"
    }
  ],
  "disabled": false
}
```

## <a name="notification-hub-connection-string-setup"></a>Ustawienia połączenia Centrum powiadomień
Aby użyć powiązania danych wyjściowych Centrum powiadomień, należy skonfigurować parametry połączenia dla koncentratora. Można to zrobić na *integracji* kartę, wybierając Centrum powiadomień i tworzenia nowego. 

Można też ręcznie dodać parametry połączenia dla istniejącego elementu hub przez dodanie ciągu połączenia dla *DefaultFullSharedAccessSignature* do Centrum powiadomień. Te parametry połączenia zawiera uprawnień dostępu użytkownika funkcji wysyłać powiadomienia. *DefaultFullSharedAccessSignature* można uzyskać wartość ciągu połączenia z **klucze** przycisk w głównym bloku zasobu Centrum powiadomień w portalu Azure. Aby ręcznie dodać parametry połączenia Centrum, wykonaj następujące kroki: 

1. Na **aplikacji funkcji** bloku portalu Azure kliknij **ustawień aplikacji funkcji > Przejdź do ustawień usługi aplikacji**.
2. W **ustawienia** bloku, kliknij przycisk **ustawienia aplikacji**.
3. Przewiń w dół do **ustawień aplikacji** sekcji, a następnie dodanie wpisu o nazwie *DefaultFullSharedAccessSignature* wartość dla Centrum powiadomień.
4. Odwołanie nazwę aplikacji ustawienie ciągu powiązania danych wyjściowych. Podobnie jak **MyHubConnectionString** używane w powyższym przykładzie.

## <a name="apns-native-notifications-with-c-queue-triggers"></a>Natywnego powiadomienia usługi APNS z Wyzwalacze kolejkowania C#
W tym przykładzie przedstawiono użycie typów zdefiniowanych w [Biblioteka programu Microsoft Azure Notification Hubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) do wysyłania natywnych powiadomień usługi APNS. 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example the queue item is a new user to be processed in the form of a JSON string with 
    // a "name" value.
    //
    // The JSON format for a native APNS notification is ...
    // { "aps": { "alert": "notification message" }}  

    log.Info($"Sending APNS notification of a new user");    
    dynamic user = JsonConvert.DeserializeObject(myQueueItem);    
    string apnsNotificationPayload = "{\"aps\": {\"alert\": \"A new user wants to be added (" + 
                                        user.name + ")\" }}";
    log.Info($"{apnsNotificationPayload}");
    await notification.AddAsync(new AppleNotification(apnsNotificationPayload));        
}
```

## <a name="gcm-native-notifications-with-c-queue-triggers"></a>Wyzwalacze kolejki natywnego powiadomienia GCM w języku C#
W tym przykładzie przedstawiono użycie typów zdefiniowanych w [Biblioteka programu Microsoft Azure Notification Hubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) do wysyłania natywnych powiadomień usługi GCM. 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example the queue item is a new user to be processed in the form of a JSON string with 
    // a "name" value.
    //
    // The JSON format for a native GCM notification is ...
    // { "data": { "message": "notification message" }}  

    log.Info($"Sending GCM notification of a new user");    
    dynamic user = JsonConvert.DeserializeObject(myQueueItem);    
    string gcmNotificationPayload = "{\"data\": {\"message\": \"A new user wants to be added (" + 
                                        user.name + ")\" }}";
    log.Info($"{gcmNotificationPayload}");
    await notification.AddAsync(new GcmNotification(gcmNotificationPayload));        
}
```

## <a name="wns-native-notifications-with-c-queue-triggers"></a>Natywnych powiadomień WNS przy użyciu Wyzwalacze kolejkowania C#
W tym przykładzie przedstawiono użycie typów zdefiniowanych w [Biblioteka programu Microsoft Azure Notification Hubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) do wysyłania wyskakujących powiadomień WNS macierzystego. 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example the queue item is a new user to be processed in the form of a JSON string with 
    // a "name" value.
    //
    // The XML format for a native WNS toast notification is ...
    // <?xml version="1.0" encoding="utf-8"?>
    // <toast>
    //      <visual>
    //     <binding template="ToastText01">
    //       <text id="1">notification message</text>
    //     </binding>
    //   </visual>
    // </toast>

    log.Info($"Sending WNS toast notification of a new user");    
    dynamic user = JsonConvert.DeserializeObject(myQueueItem);    
    string wnsNotificationPayload = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                                    "<toast><visual><binding template=\"ToastText01\">" +
                                        "<text id=\"1\">" + 
                                            "A new user wants to be added (" + user.name + ")" + 
                                        "</text>" +
                                    "</binding></visual></toast>";

    log.Info($"{wnsNotificationPayload}");
    await notification.AddAsync(new WindowsNotification(wnsNotificationPayload));        
}
```

## <a name="template-example-for-nodejs-timer-triggers"></a>Przykład szablonu wyzwalaczy czasomierza Node.js
W tym przykładzie wysyła powiadomienie [rejestracji szablonu](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) zawierający `location` i `message`.

```javascript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();

    if(myTimer.isPastDue)
    {
        context.log('Node.js is running late!');
    }
    context.log('Node.js timer trigger function ran!', timeStamp);  
    context.bindings.notification = {
        location: "Redmond",
        message: "Hello from Node!"
    };
    context.done();
};
```

## <a name="template-example-for-f-timer-triggers"></a>Przykład szablonu wyzwalaczy czasomierza F #
W tym przykładzie wysyła powiadomienie [rejestracji szablonu](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) zawierający `location` i `message`.

```fsharp
let Run(myTimer: TimerInfo, notification: byref<IDictionary<string, string>>) =
    notification = dict [("location", "Redmond"); ("message", "Hello from F#!")]
```

## <a name="template-example-using-an-out-parameter"></a>Przykład szablonu przy użyciu parametru wyjściowego
W tym przykładzie wysyła powiadomienie [rejestracji szablonu](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) zawierający `message` symbol zastępczy w szablonie.

```cs
using System;
using System.Threading.Tasks;
using System.Collections.Generic;

public static void Run(string myQueueItem,  out IDictionary<string, string> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    notification = GetTemplateProperties(myQueueItem);
}

private static IDictionary<string, string> GetTemplateProperties(string message)
{
    Dictionary<string, string> templateProperties = new Dictionary<string, string>();
    templateProperties["message"] = message;
    return templateProperties;
}
```

## <a name="template-example-with-asynchronous-function"></a>Przykład: szablon funkcji asynchronicznych
Jeśli używasz kodu asynchroniczne parametry wyjściowe nie są dozwolone. W takim przypadku użyj `IAsyncCollector` do zwrócenia szablonu powiadomienia. Następujący kod jest przykładem asynchroniczne kodu powyżej. 

```cs
using System;
using System.Threading.Tasks;
using System.Collections.Generic;

public static async Task Run(string myQueueItem, IAsyncCollector<IDictionary<string,string>> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    log.Info($"Sending Template Notification to Notification Hub");
    await notification.AddAsync(GetTemplateProperties(myQueueItem));    
}

private static IDictionary<string, string> GetTemplateProperties(string message)
{
    Dictionary<string, string> templateProperties = new Dictionary<string, string>();
    templateProperties["user"] = "A new user wants to be added : " + message;
    return templateProperties;
}
```

## <a name="template-example-using-json"></a>Przykład szablonu przy użyciu
W tym przykładzie wysyła powiadomienie [rejestracji szablonu](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) zawierający `message` symbol zastępczy w szablonie przy użyciu prawidłowego ciągu JSON.

```cs
using System;

public static void Run(string myQueueItem,  out string notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    notification = "{\"message\":\"Hello from C#. Processed a queue item!\"}";
}
```

## <a name="template-example-using-notification-hubs-library-types"></a>Przykład szablonu przy użyciu usługi Notification Hubs biblioteki typów
W tym przykładzie przedstawiono użycie typów zdefiniowanych w [Biblioteka programu Microsoft Azure Notification Hubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/). 

```cs
#r "Microsoft.Azure.NotificationHubs"

using System;
using System.Threading.Tasks;
using Microsoft.Azure.NotificationHubs;

public static void Run(string myQueueItem,  out Notification notification, TraceWriter log)
{
   log.Info($"C# Queue trigger function processed: {myQueueItem}");
   notification = GetTemplateNotification(myQueueItem);
}

private static TemplateNotification GetTemplateNotification(string message)
{
    Dictionary<string, string> templateProperties = new Dictionary<string, string>();
    templateProperties["message"] = message;
    return new TemplateNotification(templateProperties);
}
```

## <a name="next-steps"></a>Następne kroki
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

