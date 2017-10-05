---
title: "Omówienie zestawu SDK sieci Web usługi Azure Mobile Engagement | Dokumentacja firmy Microsoft"
description: "Najnowsze aktualizacje i procedury dotyczące zestawu SDK sieci Web dla usługi Azure Mobile Engagement"
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
ms.openlocfilehash: 770a83131a3e661771db50b22ce7de25b2d541cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-mobile-engagement-web-sdk"></a><span data-ttu-id="a6ab6-103">Sieci Web usługi Azure Mobile Engagement SDK</span><span class="sxs-lookup"><span data-stu-id="a6ab6-103">Azure Mobile Engagement Web SDK</span></span>
<span data-ttu-id="a6ab6-104">Szczegółowe informacje dotyczące sposobu integracji usługi Azure Mobile Engagement w aplikacji sieci web, zacznij tutaj.</span><span class="sxs-lookup"><span data-stu-id="a6ab6-104">Start here for all the details about how to integrate Azure Mobile Engagement in a web app.</span></span> <span data-ttu-id="a6ab6-105">Jeśli chcesz go wypróbować przed rozpoczęciem pracy z aplikacją sieci web, zobacz nasze [samouczek 15 minut](mobile-engagement-web-app-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a6ab6-105">If you'd like to give it a try before getting started with your own web app, see our [15-minute tutorial](mobile-engagement-web-app-get-started.md).</span></span>

## <a name="integration-procedures"></a><span data-ttu-id="a6ab6-106">Procedury integracji</span><span class="sxs-lookup"><span data-stu-id="a6ab6-106">Integration procedures</span></span>
1. <span data-ttu-id="a6ab6-107">Dowiedz się [jak zintegrowana usługa Mobile Engagement w aplikacji sieci web](mobile-engagement-web-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="a6ab6-107">Learn [how to integrate Mobile Engagement in your web app](mobile-engagement-web-integrate-engagement.md).</span></span>
2. <span data-ttu-id="a6ab6-108">Tag planu wykonania, Dowiedz się [sposobu korzystania z zaawansowanych Mobile Engagement znakowanie interfejsu API w aplikacji sieci web](mobile-engagement-web-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="a6ab6-108">For tag plan implementation, learn [how to use the advanced Mobile Engagement tagging API in your web app](mobile-engagement-web-use-engagement-api.md).</span></span>

## <a name="release-notes"></a><span data-ttu-id="a6ab6-109">Informacje o wersji</span><span class="sxs-lookup"><span data-stu-id="a6ab6-109">Release notes</span></span>
### <a name="202-10182016"></a><span data-ttu-id="a6ab6-110">2.0.2 (10/18/2016)</span><span class="sxs-lookup"><span data-stu-id="a6ab6-110">2.0.2 (10/18/2016)</span></span>
* <span data-ttu-id="a6ab6-111">Stałe awarii na InPrivate (Safari).</span><span class="sxs-lookup"><span data-stu-id="a6ab6-111">Fixed crash on private browsing (Safari).</span></span>
* <span data-ttu-id="a6ab6-112">Stałe awarii w przeglądarkach plików cookie jest wyłączona.</span><span class="sxs-lookup"><span data-stu-id="a6ab6-112">Fixed crash on browsers with cookies disabled.</span></span>

<span data-ttu-id="a6ab6-113">Wszystkie wersje, zobacz [ukończyć wersji](mobile-engagement-web-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="a6ab6-113">For all versions, please see the [complete release notes](mobile-engagement-web-release-notes.md).</span></span>

## <a name="upgrade-procedures"></a><span data-ttu-id="a6ab6-114">Procedury uaktualniania</span><span class="sxs-lookup"><span data-stu-id="a6ab6-114">Upgrade procedures</span></span>
### <a name="upgrade-from-121-to-200"></a><span data-ttu-id="a6ab6-115">Uaktualnienie z wersji 1.2.1 do 2.0.0</span><span class="sxs-lookup"><span data-stu-id="a6ab6-115">Upgrade from 1.2.1 to 2.0.0</span></span>
<span data-ttu-id="a6ab6-116">W poniższych sekcjach opisano sposób migracji integracji zestaw SDK usługi Mobile Engagement w sieci Web w usłudze Capptain oferowanych przez Capptain SAS, aplikację usługi Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="a6ab6-116">The following sections describe how to migrate a Mobile Engagement Web SDK integration from the Capptain service, offered by Capptain SAS, to an Azure Mobile Engagement app.</span></span> <span data-ttu-id="a6ab6-117">W przypadku migracji z wersji starszej niż 1.2.1, zajrzyj do witryny sieci Web Capptain, aby przeprowadzić migrację do wersji 1.2.1, a następnie zastosuj poniższe procedury.</span><span class="sxs-lookup"><span data-stu-id="a6ab6-117">If you are migrating from a version earlier than 1.2.1, please consult the Capptain website to migrate to 1.2.1 first, and then apply the following procedures.</span></span>

<span data-ttu-id="a6ab6-118">Ta wersja zestaw SDK usługi Mobile Engagement w sieci Web nie obsługuje Samsung inteligentne TV, Opera TV, webOS lub funkcji Reach.</span><span class="sxs-lookup"><span data-stu-id="a6ab6-118">This version of the Mobile Engagement Web SDK doesn't support Samsung Smart TV, Opera TV, webOS, or the Reach feature.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a6ab6-119">Capptain i usługi Azure Mobile Engagement nie są tej samej usługi, oraz poniższych procedur zaznacz tylko sposób migracji aplikacji klienckiej.</span><span class="sxs-lookup"><span data-stu-id="a6ab6-119">Capptain and Azure Mobile Engagement are not the same service, and the following procedures highlight only how to migrate the client app.</span></span> <span data-ttu-id="a6ab6-120">Migrowanie Mobile Engagement Web SDK w aplikacji nie będą migrowane dane z serwera Capptain na serwerze usługi Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="a6ab6-120">Migrating the Mobile Engagement Web SDK in the app will not migrate your data from a Capptain server to a Mobile Engagement server.</span></span>
> 
> 

#### <a name="javascript-files"></a><span data-ttu-id="a6ab6-121">Pliki JavaScript</span><span class="sxs-lookup"><span data-stu-id="a6ab6-121">JavaScript files</span></span>
<span data-ttu-id="a6ab6-122">Zastąp plik capptain-sdk.js plików azure-engagement.js, a następnie odpowiednio zaktualizować importów Twojego skryptu.</span><span class="sxs-lookup"><span data-stu-id="a6ab6-122">Replace the file capptain-sdk.js with the file azure-engagement.js, and then update your script imports accordingly.</span></span>

#### <a name="remove-capptain-reach"></a><span data-ttu-id="a6ab6-123">Usuń Capptain Reach</span><span class="sxs-lookup"><span data-stu-id="a6ab6-123">Remove Capptain Reach</span></span>
<span data-ttu-id="a6ab6-124">Ta wersja zestaw SDK usługi Mobile Engagement w sieci Web nie obsługuje funkcji Reach.</span><span class="sxs-lookup"><span data-stu-id="a6ab6-124">This version of the Mobile Engagement Web SDK doesn't support the Reach feature.</span></span> <span data-ttu-id="a6ab6-125">Jest zintegrowany Capptain Reach do aplikacji, należy go usunąć.</span><span class="sxs-lookup"><span data-stu-id="a6ab6-125">If you have integrated Capptain Reach into your application, you need to remove it.</span></span>

<span data-ttu-id="a6ab6-126">Usuń import osiągnąć CSS ze strony i usuń plik .css powiązane (capptain-reach.css, domyślnie).</span><span class="sxs-lookup"><span data-stu-id="a6ab6-126">Remove the Reach CSS import from your page and delete the related .css file (capptain-reach.css, by default).</span></span>

<span data-ttu-id="a6ab6-127">Usuń następujące zasoby Reach: Zamknij obrazu (capptain-close.png, domyślnie) i ikonę marki (capptain powiadomienia ikona, domyślnie).</span><span class="sxs-lookup"><span data-stu-id="a6ab6-127">Delete the following Reach resources: the close image (capptain-close.png, by default) and the brand icon (capptain-notification-icon, by default).</span></span>

<span data-ttu-id="a6ab6-128">Usuń osiągnąć interfejsu użytkownika dla powiadomień w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a6ab6-128">Remove the Reach UI for in-app notifications.</span></span> <span data-ttu-id="a6ab6-129">Domyślny układ wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="a6ab6-129">The default layout looks like this:</span></span>

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

<span data-ttu-id="a6ab6-130">Usuń osiągnąć interfejsu użytkownika dla tekstu i sieci web anonsów i sond.</span><span class="sxs-lookup"><span data-stu-id="a6ab6-130">Remove the Reach UI for text and web announcements and polls.</span></span> <span data-ttu-id="a6ab6-131">Domyślny układ wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="a6ab6-131">The default layout looks like this:</span></span>

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

<span data-ttu-id="a6ab6-132">Usuń `reach` obiekt z konfiguracji, jeśli istnieje.</span><span class="sxs-lookup"><span data-stu-id="a6ab6-132">Remove the `reach` object from your configuration, if it exists.</span></span> <span data-ttu-id="a6ab6-133">Wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="a6ab6-133">It looks like this:</span></span>

    window.capptain = {
      [...]
      reach: {
        [...]
      }
    }

<span data-ttu-id="a6ab6-134">Usuń wszelkie inne dostosowania Reach, takich jak kategorii.</span><span class="sxs-lookup"><span data-stu-id="a6ab6-134">Remove any other Reach customization, such as categories.</span></span>

#### <a name="remove-deprecated-apis"></a><span data-ttu-id="a6ab6-135">Usuń przestarzałe interfejsy API</span><span class="sxs-lookup"><span data-stu-id="a6ab6-135">Remove deprecated APIs</span></span>
<span data-ttu-id="a6ab6-136">Niektóre funkcje interfejsu API z Capptain są używane w sieci Web zestaw SDK usługi Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="a6ab6-136">Some APIs from Capptain are deprecated in the Mobile Engagement Web SDK.</span></span>

<span data-ttu-id="a6ab6-137">Usuń wszystkie wywołania API: `agent.connect`, `agent.disconnect`, `agent.pause`, i `agent.sendMessageToDevice`.</span><span class="sxs-lookup"><span data-stu-id="a6ab6-137">Remove any calls to the following APIs: `agent.connect`, `agent.disconnect`, `agent.pause`, and `agent.sendMessageToDevice`.</span></span>

<span data-ttu-id="a6ab6-138">Usunąć żadnego z następujących wywołania zwrotne w konfiguracji Capptain: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, i `onPushMessageReceived`.</span><span class="sxs-lookup"><span data-stu-id="a6ab6-138">Remove any of the following callbacks from your Capptain configuration: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, and `onPushMessageReceived`.</span></span>

#### <a name="configuration"></a><span data-ttu-id="a6ab6-139">Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="a6ab6-139">Configuration</span></span>
<span data-ttu-id="a6ab6-140">Usługa Mobile Engagement używa parametrów połączenia do konfigurowania zestawu SDK identyfikatorów, na przykład identyfikator aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a6ab6-140">Mobile Engagement uses a connection string to configure SDK identifiers, for example, the application identifier.</span></span>

<span data-ttu-id="a6ab6-141">Zastąp identyfikator aplikacji parametrów połączenia.</span><span class="sxs-lookup"><span data-stu-id="a6ab6-141">Replace the application ID with your connection string.</span></span> <span data-ttu-id="a6ab6-142">Należy pamiętać, że obiekt globalny dla konfiguracji SDK zmieni się z `capptain` do `azureEngagement`.</span><span class="sxs-lookup"><span data-stu-id="a6ab6-142">Note that the global object for the SDK configuration changes from `capptain` to `azureEngagement`.</span></span>

<span data-ttu-id="a6ab6-143">Przed migracją:</span><span class="sxs-lookup"><span data-stu-id="a6ab6-143">Before migration:</span></span>

    window.capptain = {
      appId: ...,
      [...]
    };

<span data-ttu-id="a6ab6-144">Po zakończeniu migracji:</span><span class="sxs-lookup"><span data-stu-id="a6ab6-144">After migration:</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      [...]
    };

<span data-ttu-id="a6ab6-145">Ciąg połączenia dla aplikacji jest wyświetlana w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="a6ab6-145">The connection string for your application is displayed in the Azure portal.</span></span>

#### <a name="javascript-apis"></a><span data-ttu-id="a6ab6-146">Interfejsy API języka JavaScript</span><span class="sxs-lookup"><span data-stu-id="a6ab6-146">JavaScript APIs</span></span>
<span data-ttu-id="a6ab6-147">Globalnego obiektu JavaScript `window.capptain` została zmieniona `window.azureEngagement`, ale można użyć `window.engagement` alias dla interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="a6ab6-147">The global JavaScript object `window.capptain` has been renamed `window.azureEngagement`, but you can use the `window.engagement` alias for API calls.</span></span> <span data-ttu-id="a6ab6-148">Nie można użyć tego aliasu, aby zdefiniować konfigurację zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="a6ab6-148">You can't use this alias to define the SDK configuration.</span></span>

<span data-ttu-id="a6ab6-149">Na przykład `capptain.deviceId` staje się `engagement.deviceId`, `capptain.agent.startActivity` staje się `engagement.agent.startActivity`i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="a6ab6-149">For instance, `capptain.deviceId` becomes `engagement.deviceId`, `capptain.agent.startActivity` becomes `engagement.agent.startActivity`, and so on.</span></span>

<span data-ttu-id="a6ab6-150">Jeśli zintegrowano już program wcześniejszej wersji zestawu SDK usługi Azure Mobile Engagement sieci Web do aplikacji, przeczytaj informacje o [procedur uaktualniania](mobile-engagement-web-upgrade-procedure.md).</span><span class="sxs-lookup"><span data-stu-id="a6ab6-150">If you have already integrated an earlier version of the Azure Mobile Engagement Web SDK into your application, please read about [upgrade procedures](mobile-engagement-web-upgrade-procedure.md).</span></span>

