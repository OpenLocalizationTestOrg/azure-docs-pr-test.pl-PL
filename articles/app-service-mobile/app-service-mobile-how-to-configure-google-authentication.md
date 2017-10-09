---
title: "aaaHow tooconfigure Google uwierzytelniania dla aplikacji usługi aplikacji"
description: "Dowiedz się, jak uwierzytelniania serwisu Google tooconfigure aplikacji usługi aplikacji."
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: 2b2f9abf-9120-4aac-ac5b-4a268d9b6e2b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 9175c40b78c859e9e191504c41cd0bb9a3380ccd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-google-login"></a>Jak tooconfigure logowanie Google toouse aplikacji usługi aplikacji
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

W tym temacie opisano sposób tooconfigure usłudze Azure App Service toouse Google jako dostawcy uwierzytelniania.

toocomplete hello procedurze w tym temacie, musi mieć konto Google ze zweryfikowanym adresem e-mail. toocreate nowe konto Google, przejdź zbyt[accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).

## <a name="register"></a>Zarejestrować aplikację w usłudze Google
1. Zaloguj się na toohello [portalu Azure]i przejdź tooyour aplikacji. Kopiowanie z **adres URL**, która użyj nowszej tooconfigure aplikacji Google.
2. Przejdź toohello [interfejsy API Google](http://go.microsoft.com/fwlink/p/?LinkId=268303) kliknij witrynę sieci Web, zaloguj się przy użyciu poświadczeń konta Google **tworzenia projektu**, podaj **Nazwa projektu**, następnie kliknij przycisk  **Utwórz**.
3. W obszarze **społecznościowych interfejsów API** kliknij **interfejsu API Google +** , a następnie **włączyć**.
4. W hello lewy pasek nawigacyjny **poświadczenia** > **ekranu zgoda OAuth**, a następnie wybierz pozycję z **adres E-mail**, wprowadź **nazwa produktu**i kliknij przycisk **zapisać**.
5. W hello **poświadczenia** , kliknij pozycję **Utwórz poświadczenia** > **identyfikator klienta OAuth**, a następnie wybierz pozycję **aplikacji sieci Web**.
6. Wklej hello usługi aplikacji **adres URL** zostanie wcześniej skopiowany do **autoryzowany źródeł JavaScript**, Wklej przekierowania z identyfikatora URI do **autoryzowany identyfikator URI przekierowania**. Witaj przekierowania URI jest adresem URL hello aplikacji dołączony ścieżki hello, */.auth/login/google/callback*. Na przykład `https://contoso.azurewebsites.net/.auth/login/google/callback`. Upewnij się, że używasz hello schematu HTTPS. Następnie kliknij pozycję **Utwórz**.
7. Na następnym ekranie powitania zanotuj wartości powitania klienta hello klucz tajny identyfikator i klienta.

    > [!IMPORTANT]
    > klucz tajny klienta Hello jest ważne poświadczenie zabezpieczeń. Nie udostępniaj nikomu ten klucz tajny i rozpowszechnienie go w aplikacji klienta.


## <a name="secrets"></a>Google dodać informacje tooyour aplikacji
1. Po powrocie do hello [portalu Azure], przejdź tooyour aplikacji. Kliknij przycisk **ustawienia**, a następnie **uwierzytelniania / autoryzacji**.
2. Jeśli hello uwierzytelniania / autoryzacji funkcja nie jest włączona, włącz przełącznik hello zbyt**na**.
3. Kliknij przycisk **Google**. Wklej w wartości Identyfikatora aplikacji i klucz tajny aplikacji hello, które uzyskany wcześniej i opcjonalnie włączyć wszystkie zakresy wymaganych przez aplikację. Następnie kliknij przycisk **OK**.
   
   ![][1]
   
   Domyślnie usługi App Service zapewnia uwierzytelnianie, ale nie ogranicza autoryzowany dostęp do zawartości witryny tooyour i interfejsów API. Musisz zezwolić użytkownikom w kodzie aplikacji.
4. (Opcjonalnie) toorestrict dostępu tooyour lokacji tooonly użytkowników uwierzytelnionych przez firmę Google, ustaw **tootake akcji w przypadku nieuwierzytelnionego żądania** za**Google**. Wymaga to, że wszystkie żądania uwierzytelnienia, a wszystkie nieuwierzytelnione żądania są tooGoogle przekierowany do uwierzytelniania.
5. Kliknij pozycję **Zapisz**.

Wszystko jest teraz gotowy toouse Google do uwierzytelniania w aplikacji.

## <a name="related-content"></a>Związane z zawartością
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Anchors. -->

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-settings.png

<!-- URLs. -->

[Google apis]: http://go.microsoft.com/fwlink/p/?LinkId=268303

[portalu Azure]: https://portal.azure.com/

