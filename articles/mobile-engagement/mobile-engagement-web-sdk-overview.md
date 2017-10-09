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
# <a name="azure-mobile-engagement-web-sdk"></a>Sieci Web usługi Azure Mobile Engagement SDK
Szybki Start dla wszystkich hello szczegółowe informacje na temat toointegrate usługi Azure Mobile Engagement w aplikacji sieci web. Jeśli chcesz toogive go try przed rozpoczęciem pracy z własnych aplikacji sieci web, zobacz nasze [samouczek 15 minut](mobile-engagement-web-app-get-started.md).

## <a name="integration-procedures"></a>Procedury integracji
1. Dowiedz się [jak toointegrate Mobile Engagement w aplikacji sieci web](mobile-engagement-web-integrate-engagement.md).
2. Tag planu wykonania, Dowiedz się [jak toouse hello zaawansowane znakowanie interfejsu API w aplikacji sieci web usługi Mobile Engagement](mobile-engagement-web-use-engagement-api.md).

## <a name="release-notes"></a>Informacje o wersji
### <a name="202-10182016"></a>2.0.2 (10/18/2016)
* Stałe awarii na InPrivate (Safari).
* Stałe awarii w przeglądarkach plików cookie jest wyłączona.

Wszystkie wersje, zobacz hello [ukończyć wersji](mobile-engagement-web-release-notes.md).

## <a name="upgrade-procedures"></a>Procedury uaktualniania
### <a name="upgrade-from-121-too200"></a>Uaktualnienie z wersji 1.2.1 too2.0.0
Witaj poniższych sekcjach opisano sposób toomigrate zestaw SDK usługi Mobile Engagement w sieci Web integracji z usługą Capptain hello, oferowane przez Capptain SAS, tooan aplikacji usługi Azure Mobile Engagement. W przypadku migracji z wersji starszej niż 1.2.1, należy najpierw zapoznać się hello Capptain witryny sieci Web toomigrate too1.2.1, a następnie Zastosuj hello zgodnie z procedurami.

Ta wersja hello zestaw SDK usługi Mobile Engagement w sieci Web nie obsługuje Samsung inteligentne TV, Opera TV, webOS lub hello Reach funkcji.

> [!IMPORTANT]
> Capptain i usługi Azure Mobile Engagement nie hello tę samą usługę, a hello zgodnie z procedurami zaznacz tylko sposób toomigrate hello aplikacji klienckiej. Migrowanie hello zestaw SDK usługi Mobile Engagement w sieci Web w aplikacji hello nie będą migrowane dane z serwera usługi Mobile Engagement tooa Capptain serwera.
> 
> 

#### <a name="javascript-files"></a>Pliki JavaScript
Zastąp plik hello capptain-sdk.js pliku hello azure-engagement.js, a następnie zaktualizować skrypt importuje odpowiednio.

#### <a name="remove-capptain-reach"></a>Usuń Capptain Reach
Ta wersja hello zestaw SDK usługi Mobile Engagement w sieci Web nie obsługuje funkcji Reach hello. Jest zintegrowany Capptain Reach do aplikacji, konieczne będzie tooremove go.

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

#### <a name="remove-deprecated-apis"></a>Usuń przestarzałe interfejsy API
Niektóre funkcje interfejsu API z Capptain są używane w hello zestaw SDK usługi Mobile Engagement w sieci Web.

Usuń wszelkie toohello wywołania następujące interfejsy API: `agent.connect`, `agent.disconnect`, `agent.pause`, i `agent.sendMessageToDevice`.

Usuń wszystkie hello poniższych wywołań zwrotnych z konfiguracji Capptain: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, i `onPushMessageReceived`.

#### <a name="configuration"></a>Konfiguracja
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

#### <a name="javascript-apis"></a>Interfejsy API języka JavaScript
Obiekt global JavaScript Hello `window.capptain` została zmieniona `window.azureEngagement`, ale można użyć hello `window.engagement` alias dla interfejsu API. Nie można użyć tego aliasu toodefine hello SDK konfiguracji.

Na przykład `capptain.deviceId` staje się `engagement.deviceId`, `capptain.agent.startActivity` staje się `engagement.agent.startActivity`i tak dalej.

Jeśli zintegrowano już program wcześniejszej wersji hello zestaw SDK usługi Azure Mobile Engagement w sieci Web do aplikacji, przeczytaj informacje o [procedur uaktualniania](mobile-engagement-web-upgrade-procedure.md).

