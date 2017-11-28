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
# <a name="azure-functions-notification-hub-output-binding"></a><span data-ttu-id="dd799-104">Powiązanie danych wyjściowych Centrum powiadomień Azure funkcji</span><span class="sxs-lookup"><span data-stu-id="dd799-104">Azure Functions Notification Hub output binding</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="dd799-105">W tym artykule opisano sposób powiązania Centrum powiadomień Azure tooconfigure i kodu w funkcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="dd799-105">This article explains how tooconfigure and code Azure Notification Hub bindings in Azure Functions.</span></span> 

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="dd799-106">Funkcji można wysyłać powiadomienia wypychane za pomocą skonfigurowanego centrum powiadomień Azure przy użyciu kilku wierszy kodu.</span><span class="sxs-lookup"><span data-stu-id="dd799-106">Your functions can send push notifications using a configured Azure Notification Hub with a few lines of code.</span></span> <span data-ttu-id="dd799-107">Jednak hello Centrum powiadomień Azure musi być skonfigurowany dla hello ma toouse platformy powiadomienia usługi (PNS).</span><span class="sxs-lookup"><span data-stu-id="dd799-107">However, hello Azure Notification Hub must be configured for hello Platform Notifications Services (PNS) you want toouse.</span></span> <span data-ttu-id="dd799-108">Aby uzyskać więcej informacji na temat konfigurowania Centrum powiadomień Azure tworzenie aplikacji klienckich, które rejestrują tooreceive powiadomień, zobacz [wprowadzenie do korzystania z usługi Notification Hubs](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) i kliknij przycisk docelowej platformy klienta na powitania Do góry.</span><span class="sxs-lookup"><span data-stu-id="dd799-108">For more information on configuring an Azure Notification Hub and developing a client applications that register tooreceive notifications, see [Getting started with Notification Hubs](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) and click your target client platform at hello top.</span></span>

<span data-ttu-id="dd799-109">powiadomienia Hello, możesz wysłać może być natywnych powiadomień lub szablonu powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="dd799-109">hello notifications you send can be native notifications or template notifications.</span></span> <span data-ttu-id="dd799-110">Natywnych powiadomień Docelowa platforma powiadomień określonych zgodnie z konfiguracją hello `platform` właściwości hello powiązania wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="dd799-110">Native notifications target a specific notification platform as configured in hello `platform` property of hello output binding.</span></span> <span data-ttu-id="dd799-111">Szablon powiadomienia mogą być używane tootarget wielu platform.</span><span class="sxs-lookup"><span data-stu-id="dd799-111">A template notification can be used tootarget multiple platforms.</span></span>   

## <a name="notification-hub-output-binding-properties"></a><span data-ttu-id="dd799-112">Właściwości powiązania danych wyjściowych Centrum powiadomień</span><span class="sxs-lookup"><span data-stu-id="dd799-112">Notification hub output binding properties</span></span>
<span data-ttu-id="dd799-113">Plik function.json Hello zawiera hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="dd799-113">hello function.json file provides hello following properties:</span></span>

* <span data-ttu-id="dd799-114">`name`: Nazwa zmiennej używane w kodzie funkcja hello powiadomienie koncentratora.</span><span class="sxs-lookup"><span data-stu-id="dd799-114">`name` : Variable name used in function code for hello notification hub message.</span></span>
* <span data-ttu-id="dd799-115">`type`: musi być ustawiona zbyt*"notificationHub"*.</span><span class="sxs-lookup"><span data-stu-id="dd799-115">`type` : must be set too*"notificationHub"*.</span></span>
* <span data-ttu-id="dd799-116">`tagExpression`: Wyrażeń tagów Zezwalaj toospecify można dostarczyć powiadomień o tooa zbiór urządzeń, które zostały zarejestrowane tooreceive powiadomień, które odpowiada wyrażeniu tag hello.</span><span class="sxs-lookup"><span data-stu-id="dd799-116">`tagExpression` : Tag expressions allow you toospecify that notifications be delivered tooa set of devices who have registered tooreceive notifications that match hello tag expression.</span></span>  <span data-ttu-id="dd799-117">Aby uzyskać więcej informacji, zobacz [wyrażenia routingu i tagu](../notification-hubs/notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="dd799-117">For more information, see [Routing and tag expressions](../notification-hubs/notification-hubs-tags-segment-push-message.md).</span></span>
* <span data-ttu-id="dd799-118">`hubName`: Nazwa zasobu w Centrum powiadomień hello w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="dd799-118">`hubName` : Name of hello notification hub resource in hello Azure portal.</span></span>
* <span data-ttu-id="dd799-119">`connection`: Ten ciąg połączenia musi być **ustawienie aplikacji** toohello ustawić parametry połączenia *DefaultFullSharedAccessSignature* wartość dla Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="dd799-119">`connection` : This connection string must be an **Application Setting** connection string set toohello *DefaultFullSharedAccessSignature* value for your notification hub.</span></span>
* <span data-ttu-id="dd799-120">`direction`: musi być ustawiona zbyt*"out"*.</span><span class="sxs-lookup"><span data-stu-id="dd799-120">`direction` : must be set too*"out"*.</span></span> 
* <span data-ttu-id="dd799-121">`platform`: właściwość platformy hello wskazuje hello powiadomień platformy celów powiadomień.</span><span class="sxs-lookup"><span data-stu-id="dd799-121">`platform` : hello platform property indicates hello notification platform your notification targets.</span></span> <span data-ttu-id="dd799-122">Musi mieć jedną z hello następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="dd799-122">Must be one of hello following values:</span></span>
  * <span data-ttu-id="dd799-123">Domyślnie pominięcie właściwości platformy hello z danych wyjściowych hello powiązanie, szablon powiadomienia mogą być używane tootarget dowolnej platformie skonfigurowane na powitania Centrum powiadomień Azure.</span><span class="sxs-lookup"><span data-stu-id="dd799-123">By default, if hello platform property is omitted from hello output binding, template notifications can be used tootarget any platform configured on hello Azure Notification Hub.</span></span> <span data-ttu-id="dd799-124">Aby uzyskać więcej informacji na ogólnie za pomocą szablonów Zobacz toosend cross platform powiadomienia z Centrum powiadomień Azure [szablony](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="dd799-124">For more information on using templates in general toosend cross platform notifications with an Azure Notification Hub, see [Templates](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span></span>
  * <span data-ttu-id="dd799-125">`apns`: Apple Push Notification Service.</span><span class="sxs-lookup"><span data-stu-id="dd799-125">`apns` : Apple Push Notification Service.</span></span> <span data-ttu-id="dd799-126">Aby uzyskać więcej informacji na temat konfigurowania Centrum powiadomień hello w przypadku usługi APNS odbieranie hello powiadomienia w aplikacji klienta, zobacz [tooiOS powiadomień wypychanych wysyłanie przy użyciu usługi Azure Notification Hubs](../notification-hubs/notification-hubs-ios-apple-push-notification-apns-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="dd799-126">For more information on configuring hello notification hub for APNS and receiving hello notification in a client app, see [Sending push notifications tooiOS with Azure Notification Hubs](../notification-hubs/notification-hubs-ios-apple-push-notification-apns-get-started.md)</span></span> 
  * <span data-ttu-id="dd799-127">`adm`: [Usługi Amazon Device Messaging](https://developer.amazon.com/device-messaging).</span><span class="sxs-lookup"><span data-stu-id="dd799-127">`adm` : [Amazon Device Messaging](https://developer.amazon.com/device-messaging).</span></span> <span data-ttu-id="dd799-128">Aby uzyskać więcej informacji na temat konfigurowania hello Centrum powiadomień dla ADM odbieranie powiadomień hello w aplikację dla urządzeń Kindle, zobacz [wprowadzenie do korzystania z usługi Notification Hubs dla aplikacji dla urządzeń Kindle](../notification-hubs/notification-hubs-kindle-amazon-adm-push-notification.md)</span><span class="sxs-lookup"><span data-stu-id="dd799-128">For more information on configuring hello notification hub for ADM and receiving hello notification in a Kindle app, see [Getting Started with Notification Hubs for Kindle apps](../notification-hubs/notification-hubs-kindle-amazon-adm-push-notification.md)</span></span> 
  * <span data-ttu-id="dd799-129">`gcm`: [Usługi Google Cloud Messaging](https://developers.google.com/cloud-messaging/).</span><span class="sxs-lookup"><span data-stu-id="dd799-129">`gcm` : [Google Cloud Messaging](https://developers.google.com/cloud-messaging/).</span></span> <span data-ttu-id="dd799-130">Firebase Cloud Messaging, która jest nowa wersja usługi GCM hello, jest również obsługiwany.</span><span class="sxs-lookup"><span data-stu-id="dd799-130">Firebase Cloud Messaging, which is hello new version of GCM, is also supported.</span></span> <span data-ttu-id="dd799-131">Aby uzyskać więcej informacji na temat konfigurowania hello Centrum powiadomień dla usługi GCM/FCM odbieranie powiadomień hello w aplikację kliencką dla systemu Android, zobacz [tooAndroid powiadomień wypychanych wysyłanie przy użyciu usługi Azure Notification Hubs](../notification-hubs/notification-hubs-android-push-notification-google-fcm-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="dd799-131">For more information on configuring hello notification hub for GCM/FCM and receiving hello notification in an Android client app, see [Sending push notifications tooAndroid with Azure Notification Hubs](../notification-hubs/notification-hubs-android-push-notification-google-fcm-get-started.md)</span></span>
  * <span data-ttu-id="dd799-132">`wns`: [Usług powiadomień Wns](https://msdn.microsoft.com/en-us/windows/uwp/controls-and-patterns/tiles-and-notifications-windows-push-notification-services--wns--overview) przeznaczonych dla platformy systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="dd799-132">`wns` : [Windows Push Notification Services](https://msdn.microsoft.com/en-us/windows/uwp/controls-and-patterns/tiles-and-notifications-windows-push-notification-services--wns--overview) targeting Windows platforms.</span></span> <span data-ttu-id="dd799-133">Windows Phone 8.1 lub nowszy jest również obsługiwana przez usługi WNS.</span><span class="sxs-lookup"><span data-stu-id="dd799-133">Windows Phone 8.1 and later is also supported by WNS.</span></span> <span data-ttu-id="dd799-134">Aby uzyskać więcej informacji na temat konfigurowania hello Centrum powiadomień w przypadku usługi WNS odbieranie hello powiadomienia w aplikacji Windows platformy Uniwersalnej, zobacz [wprowadzenie Notification Hubs dla uniwersalnych aplikacji systemu Windows platformy](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)</span><span class="sxs-lookup"><span data-stu-id="dd799-134">For more information on configuring hello notification hub for WNS and receiving hello notification in a Universal Windows Platform (UWP) app, see [Getting started with Notification Hubs for Windows Universal Platform Apps](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)</span></span>
  * <span data-ttu-id="dd799-135">`mpns`: [Usługi powiadomień wypychanych firmy Microsoft](https://msdn.microsoft.com/en-us/library/windows/apps/ff402558.aspx).</span><span class="sxs-lookup"><span data-stu-id="dd799-135">`mpns` : [Microsoft Push Notification Service](https://msdn.microsoft.com/en-us/library/windows/apps/ff402558.aspx).</span></span> <span data-ttu-id="dd799-136">Ta platforma obsługuje starszych platform Windows Phone i Windows Phone 8.</span><span class="sxs-lookup"><span data-stu-id="dd799-136">This platform supports Windows Phone 8 and earlier Windows Phone platforms.</span></span> <span data-ttu-id="dd799-137">Aby uzyskać więcej informacji na temat konfigurowania hello Centrum powiadomień dla usługi MPNS odbieranie hello powiadomienia w aplikacji Windows Phone, zobacz [wysyłanie powiadomień wypychanych przy użyciu usługi Azure Notification Hubs na Windows Phone](../notification-hubs/notification-hubs-windows-mobile-push-notifications-mpns.md)</span><span class="sxs-lookup"><span data-stu-id="dd799-137">For more information on configuring hello notification hub for MPNS and receiving hello notification in a Windows Phone app, see [Sending push notifications with Azure Notification Hubs on Windows Phone](../notification-hubs/notification-hubs-windows-mobile-push-notifications-mpns.md)</span></span>

<span data-ttu-id="dd799-138">Przykład function.json:</span><span class="sxs-lookup"><span data-stu-id="dd799-138">Example function.json:</span></span>

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

## <a name="notification-hub-connection-string-setup"></a><span data-ttu-id="dd799-139">Ustawienia połączenia Centrum powiadomień</span><span class="sxs-lookup"><span data-stu-id="dd799-139">Notification hub connection string setup</span></span>
<span data-ttu-id="dd799-140">powiązania wyjściowego toouse Centrum powiadomień, należy skonfigurować hello parametry połączenia dla koncentratora hello.</span><span class="sxs-lookup"><span data-stu-id="dd799-140">toouse a Notification hub output binding, you must configure hello connection string for hello hub.</span></span> <span data-ttu-id="dd799-141">Można to zrobić na powitania *integracji* kartę, wybierając Centrum powiadomień i tworzenia nowego.</span><span class="sxs-lookup"><span data-stu-id="dd799-141">This can be done on hello *Integrate* tab by selecting your notification hub or creating a new one.</span></span> 

<span data-ttu-id="dd799-142">Można też ręcznie dodać parametry połączenia dla istniejącego elementu hub przez dodanie ciągu połączenia dla hello *DefaultFullSharedAccessSignature* tooyour Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="dd799-142">You can also manually add a connection string for an existing hub by adding a connection string for hello *DefaultFullSharedAccessSignature* tooyour notification hub.</span></span> <span data-ttu-id="dd799-143">Ten ciąg połączenia zapewnia dostęp funkcja komunikatów powiadomień toosend uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="dd799-143">This connection string provides your function access permission toosend notification messages.</span></span> <span data-ttu-id="dd799-144">Witaj *DefaultFullSharedAccessSignature* można uzyskać wartość ciągu połączenia z hello **kluczy** przycisku na powitania głównego bloku zasobu Centrum powiadomień w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="dd799-144">hello *DefaultFullSharedAccessSignature* connection string value can be accessed from hello **keys** button in hello main blade of your notification hub resource in hello Azure portal.</span></span> <span data-ttu-id="dd799-145">toomanually Dodaj parametry połączenia Centrum, użyj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="dd799-145">toomanually add a connection string for your hub, use hello following steps:</span></span> 

1. <span data-ttu-id="dd799-146">Na powitania **aplikacji funkcji** bloku hello portalu Azure, kliknij przycisk **ustawień aplikacji funkcji > Przejdź do ustawień usługi tooApp**.</span><span class="sxs-lookup"><span data-stu-id="dd799-146">On hello **Function app** blade of hello Azure portal, click **Function App Settings > Go tooApp Service settings**.</span></span>
2. <span data-ttu-id="dd799-147">W hello **ustawienia** bloku, kliknij przycisk **ustawienia aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="dd799-147">In hello **Settings** blade, click **Application Settings**.</span></span>
3. <span data-ttu-id="dd799-148">Przewiń w dół toohello **ustawień aplikacji** sekcji, a następnie dodanie wpisu o nazwie *DefaultFullSharedAccessSignature* wartość dla Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="dd799-148">Scroll down toohello **App settings** section, and add a named entry for *DefaultFullSharedAccessSignature* value for your notification hub.</span></span>
4. <span data-ttu-id="dd799-149">Odwoływać się do aplikacji ustawienie nazwy ciągu w hello powiązania danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="dd799-149">Reference your App setting string name in hello output bindings.</span></span> <span data-ttu-id="dd799-150">Podobnie za**MyHubConnectionString** używane w powyższym przykładzie hello.</span><span class="sxs-lookup"><span data-stu-id="dd799-150">Similar too**MyHubConnectionString** used in hello example above.</span></span>

## <a name="apns-native-notifications-with-c-queue-triggers"></a><span data-ttu-id="dd799-151">Natywnego powiadomienia usługi APNS z Wyzwalacze kolejkowania C#</span><span class="sxs-lookup"><span data-stu-id="dd799-151">APNS native notifications with C# queue triggers</span></span>
<span data-ttu-id="dd799-152">W tym przykładzie pokazano, jak toouse typy zdefiniowane w hello [Biblioteka programu Microsoft Azure Notification Hubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend natywnego powiadomienia usługi APNS.</span><span class="sxs-lookup"><span data-stu-id="dd799-152">This example shows how toouse types defined in hello [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend a native APNS notification.</span></span> 

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

## <a name="gcm-native-notifications-with-c-queue-triggers"></a><span data-ttu-id="dd799-153">Wyzwalacze kolejki natywnego powiadomienia GCM w języku C#</span><span class="sxs-lookup"><span data-stu-id="dd799-153">GCM native notifications with C# queue triggers</span></span>
<span data-ttu-id="dd799-154">W tym przykładzie pokazano, jak toouse typy zdefiniowane w hello [Biblioteka programu Microsoft Azure Notification Hubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend natywnych powiadomień usługi GCM.</span><span class="sxs-lookup"><span data-stu-id="dd799-154">This example shows how toouse types defined in hello [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend a native GCM notification.</span></span> 

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

## <a name="wns-native-notifications-with-c-queue-triggers"></a><span data-ttu-id="dd799-155">Natywnych powiadomień WNS przy użyciu Wyzwalacze kolejkowania C#</span><span class="sxs-lookup"><span data-stu-id="dd799-155">WNS native notifications with C# queue triggers</span></span>
<span data-ttu-id="dd799-156">W tym przykładzie pokazano, jak toouse typy zdefiniowane w hello [Biblioteka programu Microsoft Azure Notification Hubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend WNS natywnego wyskakujących powiadomień.</span><span class="sxs-lookup"><span data-stu-id="dd799-156">This example shows how toouse types defined in hello [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend a native WNS toast notification.</span></span> 

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

## <a name="template-example-for-nodejs-timer-triggers"></a><span data-ttu-id="dd799-157">Przykład szablonu wyzwalaczy czasomierza Node.js</span><span class="sxs-lookup"><span data-stu-id="dd799-157">Template example for Node.js timer triggers</span></span>
<span data-ttu-id="dd799-158">W tym przykładzie wysyła powiadomienie [rejestracji szablonu](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) zawierający `location` i `message`.</span><span class="sxs-lookup"><span data-stu-id="dd799-158">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains `location` and `message`.</span></span>

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

## <a name="template-example-for-f-timer-triggers"></a><span data-ttu-id="dd799-159">Przykład szablonu wyzwalaczy czasomierza F #</span><span class="sxs-lookup"><span data-stu-id="dd799-159">Template example for F# timer triggers</span></span>
<span data-ttu-id="dd799-160">W tym przykładzie wysyła powiadomienie [rejestracji szablonu](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) zawierający `location` i `message`.</span><span class="sxs-lookup"><span data-stu-id="dd799-160">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains `location` and `message`.</span></span>

```fsharp
let Run(myTimer: TimerInfo, notification: byref<IDictionary<string, string>>) =
    notification = dict [("location", "Redmond"); ("message", "Hello from F#!")]
```

## <a name="template-example-using-an-out-parameter"></a><span data-ttu-id="dd799-161">Przykład szablonu przy użyciu parametru wyjściowego</span><span class="sxs-lookup"><span data-stu-id="dd799-161">Template example using an out parameter</span></span>
<span data-ttu-id="dd799-162">W tym przykładzie wysyła powiadomienie [rejestracji szablonu](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) zawierający `message` symbol zastępczy w szablonie hello.</span><span class="sxs-lookup"><span data-stu-id="dd799-162">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains a `message` place holder in hello template.</span></span>

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

## <a name="template-example-with-asynchronous-function"></a><span data-ttu-id="dd799-163">Przykład: szablon funkcji asynchronicznych</span><span class="sxs-lookup"><span data-stu-id="dd799-163">Template example with asynchronous function</span></span>
<span data-ttu-id="dd799-164">Jeśli używasz kodu asynchroniczne parametry wyjściowe nie są dozwolone.</span><span class="sxs-lookup"><span data-stu-id="dd799-164">If you are using asynchronous code, out parameters are not allowed.</span></span> <span data-ttu-id="dd799-165">W takim przypadku użyj `IAsyncCollector` tooreturn szablonu powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="dd799-165">In this case use `IAsyncCollector` tooreturn your template notification.</span></span> <span data-ttu-id="dd799-166">Hello następujący kod jest przykładem asynchroniczne hello kodu powyżej.</span><span class="sxs-lookup"><span data-stu-id="dd799-166">hello following code is an asynchronous example of hello code above.</span></span> 

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

## <a name="template-example-using-json"></a><span data-ttu-id="dd799-167">Przykład szablonu przy użyciu</span><span class="sxs-lookup"><span data-stu-id="dd799-167">Template example using JSON</span></span>
<span data-ttu-id="dd799-168">W tym przykładzie wysyła powiadomienie [rejestracji szablonu](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) zawierający `message` symbol zastępczy w szablonie hello przy użyciu prawidłowego ciągu JSON.</span><span class="sxs-lookup"><span data-stu-id="dd799-168">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains a `message` place holder in hello template using a valid JSON string.</span></span>

```cs
using System;

public static void Run(string myQueueItem,  out string notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    notification = "{\"message\":\"Hello from C#. Processed a queue item!\"}";
}
```

## <a name="template-example-using-notification-hubs-library-types"></a><span data-ttu-id="dd799-169">Przykład szablonu przy użyciu usługi Notification Hubs biblioteki typów</span><span class="sxs-lookup"><span data-stu-id="dd799-169">Template example using Notification Hubs library types</span></span>
<span data-ttu-id="dd799-170">W tym przykładzie pokazano, jak toouse typy zdefiniowane w hello [Biblioteka programu Microsoft Azure Notification Hubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="dd799-170">This example shows how toouse types defined in hello [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="dd799-171">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="dd799-171">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

