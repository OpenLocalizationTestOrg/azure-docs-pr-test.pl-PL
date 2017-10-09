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
# <a name="how-to-send-scheduled-notifications"></a>Porady: Wysyłanie powiadomień według harmonogramu
## <a name="overview"></a>Omówienie
Jeśli scenariusz, w którym mają toosend powiadomienie w pewnym momencie hello przyszłych, ale nie ma toowake łatwo się powiadomienia hello toosend kod zaplecza. Centra powiadomień w warstwie standardowa obsługuje funkcja umożliwiająca powiadomienia tooschedule się too7 dni w przyszłości hello.

Podczas wysyłania powiadomienia, po prostu użyć hello [ScheduledNotification](https://msdn.microsoft.com/library/microsoft.azure.notificationhubs.schedulednotification.aspx) klasy w hello zestaw SDK usługi Notification Hubs, jak pokazano w hello poniższy przykład:

    Notification notification = new AppleNotification("{\"aps\":{\"alert\":\"Happy birthday!\"}}");
    var scheduled = await hub.ScheduleNotificationAsync(notification, new DateTime(2014, 7, 19, 0, 0, 0));

Ponadto można anulować wcześniej zaplanowanym powiadomienia za pomocą jego notificationId:

    await hub.CancelNotificationAsync(scheduled.ScheduledNotificationId);

Nie ma żadnych limitów na powitania liczba zaplanowanych powiadomień, możesz wysłać.

