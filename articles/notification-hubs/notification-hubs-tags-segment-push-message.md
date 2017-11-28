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
# <a name="routing-and-tag-expressions"></a><span data-ttu-id="19a5f-103">Wyrażenia routingu i tagów</span><span class="sxs-lookup"><span data-stu-id="19a5f-103">Routing and tag expressions</span></span>
## <a name="overview"></a><span data-ttu-id="19a5f-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="19a5f-104">Overview</span></span>
<span data-ttu-id="19a5f-105">Wyrażeń tagów Włącz tootarget określonych zestawów urządzeń lub dokładniej rejestracji podczas wysyłania powiadomień wypychanych przy użyciu usługi Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="19a5f-105">Tag expressions enable you tootarget specific sets of devices, or more specifically registrations, when sending a push notification through Notification Hubs.</span></span>

## <a name="targeting-specific-registrations"></a><span data-ttu-id="19a5f-106">Przeznaczonych dla określonych rejestracji</span><span class="sxs-lookup"><span data-stu-id="19a5f-106">Targeting specific registrations</span></span>
<span data-ttu-id="19a5f-107">Witaj tylko sposób tootarget określonych powiadomienia rejestracji jest tagi tooassociate za ich pomocą skierować tych tagów.</span><span class="sxs-lookup"><span data-stu-id="19a5f-107">hello only way tootarget specific notification registrations is tooassociate tags with them, then target those tags.</span></span> <span data-ttu-id="19a5f-108">Zgodnie z opisem w [zarządzania rejestracji](notification-hubs-push-notification-registration-management.md), w kolejności tooreceive wypychania powiadomień aplikacja ma tooregister urządzenia jest obsługiwana w Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="19a5f-108">As discussed in [Registration Management](notification-hubs-push-notification-registration-management.md), in order tooreceive push notifications an app has tooregister a device handle on a notification hub.</span></span> <span data-ttu-id="19a5f-109">Po utworzeniu rejestracji w Centrum powiadomień aplikacji hello wewnętrznej bazy danych można wysyłać tooit powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="19a5f-109">Once a registration is created on a notification hub, hello application backend can send push notifications tooit.</span></span>
<span data-ttu-id="19a5f-110">zaplecza aplikacji Hello można wybrać hello tootarget rejestracje z określonych powiadomień w hello następujące sposoby:</span><span class="sxs-lookup"><span data-stu-id="19a5f-110">hello application backend can choose hello registrations tootarget with a specific notification in hello following ways:</span></span>

1. <span data-ttu-id="19a5f-111">**Emisji**: wszystkich rejestracji w Centrum powiadomień hello hello powiadomienie.</span><span class="sxs-lookup"><span data-stu-id="19a5f-111">**Broadcast**: all registrations in hello notification hub receive hello notification.</span></span>
2. <span data-ttu-id="19a5f-112">**Tag**: wszystkie rejestracji, które zawierają hello określony tag hello powiadomienie.</span><span class="sxs-lookup"><span data-stu-id="19a5f-112">**Tag**: all registrations that contain hello specified tag receive hello notification.</span></span>
3. <span data-ttu-id="19a5f-113">**Tag wyrażenie**: wszystkich rejestracji, którego zestawu tagów dopasowania hello określone wyrażenie hello powiadomienie.</span><span class="sxs-lookup"><span data-stu-id="19a5f-113">**Tag expression**: all registrations whose set of tags match hello specified expression receive hello notification.</span></span>

## <a name="tags"></a><span data-ttu-id="19a5f-114">Tagi</span><span class="sxs-lookup"><span data-stu-id="19a5f-114">Tags</span></span>
<span data-ttu-id="19a5f-115">Znacznik może być dowolny ciąg w górę too120 znaków, alfanumeryczne i hello następujących znaków innych niż alfanumeryczne: "_", "@", "#", ".",":", "-".</span><span class="sxs-lookup"><span data-stu-id="19a5f-115">A tag can be any string, up too120 characters, containing alphanumeric and hello following non-alphanumeric characters: ‘_’, ‘@’, ‘#’, ‘.’, ‘:’, ‘-’.</span></span> <span data-ttu-id="19a5f-116">Witaj poniższy przykład przedstawia aplikacji, z którego może otrzymywać wyskakujące powiadomienia o muzyka określonych grup.</span><span class="sxs-lookup"><span data-stu-id="19a5f-116">hello following example shows an application from which you can receive toast notifications about specific music groups.</span></span> <span data-ttu-id="19a5f-117">W tym scenariuszu powiadomienia tooroute prosty sposób jest toolabel rejestracji przy użyciu tagów reprezentujących różne pasma hello, tak jak hello poniższej ilustracji.</span><span class="sxs-lookup"><span data-stu-id="19a5f-117">In this scenario, a simple way tooroute notifications is toolabel registrations with tags that represent hello different bands, as in hello following picture.</span></span>

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags.png)

<span data-ttu-id="19a5f-118">Na tej ilustracji oznakowane wiadomość hello **Beatles** osiągnie tylko hello tablet zarejestrowana z tagiem hello **Beatles**.</span><span class="sxs-lookup"><span data-stu-id="19a5f-118">In this picture, hello message tagged **Beatles** reaches only hello tablet that registered with hello tag **Beatles**.</span></span>

<span data-ttu-id="19a5f-119">Aby uzyskać więcej informacji o tworzeniu rejestracji dla tagów, zobacz [zarządzania rejestracji](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="19a5f-119">For more information about creating registrations for tags, see [Registration Management](notification-hubs-push-notification-registration-management.md).</span></span>

<span data-ttu-id="19a5f-120">Możesz wysłać tootags powiadomienia za pomocą hello wysyłania powiadomień metody hello `Microsoft.Azure.NotificationHubs.NotificationHubClient` klasy w hello [centra powiadomień Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="19a5f-120">You can send notifications tootags using hello send notifications methods of hello `Microsoft.Azure.NotificationHubs.NotificationHubClient` class in hello [Microsoft Azure Notification Hubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) SDK.</span></span> <span data-ttu-id="19a5f-121">Można również użyć środowiska Node.js lub hello wypychanie powiadomień interfejsów API REST.</span><span class="sxs-lookup"><span data-stu-id="19a5f-121">You can also use Node.js, or hello Push Notifications REST APIs.</span></span>  <span data-ttu-id="19a5f-122">Oto przykład przy użyciu hello zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="19a5f-122">Here's an example using hello SDK.</span></span>

    Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;

    // Windows 8.1 / Windows Phone 8.1
    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" +
    "You requested a Beatles notification</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, "Beatles");

    // Windows 10
    toast = @"<toast><visual><binding template=""ToastGeneric""><text id=""1"">" +
    "You requested a Wailers notification</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, "Wailers");




<span data-ttu-id="19a5f-123">Tagi nie ma wstępnie tworzyć toobe i może odnosić się toomultiple pojęcia specyficzny dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="19a5f-123">Tags do not have toobe pre-provisioned and can refer toomultiple app-specific concepts.</span></span> <span data-ttu-id="19a5f-124">Na przykład użytkownicy tej przykładowej aplikacji można dodać komentarz dotyczący przedziałów i mają tooreceive wyskakujące powiadomienia, nie tylko dla hello komentarze dotyczące ich ulubionych pasma, ale także dla wszystkich komentarzy z swoich znajomych, niezależnie od ich komentowania pasmem hello.</span><span class="sxs-lookup"><span data-stu-id="19a5f-124">For example, users of this example application can comment on bands and want tooreceive toasts, not only for hello comments on their favorite bands, but also for all comments from their friends, regardless of hello band on which they are commenting.</span></span> <span data-ttu-id="19a5f-125">Witaj, na poniższej ilustracji przedstawiono przykład tego scenariusza:</span><span class="sxs-lookup"><span data-stu-id="19a5f-125">hello following picture shows an example of this scenario:</span></span>

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags2.png)

<span data-ttu-id="19a5f-126">Na tej ilustracji Alicja jest zainteresowane w aktualizacjach dla hello Beatles i Robert jest zainteresowane w aktualizacjach dla hello Wailers.</span><span class="sxs-lookup"><span data-stu-id="19a5f-126">In this picture, Alice is interested in updates for hello Beatles, and Bob is interested in updates for hello Wailers.</span></span> <span data-ttu-id="19a5f-127">Robert jest również zainteresowana komentarze na marek i marek znajduje się w zainteresowani hello Wailers.</span><span class="sxs-lookup"><span data-stu-id="19a5f-127">Bob is also interested in Charlie’s comments, and Charlie is in interested in hello Wailers.</span></span> <span data-ttu-id="19a5f-128">Jeśli powiadomienie jest wysyłane do firmy marek komentarz na powitania Beatles, zarówno Alicja i Robert odebrane.</span><span class="sxs-lookup"><span data-stu-id="19a5f-128">When a notification is sent for Charlie’s comment on hello Beatles, both Alice and Bob receive it.</span></span>

<span data-ttu-id="19a5f-129">Tagi może zakodować wiele problemów w tagów (na przykład "band_Beatles" lub "follows_Charlie"), są proste ciągów nie właściwości i wartości.</span><span class="sxs-lookup"><span data-stu-id="19a5f-129">While you can encode multiple concerns in tags (for example, “band_Beatles” or “follows_Charlie”), tags are simple strings and not properties with values.</span></span> <span data-ttu-id="19a5f-130">Rejestracja jest zgodny tylko na powitania obecności lub braku konkretnego znacznika.</span><span class="sxs-lookup"><span data-stu-id="19a5f-130">A registration is matched only on hello presence or absence of a specific tag.</span></span>

<span data-ttu-id="19a5f-131">Pełne krok samouczek dotyczący jak toouse tagów do wysyłania toointerest grup, zobacz [fundamentalne wiadomości](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md).</span><span class="sxs-lookup"><span data-stu-id="19a5f-131">For a full step-by-step tutorial on how toouse tags for sending toointerest groups, see [Breaking News](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md).</span></span>

## <a name="using-tags-tootarget-users"></a><span data-ttu-id="19a5f-132">Za pomocą tagów tootarget użytkowników</span><span class="sxs-lookup"><span data-stu-id="19a5f-132">Using tags tootarget users</span></span>
<span data-ttu-id="19a5f-133">Inny sposób toouse tagów jest tooidentify wszystkie urządzenia hello określonego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="19a5f-133">Another way toouse tags is tooidentify all hello devices of a particular user.</span></span> <span data-ttu-id="19a5f-134">Rejestracje mogą być oznaczane tagu, który zawiera identyfikator użytkownika, tak jak na poniższej ilustracji hello:</span><span class="sxs-lookup"><span data-stu-id="19a5f-134">Registrations can be tagged with a tag that contains a user id, as in hello following picture:</span></span>

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags3.png)

<span data-ttu-id="19a5f-135">Na tej ilustracji uid:Alice oznakowane wiadomość hello osiągnie wszystkich uid:Alice oznakowanych rejestracji; w związku z tym wszystkie urządzenia Alicji.</span><span class="sxs-lookup"><span data-stu-id="19a5f-135">In this picture, hello message tagged uid:Alice reaches all registrations tagged uid:Alice; hence, all of Alice’s devices.</span></span>

## <a name="tag-expressions"></a><span data-ttu-id="19a5f-136">Wyrażeń tagów</span><span class="sxs-lookup"><span data-stu-id="19a5f-136">Tag expressions</span></span>
<span data-ttu-id="19a5f-137">Istnieją przypadki, w których powiadomienie ma tootarget zestaw rejestracji, który jest identyfikowany nie przez jeden tag, ale przez wyrażenie logiczne w tagach.</span><span class="sxs-lookup"><span data-stu-id="19a5f-137">There are cases in which a notification has tootarget a set of registrations that is identified not by a single tag, but by a Boolean expression on tags.</span></span>

<span data-ttu-id="19a5f-138">Należy wziąć pod uwagę aplikacji sportowych, która wysyła tooeveryone monitu w Boston o gry między hello czerwony Sox i Cardinals.</span><span class="sxs-lookup"><span data-stu-id="19a5f-138">Consider a sports application that sends a reminder tooeveryone in Boston about a game between hello Red Sox and Cardinals.</span></span> <span data-ttu-id="19a5f-139">Jeśli aplikacja kliencka hello rejestruje tagi o zainteresowanie zespołów i lokalizacji, hello powiadomień należy tooeveryone docelowych w Boston chcący Sox czerwony hello lub hello Cardinals.</span><span class="sxs-lookup"><span data-stu-id="19a5f-139">If hello client app registers tags about interest in teams and location, then hello notification should be targeted tooeveryone in Boston who is interested in either hello Red Sox or hello Cardinals.</span></span> <span data-ttu-id="19a5f-140">Ten warunek może zostać wyrażona z hello następującego wyrażenia logicznego:</span><span class="sxs-lookup"><span data-stu-id="19a5f-140">This condition can be expressed with hello following Boolean expression:</span></span>

    (follows_RedSox || follows_Cardinals) && location_Boston


![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags4.png)

<span data-ttu-id="19a5f-141">Wyrażeń tagów może zawierać wszystkich operatorów logicznych, takich jak AND (& &), lub (|), a nie (!).</span><span class="sxs-lookup"><span data-stu-id="19a5f-141">Tag expressions can contain all Boolean operators, such as AND (&&), OR (||), and NOT (!).</span></span> <span data-ttu-id="19a5f-142">Może również zawierać nawiasów.</span><span class="sxs-lookup"><span data-stu-id="19a5f-142">They can also contain parentheses.</span></span> <span data-ttu-id="19a5f-143">Wyrażeń tagów są ograniczone too20 znaczników, jeśli zawierają one tylko ORs; w przeciwnym razie są one ograniczone too6 tagów.</span><span class="sxs-lookup"><span data-stu-id="19a5f-143">Tag expressions are limited too20 tags if they contain only ORs; otherwise they are limited too6 tags.</span></span>

<span data-ttu-id="19a5f-144">Oto przykład wysyłania powiadomień za pomocą wyrażeń tag przy użyciu hello zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="19a5f-144">Here's an example for sending notifications with tag expressions using hello SDK.</span></span>

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
