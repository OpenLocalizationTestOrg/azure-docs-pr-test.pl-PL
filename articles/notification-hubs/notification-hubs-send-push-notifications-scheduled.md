---
title: "Jak wysyłać powiadomienia zaplanowane | Dokumentacja firmy Microsoft"
description: "W tym temacie opisano, w usłudze Azure Notification Hubs przy użyciu powiadomienia zaplanowane."
services: notification-hubs
documentationcenter: .net
keywords: "powiadomienia wypychane, powiadomień wypychanych, planowania powiadomień wypychanych"
author: ysxu
manager: erikre
editor: 
ms.assetid: 6b718c75-75dd-4c99-aee3-db1288235c1a
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: efac6e1ecc00359f1622d380333140bc055c83e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-send-scheduled-notifications"></a><span data-ttu-id="05ac0-104">Porady: Wysyłanie powiadomień według harmonogramu</span><span class="sxs-lookup"><span data-stu-id="05ac0-104">How To: Send scheduled notifications</span></span>
## <a name="overview"></a><span data-ttu-id="05ac0-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="05ac0-105">Overview</span></span>
<span data-ttu-id="05ac0-106">Jeśli scenariusz, w którym chcesz wysłać powiadomienie w pewnym momencie w przyszłości, ale nie mają w prosty sposób wake zapasowej swój kod zaplecza, aby wysłać powiadomienie.</span><span class="sxs-lookup"><span data-stu-id="05ac0-106">If you have a scenario in which you want to send a notification at some point in the future, but do not have an easy way to wake up your back-end code to send the notification.</span></span> <span data-ttu-id="05ac0-107">Centra powiadomień w warstwie standardowa obsługuje funkcja, która umożliwia planowanie powiadomienia w górę do 7 dni w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="05ac0-107">Standard tier Notification Hubs supports a feature that enables you to schedule notifications up to 7 days in the future.</span></span>

<span data-ttu-id="05ac0-108">Podczas wysyłania powiadomienia, po prostu użyć [ScheduledNotification](https://msdn.microsoft.com/library/microsoft.azure.notificationhubs.schedulednotification.aspx) klasy w zestaw SDK usługi Notification Hubs, jak pokazano w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="05ac0-108">When sending a notification, simply use the [ScheduledNotification](https://msdn.microsoft.com/library/microsoft.azure.notificationhubs.schedulednotification.aspx) class in the Notification Hubs SDK as shown in the following example:</span></span>

    Notification notification = new AppleNotification("{\"aps\":{\"alert\":\"Happy birthday!\"}}");
    var scheduled = await hub.ScheduleNotificationAsync(notification, new DateTime(2014, 7, 19, 0, 0, 0));

<span data-ttu-id="05ac0-109">Ponadto można anulować wcześniej zaplanowanym powiadomienia za pomocą jego notificationId:</span><span class="sxs-lookup"><span data-stu-id="05ac0-109">Also, you can cancel a previously scheduled notification using its notificationId:</span></span>

    await hub.CancelNotificationAsync(scheduled.ScheduledNotificationId);

<span data-ttu-id="05ac0-110">Nie ma żadnych limitów liczby zaplanowanych powiadomienia, który można wysłać.</span><span class="sxs-lookup"><span data-stu-id="05ac0-110">There are no limits on the number of scheduled notifications you can send.</span></span>

