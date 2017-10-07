---
title: "powiązanie funkcji Centrum powiadomień aaaAzure | Dokumentacja firmy Microsoft"
description: "Zrozumienie sposobu toouse Centrum powiadomień Azure powiązanie w funkcji platformy Azure."
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
ms.openlocfilehash: d192424a8ec701d02f8bcb4aa4c1d189b20537a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-notification-hub-output-binding"></a>Powiązanie danych wyjściowych Centrum powiadomień Azure funkcji
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

W tym artykule opisano sposób powiązania Centrum powiadomień Azure tooconfigure i kodu w funkcji platformy Azure. 

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

Funkcji można wysyłać powiadomienia wypychane za pomocą skonfigurowanego centrum powiadomień Azure przy użyciu kilku wierszy kodu. Jednak hello Centrum powiadomień Azure musi być skonfigurowany dla hello ma toouse platformy powiadomienia usługi (PNS). Aby uzyskać więcej informacji na temat konfigurowania Centrum powiadomień Azure tworzenie aplikacji klienckich, które rejestrują tooreceive powiadomień, zobacz [wprowadzenie do korzystania z usługi Notification Hubs](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) i kliknij przycisk docelowej platformy klienta na powitania Do góry.

powiadomienia Hello, możesz wysłać może być natywnych powiadomień lub szablonu powiadomienia. Natywnych powiadomień Docelowa platforma powiadomień określonych zgodnie z konfiguracją hello `platform` właściwości hello powiązania wyjściowego. Szablon powiadomienia mogą być używane tootarget wielu platform.   

## <a name="notification-hub-output-binding-properties"></a>Właściwości powiązania danych wyjściowych Centrum powiadomień
Plik function.json Hello zawiera hello następujące właściwości:

* `name`: Nazwa zmiennej używane w kodzie funkcja hello powiadomienie koncentratora.
* `type`: musi być ustawiona zbyt*"notificationHub"*.
* `tagExpression`: Wyrażeń tagów Zezwalaj toospecify można dostarczyć powiadomień o tooa zbiór urządzeń, które zostały zarejestrowane tooreceive powiadomień, które odpowiada wyrażeniu tag hello.  Aby uzyskać więcej informacji, zobacz [wyrażenia routingu i tagu](../notification-hubs/notification-hubs-tags-segment-push-message.md).
* `hubName`: Nazwa zasobu w Centrum powiadomień hello w hello portalu Azure.
* `connection`: Ten ciąg połączenia musi być **ustawienie aplikacji** toohello ustawić parametry połączenia *DefaultFullSharedAccessSignature* wartość dla Centrum powiadomień.
* `direction`: musi być ustawiona zbyt*"out"*. 
* `platform`: właściwość platformy hello wskazuje hello powiadomień platformy celów powiadomień. Musi mieć jedną z hello następujące wartości:
  * Domyślnie pominięcie właściwości platformy hello z danych wyjściowych hello powiązanie, szablon powiadomienia mogą być używane tootarget dowolnej platformie skonfigurowane na powitania Centrum powiadomień Azure. Aby uzyskać więcej informacji na ogólnie za pomocą szablonów Zobacz toosend cross platform powiadomienia z Centrum powiadomień Azure [szablony](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).
  * `apns`: Apple Push Notification Service. Aby uzyskać więcej informacji na temat konfigurowania Centrum powiadomień hello w przypadku usługi APNS odbieranie hello powiadomienia w aplikacji klienta, zobacz [tooiOS powiadomień wypychanych wysyłanie przy użyciu usługi Azure Notification Hubs](../notification-hubs/notification-hubs-ios-apple-push-notification-apns-get-started.md) 
  * `adm`: [Usługi Amazon Device Messaging](https://developer.amazon.com/device-messaging). Aby uzyskać więcej informacji na temat konfigurowania hello Centrum powiadomień dla ADM odbieranie powiadomień hello w aplikację dla urządzeń Kindle, zobacz [wprowadzenie do korzystania z usługi Notification Hubs dla aplikacji dla urządzeń Kindle](../notification-hubs/notification-hubs-kindle-amazon-adm-push-notification.md) 
  * `gcm`: [Usługi Google Cloud Messaging](https://developers.google.com/cloud-messaging/). Firebase Cloud Messaging, która jest nowa wersja usługi GCM hello, jest również obsługiwany. Aby uzyskać więcej informacji na temat konfigurowania hello Centrum powiadomień dla usługi GCM/FCM odbieranie powiadomień hello w aplikację kliencką dla systemu Android, zobacz [tooAndroid powiadomień wypychanych wysyłanie przy użyciu usługi Azure Notification Hubs](../notification-hubs/notification-hubs-android-push-notification-google-fcm-get-started.md)
  * `wns`: [Usług powiadomień Wns](https://msdn.microsoft.com/en-us/windows/uwp/controls-and-patterns/tiles-and-notifications-windows-push-notification-services--wns--overview) przeznaczonych dla platformy systemu Windows. Windows Phone 8.1 lub nowszy jest również obsługiwana przez usługi WNS. Aby uzyskać więcej informacji na temat konfigurowania hello Centrum powiadomień w przypadku usługi WNS odbieranie hello powiadomienia w aplikacji Windows platformy Uniwersalnej, zobacz [wprowadzenie Notification Hubs dla uniwersalnych aplikacji systemu Windows platformy](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)
  * `mpns`: [Usługi powiadomień wypychanych firmy Microsoft](https://msdn.microsoft.com/en-us/library/windows/apps/ff402558.aspx). Ta platforma obsługuje starszych platform Windows Phone i Windows Phone 8. Aby uzyskać więcej informacji na temat konfigurowania hello Centrum powiadomień dla usługi MPNS odbieranie hello powiadomienia w aplikacji Windows Phone, zobacz [wysyłanie powiadomień wypychanych przy użyciu usługi Azure Notification Hubs na Windows Phone](../notification-hubs/notification-hubs-windows-mobile-push-notifications-mpns.md)

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
powiązania wyjściowego toouse Centrum powiadomień, należy skonfigurować hello parametry połączenia dla koncentratora hello. Można to zrobić na powitania *integracji* kartę, wybierając Centrum powiadomień i tworzenia nowego. 

Można też ręcznie dodać parametry połączenia dla istniejącego elementu hub przez dodanie ciągu połączenia dla hello *DefaultFullSharedAccessSignature* tooyour Centrum powiadomień. Ten ciąg połączenia zapewnia dostęp funkcja komunikatów powiadomień toosend uprawnienia. Witaj *DefaultFullSharedAccessSignature* można uzyskać wartość ciągu połączenia z hello **kluczy** przycisku na powitania głównego bloku zasobu Centrum powiadomień w hello portalu Azure. toomanually Dodaj parametry połączenia Centrum, użyj hello następujące kroki: 

1. Na powitania **aplikacji funkcji** bloku hello portalu Azure, kliknij przycisk **ustawień aplikacji funkcji > Przejdź do ustawień usługi tooApp**.
2. W hello **ustawienia** bloku, kliknij przycisk **ustawienia aplikacji**.
3. Przewiń w dół toohello **ustawień aplikacji** sekcji, a następnie dodanie wpisu o nazwie *DefaultFullSharedAccessSignature* wartość dla Centrum powiadomień.
4. Odwoływać się do aplikacji ustawienie nazwy ciągu w hello powiązania danych wyjściowych. Podobnie za**MyHubConnectionString** używane w powyższym przykładzie hello.

## <a name="apns-native-notifications-with-c-queue-triggers"></a>Natywnego powiadomienia usługi APNS z Wyzwalacze kolejkowania C#
W tym przykładzie pokazano, jak toouse typy zdefiniowane w hello [Biblioteka programu Microsoft Azure Notification Hubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend natywnego powiadomienia usługi APNS. 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example hello queue item is a new user toobe processed in hello form of a JSON string with 
    // a "name" value.
    //
    // hello JSON format for a native APNS notification is ...
    // { "aps": { "alert": "notification message" }}  

    log.Info($"Sending APNS notification of a new user");    
    dynamic user = JsonConvert.DeserializeObject(myQueueItem);    
    string apnsNotificationPayload = "{\"aps\": {\"alert\": \"A new user wants toobe added (" + 
                                        user.name + ")\" }}";
    log.Info($"{apnsNotificationPayload}");
    await notification.AddAsync(new AppleNotification(apnsNotificationPayload));        
}
```

## <a name="gcm-native-notifications-with-c-queue-triggers"></a>Wyzwalacze kolejki natywnego powiadomienia GCM w języku C#
W tym przykładzie pokazano, jak toouse typy zdefiniowane w hello [Biblioteka programu Microsoft Azure Notification Hubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend natywnych powiadomień usługi GCM. 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example hello queue item is a new user toobe processed in hello form of a JSON string with 
    // a "name" value.
    //
    // hello JSON format for a native GCM notification is ...
    // { "data": { "message": "notification message" }}  

    log.Info($"Sending GCM notification of a new user");    
    dynamic user = JsonConvert.DeserializeObject(myQueueItem);    
    string gcmNotificationPayload = "{\"data\": {\"message\": \"A new user wants toobe added (" + 
                                        user.name + ")\" }}";
    log.Info($"{gcmNotificationPayload}");
    await notification.AddAsync(new GcmNotification(gcmNotificationPayload));        
}
```

## <a name="wns-native-notifications-with-c-queue-triggers"></a>Natywnych powiadomień WNS przy użyciu Wyzwalacze kolejkowania C#
W tym przykładzie pokazano, jak toouse typy zdefiniowane w hello [Biblioteka programu Microsoft Azure Notification Hubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend WNS natywnego wyskakujących powiadomień. 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example hello queue item is a new user toobe processed in hello form of a JSON string with 
    // a "name" value.
    //
    // hello XML format for a native WNS toast notification is ...
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
                                            "A new user wants toobe added (" + user.name + ")" + 
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
W tym przykładzie wysyła powiadomienie [rejestracji szablonu](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) zawierający `message` symbol zastępczy w szablonie hello.

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
Jeśli używasz kodu asynchroniczne parametry wyjściowe nie są dozwolone. W takim przypadku użyj `IAsyncCollector` tooreturn szablonu powiadomienia. Hello następujący kod jest przykładem asynchroniczne hello kodu powyżej. 

```cs
using System;
using System.Threading.Tasks;
using System.Collections.Generic;

public static async Task Run(string myQueueItem, IAsyncCollector<IDictionary<string,string>> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    log.Info($"Sending Template Notification tooNotification Hub");
    await notification.AddAsync(GetTemplateProperties(myQueueItem));    
}

private static IDictionary<string, string> GetTemplateProperties(string message)
{
    Dictionary<string, string> templateProperties = new Dictionary<string, string>();
    templateProperties["user"] = "A new user wants toobe added : " + message;
    return templateProperties;
}
```

## <a name="template-example-using-json"></a>Przykład szablonu przy użyciu
W tym przykładzie wysyła powiadomienie [rejestracji szablonu](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) zawierający `message` symbol zastępczy w szablonie hello przy użyciu prawidłowego ciągu JSON.

```cs
using System;

public static void Run(string myQueueItem,  out string notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    notification = "{\"message\":\"Hello from C#. Processed a queue item!\"}";
}
```

## <a name="template-example-using-notification-hubs-library-types"></a>Przykład szablonu przy użyciu usługi Notification Hubs biblioteki typów
W tym przykładzie pokazano, jak toouse typy zdefiniowane w hello [Biblioteka programu Microsoft Azure Notification Hubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/). 

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

