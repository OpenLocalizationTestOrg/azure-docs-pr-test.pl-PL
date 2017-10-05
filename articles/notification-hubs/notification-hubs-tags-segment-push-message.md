---
title: "Routing i wyrażeń tagów"
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
ms.openlocfilehash: 18faa88641623e1248d6a33bc2d87099e1c9f624
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="routing-and-tag-expressions"></a><span data-ttu-id="467fd-103">Wyrażenia routingu i tagów</span><span class="sxs-lookup"><span data-stu-id="467fd-103">Routing and tag expressions</span></span>
## <a name="overview"></a><span data-ttu-id="467fd-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="467fd-104">Overview</span></span>
<span data-ttu-id="467fd-105">Wyrażeń tagów umożliwia określonych zestawów docelowych urządzeń lub dokładniej rejestracji podczas wysyłania powiadomień wypychanych przy użyciu usługi Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="467fd-105">Tag expressions enable you to target specific sets of devices, or more specifically registrations, when sending a push notification through Notification Hubs.</span></span>

## <a name="targeting-specific-registrations"></a><span data-ttu-id="467fd-106">Przeznaczonych dla określonych rejestracji</span><span class="sxs-lookup"><span data-stu-id="467fd-106">Targeting specific registrations</span></span>
<span data-ttu-id="467fd-107">Jedynym sposobem na docelowych określonych powiadomień jest rejestracji, aby skojarzyć tagi z nich, skierować tych tagów.</span><span class="sxs-lookup"><span data-stu-id="467fd-107">The only way to target specific notification registrations is to associate tags with them, then target those tags.</span></span> <span data-ttu-id="467fd-108">Zgodnie z opisem w [zarządzania rejestracji](notification-hubs-push-notification-registration-management.md), aby otrzymać obsługi powiadomień aplikacja ma zarejestrować urządzenie w Centrum powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="467fd-108">As discussed in [Registration Management](notification-hubs-push-notification-registration-management.md), in order to receive push notifications an app has to register a device handle on a notification hub.</span></span> <span data-ttu-id="467fd-109">Po utworzeniu rejestracji w Centrum powiadomień zaplecza aplikacji może wysyłać powiadomienia wypychane do niej.</span><span class="sxs-lookup"><span data-stu-id="467fd-109">Once a registration is created on a notification hub, the application backend can send push notifications to it.</span></span>
<span data-ttu-id="467fd-110">Aplikacja wewnętrznej bazy danych można wybrać rejestracji do miejsca docelowego z określonym powiadomień w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="467fd-110">The application backend can choose the registrations to target with a specific notification in the following ways:</span></span>

1. <span data-ttu-id="467fd-111">**Emisji**: powiadomienie wszystkich rejestracji w Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="467fd-111">**Broadcast**: all registrations in the notification hub receive the notification.</span></span>
2. <span data-ttu-id="467fd-112">**Tag**: wszystkich rejestracji, które zawierają określonego tagu powiadomienie.</span><span class="sxs-lookup"><span data-stu-id="467fd-112">**Tag**: all registrations that contain the specified tag receive the notification.</span></span>
3. <span data-ttu-id="467fd-113">**Tag wyrażenie**: powiadomienie wszystkich rejestracji, w których zestaw tagi pasują podanego wyrażenia.</span><span class="sxs-lookup"><span data-stu-id="467fd-113">**Tag expression**: all registrations whose set of tags match the specified expression receive the notification.</span></span>

## <a name="tags"></a><span data-ttu-id="467fd-114">Tagi</span><span class="sxs-lookup"><span data-stu-id="467fd-114">Tags</span></span>
<span data-ttu-id="467fd-115">Znacznik może być dowolny ciąg, maksymalnie 120 znaków, alfanumerycznego i następujące znaki inne niż alfanumeryczne: "_", "@", "#", ".",":", "-".</span><span class="sxs-lookup"><span data-stu-id="467fd-115">A tag can be any string, up to 120 characters, containing alphanumeric and the following non-alphanumeric characters: ‘_’, ‘@’, ‘#’, ‘.’, ‘:’, ‘-’.</span></span> <span data-ttu-id="467fd-116">W poniższym przykładzie przedstawiono aplikację, z którego może otrzymywać wyskakujące powiadomienia o muzyka określonych grup.</span><span class="sxs-lookup"><span data-stu-id="467fd-116">The following example shows an application from which you can receive toast notifications about specific music groups.</span></span> <span data-ttu-id="467fd-117">W tym scenariuszu w prosty sposób powiadomienia trasy jest etykieta rejestracji przy użyciu tagów reprezentujących różne pasma, tak jak na poniższej ilustracji.</span><span class="sxs-lookup"><span data-stu-id="467fd-117">In this scenario, a simple way to route notifications is to label registrations with tags that represent the different bands, as in the following picture.</span></span>

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags.png)

<span data-ttu-id="467fd-118">Na tej ilustracji oznakowane komunikat **Beatles** osiągnie tylko tablet zarejestrowany w tagu **Beatles**.</span><span class="sxs-lookup"><span data-stu-id="467fd-118">In this picture, the message tagged **Beatles** reaches only the tablet that registered with the tag **Beatles**.</span></span>

<span data-ttu-id="467fd-119">Aby uzyskać więcej informacji o tworzeniu rejestracji dla tagów, zobacz [zarządzania rejestracji](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="467fd-119">For more information about creating registrations for tags, see [Registration Management](notification-hubs-push-notification-registration-management.md).</span></span>

<span data-ttu-id="467fd-120">Możesz wysłać powiadomienia do tagów za pomocą metod wysyłania powiadomień z `Microsoft.Azure.NotificationHubs.NotificationHubClient` klasy w [centra powiadomień Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="467fd-120">You can send notifications to tags using the send notifications methods of the `Microsoft.Azure.NotificationHubs.NotificationHubClient` class in the [Microsoft Azure Notification Hubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) SDK.</span></span> <span data-ttu-id="467fd-121">Można również użyć środowiska Node.js lub wypychanie powiadomień interfejsów API REST.</span><span class="sxs-lookup"><span data-stu-id="467fd-121">You can also use Node.js, or the Push Notifications REST APIs.</span></span>  <span data-ttu-id="467fd-122">Oto przykład przy użyciu zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="467fd-122">Here's an example using the SDK.</span></span>

    Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;

    // Windows 8.1 / Windows Phone 8.1
    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" +
    "You requested a Beatles notification</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, "Beatles");

    // Windows 10
    toast = @"<toast><visual><binding template=""ToastGeneric""><text id=""1"">" +
    "You requested a Wailers notification</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, "Wailers");




<span data-ttu-id="467fd-123">Tagów nie trzeba być wstępnie przygotowany i mogą odwoływać się do wielu pojęć specyficzny dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="467fd-123">Tags do not have to be pre-provisioned and can refer to multiple app-specific concepts.</span></span> <span data-ttu-id="467fd-124">Na przykład użytkownicy tej przykładowej aplikacji można dodać komentarz dotyczący przedziałów i chcesz otrzymywać wyskakujące powiadomienia, nie tylko dla komentarze dotyczące ich ulubionych pasma, ale dla komentarzy do wszystkich swoich znajomych, niezależnie od tego, poza pasmem, na którym są komentarzy.</span><span class="sxs-lookup"><span data-stu-id="467fd-124">For example, users of this example application can comment on bands and want to receive toasts, not only for the comments on their favorite bands, but also for all comments from their friends, regardless of the band on which they are commenting.</span></span> <span data-ttu-id="467fd-125">Na poniższej ilustracji przedstawiono przykład tego scenariusza:</span><span class="sxs-lookup"><span data-stu-id="467fd-125">The following picture shows an example of this scenario:</span></span>

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags2.png)

<span data-ttu-id="467fd-126">Na tej ilustracji Alicja jest zainteresowane w aktualizacjach dla Beatles i Robert jest zainteresowane w aktualizacjach dla Wailers.</span><span class="sxs-lookup"><span data-stu-id="467fd-126">In this picture, Alice is interested in updates for the Beatles, and Bob is interested in updates for the Wailers.</span></span> <span data-ttu-id="467fd-127">Robert jest również zainteresowana komentarze na marek i marek znajduje się w zainteresowani Wailers.</span><span class="sxs-lookup"><span data-stu-id="467fd-127">Bob is also interested in Charlie’s comments, and Charlie is in interested in the Wailers.</span></span> <span data-ttu-id="467fd-128">Jeśli powiadomienie jest wysyłane do firmy marek komentarz na Beatles, zarówno Alicja i Robert odebrane.</span><span class="sxs-lookup"><span data-stu-id="467fd-128">When a notification is sent for Charlie’s comment on the Beatles, both Alice and Bob receive it.</span></span>

<span data-ttu-id="467fd-129">Tagi może zakodować wiele problemów w tagów (na przykład "band_Beatles" lub "follows_Charlie"), są proste ciągów nie właściwości i wartości.</span><span class="sxs-lookup"><span data-stu-id="467fd-129">While you can encode multiple concerns in tags (for example, “band_Beatles” or “follows_Charlie”), tags are simple strings and not properties with values.</span></span> <span data-ttu-id="467fd-130">Rejestracja jest zgodny tylko w obecności lub braku konkretnego znacznika.</span><span class="sxs-lookup"><span data-stu-id="467fd-130">A registration is matched only on the presence or absence of a specific tag.</span></span>

<span data-ttu-id="467fd-131">Samouczek pełnej krok po kroku dotyczące sposobu użycia znaczników podczas wysyłania do grup zainteresowań, zobacz [fundamentalne wiadomości](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md).</span><span class="sxs-lookup"><span data-stu-id="467fd-131">For a full step-by-step tutorial on how to use tags for sending to interest groups, see [Breaking News](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md).</span></span>

## <a name="using-tags-to-target-users"></a><span data-ttu-id="467fd-132">Przy użyciu tagów użytkowników docelowych</span><span class="sxs-lookup"><span data-stu-id="467fd-132">Using tags to target users</span></span>
<span data-ttu-id="467fd-133">Innym sposobem użycia znaczników jest zidentyfikować wszystkie urządzenia określonego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="467fd-133">Another way to use tags is to identify all the devices of a particular user.</span></span> <span data-ttu-id="467fd-134">Rejestracje mogą być oznaczane tagu, który zawiera identyfikator użytkownika, tak jak na poniższej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="467fd-134">Registrations can be tagged with a tag that contains a user id, as in the following picture:</span></span>

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags3.png)

<span data-ttu-id="467fd-135">Na tej ilustracji uid:Alice oznakowane wiadomość osiągnie wszystkich uid:Alice oznakowanych rejestracji; w związku z tym wszystkie urządzenia Alicji.</span><span class="sxs-lookup"><span data-stu-id="467fd-135">In this picture, the message tagged uid:Alice reaches all registrations tagged uid:Alice; hence, all of Alice’s devices.</span></span>

## <a name="tag-expressions"></a><span data-ttu-id="467fd-136">Wyrażeń tagów</span><span class="sxs-lookup"><span data-stu-id="467fd-136">Tag expressions</span></span>
<span data-ttu-id="467fd-137">Istnieją przypadki, w których powiadomienie ma docelowy zestaw rejestracji, który jest identyfikowany nie przez jeden tag, ale przez wyrażenie logiczne w tagach.</span><span class="sxs-lookup"><span data-stu-id="467fd-137">There are cases in which a notification has to target a set of registrations that is identified not by a single tag, but by a Boolean expression on tags.</span></span>

<span data-ttu-id="467fd-138">Należy wziąć pod uwagę aplikacji sportowych, która wysyła przypomnienie wszystkim Boston o gry między czerwony Sox i Cardinals.</span><span class="sxs-lookup"><span data-stu-id="467fd-138">Consider a sports application that sends a reminder to everyone in Boston about a game between the Red Sox and Cardinals.</span></span> <span data-ttu-id="467fd-139">Jeśli aplikacja kliencka rejestruje tagi o zainteresowanie zespołów i lokalizacji, powiadomienia mają być uwzględniani wszystkim Boston chcący Sox czerwony lub Cardinals.</span><span class="sxs-lookup"><span data-stu-id="467fd-139">If the client app registers tags about interest in teams and location, then the notification should be targeted to everyone in Boston who is interested in either the Red Sox or the Cardinals.</span></span> <span data-ttu-id="467fd-140">Ten warunek może zostać wyrażona z następującym wyrażeniem logiczna:</span><span class="sxs-lookup"><span data-stu-id="467fd-140">This condition can be expressed with the following Boolean expression:</span></span>

    (follows_RedSox || follows_Cardinals) && location_Boston


![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags4.png)

<span data-ttu-id="467fd-141">Wyrażeń tagów może zawierać wszystkich operatorów logicznych, takich jak AND (& &), lub (|), a nie (!).</span><span class="sxs-lookup"><span data-stu-id="467fd-141">Tag expressions can contain all Boolean operators, such as AND (&&), OR (||), and NOT (!).</span></span> <span data-ttu-id="467fd-142">Może również zawierać nawiasów.</span><span class="sxs-lookup"><span data-stu-id="467fd-142">They can also contain parentheses.</span></span> <span data-ttu-id="467fd-143">Wyrażeń tagów jest ograniczona do 20 znaczników, jeśli zawierają one tylko ORs; w przeciwnym razie są one ograniczone do 6 tagów.</span><span class="sxs-lookup"><span data-stu-id="467fd-143">Tag expressions are limited to 20 tags if they contain only ORs; otherwise they are limited to 6 tags.</span></span>

<span data-ttu-id="467fd-144">Oto przykład wysyłania powiadomień przy użyciu wyrażeń tagów za pomocą zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="467fd-144">Here's an example for sending notifications with tag expressions using the SDK.</span></span>

    Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;

    String userTag = "(location_Boston && !follows_Cardinals)";    

    // Windows 8.1 / Windows Phone 8.1
    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" +
    "You want info on the Red Socks</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);

    // Windows 10
    toast = @"<toast><visual><binding template=""ToastGeneric""><text id=""1"">" +
    "You want info on the Red Socks</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);
