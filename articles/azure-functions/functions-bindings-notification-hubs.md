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
# <a name="azure-functions-notification-hub-output-binding"></a><span data-ttu-id="1585b-104">Powiązanie danych wyjściowych Centrum powiadomień Azure funkcji</span><span class="sxs-lookup"><span data-stu-id="1585b-104">Azure Functions Notification Hub output binding</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="1585b-105">W tym artykule opisano sposób konfigurowania i Zakoduj powiązania Centrum powiadomień Azure w funkcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1585b-105">This article explains how to configure and code Azure Notification Hub bindings in Azure Functions.</span></span> 

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="1585b-106">Funkcji można wysyłać powiadomienia wypychane za pomocą skonfigurowanego centrum powiadomień Azure przy użyciu kilku wierszy kodu.</span><span class="sxs-lookup"><span data-stu-id="1585b-106">Your functions can send push notifications using a configured Azure Notification Hub with a few lines of code.</span></span> <span data-ttu-id="1585b-107">Jednak Centrum powiadomień Azure musi być skonfigurowana dla platformy powiadomienia usługi (PNS) ma być używany.</span><span class="sxs-lookup"><span data-stu-id="1585b-107">However, the Azure Notification Hub must be configured for the Platform Notifications Services (PNS) you want to use.</span></span> <span data-ttu-id="1585b-108">Aby uzyskać więcej informacji na temat konfigurowania Centrum powiadomień Azure tworzenie aplikacji klienckich, które Zarejestruj, aby otrzymywać powiadomienia, zobacz [wprowadzenie do korzystania z usługi Notification Hubs](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) i kliknij przycisk docelowej platformy klienta u góry .</span><span class="sxs-lookup"><span data-stu-id="1585b-108">For more information on configuring an Azure Notification Hub and developing a client applications that register to receive notifications, see [Getting started with Notification Hubs](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) and click your target client platform at the top.</span></span>

<span data-ttu-id="1585b-109">Możesz wysłać powiadomienia mogą być natywnych powiadomień lub szablonu powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="1585b-109">The notifications you send can be native notifications or template notifications.</span></span> <span data-ttu-id="1585b-110">Natywnych powiadomień Docelowa platforma powiadomień określonych zgodnie z konfiguracją `platform` właściwości powiązania danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="1585b-110">Native notifications target a specific notification platform as configured in the `platform` property of the output binding.</span></span> <span data-ttu-id="1585b-111">Powiadomienie o szablonu może służyć do wielu platform docelowych.</span><span class="sxs-lookup"><span data-stu-id="1585b-111">A template notification can be used to target multiple platforms.</span></span>   

## <a name="notification-hub-output-binding-properties"></a><span data-ttu-id="1585b-112">Właściwości powiązania danych wyjściowych Centrum powiadomień</span><span class="sxs-lookup"><span data-stu-id="1585b-112">Notification hub output binding properties</span></span>
<span data-ttu-id="1585b-113">Plik function.json zawiera następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="1585b-113">The function.json file provides the following properties:</span></span>

* <span data-ttu-id="1585b-114">`name`: Nazwa zmiennej używane w kodzie funkcja komunikat Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="1585b-114">`name` : Variable name used in function code for the notification hub message.</span></span>
* <span data-ttu-id="1585b-115">`type`: musi być ustawiona na *"notificationHub"*.</span><span class="sxs-lookup"><span data-stu-id="1585b-115">`type` : must be set to *"notificationHub"*.</span></span>
* <span data-ttu-id="1585b-116">`tagExpression`: Wyrażeń tagów umożliwiają określenie, czy do zestawu urządzeń, które zostały zarejestrowane, aby otrzymywać powiadomienia, które odpowiada wyrażeniu tagu można dostarczyć powiadomień.</span><span class="sxs-lookup"><span data-stu-id="1585b-116">`tagExpression` : Tag expressions allow you to specify that notifications be delivered to a set of devices who have registered to receive notifications that match the tag expression.</span></span>  <span data-ttu-id="1585b-117">Aby uzyskać więcej informacji, zobacz [wyrażenia routingu i tagu](../notification-hubs/notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="1585b-117">For more information, see [Routing and tag expressions](../notification-hubs/notification-hubs-tags-segment-push-message.md).</span></span>
* <span data-ttu-id="1585b-118">`hubName`: Nazwa zasobu Centrum powiadomień, w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="1585b-118">`hubName` : Name of the notification hub resource in the Azure portal.</span></span>
* <span data-ttu-id="1585b-119">`connection`: Ten ciąg połączenia musi być **ustawienie aplikacji** ustawić parametry połączenia *DefaultFullSharedAccessSignature* wartość dla Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="1585b-119">`connection` : This connection string must be an **Application Setting** connection string set to the *DefaultFullSharedAccessSignature* value for your notification hub.</span></span>
* <span data-ttu-id="1585b-120">`direction`: musi być ustawiona na *"out"*.</span><span class="sxs-lookup"><span data-stu-id="1585b-120">`direction` : must be set to *"out"*.</span></span> 
* <span data-ttu-id="1585b-121">`platform`: Właściwość platformy wskazuje powiadomień platformy celów powiadomień.</span><span class="sxs-lookup"><span data-stu-id="1585b-121">`platform` : The platform property indicates the notification platform your notification targets.</span></span> <span data-ttu-id="1585b-122">Musi mieć jedną z następujących wartości:</span><span class="sxs-lookup"><span data-stu-id="1585b-122">Must be one of the following values:</span></span>
  * <span data-ttu-id="1585b-123">Domyślnie w przypadku pominięcia właściwości platformy z wiązania danych wyjściowych szablonu powiadomienia można współpracować z dowolną platformą skonfigurowany w Centrum powiadomień Azure.</span><span class="sxs-lookup"><span data-stu-id="1585b-123">By default, if the platform property is omitted from the output binding, template notifications can be used to target any platform configured on the Azure Notification Hub.</span></span> <span data-ttu-id="1585b-124">Aby uzyskać więcej informacji na korzystanie z szablonów ogólnie do wysyłania wielu powiadomień platformy przy użyciu Centrum powiadomień Azure, zobacz [szablony](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="1585b-124">For more information on using templates in general to send cross platform notifications with an Azure Notification Hub, see [Templates](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span></span>
  * <span data-ttu-id="1585b-125">`apns`: Apple Push Notification Service.</span><span class="sxs-lookup"><span data-stu-id="1585b-125">`apns` : Apple Push Notification Service.</span></span> <span data-ttu-id="1585b-126">Aby uzyskać więcej informacji na temat konfigurowania Centrum powiadomień dla APNS odbieranie powiadomień w aplikacji klienta, zobacz [wysyłanie powiadomień wypychanych do systemu iOS przy użyciu usługi Azure Notification Hubs](../notification-hubs/notification-hubs-ios-apple-push-notification-apns-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="1585b-126">For more information on configuring the notification hub for APNS and receiving the notification in a client app, see [Sending push notifications to iOS with Azure Notification Hubs](../notification-hubs/notification-hubs-ios-apple-push-notification-apns-get-started.md)</span></span> 
  * <span data-ttu-id="1585b-127">`adm`: [Usługi Amazon Device Messaging](https://developer.amazon.com/device-messaging).</span><span class="sxs-lookup"><span data-stu-id="1585b-127">`adm` : [Amazon Device Messaging](https://developer.amazon.com/device-messaging).</span></span> <span data-ttu-id="1585b-128">Aby uzyskać więcej informacji na temat konfigurowania Centrum powiadomień dla ADM odbieranie powiadomień w aplikację dla urządzeń Kindle, zobacz [wprowadzenie do korzystania z usługi Notification Hubs dla aplikacji dla urządzeń Kindle](../notification-hubs/notification-hubs-kindle-amazon-adm-push-notification.md)</span><span class="sxs-lookup"><span data-stu-id="1585b-128">For more information on configuring the notification hub for ADM and receiving the notification in a Kindle app, see [Getting Started with Notification Hubs for Kindle apps](../notification-hubs/notification-hubs-kindle-amazon-adm-push-notification.md)</span></span> 
  * <span data-ttu-id="1585b-129">`gcm`: [Usługi Google Cloud Messaging](https://developers.google.com/cloud-messaging/).</span><span class="sxs-lookup"><span data-stu-id="1585b-129">`gcm` : [Google Cloud Messaging](https://developers.google.com/cloud-messaging/).</span></span> <span data-ttu-id="1585b-130">Firebase Cloud Messaging, która jest nowa wersja usługi GCM, jest również obsługiwany.</span><span class="sxs-lookup"><span data-stu-id="1585b-130">Firebase Cloud Messaging, which is the new version of GCM, is also supported.</span></span> <span data-ttu-id="1585b-131">Aby uzyskać więcej informacji na temat konfigurowania Centrum powiadomień dla usługi GCM/FCM odbieranie powiadomień w aplikację kliencką dla systemu Android, zobacz [wysyłanie powiadomień wypychanych w systemie Android przy użyciu usługi Azure Notification Hubs](../notification-hubs/notification-hubs-android-push-notification-google-fcm-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="1585b-131">For more information on configuring the notification hub for GCM/FCM and receiving the notification in an Android client app, see [Sending push notifications to Android with Azure Notification Hubs](../notification-hubs/notification-hubs-android-push-notification-google-fcm-get-started.md)</span></span>
  * <span data-ttu-id="1585b-132">`wns`: [Usług powiadomień Wns](https://msdn.microsoft.com/en-us/windows/uwp/controls-and-patterns/tiles-and-notifications-windows-push-notification-services--wns--overview) przeznaczonych dla platformy systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="1585b-132">`wns` : [Windows Push Notification Services](https://msdn.microsoft.com/en-us/windows/uwp/controls-and-patterns/tiles-and-notifications-windows-push-notification-services--wns--overview) targeting Windows platforms.</span></span> <span data-ttu-id="1585b-133">Windows Phone 8.1 lub nowszy jest również obsługiwana przez usługi WNS.</span><span class="sxs-lookup"><span data-stu-id="1585b-133">Windows Phone 8.1 and later is also supported by WNS.</span></span> <span data-ttu-id="1585b-134">Aby uzyskać więcej informacji na temat konfigurowania Centrum powiadomień w przypadku usługi WNS odbieranie powiadomień w aplikacji Windows platformy Uniwersalnej, zobacz [wprowadzenie Notification Hubs dla uniwersalnych aplikacji systemu Windows platformy](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)</span><span class="sxs-lookup"><span data-stu-id="1585b-134">For more information on configuring the notification hub for WNS and receiving the notification in a Universal Windows Platform (UWP) app, see [Getting started with Notification Hubs for Windows Universal Platform Apps](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)</span></span>
  * <span data-ttu-id="1585b-135">`mpns`: [Usługi powiadomień wypychanych firmy Microsoft](https://msdn.microsoft.com/en-us/library/windows/apps/ff402558.aspx).</span><span class="sxs-lookup"><span data-stu-id="1585b-135">`mpns` : [Microsoft Push Notification Service](https://msdn.microsoft.com/en-us/library/windows/apps/ff402558.aspx).</span></span> <span data-ttu-id="1585b-136">Ta platforma obsługuje starszych platform Windows Phone i Windows Phone 8.</span><span class="sxs-lookup"><span data-stu-id="1585b-136">This platform supports Windows Phone 8 and earlier Windows Phone platforms.</span></span> <span data-ttu-id="1585b-137">Aby uzyskać więcej informacji na temat konfigurowania Centrum powiadomień dla usługi MPNS odbieranie powiadomień w aplikacji Windows Phone, zobacz [wysyłanie powiadomień wypychanych przy użyciu usługi Azure Notification Hubs na Windows Phone](../notification-hubs/notification-hubs-windows-mobile-push-notifications-mpns.md)</span><span class="sxs-lookup"><span data-stu-id="1585b-137">For more information on configuring the notification hub for MPNS and receiving the notification in a Windows Phone app, see [Sending push notifications with Azure Notification Hubs on Windows Phone](../notification-hubs/notification-hubs-windows-mobile-push-notifications-mpns.md)</span></span>

<span data-ttu-id="1585b-138">Przykład function.json:</span><span class="sxs-lookup"><span data-stu-id="1585b-138">Example function.json:</span></span>

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

## <a name="notification-hub-connection-string-setup"></a><span data-ttu-id="1585b-139">Ustawienia połączenia Centrum powiadomień</span><span class="sxs-lookup"><span data-stu-id="1585b-139">Notification hub connection string setup</span></span>
<span data-ttu-id="1585b-140">Aby użyć powiązania danych wyjściowych Centrum powiadomień, należy skonfigurować parametry połączenia dla koncentratora.</span><span class="sxs-lookup"><span data-stu-id="1585b-140">To use a Notification hub output binding, you must configure the connection string for the hub.</span></span> <span data-ttu-id="1585b-141">Można to zrobić na *integracji* kartę, wybierając Centrum powiadomień i tworzenia nowego.</span><span class="sxs-lookup"><span data-stu-id="1585b-141">This can be done on the *Integrate* tab by selecting your notification hub or creating a new one.</span></span> 

<span data-ttu-id="1585b-142">Można też ręcznie dodać parametry połączenia dla istniejącego elementu hub przez dodanie ciągu połączenia dla *DefaultFullSharedAccessSignature* do Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="1585b-142">You can also manually add a connection string for an existing hub by adding a connection string for the *DefaultFullSharedAccessSignature* to your notification hub.</span></span> <span data-ttu-id="1585b-143">Te parametry połączenia zawiera uprawnień dostępu użytkownika funkcji wysyłać powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="1585b-143">This connection string provides your function access permission to send notification messages.</span></span> <span data-ttu-id="1585b-144">*DefaultFullSharedAccessSignature* można uzyskać wartość ciągu połączenia z **klucze** przycisk w głównym bloku zasobu Centrum powiadomień w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="1585b-144">The *DefaultFullSharedAccessSignature* connection string value can be accessed from the **keys** button in the main blade of your notification hub resource in the Azure portal.</span></span> <span data-ttu-id="1585b-145">Aby ręcznie dodać parametry połączenia Centrum, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="1585b-145">To manually add a connection string for your hub, use the following steps:</span></span> 

1. <span data-ttu-id="1585b-146">Na **aplikacji funkcji** bloku portalu Azure kliknij **ustawień aplikacji funkcji > Przejdź do ustawień usługi aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="1585b-146">On the **Function app** blade of the Azure portal, click **Function App Settings > Go to App Service settings**.</span></span>
2. <span data-ttu-id="1585b-147">W **ustawienia** bloku, kliknij przycisk **ustawienia aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="1585b-147">In the **Settings** blade, click **Application Settings**.</span></span>
3. <span data-ttu-id="1585b-148">Przewiń w dół do **ustawień aplikacji** sekcji, a następnie dodanie wpisu o nazwie *DefaultFullSharedAccessSignature* wartość dla Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="1585b-148">Scroll down to the **App settings** section, and add a named entry for *DefaultFullSharedAccessSignature* value for your notification hub.</span></span>
4. <span data-ttu-id="1585b-149">Odwołanie nazwę aplikacji ustawienie ciągu powiązania danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="1585b-149">Reference your App setting string name in the output bindings.</span></span> <span data-ttu-id="1585b-150">Podobnie jak **MyHubConnectionString** używane w powyższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="1585b-150">Similar to **MyHubConnectionString** used in the example above.</span></span>

## <a name="apns-native-notifications-with-c-queue-triggers"></a><span data-ttu-id="1585b-151">Natywnego powiadomienia usługi APNS z Wyzwalacze kolejkowania C#</span><span class="sxs-lookup"><span data-stu-id="1585b-151">APNS native notifications with C# queue triggers</span></span>
<span data-ttu-id="1585b-152">W tym przykładzie przedstawiono użycie typów zdefiniowanych w [Biblioteka programu Microsoft Azure Notification Hubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) do wysyłania natywnych powiadomień usługi APNS.</span><span class="sxs-lookup"><span data-stu-id="1585b-152">This example shows how to use types defined in the [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) to send a native APNS notification.</span></span> 

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

## <a name="gcm-native-notifications-with-c-queue-triggers"></a><span data-ttu-id="1585b-153">Wyzwalacze kolejki natywnego powiadomienia GCM w języku C#</span><span class="sxs-lookup"><span data-stu-id="1585b-153">GCM native notifications with C# queue triggers</span></span>
<span data-ttu-id="1585b-154">W tym przykładzie przedstawiono użycie typów zdefiniowanych w [Biblioteka programu Microsoft Azure Notification Hubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) do wysyłania natywnych powiadomień usługi GCM.</span><span class="sxs-lookup"><span data-stu-id="1585b-154">This example shows how to use types defined in the [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) to send a native GCM notification.</span></span> 

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

## <a name="wns-native-notifications-with-c-queue-triggers"></a><span data-ttu-id="1585b-155">Natywnych powiadomień WNS przy użyciu Wyzwalacze kolejkowania C#</span><span class="sxs-lookup"><span data-stu-id="1585b-155">WNS native notifications with C# queue triggers</span></span>
<span data-ttu-id="1585b-156">W tym przykładzie przedstawiono użycie typów zdefiniowanych w [Biblioteka programu Microsoft Azure Notification Hubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) do wysyłania wyskakujących powiadomień WNS macierzystego.</span><span class="sxs-lookup"><span data-stu-id="1585b-156">This example shows how to use types defined in the [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) to send a native WNS toast notification.</span></span> 

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

## <a name="template-example-for-nodejs-timer-triggers"></a><span data-ttu-id="1585b-157">Przykład szablonu wyzwalaczy czasomierza Node.js</span><span class="sxs-lookup"><span data-stu-id="1585b-157">Template example for Node.js timer triggers</span></span>
<span data-ttu-id="1585b-158">W tym przykładzie wysyła powiadomienie [rejestracji szablonu](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) zawierający `location` i `message`.</span><span class="sxs-lookup"><span data-stu-id="1585b-158">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains `location` and `message`.</span></span>

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

## <a name="template-example-for-f-timer-triggers"></a><span data-ttu-id="1585b-159">Przykład szablonu wyzwalaczy czasomierza F #</span><span class="sxs-lookup"><span data-stu-id="1585b-159">Template example for F# timer triggers</span></span>
<span data-ttu-id="1585b-160">W tym przykładzie wysyła powiadomienie [rejestracji szablonu](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) zawierający `location` i `message`.</span><span class="sxs-lookup"><span data-stu-id="1585b-160">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains `location` and `message`.</span></span>

```fsharp
let Run(myTimer: TimerInfo, notification: byref<IDictionary<string, string>>) =
    notification = dict [("location", "Redmond"); ("message", "Hello from F#!")]
```

## <a name="template-example-using-an-out-parameter"></a><span data-ttu-id="1585b-161">Przykład szablonu przy użyciu parametru wyjściowego</span><span class="sxs-lookup"><span data-stu-id="1585b-161">Template example using an out parameter</span></span>
<span data-ttu-id="1585b-162">W tym przykładzie wysyła powiadomienie [rejestracji szablonu](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) zawierający `message` symbol zastępczy w szablonie.</span><span class="sxs-lookup"><span data-stu-id="1585b-162">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains a `message` place holder in the template.</span></span>

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

## <a name="template-example-with-asynchronous-function"></a><span data-ttu-id="1585b-163">Przykład: szablon funkcji asynchronicznych</span><span class="sxs-lookup"><span data-stu-id="1585b-163">Template example with asynchronous function</span></span>
<span data-ttu-id="1585b-164">Jeśli używasz kodu asynchroniczne parametry wyjściowe nie są dozwolone.</span><span class="sxs-lookup"><span data-stu-id="1585b-164">If you are using asynchronous code, out parameters are not allowed.</span></span> <span data-ttu-id="1585b-165">W takim przypadku użyj `IAsyncCollector` do zwrócenia szablonu powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="1585b-165">In this case use `IAsyncCollector` to return your template notification.</span></span> <span data-ttu-id="1585b-166">Następujący kod jest przykładem asynchroniczne kodu powyżej.</span><span class="sxs-lookup"><span data-stu-id="1585b-166">The following code is an asynchronous example of the code above.</span></span> 

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

## <a name="template-example-using-json"></a><span data-ttu-id="1585b-167">Przykład szablonu przy użyciu</span><span class="sxs-lookup"><span data-stu-id="1585b-167">Template example using JSON</span></span>
<span data-ttu-id="1585b-168">W tym przykładzie wysyła powiadomienie [rejestracji szablonu](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) zawierający `message` symbol zastępczy w szablonie przy użyciu prawidłowego ciągu JSON.</span><span class="sxs-lookup"><span data-stu-id="1585b-168">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains a `message` place holder in the template using a valid JSON string.</span></span>

```cs
using System;

public static void Run(string myQueueItem,  out string notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    notification = "{\"message\":\"Hello from C#. Processed a queue item!\"}";
}
```

## <a name="template-example-using-notification-hubs-library-types"></a><span data-ttu-id="1585b-169">Przykład szablonu przy użyciu usługi Notification Hubs biblioteki typów</span><span class="sxs-lookup"><span data-stu-id="1585b-169">Template example using Notification Hubs library types</span></span>
<span data-ttu-id="1585b-170">W tym przykładzie przedstawiono użycie typów zdefiniowanych w [Biblioteka programu Microsoft Azure Notification Hubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="1585b-170">This example shows how to use types defined in the [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="1585b-171">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1585b-171">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

