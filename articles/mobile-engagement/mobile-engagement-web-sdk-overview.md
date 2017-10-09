---
title: "Omówienie zestawu SDK sieci Web usługi Engagement Mobile aaaAzure | Dokumentacja firmy Microsoft"
description: "Witaj najnowsze aktualizacje i procedury dotyczące hello zestawu SDK sieci Web dla usługi Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 5bbc2fda-0f3f-43d0-a73d-0f2c0f8dc25b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 10/18/2016
ms.author: piyushjo
ms.openlocfilehash: 9e60a232b5eb2c41c405041a88e09d7137563513
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-web-sdk"></a><span data-ttu-id="9d593-103">Sieci Web usługi Azure Mobile Engagement SDK</span><span class="sxs-lookup"><span data-stu-id="9d593-103">Azure Mobile Engagement Web SDK</span></span>
<span data-ttu-id="9d593-104">Szybki Start dla wszystkich hello szczegółowe informacje na temat toointegrate usługi Azure Mobile Engagement w aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="9d593-104">Start here for all hello details about how toointegrate Azure Mobile Engagement in a web app.</span></span> <span data-ttu-id="9d593-105">Jeśli chcesz toogive go try przed rozpoczęciem pracy z własnych aplikacji sieci web, zobacz nasze [samouczek 15 minut](mobile-engagement-web-app-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="9d593-105">If you'd like toogive it a try before getting started with your own web app, see our [15-minute tutorial](mobile-engagement-web-app-get-started.md).</span></span>

## <a name="integration-procedures"></a><span data-ttu-id="9d593-106">Procedury integracji</span><span class="sxs-lookup"><span data-stu-id="9d593-106">Integration procedures</span></span>
1. <span data-ttu-id="9d593-107">Dowiedz się [jak toointegrate Mobile Engagement w aplikacji sieci web](mobile-engagement-web-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="9d593-107">Learn [how toointegrate Mobile Engagement in your web app](mobile-engagement-web-integrate-engagement.md).</span></span>
2. <span data-ttu-id="9d593-108">Tag planu wykonania, Dowiedz się [jak toouse hello zaawansowane znakowanie interfejsu API w aplikacji sieci web usługi Mobile Engagement](mobile-engagement-web-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="9d593-108">For tag plan implementation, learn [how toouse hello advanced Mobile Engagement tagging API in your web app](mobile-engagement-web-use-engagement-api.md).</span></span>

## <a name="release-notes"></a><span data-ttu-id="9d593-109">Informacje o wersji</span><span class="sxs-lookup"><span data-stu-id="9d593-109">Release notes</span></span>
### <a name="202-10182016"></a><span data-ttu-id="9d593-110">2.0.2 (10/18/2016)</span><span class="sxs-lookup"><span data-stu-id="9d593-110">2.0.2 (10/18/2016)</span></span>
* <span data-ttu-id="9d593-111">Stałe awarii na InPrivate (Safari).</span><span class="sxs-lookup"><span data-stu-id="9d593-111">Fixed crash on private browsing (Safari).</span></span>
* <span data-ttu-id="9d593-112">Stałe awarii w przeglądarkach plików cookie jest wyłączona.</span><span class="sxs-lookup"><span data-stu-id="9d593-112">Fixed crash on browsers with cookies disabled.</span></span>

<span data-ttu-id="9d593-113">Wszystkie wersje, zobacz hello [ukończyć wersji](mobile-engagement-web-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="9d593-113">For all versions, please see hello [complete release notes](mobile-engagement-web-release-notes.md).</span></span>

## <a name="upgrade-procedures"></a><span data-ttu-id="9d593-114">Procedury uaktualniania</span><span class="sxs-lookup"><span data-stu-id="9d593-114">Upgrade procedures</span></span>
### <a name="upgrade-from-121-too200"></a><span data-ttu-id="9d593-115">Uaktualnienie z wersji 1.2.1 too2.0.0</span><span class="sxs-lookup"><span data-stu-id="9d593-115">Upgrade from 1.2.1 too2.0.0</span></span>
<span data-ttu-id="9d593-116">Witaj poniższych sekcjach opisano sposób toomigrate zestaw SDK usługi Mobile Engagement w sieci Web integracji z usługą Capptain hello, oferowane przez Capptain SAS, tooan aplikacji usługi Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="9d593-116">hello following sections describe how toomigrate a Mobile Engagement Web SDK integration from hello Capptain service, offered by Capptain SAS, tooan Azure Mobile Engagement app.</span></span> <span data-ttu-id="9d593-117">W przypadku migracji z wersji starszej niż 1.2.1, należy najpierw zapoznać się hello Capptain witryny sieci Web toomigrate too1.2.1, a następnie Zastosuj hello zgodnie z procedurami.</span><span class="sxs-lookup"><span data-stu-id="9d593-117">If you are migrating from a version earlier than 1.2.1, please consult hello Capptain website toomigrate too1.2.1 first, and then apply hello following procedures.</span></span>

<span data-ttu-id="9d593-118">Ta wersja hello zestaw SDK usługi Mobile Engagement w sieci Web nie obsługuje Samsung inteligentne TV, Opera TV, webOS lub hello Reach funkcji.</span><span class="sxs-lookup"><span data-stu-id="9d593-118">This version of hello Mobile Engagement Web SDK doesn't support Samsung Smart TV, Opera TV, webOS, or hello Reach feature.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9d593-119">Capptain i usługi Azure Mobile Engagement nie hello tę samą usługę, a hello zgodnie z procedurami zaznacz tylko sposób toomigrate hello aplikacji klienckiej.</span><span class="sxs-lookup"><span data-stu-id="9d593-119">Capptain and Azure Mobile Engagement are not hello same service, and hello following procedures highlight only how toomigrate hello client app.</span></span> <span data-ttu-id="9d593-120">Migrowanie hello zestaw SDK usługi Mobile Engagement w sieci Web w aplikacji hello nie będą migrowane dane z serwera usługi Mobile Engagement tooa Capptain serwera.</span><span class="sxs-lookup"><span data-stu-id="9d593-120">Migrating hello Mobile Engagement Web SDK in hello app will not migrate your data from a Capptain server tooa Mobile Engagement server.</span></span>
> 
> 

#### <a name="javascript-files"></a><span data-ttu-id="9d593-121">Pliki JavaScript</span><span class="sxs-lookup"><span data-stu-id="9d593-121">JavaScript files</span></span>
<span data-ttu-id="9d593-122">Zastąp plik hello capptain-sdk.js pliku hello azure-engagement.js, a następnie zaktualizować skrypt importuje odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="9d593-122">Replace hello file capptain-sdk.js with hello file azure-engagement.js, and then update your script imports accordingly.</span></span>

#### <a name="remove-capptain-reach"></a><span data-ttu-id="9d593-123">Usuń Capptain Reach</span><span class="sxs-lookup"><span data-stu-id="9d593-123">Remove Capptain Reach</span></span>
<span data-ttu-id="9d593-124">Ta wersja hello zestaw SDK usługi Mobile Engagement w sieci Web nie obsługuje funkcji Reach hello.</span><span class="sxs-lookup"><span data-stu-id="9d593-124">This version of hello Mobile Engagement Web SDK doesn't support hello Reach feature.</span></span> <span data-ttu-id="9d593-125">Jest zintegrowany Capptain Reach do aplikacji, konieczne będzie tooremove go.</span><span class="sxs-lookup"><span data-stu-id="9d593-125">If you have integrated Capptain Reach into your application, you need tooremove it.</span></span>

<span data-ttu-id="9d593-126">Usuń import osiągnąć CSS hello ze strony użytkownika i spróbuj usunąć plik .css powiązane hello (capptain-reach.css, domyślnie).</span><span class="sxs-lookup"><span data-stu-id="9d593-126">Remove hello Reach CSS import from your page and delete hello related .css file (capptain-reach.css, by default).</span></span>

<span data-ttu-id="9d593-127">Usuń następujące zasoby Reach hello: hello Zamknij obrazu (capptain-close.png, domyślnie) i hello brand ikona (capptain powiadomienia-, domyślnie).</span><span class="sxs-lookup"><span data-stu-id="9d593-127">Delete hello following Reach resources: hello close image (capptain-close.png, by default) and hello brand icon (capptain-notification-icon, by default).</span></span>

<span data-ttu-id="9d593-128">Usuń hello osiągnąć interfejsu użytkownika dla powiadomień w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9d593-128">Remove hello Reach UI for in-app notifications.</span></span> <span data-ttu-id="9d593-129">Układ domyślny Hello wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="9d593-129">hello default layout looks like this:</span></span>

    <!-- capptain notification -->
    <div id="capptain_notification_area" class="capptain_category_default">
      <div class="icon">
        <img src="capptain-notification-icon.png" alt="icon" />
      </div>
      <div class="content">
        <div class="title" id="capptain_notification_title"></div>
        <div class="message" id="capptain_notification_message"></div>
      </div>
      <div id="capptain_notification_image"></div>
      <div>
        <button id="capptain_notification_close">Close</button>
      </div>
    </div>

<span data-ttu-id="9d593-130">Usuń hello osiągnąć interfejsu użytkownika dla sieci web i tekst anonsów i sond.</span><span class="sxs-lookup"><span data-stu-id="9d593-130">Remove hello Reach UI for text and web announcements and polls.</span></span> <span data-ttu-id="9d593-131">Układ domyślny Hello wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="9d593-131">hello default layout looks like this:</span></span>

    <div id="capptain_overlay" class="capptain_category_default">
      <button id="capptain_overlay_close">x</button>
      <div id="capptain_overlay_title"></div>
      <div id="capptain_overlay_body"></div>
      <div id="capptain_overlay_poll"></div>
      <div id="capptain_overlay_buttons">
        <button id="capptain_overlay_exit"></button>
        <button id="capptain_overlay_action"></button>
      </div>
    </div>

<span data-ttu-id="9d593-132">Usuń hello `reach` obiekt z konfiguracji, jeśli istnieje.</span><span class="sxs-lookup"><span data-stu-id="9d593-132">Remove hello `reach` object from your configuration, if it exists.</span></span> <span data-ttu-id="9d593-133">Wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="9d593-133">It looks like this:</span></span>

    window.capptain = {
      [...]
      reach: {
        [...]
      }
    }

<span data-ttu-id="9d593-134">Usuń wszelkie inne dostosowania Reach, takich jak kategorii.</span><span class="sxs-lookup"><span data-stu-id="9d593-134">Remove any other Reach customization, such as categories.</span></span>

#### <a name="remove-deprecated-apis"></a><span data-ttu-id="9d593-135">Usuń przestarzałe interfejsy API</span><span class="sxs-lookup"><span data-stu-id="9d593-135">Remove deprecated APIs</span></span>
<span data-ttu-id="9d593-136">Niektóre funkcje interfejsu API z Capptain są używane w hello zestaw SDK usługi Mobile Engagement w sieci Web.</span><span class="sxs-lookup"><span data-stu-id="9d593-136">Some APIs from Capptain are deprecated in hello Mobile Engagement Web SDK.</span></span>

<span data-ttu-id="9d593-137">Usuń wszelkie toohello wywołania następujące interfejsy API: `agent.connect`, `agent.disconnect`, `agent.pause`, i `agent.sendMessageToDevice`.</span><span class="sxs-lookup"><span data-stu-id="9d593-137">Remove any calls toohello following APIs: `agent.connect`, `agent.disconnect`, `agent.pause`, and `agent.sendMessageToDevice`.</span></span>

<span data-ttu-id="9d593-138">Usuń wszystkie hello poniższych wywołań zwrotnych z konfiguracji Capptain: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, i `onPushMessageReceived`.</span><span class="sxs-lookup"><span data-stu-id="9d593-138">Remove any of hello following callbacks from your Capptain configuration: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, and `onPushMessageReceived`.</span></span>

#### <a name="configuration"></a><span data-ttu-id="9d593-139">Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="9d593-139">Configuration</span></span>
<span data-ttu-id="9d593-140">Połączenie tooconfigure SDK identyfikatory ciągów, na przykład identyfikator aplikacji hello korzysta z usługi Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="9d593-140">Mobile Engagement uses a connection string tooconfigure SDK identifiers, for example, hello application identifier.</span></span>

<span data-ttu-id="9d593-141">Zastąp identyfikator aplikacji hello parametrów połączenia.</span><span class="sxs-lookup"><span data-stu-id="9d593-141">Replace hello application ID with your connection string.</span></span> <span data-ttu-id="9d593-142">Należy zwrócić uwagę hello obiektu globalnego dla hello konfiguracji SDK zmieni się z `capptain` zbyt`azureEngagement`.</span><span class="sxs-lookup"><span data-stu-id="9d593-142">Note that hello global object for hello SDK configuration changes from `capptain` too`azureEngagement`.</span></span>

<span data-ttu-id="9d593-143">Przed migracją:</span><span class="sxs-lookup"><span data-stu-id="9d593-143">Before migration:</span></span>

    window.capptain = {
      appId: ...,
      [...]
    };

<span data-ttu-id="9d593-144">Po zakończeniu migracji:</span><span class="sxs-lookup"><span data-stu-id="9d593-144">After migration:</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      [...]
    };

<span data-ttu-id="9d593-145">Parametry połączenia Hello aplikacji jest wyświetlany w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="9d593-145">hello connection string for your application is displayed in hello Azure portal.</span></span>

#### <a name="javascript-apis"></a><span data-ttu-id="9d593-146">Interfejsy API języka JavaScript</span><span class="sxs-lookup"><span data-stu-id="9d593-146">JavaScript APIs</span></span>
<span data-ttu-id="9d593-147">Obiekt global JavaScript Hello `window.capptain` została zmieniona `window.azureEngagement`, ale można użyć hello `window.engagement` alias dla interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="9d593-147">hello global JavaScript object `window.capptain` has been renamed `window.azureEngagement`, but you can use hello `window.engagement` alias for API calls.</span></span> <span data-ttu-id="9d593-148">Nie można użyć tego aliasu toodefine hello SDK konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="9d593-148">You can't use this alias toodefine hello SDK configuration.</span></span>

<span data-ttu-id="9d593-149">Na przykład `capptain.deviceId` staje się `engagement.deviceId`, `capptain.agent.startActivity` staje się `engagement.agent.startActivity`i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="9d593-149">For instance, `capptain.deviceId` becomes `engagement.deviceId`, `capptain.agent.startActivity` becomes `engagement.agent.startActivity`, and so on.</span></span>

<span data-ttu-id="9d593-150">Jeśli zintegrowano już program wcześniejszej wersji hello zestaw SDK usługi Azure Mobile Engagement w sieci Web do aplikacji, przeczytaj informacje o [procedur uaktualniania](mobile-engagement-web-upgrade-procedure.md).</span><span class="sxs-lookup"><span data-stu-id="9d593-150">If you have already integrated an earlier version of hello Azure Mobile Engagement Web SDK into your application, please read about [upgrade procedures](mobile-engagement-web-upgrade-procedure.md).</span></span>

