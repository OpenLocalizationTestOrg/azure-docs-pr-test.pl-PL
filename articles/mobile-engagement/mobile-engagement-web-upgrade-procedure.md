---
title: Azure Mobile Engagement Web SDK procedur uaktualniania | Dokumentacja firmy Microsoft
description: "Najnowsze aktualizacje i procedury dotyczące zestawu SDK sieci Web dla usługi Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a20529b4-ec8d-4503-8ae9-09b5f0846d5b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 06/07/2016
ms.author: piyushjo
ms.openlocfilehash: afa8037dcb7a53042fa606e2c4014b442d4be326
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-mobile-engagement-web-sdk-upgrade-procedures"></a><span data-ttu-id="b5422-103">Azure procedur uaktualniania zestaw SDK usługi Mobile Engagement w sieci Web</span><span class="sxs-lookup"><span data-stu-id="b5422-103">Azure Mobile Engagement Web SDK upgrade procedures</span></span>
<span data-ttu-id="b5422-104">Jeśli zintegrowano już program wcześniejszej wersji zestawu SDK usługi Azure Mobile Engagement sieci Web do aplikacji sieci web, należy wziąć pod uwagę następujące kwestie, po uaktualnieniu zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="b5422-104">If you have already integrated an earlier version of the Azure Mobile Engagement Web SDK into your web application, you need to consider the following points when you upgrade the SDK.</span></span>

<span data-ttu-id="b5422-105">Wiele wersji zestaw SDK usługi Mobile Engagement w sieci Web została pominięta, może być konieczne podczas procesu uaktualniania należy wykonać kilka procedury.</span><span class="sxs-lookup"><span data-stu-id="b5422-105">If you skipped multiple versions of the Mobile Engagement Web SDK, you might need to complete several procedures during the upgrade process.</span></span> <span data-ttu-id="b5422-106">Na przykład w przypadku migrowania z 1.4.0 do 1.6.0 najpierw wykonać procedury uaktualniania z 1.4.0 do 1.5.0.</span><span class="sxs-lookup"><span data-stu-id="b5422-106">For example, if you migrate from 1.4.0 to 1.6.0, first follow the procedures to upgrade from 1.4.0 to 1.5.0.</span></span> <span data-ttu-id="b5422-107">Następnie wykonaj procedury uaktualniania z 1.5.0 do 1.6.0.</span><span class="sxs-lookup"><span data-stu-id="b5422-107">Then, follow the procedures to upgrade from 1.5.0 to 1.6.0.</span></span>

<span data-ttu-id="b5422-108">Niezależnie od wersji uaktualnienia, Zamień jakakolwiek wcześniejsza wersja pliku azure-engagement.js najnowszej wersji pliku.</span><span class="sxs-lookup"><span data-stu-id="b5422-108">Whichever version you upgrade from, replace any earlier version of the file azure-engagement.js with the latest version of the file.</span></span>

## <a name="upgrade-from-121-to-200"></a><span data-ttu-id="b5422-109">Uaktualnienie z wersji 1.2.1 do 2.0.0</span><span class="sxs-lookup"><span data-stu-id="b5422-109">Upgrade from 1.2.1 to 2.0.0</span></span>
<span data-ttu-id="b5422-110">W tej sekcji opisano sposób migracji integracji zestaw SDK usługi Mobile Engagement w sieci Web w usłudze Capptain oferowanych przez Capptain SAS, aplikację usługi Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="b5422-110">This section describes how to migrate a Mobile Engagement Web SDK integration from the Capptain service, offered by Capptain SAS, to an Azure Mobile Engagement app.</span></span> <span data-ttu-id="b5422-111">W przypadku migracji z wcześniejszej wersji, zajrzyj do witryny sieci Web Capptain najpierw migracji do wersji 1.2.1, a następnie zastosuj poniższe procedury.</span><span class="sxs-lookup"><span data-stu-id="b5422-111">If you are migrating from an earlier version, please consult the Capptain website to first migrate to 1.2.1, and then apply the following procedures.</span></span>

<span data-ttu-id="b5422-112">Ta wersja zestaw SDK usługi Mobile Engagement w sieci Web nie obsługuje Samsung inteligentne TV, Opera TV, webOS lub funkcji Reach.</span><span class="sxs-lookup"><span data-stu-id="b5422-112">This version of the Mobile Engagement Web SDK doesn't support Samsung Smart TV, Opera TV, webOS, or the Reach feature.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b5422-113">Capptain i usługi Azure Mobile Engagement nie są tę samą usługę.</span><span class="sxs-lookup"><span data-stu-id="b5422-113">Capptain and Azure Mobile Engagement are not the same service.</span></span> <span data-ttu-id="b5422-114">Poniższa procedura zawiera wyróżnione tylko sposób migracji aplikacji klienckiej.</span><span class="sxs-lookup"><span data-stu-id="b5422-114">The following procedure highlights only how to migrate the client app.</span></span> <span data-ttu-id="b5422-115">Migrowanie Mobile Engagement Web SDK w aplikacji nie będą migrowane dane z serwera Capptain na serwerze usługi Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="b5422-115">Migrating the Mobile Engagement Web SDK in the app will not migrate your data from a Capptain server to a Mobile Engagement server.</span></span>
> 
> 

### <a name="javascript-files"></a><span data-ttu-id="b5422-116">Pliki JavaScript</span><span class="sxs-lookup"><span data-stu-id="b5422-116">JavaScript files</span></span>
<span data-ttu-id="b5422-117">Zastąp plik capptain-sdk.js plików azure-engagement.js, a następnie odpowiednio zaktualizować importów Twojego skryptu.</span><span class="sxs-lookup"><span data-stu-id="b5422-117">Replace the file capptain-sdk.js with the file azure-engagement.js, and then update your script imports accordingly.</span></span>

### <a name="remove-capptain-reach"></a><span data-ttu-id="b5422-118">Usuń Capptain Reach</span><span class="sxs-lookup"><span data-stu-id="b5422-118">Remove Capptain Reach</span></span>
<span data-ttu-id="b5422-119">Ta wersja zestaw SDK usługi Mobile Engagement w sieci Web nie obsługuje funkcji Reach.</span><span class="sxs-lookup"><span data-stu-id="b5422-119">This version of the Mobile Engagement Web SDK doesn't support the Reach feature.</span></span> <span data-ttu-id="b5422-120">Jeśli Capptain Reach zintegrowana aplikacja, należy go usunąć.</span><span class="sxs-lookup"><span data-stu-id="b5422-120">If you integrated Capptain Reach into your application, you need to remove it.</span></span>

<span data-ttu-id="b5422-121">Usuń import osiągnąć CSS ze strony i usuń plik .css powiązane (capptain-reach.css, domyślnie).</span><span class="sxs-lookup"><span data-stu-id="b5422-121">Remove the Reach CSS import from your page and delete the related .css file (capptain-reach.css, by default).</span></span>

<span data-ttu-id="b5422-122">Usuń następujące zasoby Reach: Zamknij obrazu (capptain-close.png, domyślnie) i ikonę marki (capptain powiadomienia ikona, domyślnie).</span><span class="sxs-lookup"><span data-stu-id="b5422-122">Delete the following Reach resources: the close image (capptain-close.png, by default) and the brand icon (capptain-notification-icon, by default).</span></span>

<span data-ttu-id="b5422-123">Usuń osiągnąć interfejsu użytkownika dla powiadomień w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b5422-123">Remove the Reach UI for in-app notifications.</span></span> <span data-ttu-id="b5422-124">Domyślny układ wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="b5422-124">The default layout looks like this:</span></span>

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

<span data-ttu-id="b5422-125">Usuń osiągnąć interfejsu użytkownika dla tekstu i sieci web anonsów i sond.</span><span class="sxs-lookup"><span data-stu-id="b5422-125">Remove the Reach UI for text and web announcements and polls.</span></span> <span data-ttu-id="b5422-126">Domyślny układ wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="b5422-126">The default layout looks like this:</span></span>

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

<span data-ttu-id="b5422-127">Usuń `reach` obiekt z konfiguracji, jeśli istnieje.</span><span class="sxs-lookup"><span data-stu-id="b5422-127">Remove the `reach` object from your configuration, if it exists.</span></span> <span data-ttu-id="b5422-128">Wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="b5422-128">It looks like this:</span></span>

    window.capptain = {
      [...]
      reach: {
        [...]
      }
    }

<span data-ttu-id="b5422-129">Usuń wszelkie inne dostosowania Reach, takich jak kategorii.</span><span class="sxs-lookup"><span data-stu-id="b5422-129">Remove any other Reach customization, such as categories.</span></span>

### <a name="remove-deprecated-apis"></a><span data-ttu-id="b5422-130">Usuń przestarzałe interfejsy API</span><span class="sxs-lookup"><span data-stu-id="b5422-130">Remove deprecated APIs</span></span>
<span data-ttu-id="b5422-131">Niektóre funkcje interfejsu API z Capptain są używane w sieci Web zestaw SDK usługi Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="b5422-131">Some APIs from Capptain are deprecated in the Mobile Engagement Web SDK.</span></span>

<span data-ttu-id="b5422-132">Usuń wszystkie wywołania API: `agent.connect`, `agent.disconnect`, `agent.pause`, i `agent.sendMessageToDevice`.</span><span class="sxs-lookup"><span data-stu-id="b5422-132">Remove any calls to the following APIs: `agent.connect`, `agent.disconnect`, `agent.pause`, and `agent.sendMessageToDevice`.</span></span>

<span data-ttu-id="b5422-133">Usuń wszystkie wystąpienia elementu następujące wywołania zwrotne w konfiguracji Capptain: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, i `onPushMessageReceived`.</span><span class="sxs-lookup"><span data-stu-id="b5422-133">Remove any instances of the following callbacks from your Capptain configuration: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, and `onPushMessageReceived`.</span></span>

### <a name="configuration"></a><span data-ttu-id="b5422-134">Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="b5422-134">Configuration</span></span>
<span data-ttu-id="b5422-135">Usługa Mobile Engagement używa parametrów połączenia do konfigurowania zestawu SDK identyfikatorów, na przykład identyfikator aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b5422-135">Mobile Engagement uses a connection string to configure SDK identifiers, for example, the application identifier.</span></span>

<span data-ttu-id="b5422-136">Zastąp identyfikator aplikacji parametrów połączenia.</span><span class="sxs-lookup"><span data-stu-id="b5422-136">Replace the application ID with your connection string.</span></span> <span data-ttu-id="b5422-137">Należy pamiętać, że obiekt globalny dla konfiguracji SDK zmieni się z `capptain` do `azureEngagement`.</span><span class="sxs-lookup"><span data-stu-id="b5422-137">Note that the global object for the SDK configuration changes from `capptain` to `azureEngagement`.</span></span>

<span data-ttu-id="b5422-138">Przed migracją:</span><span class="sxs-lookup"><span data-stu-id="b5422-138">Before migration:</span></span>

    window.capptain = {
      appId: ...,
      [...]
    };

<span data-ttu-id="b5422-139">Po zakończeniu migracji:</span><span class="sxs-lookup"><span data-stu-id="b5422-139">After migration:</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      [...]
    };

<span data-ttu-id="b5422-140">Ciąg połączenia dla aplikacji jest wyświetlana w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="b5422-140">The connection string for your application is displayed in the Azure Portal.</span></span>

### <a name="javascript-apis"></a><span data-ttu-id="b5422-141">Interfejsy API języka JavaScript</span><span class="sxs-lookup"><span data-stu-id="b5422-141">JavaScript APIs</span></span>
<span data-ttu-id="b5422-142">Obiekt globalny JavaScript `window.capptain` została zmieniona `window.azureEngagement` , ale można użyć `window.engagement` alias dla interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="b5422-142">The global JavaScript object `window.capptain` has been renamed `window.azureEngagement` but you can use the `window.engagement` alias for API calls.</span></span> <span data-ttu-id="b5422-143">Nie można użyć aliasu, aby zdefiniować konfigurację zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="b5422-143">You can't use the alias to define the SDK configuration.</span></span>

<span data-ttu-id="b5422-144">Na przykład `capptain.deviceId` staje się `engagement.deviceId`, `capptain.agent.startActivity` staje się `engagement.agent.startActivity`i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="b5422-144">For instance, `capptain.deviceId` becomes `engagement.deviceId`, `capptain.agent.startActivity` becomes `engagement.agent.startActivity`, and so on.</span></span>

