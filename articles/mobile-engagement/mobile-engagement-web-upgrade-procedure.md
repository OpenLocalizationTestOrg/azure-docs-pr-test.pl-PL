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
# <a name="azure-mobile-engagement-web-sdk-upgrade-procedures"></a>Azure procedur uaktualniania zestaw SDK usługi Mobile Engagement w sieci Web
Jeśli zintegrowano już program wcześniejszej wersji hello zestaw SDK usługi Azure Mobile Engagement w sieci Web do aplikacji sieci web, należy hello tooconsider następujące punkty po uaktualnieniu hello zestawu SDK.

Wiele wersji hello zestaw SDK usługi Mobile Engagement w sieci Web została pominięta, może być konieczne toocomplete kilka procedur podczas procesu uaktualniania hello. Na przykład w przypadku migracji z 1.4.0 too1.6.0, pierwszy tooupgrade procedury hello postępuj zgodnie z 1.4.0 too1.5.0. Następnie wykonaj hello procedury tooupgrade z 1.5.0 too1.6.0.

Niezależnie od wersji uaktualnienia, Zamień hello najnowszą wersję pliku hello jakakolwiek wcześniejsza wersja pliku hello azure-engagement.js.

## <a name="upgrade-from-121-too200"></a>Uaktualnienie z wersji 1.2.1 too2.0.0
W tej sekcji opisano, jak toomigrate zestaw SDK usługi Mobile Engagement w sieci Web integracji z usługą Capptain hello, oferowane przez Capptain SAS, tooan aplikacji usługi Azure Mobile Engagement. W przypadku migracji z wcześniejszej wersji, należy hello należy zapoznać się z toofirst witryny sieci Web Capptain too1.2.1 migracji, a następnie Zastosuj hello zgodnie z procedurami.

Ta wersja hello zestaw SDK usługi Mobile Engagement w sieci Web nie obsługuje Samsung inteligentne TV, Opera TV, webOS lub hello Reach funkcji.

> [!IMPORTANT]
> Capptain i usługi Azure Mobile Engagement nie są hello tę samą usługę. Witaj procedury prezentuje tylko sposób toomigrate hello aplikacji klienta. Migrowanie hello zestaw SDK usługi Mobile Engagement w sieci Web w aplikacji hello nie będą migrowane dane z serwera usługi Mobile Engagement tooa Capptain serwera.
> 
> 

### <a name="javascript-files"></a>Pliki JavaScript
Zastąp plik hello capptain-sdk.js pliku hello azure-engagement.js, a następnie zaktualizować skrypt importuje odpowiednio.

### <a name="remove-capptain-reach"></a>Usuń Capptain Reach
Ta wersja hello zestaw SDK usługi Mobile Engagement w sieci Web nie obsługuje funkcji Reach hello. Jeśli Capptain Reach zintegrowana aplikacja, należy tooremove go.

Usuń import osiągnąć CSS hello ze strony użytkownika i spróbuj usunąć plik .css powiązane hello (capptain-reach.css, domyślnie).

Usuń następujące zasoby Reach hello: hello Zamknij obrazu (capptain-close.png, domyślnie) i hello brand ikona (capptain powiadomienia-, domyślnie).

Usuń hello osiągnąć interfejsu użytkownika dla powiadomień w aplikacji. Układ domyślny Hello wygląda następująco:

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

Usuń hello osiągnąć interfejsu użytkownika dla sieci web i tekst anonsów i sond. Układ domyślny Hello wygląda następująco:

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

Usuń hello `reach` obiekt z konfiguracji, jeśli istnieje. Wygląda następująco:

    window.capptain = {
      [...]
      reach: {
        [...]
      }
    }

Usuń wszelkie inne dostosowania Reach, takich jak kategorii.

### <a name="remove-deprecated-apis"></a>Usuń przestarzałe interfejsy API
Niektóre funkcje interfejsu API z Capptain są używane w hello zestaw SDK usługi Mobile Engagement w sieci Web.

Usuń wszelkie toohello wywołania następujące interfejsy API: `agent.connect`, `agent.disconnect`, `agent.pause`, i `agent.sendMessageToDevice`.

Usuń wszystkie wystąpienia poniższych wywołań zwrotnych z konfiguracji Capptain hello: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, i `onPushMessageReceived`.

### <a name="configuration"></a>Konfiguracja
Połączenie tooconfigure SDK identyfikatory ciągów, na przykład identyfikator aplikacji hello korzysta z usługi Mobile Engagement.

Zastąp identyfikator aplikacji hello parametrów połączenia. Należy zwrócić uwagę hello obiektu globalnego dla hello konfiguracji SDK zmieni się z `capptain` zbyt`azureEngagement`.

Przed migracją:

    window.capptain = {
      appId: ...,
      [...]
    };

Po zakończeniu migracji:

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      [...]
    };

Parametry połączenia Hello aplikacji jest wyświetlany w hello portalu Azure.

### <a name="javascript-apis"></a>Interfejsy API języka JavaScript
Obiekt global JavaScript Hello `window.capptain` została zmieniona `window.azureEngagement` , ale można użyć hello `window.engagement` alias dla interfejsu API. Nie można użyć hello alias toodefine hello SDK konfiguracji.

Na przykład `capptain.deviceId` staje się `engagement.deviceId`, `capptain.agent.startActivity` staje się `engagement.agent.startActivity`i tak dalej.

