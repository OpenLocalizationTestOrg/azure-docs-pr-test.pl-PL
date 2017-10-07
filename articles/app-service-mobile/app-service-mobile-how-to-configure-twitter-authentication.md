---
title: "aaaHow tooconfigure Twitter uwierzytelniania dla aplikacji usługi aplikacji"
description: "Dowiedz się, jak tooconfigure Twitter uwierzytelniania dla aplikacji usługi aplikacji."
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: c6dc91d7-30f6-448c-9f2d-8e91104cde73
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 0d16ac44d7b54e3567b793a904059d31ab1d8911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-twitter-login"></a>Jak tooconfigure logowanie Twitter toouse aplikacji usługi aplikacji
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

W tym temacie opisano sposób tooconfigure usłudze Azure App Service toouse Twitter jako dostawcy uwierzytelniania.

toocomplete hello procedurze w tym temacie, musi mieć konto usługi Twitter, które ma zweryfikowano e-mail adres i numer telefonu. toocreate nowe konto usługi Twitter, przejdź zbyt<a href="http://go.microsoft.com/fwlink/p/?LinkID=268287" target="_blank">twitter.com</a>.

## <a name="register"></a>Zarejestrować aplikację w usłudze Twitter
1. Zaloguj się na toohello [portalu Azure]i przejdź tooyour aplikacji. Kopiowanie z **adres URL**. Użyjesz tego tooconfigure aplikacji Twitter.
2. Przejdź toohello [Twitter deweloperzy] witryny sieci Web, zaloguj się przy użyciu poświadczeń konta usługi Twitter, a następnie kliknij przycisk **Utwórz nową aplikację**.
3. Typ w hello **nazwa** i **opis** dla nowej aplikacji. Wklej do aplikacji **adres URL** dla hello **witryny sieci Web** wartość. Następnie dla hello **wywołania zwrotnego adresu URL**, Wklej hello **wywołania zwrotnego adresu URL** wcześniej zostały skopiowane. To jest Centrum aplikacji mobilnej dołączony ścieżki hello */.auth/login/twitter/callback*. Na przykład `https://contoso.azurewebsites.net/.auth/login/twitter/callback`. Upewnij się, że używasz hello schematu HTTPS.
4. Na stronie powitania dolnej hello przeczytaj i zaakceptuj postanowienia hello. Następnie kliknij przycisk **tworzenie aplikacji Twitter**. Ta aplikacja hello rejestrów Wyświetla szczegóły aplikacji hello.
5. Kliknij przycisk hello **ustawienia** karcie wyboru **Zezwalaj toosign toobe używać tej aplikacji za pomocą usługi Twitter**, następnie kliknij przycisk **ustawienia aktualizacji**.
6. Wybierz hello **kluczy i tokenów dostępu** kartę. Zanotuj wartości hello **konsumenta (klucz interfejsu API)** i **klucz tajny klienta (klucz tajny interfejsu API)**.
   
   > [!NOTE]
   > klucz tajny klienta Hello jest ważne poświadczenie zabezpieczeń. Nie udostępniaj nikomu ten klucz tajny i rozpowszechnienie go z aplikacją.
   > 
   > 

## <a name="secrets"></a>Dodaj Twitter informacji tooyour aplikacji
1. Po powrocie do hello [portalu Azure], przejdź tooyour aplikacji. Kliknij przycisk **ustawienia**, a następnie **uwierzytelniania / autoryzacji**.
2. Jeśli hello uwierzytelniania / autoryzacji funkcja nie jest włączona, włącz przełącznik hello zbyt**na**.
3. Kliknij przycisk **Twitter**. Wklej wartości, które uzyskany wcześniej hello identyfikator aplikacji i klucz tajny aplikacji. Następnie kliknij przycisk **OK**.
   
   ![][1]
   
   Domyślnie usługi App Service zapewnia uwierzytelnianie, ale nie ogranicza autoryzowany dostęp do zawartości witryny tooyour i interfejsów API. Musisz zezwolić użytkownikom w kodzie aplikacji.
4. (Opcjonalnie) toorestrict dostępu tooyour lokacji tooonly użytkowników uwierzytelnionych przez Twitter, ustaw **tootake akcji w przypadku nieuwierzytelnionego żądania** za**Twitter**. Wymaga to, że wszystkie żądania uwierzytelnienia, a wszystkie nieuwierzytelnione żądania są tooTwitter przekierowany do uwierzytelniania.
5. Kliknij pozycję **Zapisz**.

Wszystko jest teraz gotowy toouse usługi Twitter dla uwierzytelniania w aplikacji.

## <a name="related-content"></a>Związane z zawartością
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-twitter-authentication/app-service-twitter-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-twitter-authentication/mobile-app-twitter-settings.png

<!-- URLs. -->

[Twitter deweloperzy]: http://go.microsoft.com/fwlink/p/?LinkId=268300
[portalu Azure]: https://portal.azure.com/
[xamarin]: ../app-services-mobile-app-xamarin-ios-get-started-users.md
