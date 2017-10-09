---
title: aaaHow toosend zaplanowane powiadomienia | Dokumentacja firmy Microsoft
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
ms.openlocfilehash: 9b3ba715dad6f5d824a615e83f2863b0db47b533
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-send-scheduled-notifications"></a><span data-ttu-id="a384e-104">Porady: Wysyłanie powiadomień według harmonogramu</span><span class="sxs-lookup"><span data-stu-id="a384e-104">How To: Send scheduled notifications</span></span>
## <a name="overview"></a><span data-ttu-id="a384e-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="a384e-105">Overview</span></span>
<span data-ttu-id="a384e-106">Jeśli scenariusz, w którym mają toosend powiadomienie w pewnym momencie hello przyszłych, ale nie ma toowake łatwo się powiadomienia hello toosend kod zaplecza.</span><span class="sxs-lookup"><span data-stu-id="a384e-106">If you have a scenario in which you want toosend a notification at some point in hello future, but do not have an easy way toowake up your back-end code toosend hello notification.</span></span> <span data-ttu-id="a384e-107">Centra powiadomień w warstwie standardowa obsługuje funkcja umożliwiająca powiadomienia tooschedule się too7 dni w przyszłości hello.</span><span class="sxs-lookup"><span data-stu-id="a384e-107">Standard tier Notification Hubs supports a feature that enables you tooschedule notifications up too7 days in hello future.</span></span>

<span data-ttu-id="a384e-108">Podczas wysyłania powiadomienia, po prostu użyć hello [ScheduledNotification](https://msdn.microsoft.com/library/microsoft.azure.notificationhubs.schedulednotification.aspx) klasy w hello zestaw SDK usługi Notification Hubs, jak pokazano w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="a384e-108">When sending a notification, simply use hello [ScheduledNotification](https://msdn.microsoft.com/library/microsoft.azure.notificationhubs.schedulednotification.aspx) class in hello Notification Hubs SDK as shown in hello following example:</span></span>

    Notification notification = new AppleNotification("{\"aps\":{\"alert\":\"Happy birthday!\"}}");
    var scheduled = await hub.ScheduleNotificationAsync(notification, new DateTime(2014, 7, 19, 0, 0, 0));

<span data-ttu-id="a384e-109">Ponadto można anulować wcześniej zaplanowanym powiadomienia za pomocą jego notificationId:</span><span class="sxs-lookup"><span data-stu-id="a384e-109">Also, you can cancel a previously scheduled notification using its notificationId:</span></span>

    await hub.CancelNotificationAsync(scheduled.ScheduledNotificationId);

<span data-ttu-id="a384e-110">Nie ma żadnych limitów na powitania liczba zaplanowanych powiadomień, możesz wysłać.</span><span class="sxs-lookup"><span data-stu-id="a384e-110">There are no limits on hello number of scheduled notifications you can send.</span></span>

