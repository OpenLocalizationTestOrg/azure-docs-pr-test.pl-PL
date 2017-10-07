---
title: "aaaRouting i wyrażeń tagów"
description: "W tym temacie wyjaśniono wyrażeń routingu i tag do usługi Azure notification hubs."
services: notification-hubs
documentationcenter: .net
author: ysxu
manager: erikre
editor: 
ms.assetid: 0fffb3bb-8ed8-4e0f-89e8-0de24a47f644
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: c2c60500f7469f1cb1a73a5cf63c221a9ad6cbb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="routing-and-tag-expressions"></a>Wyrażenia routingu i tagów
## <a name="overview"></a>Omówienie
Wyrażeń tagów Włącz tootarget określonych zestawów urządzeń lub dokładniej rejestracji podczas wysyłania powiadomień wypychanych przy użyciu usługi Notification Hubs.

## <a name="targeting-specific-registrations"></a>Przeznaczonych dla określonych rejestracji
Witaj tylko sposób tootarget określonych powiadomienia rejestracji jest tagi tooassociate za ich pomocą skierować tych tagów. Zgodnie z opisem w [zarządzania rejestracji](notification-hubs-push-notification-registration-management.md), w kolejności tooreceive wypychania powiadomień aplikacja ma tooregister urządzenia jest obsługiwana w Centrum powiadomień. Po utworzeniu rejestracji w Centrum powiadomień aplikacji hello wewnętrznej bazy danych można wysyłać tooit powiadomień wypychanych.
zaplecza aplikacji Hello można wybrać hello tootarget rejestracje z określonych powiadomień w hello następujące sposoby:

1. **Emisji**: wszystkich rejestracji w Centrum powiadomień hello hello powiadomienie.
2. **Tag**: wszystkie rejestracji, które zawierają hello określony tag hello powiadomienie.
3. **Tag wyrażenie**: wszystkich rejestracji, którego zestawu tagów dopasowania hello określone wyrażenie hello powiadomienie.

## <a name="tags"></a>Tagi
Znacznik może być dowolny ciąg w górę too120 znaków, alfanumeryczne i hello następujących znaków innych niż alfanumeryczne: "_", "@", "#", ".",":", "-". Witaj poniższy przykład przedstawia aplikacji, z którego może otrzymywać wyskakujące powiadomienia o muzyka określonych grup. W tym scenariuszu powiadomienia tooroute prosty sposób jest toolabel rejestracji przy użyciu tagów reprezentujących różne pasma hello, tak jak hello poniższej ilustracji.

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags.png)

Na tej ilustracji oznakowane wiadomość hello **Beatles** osiągnie tylko hello tablet zarejestrowana z tagiem hello **Beatles**.

Aby uzyskać więcej informacji o tworzeniu rejestracji dla tagów, zobacz [zarządzania rejestracji](notification-hubs-push-notification-registration-management.md).

Możesz wysłać tootags powiadomienia za pomocą hello wysyłania powiadomień metody hello `Microsoft.Azure.NotificationHubs.NotificationHubClient` klasy w hello [centra powiadomień Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) zestawu SDK. Można również użyć środowiska Node.js lub hello wypychanie powiadomień interfejsów API REST.  Oto przykład przy użyciu hello zestawu SDK.

    Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;

    // Windows 8.1 / Windows Phone 8.1
    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" +
    "You requested a Beatles notification</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, "Beatles");

    // Windows 10
    toast = @"<toast><visual><binding template=""ToastGeneric""><text id=""1"">" +
    "You requested a Wailers notification</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, "Wailers");




Tagi nie ma wstępnie tworzyć toobe i może odnosić się toomultiple pojęcia specyficzny dla aplikacji. Na przykład użytkownicy tej przykładowej aplikacji można dodać komentarz dotyczący przedziałów i mają tooreceive wyskakujące powiadomienia, nie tylko dla hello komentarze dotyczące ich ulubionych pasma, ale także dla wszystkich komentarzy z swoich znajomych, niezależnie od ich komentowania pasmem hello. Witaj, na poniższej ilustracji przedstawiono przykład tego scenariusza:

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags2.png)

Na tej ilustracji Alicja jest zainteresowane w aktualizacjach dla hello Beatles i Robert jest zainteresowane w aktualizacjach dla hello Wailers. Robert jest również zainteresowana komentarze na marek i marek znajduje się w zainteresowani hello Wailers. Jeśli powiadomienie jest wysyłane do firmy marek komentarz na powitania Beatles, zarówno Alicja i Robert odebrane.

Tagi może zakodować wiele problemów w tagów (na przykład "band_Beatles" lub "follows_Charlie"), są proste ciągów nie właściwości i wartości. Rejestracja jest zgodny tylko na powitania obecności lub braku konkretnego znacznika.

Pełne krok samouczek dotyczący jak toouse tagów do wysyłania toointerest grup, zobacz [fundamentalne wiadomości](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md).

## <a name="using-tags-tootarget-users"></a>Za pomocą tagów tootarget użytkowników
Inny sposób toouse tagów jest tooidentify wszystkie urządzenia hello określonego użytkownika. Rejestracje mogą być oznaczane tagu, który zawiera identyfikator użytkownika, tak jak na poniższej ilustracji hello:

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags3.png)

Na tej ilustracji uid:Alice oznakowane wiadomość hello osiągnie wszystkich uid:Alice oznakowanych rejestracji; w związku z tym wszystkie urządzenia Alicji.

## <a name="tag-expressions"></a>Wyrażeń tagów
Istnieją przypadki, w których powiadomienie ma tootarget zestaw rejestracji, który jest identyfikowany nie przez jeden tag, ale przez wyrażenie logiczne w tagach.

Należy wziąć pod uwagę aplikacji sportowych, która wysyła tooeveryone monitu w Boston o gry między hello czerwony Sox i Cardinals. Jeśli aplikacja kliencka hello rejestruje tagi o zainteresowanie zespołów i lokalizacji, hello powiadomień należy tooeveryone docelowych w Boston chcący Sox czerwony hello lub hello Cardinals. Ten warunek może zostać wyrażona z hello następującego wyrażenia logicznego:

    (follows_RedSox || follows_Cardinals) && location_Boston


![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags4.png)

Wyrażeń tagów może zawierać wszystkich operatorów logicznych, takich jak AND (& &), lub (|), a nie (!). Może również zawierać nawiasów. Wyrażeń tagów są ograniczone too20 znaczników, jeśli zawierają one tylko ORs; w przeciwnym razie są one ograniczone too6 tagów.

Oto przykład wysyłania powiadomień za pomocą wyrażeń tag przy użyciu hello zestawu SDK.

    Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;

    String userTag = "(location_Boston && !follows_Cardinals)";    

    // Windows 8.1 / Windows Phone 8.1
    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" +
    "You want info on hello Red Socks</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);

    // Windows 10
    toast = @"<toast><visual><binding template=""ToastGeneric""><text id=""1"">" +
    "You want info on hello Red Socks</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);
