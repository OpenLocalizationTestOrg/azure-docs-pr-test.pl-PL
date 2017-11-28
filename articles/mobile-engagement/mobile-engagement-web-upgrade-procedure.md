---
title: "procedury uaktualniania zestaw SDK usługi Mobile Engagement Web aaaAzure | Dokumentacja firmy Microsoft"
description: "Witaj najnowsze aktualizacje i procedury dotyczące hello zestawu SDK sieci Web dla usługi Azure Mobile Engagement"
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
ms.openlocfilehash: a2df65904c6b56584ce6588ed26a9b79f3aa27ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-web-sdk-upgrade-procedures"></a><span data-ttu-id="dda55-103">Azure procedur uaktualniania zestaw SDK usługi Mobile Engagement w sieci Web</span><span class="sxs-lookup"><span data-stu-id="dda55-103">Azure Mobile Engagement Web SDK upgrade procedures</span></span>
<span data-ttu-id="dda55-104">Jeśli zintegrowano już program wcześniejszej wersji hello zestaw SDK usługi Azure Mobile Engagement w sieci Web do aplikacji sieci web, należy hello tooconsider następujące punkty po uaktualnieniu hello zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="dda55-104">If you have already integrated an earlier version of hello Azure Mobile Engagement Web SDK into your web application, you need tooconsider hello following points when you upgrade hello SDK.</span></span>

<span data-ttu-id="dda55-105">Wiele wersji hello zestaw SDK usługi Mobile Engagement w sieci Web została pominięta, może być konieczne toocomplete kilka procedur podczas procesu uaktualniania hello.</span><span class="sxs-lookup"><span data-stu-id="dda55-105">If you skipped multiple versions of hello Mobile Engagement Web SDK, you might need toocomplete several procedures during hello upgrade process.</span></span> <span data-ttu-id="dda55-106">Na przykład w przypadku migracji z 1.4.0 too1.6.0, pierwszy tooupgrade procedury hello postępuj zgodnie z 1.4.0 too1.5.0.</span><span class="sxs-lookup"><span data-stu-id="dda55-106">For example, if you migrate from 1.4.0 too1.6.0, first follow hello procedures tooupgrade from 1.4.0 too1.5.0.</span></span> <span data-ttu-id="dda55-107">Następnie wykonaj hello procedury tooupgrade z 1.5.0 too1.6.0.</span><span class="sxs-lookup"><span data-stu-id="dda55-107">Then, follow hello procedures tooupgrade from 1.5.0 too1.6.0.</span></span>

<span data-ttu-id="dda55-108">Niezależnie od wersji uaktualnienia, Zamień hello najnowszą wersję pliku hello jakakolwiek wcześniejsza wersja pliku hello azure-engagement.js.</span><span class="sxs-lookup"><span data-stu-id="dda55-108">Whichever version you upgrade from, replace any earlier version of hello file azure-engagement.js with hello latest version of hello file.</span></span>

## <a name="upgrade-from-121-too200"></a><span data-ttu-id="dda55-109">Uaktualnienie z wersji 1.2.1 too2.0.0</span><span class="sxs-lookup"><span data-stu-id="dda55-109">Upgrade from 1.2.1 too2.0.0</span></span>
<span data-ttu-id="dda55-110">W tej sekcji opisano, jak toomigrate zestaw SDK usługi Mobile Engagement w sieci Web integracji z usługą Capptain hello, oferowane przez Capptain SAS, tooan aplikacji usługi Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="dda55-110">This section describes how toomigrate a Mobile Engagement Web SDK integration from hello Capptain service, offered by Capptain SAS, tooan Azure Mobile Engagement app.</span></span> <span data-ttu-id="dda55-111">W przypadku migracji z wcześniejszej wersji, należy hello należy zapoznać się z toofirst witryny sieci Web Capptain too1.2.1 migracji, a następnie Zastosuj hello zgodnie z procedurami.</span><span class="sxs-lookup"><span data-stu-id="dda55-111">If you are migrating from an earlier version, please consult hello Capptain website toofirst migrate too1.2.1, and then apply hello following procedures.</span></span>

<span data-ttu-id="dda55-112">Ta wersja hello zestaw SDK usługi Mobile Engagement w sieci Web nie obsługuje Samsung inteligentne TV, Opera TV, webOS lub hello Reach funkcji.</span><span class="sxs-lookup"><span data-stu-id="dda55-112">This version of hello Mobile Engagement Web SDK doesn't support Samsung Smart TV, Opera TV, webOS, or hello Reach feature.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dda55-113">Capptain i usługi Azure Mobile Engagement nie są hello tę samą usługę.</span><span class="sxs-lookup"><span data-stu-id="dda55-113">Capptain and Azure Mobile Engagement are not hello same service.</span></span> <span data-ttu-id="dda55-114">Witaj procedury prezentuje tylko sposób toomigrate hello aplikacji klienta.</span><span class="sxs-lookup"><span data-stu-id="dda55-114">hello following procedure highlights only how toomigrate hello client app.</span></span> <span data-ttu-id="dda55-115">Migrowanie hello zestaw SDK usługi Mobile Engagement w sieci Web w aplikacji hello nie będą migrowane dane z serwera usługi Mobile Engagement tooa Capptain serwera.</span><span class="sxs-lookup"><span data-stu-id="dda55-115">Migrating hello Mobile Engagement Web SDK in hello app will not migrate your data from a Capptain server tooa Mobile Engagement server.</span></span>
> 
> 

### <a name="javascript-files"></a><span data-ttu-id="dda55-116">Pliki JavaScript</span><span class="sxs-lookup"><span data-stu-id="dda55-116">JavaScript files</span></span>
<span data-ttu-id="dda55-117">Zastąp plik hello capptain-sdk.js pliku hello azure-engagement.js, a następnie zaktualizować skrypt importuje odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="dda55-117">Replace hello file capptain-sdk.js with hello file azure-engagement.js, and then update your script imports accordingly.</span></span>

### <a name="remove-capptain-reach"></a><span data-ttu-id="dda55-118">Usuń Capptain Reach</span><span class="sxs-lookup"><span data-stu-id="dda55-118">Remove Capptain Reach</span></span>
<span data-ttu-id="dda55-119">Ta wersja hello zestaw SDK usługi Mobile Engagement w sieci Web nie obsługuje funkcji Reach hello.</span><span class="sxs-lookup"><span data-stu-id="dda55-119">This version of hello Mobile Engagement Web SDK doesn't support hello Reach feature.</span></span> <span data-ttu-id="dda55-120">Jeśli Capptain Reach zintegrowana aplikacja, należy tooremove go.</span><span class="sxs-lookup"><span data-stu-id="dda55-120">If you integrated Capptain Reach into your application, you need tooremove it.</span></span>

<span data-ttu-id="dda55-121">Usuń import osiągnąć CSS hello ze strony użytkownika i spróbuj usunąć plik .css powiązane hello (capptain-reach.css, domyślnie).</span><span class="sxs-lookup"><span data-stu-id="dda55-121">Remove hello Reach CSS import from your page and delete hello related .css file (capptain-reach.css, by default).</span></span>

<span data-ttu-id="dda55-122">Usuń następujące zasoby Reach hello: hello Zamknij obrazu (capptain-close.png, domyślnie) i hello brand ikona (capptain powiadomienia-, domyślnie).</span><span class="sxs-lookup"><span data-stu-id="dda55-122">Delete hello following Reach resources: hello close image (capptain-close.png, by default) and hello brand icon (capptain-notification-icon, by default).</span></span>

<span data-ttu-id="dda55-123">Usuń hello osiągnąć interfejsu użytkownika dla powiadomień w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="dda55-123">Remove hello Reach UI for in-app notifications.</span></span> <span data-ttu-id="dda55-124">Układ domyślny Hello wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="dda55-124">hello default layout looks like this:</span></span>

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

<span data-ttu-id="dda55-125">Usuń hello osiągnąć interfejsu użytkownika dla sieci web i tekst anonsów i sond.</span><span class="sxs-lookup"><span data-stu-id="dda55-125">Remove hello Reach UI for text and web announcements and polls.</span></span> <span data-ttu-id="dda55-126">Układ domyślny Hello wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="dda55-126">hello default layout looks like this:</span></span>

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

<span data-ttu-id="dda55-127">Usuń hello `reach` obiekt z konfiguracji, jeśli istnieje.</span><span class="sxs-lookup"><span data-stu-id="dda55-127">Remove hello `reach` object from your configuration, if it exists.</span></span> <span data-ttu-id="dda55-128">Wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="dda55-128">It looks like this:</span></span>

    window.capptain = {
      [...]
      reach: {
        [...]
      }
    }

<span data-ttu-id="dda55-129">Usuń wszelkie inne dostosowania Reach, takich jak kategorii.</span><span class="sxs-lookup"><span data-stu-id="dda55-129">Remove any other Reach customization, such as categories.</span></span>

### <a name="remove-deprecated-apis"></a><span data-ttu-id="dda55-130">Usuń przestarzałe interfejsy API</span><span class="sxs-lookup"><span data-stu-id="dda55-130">Remove deprecated APIs</span></span>
<span data-ttu-id="dda55-131">Niektóre funkcje interfejsu API z Capptain są używane w hello zestaw SDK usługi Mobile Engagement w sieci Web.</span><span class="sxs-lookup"><span data-stu-id="dda55-131">Some APIs from Capptain are deprecated in hello Mobile Engagement Web SDK.</span></span>

<span data-ttu-id="dda55-132">Usuń wszelkie toohello wywołania następujące interfejsy API: `agent.connect`, `agent.disconnect`, `agent.pause`, i `agent.sendMessageToDevice`.</span><span class="sxs-lookup"><span data-stu-id="dda55-132">Remove any calls toohello following APIs: `agent.connect`, `agent.disconnect`, `agent.pause`, and `agent.sendMessageToDevice`.</span></span>

<span data-ttu-id="dda55-133">Usuń wszystkie wystąpienia poniższych wywołań zwrotnych z konfiguracji Capptain hello: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, i `onPushMessageReceived`.</span><span class="sxs-lookup"><span data-stu-id="dda55-133">Remove any instances of hello following callbacks from your Capptain configuration: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, and `onPushMessageReceived`.</span></span>

### <a name="configuration"></a><span data-ttu-id="dda55-134">Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="dda55-134">Configuration</span></span>
<span data-ttu-id="dda55-135">Połączenie tooconfigure SDK identyfikatory ciągów, na przykład identyfikator aplikacji hello korzysta z usługi Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="dda55-135">Mobile Engagement uses a connection string tooconfigure SDK identifiers, for example, hello application identifier.</span></span>

<span data-ttu-id="dda55-136">Zastąp identyfikator aplikacji hello parametrów połączenia.</span><span class="sxs-lookup"><span data-stu-id="dda55-136">Replace hello application ID with your connection string.</span></span> <span data-ttu-id="dda55-137">Należy zwrócić uwagę hello obiektu globalnego dla hello konfiguracji SDK zmieni się z `capptain` zbyt`azureEngagement`.</span><span class="sxs-lookup"><span data-stu-id="dda55-137">Note that hello global object for hello SDK configuration changes from `capptain` too`azureEngagement`.</span></span>

<span data-ttu-id="dda55-138">Przed migracją:</span><span class="sxs-lookup"><span data-stu-id="dda55-138">Before migration:</span></span>

    window.capptain = {
      appId: ...,
      [...]
    };

<span data-ttu-id="dda55-139">Po zakończeniu migracji:</span><span class="sxs-lookup"><span data-stu-id="dda55-139">After migration:</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      [...]
    };

<span data-ttu-id="dda55-140">Parametry połączenia Hello aplikacji jest wyświetlany w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="dda55-140">hello connection string for your application is displayed in hello Azure Portal.</span></span>

### <a name="javascript-apis"></a><span data-ttu-id="dda55-141">Interfejsy API języka JavaScript</span><span class="sxs-lookup"><span data-stu-id="dda55-141">JavaScript APIs</span></span>
<span data-ttu-id="dda55-142">Obiekt global JavaScript Hello `window.capptain` została zmieniona `window.azureEngagement` , ale można użyć hello `window.engagement` alias dla interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="dda55-142">hello global JavaScript object `window.capptain` has been renamed `window.azureEngagement` but you can use hello `window.engagement` alias for API calls.</span></span> <span data-ttu-id="dda55-143">Nie można użyć hello alias toodefine hello SDK konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="dda55-143">You can't use hello alias toodefine hello SDK configuration.</span></span>

<span data-ttu-id="dda55-144">Na przykład `capptain.deviceId` staje się `engagement.deviceId`, `capptain.agent.startActivity` staje się `engagement.agent.startActivity`i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="dda55-144">For instance, `capptain.deviceId` becomes `engagement.deviceId`, `capptain.agent.startActivity` becomes `engagement.agent.startActivity`, and so on.</span></span>

